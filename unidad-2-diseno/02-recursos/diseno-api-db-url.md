# Diseño de APIs vs DB vs URLs

Cuando se genera un contrato con OpenAPI Specification (OAS) y se quiere mantener una relación clara entre el esquema de OAS y la entidad (tabla) de la base de datos, es fundamental elegir la **nomenclatura** adecuada.

Este es un punto crucial en el diseño de APIs y una fuente común de debate, hablamos del desacoplamiento entre la capa de persistencia (base de datos) y la capa de presentación (la API).

¿Qué convención debo utilizar?

La respuesta corta es: **debes usar convenciones diferentes para la base de datos y para la API, y dejar que tu aplicación se encargue de la traducción.**


---
### 1. Nomenclatura en el Schema de OAS (Cuerpo JSON)

Para los objetos y propiedades dentro de la especificación OpenAPI (es decir, lo que irá en los cuerpos de las peticiones y respuestas JSON), la convención estándar y **fuertemente recomendada es `camelCase`**.

- **Formato:** La primera palabra en minúscula, y la primera letra de cada palabra subsecuente en mayúscula.
    
- **Ejemplos:** `firstName`, `productOrder`, `createdAt`.
    

**¿Por qué `camelCase` y no `snake_case` (guion bajo)?**

El principal consumidor de APIs web es el ecosistema JavaScript (navegadores con frameworks como React, Angular, Vue, o servidores con Node.js). En JavaScript, la convención de facto para nombrar variables y propiedades de objetos es `camelCase`.

- **Si usas `camelCase` en tu API:** El desarrollador front-end puede acceder a los datos de forma natural: `const name = response.data.firstName;`
    
- **Si usas `snake_case` en tu API:** El acceso se vuelve incómodo y rompe con el estilo del lenguaje: `const name = response.data['first_name'];`
    

**¿Por qué NO `kebab-case` (guion medio)?**

El guion medio (`-`) **no es un carácter válido para nombres de propiedades en JavaScript** (y en la mayoría de los lenguajes) sin usar comillas. `objeto.mi-propiedad` es interpretado como `objeto.mi MENOS propiedad`, lo cual es un error de sintaxis. Por lo tanto, **nunca uses `kebab-case` para los nombres de los campos en tus schemas JSON.**

> **Conclusión para el Schema:** Tu intuición es parcialmente correcta. Se desaconseja el guion bajo (`snake_case`), pero la alternativa correcta no es el guion medio (`kebab-case`), sino **`camelCase`**.

### 2. La Relación entre el Schema (API) y la Entidad (BD)

Aquí está la clave de la pregunta. ¿Cómo mantienes la relación si la base de datos usa `snake_case` (ej. `first_name`) y la API usa `camelCase` (ej. `firstName`)?

La solución es una **capa de transformación (o mapeo)** en tu backend.

Tu aplicación (escrita en Java, Python, C#, Go, etc.) es la responsable de "traducir" los nombres entre la base de datos y la API. **No debes forzar a que la base de datos y la API usen la misma convención.**

- **Entrada (Request):** El backend recibe un JSON con `camelCase` y lo transforma a `snake_case` antes de guardarlo en la base de datos.
    
- **Salida (Response):** El backend lee los datos de la base de datos en `snake_case` y los transforma a `camelCase` antes de enviarlos como respuesta JSON.
    

Casi todos los frameworks modernos hacen esto de forma automática o con una configuración mínima:

- **Java (con Jackson):** Puedes configurar una `PropertyNamingStrategy` global para que haga la conversión automática.
    
- **Python (con Pydantic/FastAPI):** Puedes usar alias en los modelos: `first_name: str = Field(alias="firstName")`. O configurar el modelo para que la conversión sea automática.
    
- **C# (ASP.NET Core):** Las opciones de serialización de JSON se pueden configurar para que manejen esta conversión de forma predeterminada.
    
- **Ruby on Rails:** El serializador (como Active Model Serializers) maneja esto de forma nativa.
    

Este enfoque te da lo mejor de ambos mundos:

1. **Base de Datos Robusta:** Usas `snake_case`, la convención ideal para SQL.
    
2. **API Moderna y Ergonómica:** Usas `camelCase`, la convención ideal para los consumidores de la API.
    

### 3. Nomenclatura en las URLs (Endpoints)

Aquí es donde el **guion medio (`kebab-case`) sí es el rey**.

Para las rutas de tus recursos en la URL, las mejores prácticas son:

1. **Recursos en Plural:** Usa sustantivos en plural para identificar colecciones de recursos.
    
    - Bien: `/users`, `/product-orders`
        
    - Mal: `/user`, `/productOrder`
        
2. **Usa `kebab-case` para Recursos de Múltiples Palabras:** El guion medio es el separador de palabras estándar en las URLs. Es legible tanto para humanos como para los motores de búsqueda (SEO).
    
    - Bien: `/product-orders`
        
    - Mal: `/product_orders` (Google lo trata como una sola palabra)
        
    - Mal: `/productOrders` (Difícil de leer y no estándar)
        
3. **Parámetros de Ruta y Consulta:** Para mantener la consistencia con el cuerpo JSON, se recomienda usar `camelCase` para los parámetros.
    
    - **Parámetro de ruta:** `/users/{userId}/posts`
        
    - **Parámetro de consulta (query param):** `/products?sortBy=price&pageNumber=2`
        

---

### Resumen General: Guía Rápida

|Elemento|Convención Recomendada|Ejemplo|
|---|---|---|
|**BD (Tablas/Columnas)**|`snake_case`|`product_orders`, `first_name`|
|**API: Propiedades JSON**|`camelCase`|`firstName`, `productOrder`|
|**API: Recursos en URL**|plural y `kebab-case`|`/product-orders`|
|**API: Parámetros de Ruta**|`camelCase`|`.../{orderId}`|
|**API: Parámetros de Consulta**|`camelCase`|`?sortBy=price`|

### Ejemplo Completo en OpenAPI 3.1

Imagina una tabla `product_orders` con una columna `order_date`. La especificación para obtener un pedido específico se vería así:

YAML

```yaml
openapi: 3.1.0
info:
  title: Orders API
  version: 1.0.0

paths:
  /product-orders/{orderId}:
    get:
      summary: Get a specific product order
      parameters:
        - name: orderId
          in: path
          required: true
          schema:
            type: string
            format: uuid
      responses:
        '200':
          description: A product order object
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/ProductOrder'

components:
  schemas:
    ProductOrder:
      type: object
      properties:
        id:
          type: string
          format: uuid
        # La propiedad en la API es 'orderDate' (camelCase)
        orderDate:
          type: string
          format: date-time
        # ... otras propiedades en camelCase
```

En tu backend, el serializador se encargaría de mapear `orderDate` del JSON a la columna `order_date` de tu base de datos.