# Creación de OpenAPI Specification

## 🎯 Objetivo

Aprender a crear un contrato `OpenAPI Specification` (OAS) desde cero, entendiendo cada elemento y construyendo progresivamente las operaciones de una API REST para un sistema de catálogo de productos de e-commerce.

---

## 📖 ¿Qué es OpenAPI Specification (OAS)?

**OpenAPI Specification** es un estándar para describir APIs REST de manera clara y comprensible, permitiendo:

- **Documentación automática** (Swagger UI)
- **Generación de código** (cliente y servidor)
- **Validación** de requests/responses
- **Testing automatizado**

---

## 🏗️ Paso 1: Estructura básica del documento

Comenzamos con el esqueleto mínimo:

```yaml
openapi: 3.0.4 # Versión de OpenAPI que usaremos
```

### ¿Por qué empezar aquí?

- `openapi: 3.0.4` es la versión más reciente y estable
- **Obligatorio**: Todo documento OAS debe empezar con esto

---

## 📋 Paso 2: Información general (info)

Agregamos metadatos del proyecto:

```yaml
openapi: 3.0.4
info:
  title: Product Catalog API           # Nombre de tu API
  description: API REST para gestión de catálogo de productos de e-commerce
  version: 1.0.0                      # Versión de tu API
  contact:
    name: ITQ distributed and cloud systems
    email: ivonne.al@queretaro.tecnm.mx
  license:
    name: Apache 2.0
    url: https://www.apache.org/licenses/LICENSE-2.0.html
```

### Elementos explicados:

- **`title`**: Nombre que aparecerá en la documentación
- **`description`**: Explicación breve de qué hace la API
- **`version`**: Versión semántica (1.0.0, 1.2.3, etc.)
- **`contact`**: Información de contacto del equipo
- **`license`**: Licencia bajo la cual se distribuye

---

## 🌐 Paso 3: Servidores (servers)

Definimos dónde está disponible la API:

```yaml
openapi: 3.0.4
info:
  # ... información anterior ...

servers:
  - url: http://localhost:8080/api/v1
    description: Servidor de desarrollo
  - url: https://api.ecommerce.com/api/v1
    description: Servidor de producción
```

### ¿Para qué sirve?

- **Múltiples ambientes**: desarrollo, pruebas, producción
- **URL base**: Todas las rutas se construyen desde aquí
- **Flexibilidad**: Cambiar fácilmente entre ambientes

---

## 🏷️ Paso 4: Etiquetas (tags)

Organizamos las operaciones por categorías:

```yaml
openapi: 3.0.4
info:
  # ... información anterior ...
servers:
  # ... servidores anteriores ...

tags:
  - name: products
    description: Operaciones relacionadas con catálogo de productos
```

### Beneficio:

- **Organización**: Agrupa operaciones similares
- **Documentación clara**: Secciones en Swagger UI
- **Navegación fácil**: Encuentra rápido lo que buscas

---

## 🛣️ Paso 5: Primera operación - Crear producto (POST)

Construimos nuestra primera operación paso a paso:

```yaml
paths:
  /products:        # Ruta del endpoint
    post:           # Método HTTP
      summary: Crear nuevo producto
      description: Crea un nuevo producto en el catálogo
      operationId: createProduct        # ID único para generación de código
      tags:
        - products                      # Asociamos con el tag creado
```

### Elementos explicados:

- **`paths`**: Contenedor de todas las rutas
- **`/products`**: La ruta específica (se une con servers)
- **`post`**: Método HTTP para crear recursos
- **`operationId`**: Nombre único, útil para generar código

---

## 📤 Paso 6: Request Body - Datos de entrada

> Revisar el documento [Esquemas reutilizables](esquemas-reutilizables.md) para una explicación detallada del manejo de `Request Body` utilizando `schemas`.

Definimos los esquemas de entrada:

```yaml
# ✅ SOLUCIÓN: Schema reutilizable
paths:
  /products:
    post:
      # ... elementos anteriores ...
      requestBody:
        required: true                  # Es obligatorio enviar datos
        content:
          application/json:             # Formato de los datos
            schema:
              $ref: '#/components/schemas/Product'  # Referencia al esquema
```

---

## 📥 Paso 7: Responses - Respuestas posibles

Definimos todas las respuestas posibles:

```yaml
paths:
  /products:
    post:
      # ... elementos anteriores ...
      responses:
        '201':                          # Código HTTP de éxito
          description: Producto creado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
              example:
                id: "prod-12345"
                name: "Laptop Gaming"
                price: 1299.99
                category: "Electronics"
        '400':                          # Error del cliente
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
        '409':                          # Conflicto
          description: Conflicto - producto ya existe
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
        '500':                          # Error del servidor
          description: Error interno del servidor
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
```

### Códigos HTTP explicados:

- **`201`**: Created (recurso creado exitosamente)
- **`400`**: Bad Request (datos inválidos)
- **`409`**: Conflict (recurso ya existe o conflicto)
- **`500`**: Internal Server Error (error del servidor)

---

## 🔍 Paso 8: Segunda operación - Buscar productos (GET)

Agregamos operación de búsqueda en la misma ruta:

```yaml
paths:
  /products:
    post:
      # ... operación POST anterior ...
    
    get:                                # Nueva operación en la misma ruta
      summary: Buscar productos
      description: Busca productos existentes basado en criterios
      operationId: searchProducts
      tags:
        - products
      parameters:                       # Parámetros de consulta
        - name: category
          in: query                     # Tipo de parámetro
          description: Categoría del producto
          required: false               # Opcional
          schema:
            type: string
            enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
          example: "Electronics"
        - name: minPrice
          in: query
          description: Precio mínimo del producto
          required: false
          schema:
            type: number
            format: decimal
            minimum: 0
          example: 100.00
        - name: maxPrice
          in: query
          description: Precio máximo del producto
          required: false
          schema:
            type: number
            format: decimal
            minimum: 0
          example: 2000.00
        - name: inStock
          in: query
          description: Solo productos en stock
          required: false
          schema:
            type: boolean
          example: true
```

### Tipos de parámetros:

- **`query`**: ?param=value (filtros de búsqueda)
- **`path`**: /products/{id} (parte de la URL)
- **`header`**: En headers HTTP
- **`cookie`**: En cookies

---

## 📋 Paso 9: Responses de la operación GET

```yaml
      responses:
        '200':
          description: Lista de productos encontrados (puede estar vacía)
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductList'
              example:
                data:
                  - id: "prod-12345"
                    name: "Laptop Gaming"
                    price: 1299.99
                    category: "Electronics"
                    inStock: true
                  - id: "prod-12346"
                    name: "Mouse Gamer"
                    price: 79.99
                    category: "Electronics"
                    inStock: false
                pagination:
                  total: 2
                  page: 1
                  limit: 20
        '400':
          description: Parámetros de búsqueda inválidos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
        '404':
          description: No se encontraron productos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
```

---

## 🔍 Paso 10: Tercera operación - Obtener producto específico (GET)

Agregamos operación para obtener un producto por su ID:

```yaml
  /products/{productId}:              # Ruta con parámetro dinámico
    get:
      summary: Obtener producto por ID
      description: Obtiene los detalles de un producto específico
      operationId: getProductById
      tags:
        - products
      parameters:
        - name: productId               # Parámetro de la ruta
          in: path                      # Ubicación: en la URL
          description: ID del producto a obtener
          required: true                # Los parámetros path son siempre obligatorios
          schema:
            type: string
            pattern: '^prod-[0-9]+$'
          example: "prod-12345"
      responses:
        '200':
          description: Producto encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
              example:
                id: "prod-12345"
                name: "Laptop Gaming"
                price: 1299.99
                category: "Electronics"
                inStock: true
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
```

---

## 🔄 Paso 11: Cuarta operación - Actualizar producto (PUT)

Actualización completa:

```yaml
    put:                                # Actualización completa
      summary: Actualizar producto completo
      description: Actualiza todos los datos de un producto existente
      operationId: updateProduct
      tags:
        - products
      parameters:
        - name: productId               # Parámetro de la ruta
          in: path                      # Ubicación: en la URL
          description: ID del producto a actualizar
          required: true                # Los parámetros path son siempre obligatorios
          schema:
            type: string
            pattern: '^prod-[0-9]+$'
          example: "prod-12345"
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Product'
            example:
              name: "Laptop Gaming Pro"
              description: "Laptop de alto rendimiento para gaming"
              price: 1399.99
              category: "Electronics"
      responses:
        '200':
          description: Producto actualizado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
              example:
                id: "prod-12345"
                name: "Laptop Gaming Pro" 
                price: 1399.99
                category: "Electronics"
                inStock: true
        '400':
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
```

---

## 🔧 Paso 12: Quinta operación - Actualizar parcial (PATCH)

Actualización parcial:

```yaml
    patch:                              # Actualización parcial
      summary: Actualizar producto parcial
      description: Actualiza solo algunos campos de un producto existente
      operationId: patchProduct
      tags:
        - products
      parameters:
        - name: productId
          in: path
          description: ID del producto a actualizar
          required: true
          schema:
            type: string
            pattern: '^prod-[0-9]+$'
          example: "prod-12345"
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductPatch'
            example:
              price: 1199.99
              inStock: false
      responses:
        '200':
          description: Producto actualizado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        '400':
          description: Datos de entrada inválidos
        '404':
          description: Producto no encontrado
```

### Diferencias PUT vs PATCH:

- **PUT**: Reemplaza **todo** el recurso
- **PATCH**: Modifica **solo** los campos enviados

---

## 🗑️ Paso 13: Sexta operación - Eliminar producto (DELETE)

Eliminación de recurso:

```yaml
    delete:                             # Eliminación
      summary: Eliminar producto
      description: Elimina un producto del catálogo
      operationId: deleteProduct 
      tags:
        - products
      parameters:
        - name: productId
          in: path
          description: ID del producto a eliminar
          required: true
          schema:
            type: string
            pattern: '^prod-[0-9]+$'
          example: "prod-12345"
      responses:
        '200':
          description: Producto eliminado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/DeleteConfirmation'
              example:
                id: "prod-12345"
                message: "Producto eliminado exitosamente"
                deletedAt: "2024-01-15T15:45:00Z"
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
        '409':
          description: No se puede eliminar - producto tiene pedidos activos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
```

---

## 🧩 Paso 14: Definir Schemas reutilizables

**¡PUNTO CRÍTICO!** Ahora definimos todos los schemas:

```yaml
components:
  schemas:
    Product:
      type: object
      required:
        - name
        - price  
        - category
      properties:
        name:
          type: string
          minLength: 1
          maxLength: 200
          description: "Nombre del producto"
          example: "Laptop Gaming"
        description:
          type: string
          maxLength: 1000
          description: "Descripción detallada del producto"
          example: "Laptop de alto rendimiento para gaming"
        price:
          type: number
          format: decimal
          minimum: 0
          description: "Precio del producto en USD"
          example: 1299.99
        category:
          type: string
          enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
          description: "Categoría del producto"
          example: "Electronics"
        inStock:
          type: boolean
          description: "Indica si el producto está disponible"
          example: true
          default: true

    ProductResponse:
      allOf:
        - $ref: '#/components/schemas/Product'
        - type: object
          required:
            - id
            - sku
            - createdAt
          properties:
            id:
              type: string 
              pattern: '^prod-[0-9]+$'
              description: "ID único del producto"
              example: "prod-12345"
            sku:
              type: string
              description: "Código SKU del producto"
              example: "LAP-GAM-001"
            createdAt:
              type: string
              format: date-time
              description: "Fecha y hora de creación"
              example: "2024-01-15T10:30:00Z"
            updatedAt:
              type: string
              format: date-time
              description: "Fecha y hora de última actualización"
              example: "2024-01-15T10:30:00Z"

    ProductPatch:
      type: object
      properties:
        name:
          type: string
          minLength: 1
          maxLength: 200
        description:
          type: string
          maxLength: 1000
        price:
          type: number
          format: decimal
          minimum: 0
        category:
          type: string
          enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
        inStock:
          type: boolean

    ProductList:
      type: object
      required:
        - data
        - pagination
      properties:
        data:
          type: array
          items:
            $ref: '#/components/schemas/ProductResponse'
        pagination:
          $ref: '#/components/schemas/Pagination'

    Pagination:
      type: object
      required:
        - total
        - page
        - limit
        - totalPages
      properties:
        total:
          type: integer
          minimum: 0
          description: "Total de productos"
          example: 150
        page:
          type: integer
          minimum: 1
          description: "Página actual"
          example: 1
        limit:
          type: integer
          minimum: 1
          maximum: 100
          description: "Elementos por página"
          example: 20
        totalPages:
          type: integer
          minimum: 0
          description: "Total de páginas"
          example: 8

    DeleteConfirmation:
      type: object
      required:
        - id
        - message
        - deletedAt
      properties:
        id:
          type: string
          description: "ID del producto eliminado"
          example: "prod-12345"
        message:
          type: string
          description: "Mensaje de confirmación"
          example: "Producto eliminado exitosamente"
        deletedAt:
          type: string
          format: date-time
          description: "Fecha y hora de eliminación"
          example: "2024-01-15T15:45:00Z"

    ApiError:
      type: object
      required:
        - code
        - message
        - timestamp
      properties:
        code:
          type: string
          description: "Código de error"
          example: "PRODUCT_NOT_FOUND"
        message:
          type: string
          description: "Mensaje descriptivo del error"
          example: "El producto especificado no existe"
        details:
          type: object
          description: "Detalles adicionales del error"
          additionalProperties: true
        timestamp:
          type: string
          format: date-time
          description: "Fecha y hora del error"
          example: "2024-01-15T10:30:00Z"
        path:
          type: string
          description: "Ruta donde ocurrió el error"
          example: "/api/v1/products/prod-12345"
```

### Beneficios de `allOf`:

- **`ProductResponse`** = `Product` + campos adicionales
- Evita duplicar campos
- Mantiene consistencia
- Facilita mantenimiento

---

## 🎯 Paso 15: Validación de campos avanzada

Ejemplos de validaciones robustas:

```yaml
# Pattern matching
productId:
  type: string
  pattern: '^prod-[0-9]+$'  # Solo acepta: prod-12345
  
# Rangos numéricos
price:
  type: number
  minimum: 0
  maximum: 999999.99
  multipleOf: 0.01  # Solo centavos

# Strings con longitud
name:
  type: string
  minLength: 1
  maxLength: 200

# Enums (valores fijos)
category:
  type: string
  enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]

# Arrays con límites
tags:
  type: array
  items:
    type: string
  minItems: 1
  maxItems: 10
  uniqueItems: true

# Fechas y formatos
createdAt:
  type: string
  format: date-time  # RFC 3339: 2024-01-15T10:30:00Z
  
price:
  type: number
  format: decimal    # Para valores monetarios
```

---

## ✅ Paso 16: Documento completo

**¡Felicidades!** Has creado una especificación OpenAPI completa. Tu archivo final debe tener:

✅ **Estructura básica**: openapi, info, servers, tags  
✅ **6 operaciones CRUD**: POST, GET, GET/{id}, PUT, PATCH, DELETE  
✅ **Schemas reutilizables**: Product, ProductResponse, ProductPatch, ProductList, etc.  
✅ **Validaciones robustas**: patterns, ranges, enums, formats  
✅ **Manejo de errores**: ApiError con códigos HTTP apropiados  
✅ **Ejemplos completos**: En requests y responses  
✅ **Documentación clara**: Descriptions en todos los elementos  

---

## 🔍 Paso 17: Testing y validación

### 1. Validar en Swagger Editor

1. Ve a: https://editor.swagger.io/
2. Pega tu especificación YAML
3. Verifica que no hay errores (panel derecho)
4. Revisa la documentación generada

### 2. Probar con Swagger UI

1. En Swagger Editor, haz clic en "Try it out"
2. Completa los parámetros de ejemplo  
3. Ejecuta las operaciones
4. Verifica las respuestas

### 3. Exportar documentación

1. **File → Export → Documentation (HTML)**
2. **File → Export → Client SDK** (opcional)
3. **File → Export → Server Stub** (opcional)

### 4. Importar en Postman

1. Postman → Import → Raw Text
2. Pega tu especificación
3. Se crean automáticamente todas las requests
4. Prueba las operaciones

---

## 🎓 Paso 18: Próximos pasos

Ahora que tienes tu especificación OpenAPI completa:

### **Para Desarrollo:**

1. **Generar código servidor** (Spring Boot, Node.js, etc.)
2. **Generar cliente** (JavaScript, Python, etc.)  
3. **Implementar la lógica de negocio**
4. **Configurar base de datos**

### **Para Integración:**

1. **API Gateway**: Importar especificación para routing
2. **Testing**: Crear tests automatizados basados en contract
3. **Monitoreo**: Configurar métricas por endpoint
4. **Documentación**: Publicar en portal de desarrolladores

### **Para DevOps:**

1. **CI/CD**: Validar especificación en pipeline  
2. **Contract testing**: Verificar compatibilidad con consumidores
3. **Versionado**: Gestionar updates sin breaking changes
4. **Mock servers**: Para desarrollo paralelo

---

## 💡 Tips avanzados

### **Versionado de APIs:**

```yaml
# Opción 1: En la URL
servers:
  - url: https://api.ecommerce.com/v1
  - url: https://api.ecommerce.com/v2

# Opción 2: En headers  
components:
  parameters:
    ApiVersion:
      name: API-Version
      in: header
      schema:
        type: string
        enum: ['1.0', '2.0']
```

### **Security Schemes:**

```yaml
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
    
security:
  - bearerAuth: []
```

### **Links (HATEOAS):**

```yaml
responses:
  '200':
    content:
      application/json:
        schema:
          $ref: '#/components/schemas/ProductResponse'
    links:
      GetProductOrders:
        operationId: getOrdersByProduct
        parameters:
          productId: $response.body#/id
```

---

## 🎉 ¡Completado!

**Has dominado la creación de especificaciones OpenAPI profesionales!**

Tu especificación ahora puede ser usada para:
- 📚 **Documentar** tu API automáticamente
- 🏭 **Generar código** cliente y servidor
- 🧪 **Testing** automatizado y validación
- 🔗 **Integración** con herramientas DevOps
- 👥 **Colaboración** entre equipos front-end y back-end

**¡Excelente trabajo!** 🚀