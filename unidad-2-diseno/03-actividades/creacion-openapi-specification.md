# Creación de OpenAPI Specification

- [Creación de OpenAPI Specification](#creación-de-openapi-specification)
  - [🎯 Objetivo](#-objetivo)
  - [🛠️ Prerrequisitos](#️-prerrequisitos)
  - [🗂️ Glosario rápido](#️-glosario-rápido)
  - [📖 ¿Qué es OpenAPI Specification (OAS)?](#-qué-es-openapi-specification-oas)
  - [🏗️ Paso 1: Estructura básica del documento](#️-paso-1-estructura-básica-del-documento)
    - [¿Por qué empezar aquí?](#por-qué-empezar-aquí)
  - [📋 Paso 2: Información general (info)](#-paso-2-información-general-info)
    - [Elementos explicados](#elementos-explicados)
  - [🌐 Paso 3: Servidores (servers)](#-paso-3-servidores-servers)
    - [¿Para qué sirve?](#para-qué-sirve)
  - [🏷️ Paso 4: Etiquetas (tags)](#️-paso-4-etiquetas-tags)
    - [Beneficio](#beneficio)
  - [🛣️ Paso 5: Operación - Crear producto (POST)](#️-paso-5-operación---crear-producto-post)
    - [Elementos explicados](#elementos-explicados-1)
    - [Referencia rápida de métodos HTTP](#referencia-rápida-de-métodos-http)
  - [📤 Paso 6: Request Body - Datos de entrada](#-paso-6-request-body---datos-de-entrada)
  - [📥 Paso 7: Responses - Respuestas posibles](#-paso-7-responses---respuestas-posibles)
    - [Códigos HTTP explicados](#códigos-http-explicados)
  - [🔍 Paso 8: Operación - Buscar productos (GET)](#-paso-8-operación---buscar-productos-get)
    - [Tipos de parámetros](#tipos-de-parámetros)
  - [🔍 Paso 9: Operación - Obtener producto específico (GET)](#-paso-9-operación---obtener-producto-específico-get)
  - [🔄 Paso 10: Operación - Actualizar producto (PUT)](#-paso-10-operación---actualizar-producto-put)
  - [🔧 Paso 11: Operación - Actualizar parcial (PATCH)](#-paso-11-operación---actualizar-parcial-patch)
    - [Diferencias PUT vs PATCH](#diferencias-put-vs-patch)
  - [🗑️ Paso 12: Operación - Eliminar producto (DELETE)](#️-paso-12-operación---eliminar-producto-delete)
  - [✅ Checkpoint: Verificación intermedia](#-checkpoint-verificación-intermedia)
  - [🧩 Paso 13: Refactorización a Componentes Reutilizables (Schemas y Examples)](#-paso-13-refactorización-a-componentes-reutilizables-schemas-y-examples)
    - [¿Qué es `allOf`?](#qué-es-allof)
    - [Beneficios de `allOf` (recapitulando)](#beneficios-de-allof-recapitulando)
    - [Agregar componentes reutilizables](#agregar-componentes-reutilizables)
  - [🧩 Paso 14: Actualización de referencias](#-paso-14-actualización-de-referencias)
  - [🎯 Paso 15: Validación de campos avanzada](#-paso-15-validación-de-campos-avanzada)
  - [✅ Paso 16: Documento completo](#-paso-16-documento-completo)
  - [🔍 Paso 17: Testing y validación](#-paso-17-testing-y-validación)
    - [1. Validar en Swagger Editor](#1-validar-en-swagger-editor)
    - [2. Probar con Swagger UI](#2-probar-con-swagger-ui)
    - [3. Exportar documentación](#3-exportar-documentación)
    - [4. Importar en Postman](#4-importar-en-postman)
  - [🎓 Paso 18: Próximos pasos](#-paso-18-próximos-pasos)
    - [**Para Desarrollo:**](#para-desarrollo)
    - [**Para Integración:**](#para-integración)
    - [**Para DevOps:**](#para-devops)
  - [💡 Tips avanzados](#-tips-avanzados)
    - [**Versionado de APIs:**](#versionado-de-apis)
    - [**Security Schemes:**](#security-schemes)
    - [**Links (HATEOAS):**](#links-hateoas)
  - [📚 Recursos adicionales](#-recursos-adicionales)
  - [🎉 ¡Completado!](#-completado)


## 🎯 Objetivo

Aprender a crear un contrato `OpenAPI Specification` (OAS) desde cero, entendiendo cada elemento y construyendo progresivamente las operaciones de una API REST para un sistema de catálogo de productos de e-commerce.

> **¿Por qué aprender OpenAPI?**
>
> En el desarrollo profesional de software, la claridad y precisión en la definición de APIs es clave para la colaboración entre equipos, la automatización de pruebas y la generación de código. Dominar OAS te permitirá crear servicios robustos, bien documentados y listos para integrarse en cualquier entorno moderno de microservicios.

---

## 🛠️ Prerrequisitos

Antes de comenzar, asegúrate de tener listo:

- **Swagger Editor**: https://editor.swagger.io/ (online, sin instalación)
- **Conocimientos previos**: HTTP básico (métodos GET, POST, PUT, PATCH, DELETE)
- **Formato YAML**: Indentación con espacios (no tabuladores), sensible a la estructura

> **💡 Tip:** Trabaja en Swagger Editor desde el inicio. Pega cada paso y verifica que no haya errores antes de avanzar al siguiente.

---

## 🗂️ Glosario rápido

Antes de iniciar, familiarízate con estos términos que usaremos a lo largo del documento:

| Término        | Definición breve |
|----------------|------------------|
| **API**        | Interfaz que permite la comunicación entre sistemas de software |
| **REST**       | Estilo arquitectónico para diseñar servicios web basados en recursos |
| **Endpoint**   | Ruta específica de la API (ej. `/products`) |
| **Schema**     | Estructura de datos que define la forma de los requests y responses |
| **`$ref`**     | Referencia a un objeto definido en otro lugar del documento OAS |
| **Path**       | Ruta de acceso a un recurso dentro de la API |
| **Request**    | Solicitud que el cliente envía al servidor |
| **Response**   | Respuesta que el servidor devuelve al cliente |
| **YAML**       | Formato de serialización de datos legible por humanos, usado en OAS |

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

> ⚠️ **Errores comunes con YAML:**
> - Usar **tabuladores** en vez de espacios (YAML **solo** acepta espacios)
> - Indentación inconsistente (mantén siempre **2 espacios** por nivel)
> - Olvidar los dos puntos `:` después de una clave
> - Dejar espacios extra al final de una línea
>
> **💡 Si Swagger Editor muestra un error, lo primero que debes revisar es la indentación.**

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

### Elementos explicados

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

### Beneficio

- **Organización**: Agrupa operaciones similares
- **Documentación clara**: Secciones en Swagger UI
- **Navegación fácil**: Encuentra rápido lo que buscas

---

## 🛣️ Paso 5: Operación - Crear producto (POST)

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

### Elementos explicados

- **`paths`**: Contenedor de todas las rutas
- **`/products`**: La ruta específica (se une con servers)
- **`post`**: Método HTTP para crear recursos
- **`summary`**: Texto corto (una línea) que aparece en la lista de operaciones de Swagger UI
- **`description`**: Texto largo con detalles, soporta Markdown para formato enriquecido
- **`operationId`**: Nombre único, útil para generar código (se convierte en nombre de función/método)

### Referencia rápida de métodos HTTP

| Método  | Acción              | Idempotente | Cuerpo (Body) |
|---------|---------------------|-------------|----------------|
| POST    | Crear recurso       | No          | Sí             |
| GET     | Leer recurso(s)     | Sí          | No             |
| PUT     | Reemplazar completo | Sí          | Sí             |
| PATCH   | Actualizar parcial  | No          | Sí             |
| DELETE  | Eliminar recurso    | Sí          | No             |

> **💡 ¿Qué es idempotente?** Una operación es idempotente cuando ejecutarla múltiples veces produce el mismo resultado que ejecutarla una sola vez. Por ejemplo, un `PUT` con los mismos datos siempre deja el recurso en el mismo estado.

---

## 📤 Paso 6: Request Body - Datos de entrada

> **Nota didáctica:** Para evitar errores en Swagger Editor y comprender mejor la estructura, primero modelaremos los objetos directamente en cada operación. Más adelante, en el paso 14, aprenderás a refactorizar usando `$ref` y `schemas` reutilizables.

Definimos el objeto de entrada directamente (inline):

```yaml
paths:
  /products:
    post:
      # ... elementos anteriores ...
      requestBody:
        required: true
        content:
          application/json:
            schema:
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
                  format: double
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
              # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/Product'
```

---

## 📥 Paso 7: Responses - Respuestas posibles

Definimos todas las respuestas posibles, modelando el objeto de respuesta directamente:

```yaml
paths:
  /products:
    post:
      # ... elementos anteriores ...
      responses:
        '201':
          description: Producto creado exitosamente
          content:
            application/json:
              schema:
                type: object
                required:
                  - id
                  - name
                  - price
                  - category
                  - inStock
                  - sku
                  - createdAt
                properties:
                  id:
                    type: string
                    pattern: '^prod-[0-9]+$'
                    description: "ID único del producto"
                    example: "prod-12345"
                  name:
                    type: string
                    minLength: 1
                    maxLength: 200
                    description: "Nombre del producto"
                    example: "Laptop Gaming"
                  price:
                    type: number
                    format: double
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
              # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/ProductResponse'
        '400':
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "INVALID_INPUT"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "Los datos enviados no cumplen con el esquema."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInvalidInput
        '409':
          description: Conflicto - producto ya existe
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "PRODUCT_EXISTS"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "El producto ya existe."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorConflict
        '500':
          description: Error interno del servidor
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "INTERNAL_ERROR"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "Ocurrió un error inesperado."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInternal
```

### Códigos HTTP explicados

- **`201`**: Created (recurso creado exitosamente)
- **`400`**: Bad Request (datos inválidos)
- **`409`**: Conflict (recurso ya existe o conflicto)
- **`500`**: Internal Server Error (error del servidor)

---

## 🔍 Paso 8: Operación - Buscar productos (GET)

Agregamos operación de búsqueda en la misma ruta. El objeto de respuesta también se define inline:

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
      parameters:
        - name: category
          in: query
          description: Categoría del producto
          required: false
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
            format: double
            minimum: 0
          example: 100.00
        - name: maxPrice
          in: query
          description: Precio máximo del producto
          required: false
          schema:
            type: number
            format: double
            minimum: 0
          example: 2000.00
        - name: inStock
          in: query
          description: Solo productos en stock
          required: false
          schema:
            type: boolean
          example: true
        - name: page
          in: query
          description: Número de página (por defecto 1)
          required: false
          schema:
            type: integer
            minimum: 1
            default: 1
          example: 1
        - name: limit
          in: query
          description: Elementos por página (por defecto 20, máximo 100)
          required: false
          schema:
            type: integer
            minimum: 1
            maximum: 100
            default: 20
          example: 20
      responses:
        '200':
          description: Lista de productos encontrados (puede estar vacía)
          content:
            application/json:
              schema:
                type: object
                required:
                  - data
                  - pagination
                properties:
                  data:
                    type: array
                    items:
                      type: object
                      required:
                        - id
                        - name
                        - price
                        - category
                        - inStock
                        - sku
                        - createdAt
                      properties:
                        id:
                          type: string
                          pattern: '^prod-[0-9]+$'
                          description: "ID único del producto"
                          example: "prod-12345"
                        name:
                          type: string
                          description: "Nombre del producto"
                          example: "Laptop Gaming"
                        price:
                          type: number
                          description: "Precio del producto en USD"
                          example: 1299.99
                        category:
                          type: string
                          description: "Categoría del producto"
                          example: "Electronics"
                        inStock:
                          type: boolean
                          description: "Indica si el producto está disponible"
                          example: true
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
                  pagination:
                    type: object
                    required:
                      - total
                      - page
                      - limit
                      - totalPages
                    properties:
                      total:
                        type: integer
                        example: 2
                      page:
                        type: integer
                        example: 1
                      limit:
                        type: integer
                        example: 20
                      totalPages:
                        type: integer
                        example: 1
              # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/ProductList'
        '400':
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "INVALID_INPUT"
                  message:
                    type: string
                    example: "Los datos enviados no cumplen con el esquema."
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInvalidInput
        '500':
          description: Error interno del servidor
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "INTERNAL_ERROR"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "Ocurrió un error inesperado."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInternal
```

> **💡 Nota:** Un endpoint de búsqueda de colección (`GET /products`) **no** debe retornar `404` cuando no encuentra resultados. La respuesta correcta es un `200` con un arreglo vacío en `data`. El código `404` se reserva para cuando la ruta misma no existe o para recursos individuales (como `GET /products/{productId}`).

### Tipos de parámetros

- **`query`**: ?param=value (filtros de búsqueda)
- **`path`**: /products/{id} (parte de la URL)
- **`header`**: En headers HTTP
- **`cookie`**: En cookies

---

## 🔍 Paso 9: Operación - Obtener producto específico (GET)

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
                type: object
                required:
                  - id
                  - name
                  - price
                  - category
                  - inStock
                  - sku
                  - createdAt
                properties:
                  id:
                    type: string
                    pattern: '^prod-[0-9]+$'
                    description: "ID único del producto"
                    example: "prod-12345"
                  name:
                    type: string
                    description: "Nombre del producto"
                    example: "Laptop Gaming"
                  price:
                    type: number
                    description: "Precio del producto en USD"
                    example: 1299.99
                  category:
                    type: string
                    description: "Categoría del producto"
                    example: "Electronics"
                  inStock:
                    type: boolean
                    description: "Indica si el producto está disponible"
                    example: true
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
              # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/ProductResponse'
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "PRODUCT_NOT_FOUND"
                  message:
                    type: string
                    example: "El producto especificado no existe"
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products/prod-12345"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorNotFound
        '500':
          description: Error interno del servidor
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "INTERNAL_ERROR"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "Ocurrió un error inesperado."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInternal
```

---

## 🔄 Paso 10: Operación - Actualizar producto (PUT)

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
                  example: "Laptop Gaming Pro"
                description:
                  type: string
                  maxLength: 1000
                  example: "Laptop de alto rendimiento para gaming"
                price:
                  type: number
                  format: double
                  minimum: 0
                  example: 1399.99
                category:
                  type: string
                  enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
                  example: "Electronics"
                inStock:
                  type: boolean
                  example: true
            # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/Product'
      responses:
        '200':
          description: Producto actualizado exitosamente
          content:
            application/json:
              schema:
                type: object
                required:
                  - id
                  - name
                  - price
                  - category
                  - inStock
                  - sku
                  - createdAt
                properties:
                  id:
                    type: string
                    pattern: '^prod-[0-9]+$'
                    example: "prod-12345"
                  name:
                    type: string
                    example: "Laptop Gaming Pro"
                  price:
                    type: number
                    example: 1399.99
                  category:
                    type: string
                    example: "Electronics"
                  inStock:
                    type: boolean
                    example: true
                  sku:
                    type: string
                    example: "LAP-GAM-001"
                  createdAt:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  updatedAt:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/ProductResponse'
        '400':
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "INVALID_INPUT"
                  message:
                    type: string
                    example: "Los datos enviados no cumplen con el esquema."
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInvalidInput
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "PRODUCT_NOT_FOUND"
                  message:
                    type: string
                    example: "El producto especificado no existe"
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products/prod-12345"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorNotFound
        '500':
          description: Error interno del servidor
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "INTERNAL_ERROR"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "Ocurrió un error inesperado."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInternal
```

---

## 🔧 Paso 11: Operación - Actualizar parcial (PATCH)

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
              type: object
              properties:
                name:
                  type: string
                  minLength: 1
                  maxLength: 200
                  description: "Nombre del producto"
                  example: "Laptop Gaming Pro"
                description:
                  type: string
                  maxLength: 1000
                  description: "Descripción detallada del producto"
                  example: "Laptop de alto rendimiento para gaming"
                price:
                  type: number
                  format: double
                  minimum: 0
                  description: "Precio del producto en USD"
                  example: 1199.99
                category:
                  type: string
                  enum: ["Electronics", "Clothing", "Books", "Home", "Sports"]
                  description: "Categoría del producto"
                  example: "Electronics"
                inStock:
                  type: boolean
                  description: "Indica si el producto está disponible"
                  example: false
            # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/ProductPatch'
      responses:
        '200':
          description: Producto actualizado exitosamente
          content:
            application/json:
              schema:
                type: object
                required:
                  - id
                  - name
                  - price
                  - category
                  - inStock
                  - sku
                  - createdAt
                properties:
                  id:
                    type: string
                    pattern: '^prod-[0-9]+$'
                    example: "prod-12345"
                  name:
                    type: string
                    example: "Laptop Gaming"
                  price:
                    type: number
                    example: 1199.99
                  category:
                    type: string
                    example: "Electronics"
                  inStock:
                    type: boolean
                    example: false
                  sku:
                    type: string
                    example: "LAP-GAM-001"
                  createdAt:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  updatedAt:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/ProductResponse'
        '400':
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "INVALID_INPUT"
                  message:
                    type: string
                    example: "Los datos enviados no cumplen con el esquema."
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInvalidInput
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "PRODUCT_NOT_FOUND"
                  message:
                    type: string
                    example: "El producto especificado no existe"
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products/prod-12345"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorNotFound
        '500':
          description: Error interno del servidor
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "INTERNAL_ERROR"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "Ocurrió un error inesperado."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInternal
```

### Diferencias PUT vs PATCH

- **PUT**: Reemplaza **todo** el recurso
- **PATCH**: Modifica **solo** los campos enviados

---

## 🗑️ Paso 12: Operación - Eliminar producto (DELETE)

Eliminación de recurso:

> **💡 Nota:** Muchas APIs profesionales usan `204 No Content` (sin cuerpo de respuesta) para el DELETE exitoso. Aquí usamos `200` con un objeto de confirmación para fines didácticos, ya que permite al alumno ver claramente la respuesta.

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
                type: object
                required:
                  - id
                  - message
                  - deletedAt
                properties:
                  id:
                    type: string
                    example: "prod-12345"
                  message:
                    type: string
                    example: "Producto eliminado exitosamente"
                  deletedAt:
                    type: string
                    format: date-time
                    example: "2024-01-15T15:45:00Z"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por --> $ref: '#/components/schemas/DeleteConfirmation'
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "PRODUCT_NOT_FOUND"
                  message:
                    type: string
                    example: "El producto especificado no existe"
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products/prod-12345"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorNotFound
        '409':
          description: No se puede eliminar - producto tiene pedidos activos
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    example: "PRODUCT_HAS_ORDERS"
                  message:
                    type: string
                    example: "No se puede eliminar - producto tiene pedidos activos"
                  timestamp:
                    type: string
                    format: date-time
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    example: "/api/v1/products/prod-12345"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorProductHasOrders
        '500':
          description: Error interno del servidor
          content:
            application/json:
              schema:
                type: object
                required:
                  - code
                  - message
                  - timestamp
                properties:
                  code:
                    type: string
                    description: "Código de error"
                    example: "INTERNAL_ERROR"
                  message:
                    type: string
                    description: "Mensaje descriptivo del error"
                    example: "Ocurrió un error inesperado."
                  timestamp:
                    type: string
                    format: date-time
                    description: "Fecha y hora del error"
                    example: "2024-01-15T10:30:00Z"
                  path:
                    type: string
                    description: "Ruta donde ocurrió el error"
                    example: "/api/v1/products"
              # 🔄 El "object" definido dentro del "schema" será reemplazado por -> $ref: '#/components/schemas/ApiError'
              # Se agrega "examples" ApiErrorInternal
```

---

## ✅ Checkpoint: Verificación intermedia

**Antes de continuar**, es importante validar todo lo que llevas hasta ahora:

1. Abre [Swagger Editor](https://editor.swagger.io/)
2. Pega tu [especificación YAML completa (Pasos 1 al 12)](oas-sin-componentes.yaml)
3. Verifica que **no hay errores** en el panel derecho
4. Navega por la documentación generada y confirma que las 6 operaciones aparecen correctamente

> **💡 Si tienes errores**, revísalos uno por uno. Los más comunes son:
> - Indentación incorrecta (recuerda: siempre 2 espacios)
> - Falta de comillas en valores con caracteres especiales
> - Error en los nombres de las propiedades `required` (deben coincidir exactamente con los nombres en `properties`)

Una vez que todo funciona sin errores, continúa con la refactorización.

---

## 🧩 Paso 13: Refactorización a Componentes Reutilizables (Schemas y Examples)

**¡PUNTO CRÍTICO!** Ahora que comprendes la estructura de los objetos, es momento de refactorizar tu especificación para usar la sección components. Esta sección permite definir objetos reutilizables para mantener tu código limpio y evitar duplicidad.

Dentro de components, nos enfocaremos en dos partes principales:

- schemas: Para definir estructuras de datos (Modelos).
- examples: Para definir ejemplos de respuestas o peticiones concretas.

1. Crea la sección components al final de tu documento.
2. Reemplaza los objetos definidos inline en cada operación por referencias $ref a los componentes correspondientes.

Ejemplo de refactor:

**Antes (inline):**

```yaml
schema:
  type: object
  required:
    - name
    - price
    - category
  properties:
    name: ...
    # ...
```

**Después (con $ref):**

```yaml
schema:
  $ref: '#/components/schemas/Product'
```

> **Ventajas:**
> - Evita duplicidad de código
> - Facilita el mantenimiento
> - Permite validar y documentar de forma más eficiente

### ¿Qué es `allOf`?

Antes de ver el código, es importante entender la palabra clave `allOf`. En OpenAPI, `allOf` permite **componer un schema combinando múltiples schemas**. Es similar al concepto de **herencia** en programación orientada a objetos:

- `ProductResponse` = `Product` + campos adicionales (id, sku, createdAt, updatedAt)
- El schema resultante incluye **todas** las propiedades de ambos schemas
- Evita duplicar campos que ya están definidos en otro schema

### Beneficios de `allOf` (recapitulando)

- **`ProductResponse`** = `Product` + campos adicionales
- Evita duplicar campos
- Mantiene consistencia
- Facilita mantenimiento

### Agregar componentes reutilizables

Ahora sí, define todos los componentes reutilizables.

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
          format: double
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
            - inStock
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
          format: double
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
      description: "Estructura estándar para errores de la API"
      required:
        - code
        - message
        - timestamp
      properties:
        code:
          type: string
          description: |
            Código de error.
            Valores comunes en esta API:
            - INVALID_INPUT (400)
            - PRODUCT_NOT_FOUND (404)
            - PRODUCT_EXISTS (409 - conflicto en creación)
            - PRODUCT_HAS_ORDERS (409 - conflicto en eliminación)
            - INTERNAL_ERROR (500)
          enum:
            - INVALID_INPUT
            - PRODUCT_NOT_FOUND
            - PRODUCT_EXISTS
            - PRODUCT_HAS_ORDERS
            - INTERNAL_ERROR
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
  examples:
    ApiErrorInvalidInput:
      summary: Datos de entrada inválidos (400)
      value:
        code: "INVALID_INPUT"
        message: "Los datos enviados no cumplen con el esquema."
        timestamp: "2024-01-15T10:30:00Z"
        path: "/api/v1/products"
        details:
          field: "name"
          reason: "required"
    ApiErrorNotFound:
      summary: Producto no encontrado (404)
      value:
        code: "PRODUCT_NOT_FOUND"
        message: "El producto especificado no existe"
        timestamp: "2024-01-15T10:30:00Z"
        path: "/api/v1/products/prod-12345"
        details:
          productId: "prod-12345"
          searchedBy: "id"
    ApiErrorConflict:
      summary: Conflicto - producto ya existe (409)
      value:
        code: "PRODUCT_EXISTS"
        message: "El producto ya existe."
        timestamp: "2024-01-15T10:30:00Z"
        path: "/api/v1/products"
        details:
          existingProductId: "prod-12345"
          conflictReason: "duplicate_name"
    ApiErrorProductHasOrders:
      summary: No se puede eliminar - producto tiene pedidos activos (409)
      value:
        code: "PRODUCT_HAS_ORDERS"
        message: "No se puede eliminar - producto tiene pedidos activos"
        timestamp: "2024-01-15T10:30:00Z"
        path: "/api/v1/products/prod-12345"
        details:
          activeOrdersCount: 3
          orderIds: ["ord-001", "ord-002", "ord-003"]
    ApiErrorInternal:
      summary: Error interno del servidor (500)
      value:
        code: "INTERNAL_ERROR"
        message: "Ocurrió un error inesperado."
        timestamp: "2024-01-15T10:30:00Z"
        path: "/api/v1/products"
        details:
          errorId: "err-2024-001"
          traceId: "trace-abc123"
```

## 🧩 Paso 14: Actualización de referencias

- Reemplaza schemas para operación y responses - Crear producto (POST).

```yaml
paths:
  /products:
    post:
      # ... elementos anteriores ...
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Product'  # Referencia al esquema
      responses:
        '201':                          # Código HTTP de éxito
          description: Producto creado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        '400':                          # Error del cliente
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInvalidInput:
                  $ref: '#/components/examples/ApiErrorInvalidInput'
        '409':                          # Conflicto
          description: Conflicto - producto ya existe
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorConflict:
                  $ref: '#/components/examples/ApiErrorConflict'
        '500':                          # Error del servidor
          description: Error interno del servidor
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInternal:
                  $ref: '#/components/examples/ApiErrorInternal'
```

- Reemplaza schemas para responses - Buscar productos (GET).

```yaml
      responses:
        '200':
          description: Lista de productos encontrados (puede estar vacía)
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductList'
        '400':
          description: Parámetros de búsqueda inválidos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInvalidInput:
                  $ref: '#/components/examples/ApiErrorInvalidInput'
        '500':                          # Error del servidor
          description: Error interno del servidor
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInternal:
                  $ref: '#/components/examples/ApiErrorInternal'
```


- Reemplaza schemas para responses - Obtener producto específico (GET).

```yaml
  /products/{productId}:              # Ruta con parámetro dinámico
    get:
      # ... elementos anteriores ...
      responses:
        '200':
          description: Producto encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorNotFound:
                  $ref: '#/components/examples/ApiErrorNotFound'
        '500':                          # Error del servidor
          description: Error interno del servidor
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInternal:
                  $ref: '#/components/examples/ApiErrorInternal'
```

- Reemplaza schemas para operación y responses - Actualizar producto (PUT).

```yaml
    put:                                # Actualización completa
      # ... elementos anteriores ...
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/Product'
      responses:
        '200':
          description: Producto actualizado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        '400':
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInvalidInput:
                  $ref: '#/components/examples/ApiErrorInvalidInput'
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorNotFound:
                  $ref: '#/components/examples/ApiErrorNotFound'
        '500':                          # Error del servidor
          description: Error interno del servidor
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInternal:
                  $ref: '#/components/examples/ApiErrorInternal'
```

- Reemplaza schemas para operación y responses - Actualizar parcial (PATCH).

```yaml
    patch:                              # Actualización parcial
      # ... elementos anteriores ...
      requestBody:
        required: true
        content:
          application/json:
            schema:
              $ref: '#/components/schemas/ProductPatch'
      responses:
        '200':
          description: Producto actualizado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductResponse'
        '400':
          description: Datos de entrada inválidos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInvalidInput:
                  $ref: '#/components/examples/ApiErrorInvalidInput'
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorNotFound:
                  $ref: '#/components/examples/ApiErrorNotFound'
        '500':                          # Error del servidor
          description: Error interno del servidor
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'          
              examples:
                apiErrorInternal:
                  $ref: '#/components/examples/ApiErrorInternal'
```

- Reemplaza schemas para responses - Eliminar producto (DELETE).

```yaml
    delete:                             # Eliminación
      # ... elementos anteriores ...
      responses:
        '200':
          description: Producto eliminado exitosamente
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/DeleteConfirmation'
        '404':
          description: Producto no encontrado
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorNotFound:
                  $ref: '#/components/examples/ApiErrorNotFound'
        '409':
          description: No se puede eliminar - producto tiene pedidos activos
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorProductHasOrders:
                  $ref: '#/components/examples/ApiErrorProductHasOrders'
        '500':                          # Error del servidor
          description: Error interno del servidor
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ApiError'
              examples:
                apiErrorInternal:
                  $ref: '#/components/examples/ApiErrorInternal'
```

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
  format: double     # Formato estándar OAS para valores monetarios con decimales
```

> **✅ Buenas prácticas:**
> - Usa nombres descriptivos y consistentes para endpoints y schemas
> - Documenta **cada campo** con `description` y `example`
> - Usa `operationId` únicos y descriptivos (se convertirán en nombres de funciones en código generado)
> - Valida frecuentemente en Swagger Editor — no esperes al final
> - Usa `$ref` para evitar duplicación de schemas
> - Define `required` solo para los campos verdaderamente obligatorios

> **❌ Errores comunes:**
> - Olvidar campos en `required` que sí son obligatorios
> - No actualizar los `example` tras modificar schemas
> - Duplicar definiciones en vez de usar `$ref`
> - Usar tabuladores en YAML (solo se aceptan espacios)
> - Confundir `format: decimal` (no estándar) con `format: double` (estándar OAS)
> - Retornar `404` en endpoints de colección cuando no hay resultados (debe ser `200` con arreglo vacío)

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

Aquí puedes encontrar [especificación YAML completa con componentes](oas-con-componentes.yaml).

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

## 📚 Recursos adicionales

Para profundizar en OpenAPI Specification y APIs REST:

- [📖 Especificación oficial OpenAPI 3.0](https://spec.openapis.org/oas/v3.0.4) — Referencia completa del estándar
- [🛠️ Swagger Editor Online](https://editor.swagger.io/) — Editor en línea para crear y validar tu OAS
- [📘 Guía OpenAPI de Swagger](https://swagger.io/docs/specification/about/) — Tutorial paso a paso oficial
- [📬 Postman](https://www.postman.com/) — Herramienta para probar APIs importando tu especificación
- [🎬 OpenAPI en 5 minutos (video)](https://www.youtube.com/watch?v=pRS9LRBgjYg) — Introducción visual rápida

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