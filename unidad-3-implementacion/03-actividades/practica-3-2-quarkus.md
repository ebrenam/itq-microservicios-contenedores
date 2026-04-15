# Creación de Proyecto OAS - Quarkus

> **Objetivo:** Implementar el mismo sistema de catálogo de productos usando Quarkus para comparar frameworks y analizar diferencias en desarrollo, rendimiento y deployment.

## 📚 **Prerrequisitos**

- ✅ Práctica 3.1 (Spring Boot) completada
- ✅ Java 25+ instalado
- ✅ Maven 3.8+ configurado
- ✅ Docker Desktop (para native builds)
- ✅ GraalVM (opcional, para desarrollo nativo)

---

## 🎯 **Objetivos de aprendizaje**

Al completar esta práctica, serás capaz de:

- ✅ **Migrar** aplicaciones Spring Boot a Quarkus
- ✅ **Comparar** frameworks de microservicios
- ✅ **Implementar** APIs REST con JAX-RS
- ✅ **Configurar** persistencia con Hibernate Panache
- ✅ **Generar** native images con GraalVM
- ✅ **Evaluar** rendimiento y resource utilization
- ✅ **Decidir** cuándo usar cada framework

---

## 🚀 Paso 1: Crear el Proyecto en `code.quarkus.io`

Generaremos la estructura base del proyecto.

1. Ve a [code.quarkus.io](https://code.quarkus.io/).

2. Configura tu proyecto:

    - **Build Tool:** Maven
    - **Group ID:** `com.ejemplo.api`
    - **Artifact ID:** `api-rest`
    - **Java Version:** `25`

3. **Añadir Extensiones (Dependencias):** Busca y agrega las siguientes extensiones esenciales:

    - **REST:** Implementación de Jakarta REST que utiliza procesamiento en tiempo de compilación y Vert.x. Esta extensión no es compatible con la extensión quarkus-resteasy ni con ninguna de las extensiones que dependen de ella.

    - **Hibernate Validator:** Para usar las anotaciones de validación (ej. `@Valid`, `@NotNull`) que se generarán en los modelos.

4. Haz clic en **"Generate your application"** y luego en **"Download as zip"**.

5. Descomprime el archivo y abre el proyecto en tu IDE (IntelliJ, Eclipse, VSCode).

---

## 📦 Paso 2: Estructura de Paquetes y OAS

La organización es fundamental.

1. **Colocar el OAS:** Dentro de la carpeta `src/main/resources`, crea una nueva carpeta llamada `api`. Copia tu archivo (ej. `openapi.yaml`) dentro de ella.

    - Ruta final: `src/main/resources/api/openapi.yaml`

2. **Verificar Paquetes:** En `src/main/java`, ya tendrás tu paquete base (ej. `com.ejemplo.api`). Dentro de este, crea los siguientes sub-paquetes:

    - `com.ejemplo.api.resource` (Para nuestros "Resources", el equivalente a Controllers en Quarkus/JAX-RS)

    - `com.ejemplo.api.model` (Aquí moveremos los modelos generados)

    - `com.ejemplo.api.service` (Para la lógica de negocio)

Tu estructura debería verse así:

```text
api-rest/
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── com/ejemplo/api/
│   │   │       ├── resource/
│   │   │       ├── model/
│   │   │       └── service/
│   │   └── resources/
│   │       ├── api/
│   │       │   └── openapi.yaml  <-- Tu archivo OAS aquí
│   │       └── application.properties
└── pom.xml
```

---

## ⚙️ Paso 3: Configurar `pom.xml` para Generar Modelos

Usaremos el mismo plugin de Maven que en el ejemplo de Spring, pero lo configuraremos para que genere código compatible con JAX-RS (el estándar que usa Quarkus) en lugar de Spring MVC.

Abre tu archivo `pom.xml`.

1. **Agregar propiedades para OpenAPI Generator:** En la sección `<properties>`, después de la línea `<surefire-plugin.version>3.5.4</surefire-plugin.version>`, agrega.

    ```xml  
            <openapi-generator-maven-plugin.version>7.1.0</openapi-generator-maven-plugin.version>
            <javax.validation-api.version>2.0.1.Final</javax.validation-api.version>
    ```


2. **Añadir Dependencias que faltaron:** Asegúrate de tener estas dependencias dentro de la etiqueta `<dependencies>`:

    ```xml  
            <!-- OpenAPI Generator dependencies para modelos -->
            <dependency>
                <groupId>javax.validation</groupId>
                <artifactId>validation-api</artifactId>
                <version>${javax.validation-api.version}</version>
            </dependency>

            <dependency>
                <groupId>io.swagger.core.v3</groupId>
                <artifactId>swagger-annotations</artifactId>
                <version>2.2.16</version>
            </dependency>
            
            <dependency>
                <groupId>io.quarkus</groupId>
                <artifactId>quarkus-rest-jackson</artifactId>
            </dependency>
    ```

3. **Añadir el Plugin Generador:** En la sección `<plugins>` dentro de `<build>`, después del plugin `maven-compiler-plugin`, agrega:

    ```xml
                <plugin>
                    <groupId>org.openapitools</groupId>
                    <artifactId>openapi-generator-maven-plugin</artifactId>
                    <version>${openapi-generator-maven-plugin.version}</version>
                    <executions>
                        <execution>
                            <goals>
                                <goal>generate</goal>
                            </goals>
                            <configuration>
                                <inputSpec>${project.basedir}/src/main/resources/api/openapi.yaml</inputSpec>
                                <generatorName>java</generatorName>
                                <library>native</library>
                                <output>${project.build.directory}/generated-sources/openapi</output>
                                <modelPackage>com.ejemplo.api.model</modelPackage>
                                <generateApis>false</generateApis>
                                <generateApiTests>false</generateApiTests>
                                <generateApiDocumentation>false</generateApiDocumentation>
                                <generateModels>true</generateModels>
                                <generateModelTests>false</generateModelTests>
                                <generateModelDocumentation>false</generateModelDocumentation>
                                <generateSupportingFiles>false</generateSupportingFiles>
        
                                <configOptions>
                                    <sourceFolder>src/main/java</sourceFolder>
                                    <dateLibrary>java8</dateLibrary>
                                    <useBeanValidation>true</useBeanValidation>
                                    <performBeanValidation>true</performBeanValidation>
                                    <useJakartaEe>true</useJakartaEe>
                                    <serializationLibrary>jackson</serializationLibrary>
                                    <openApiNullable>false</openApiNullable>
                                </configOptions>
                            </configuration>
                        </execution>
                    </executions>
                </plugin>     

                <plugin>
                    <groupId>org.codehaus.mojo</groupId>
                    <artifactId>build-helper-maven-plugin</artifactId>
                    <version>3.4.0</version>
                    <executions>
                        <execution>
                            <id>add-source</id>
                            <phase>generate-sources</phase>
                            <goals>
                                <goal>add-source</goal>
                            </goals>
                            <configuration>
                                <sources>
                                    <source>${project.build.directory}/generated-sources/openapi/src/main/java</source>
                                </sources>
                            </configuration>
                        </execution>
                    </executions>
                </plugin>
    ```

## ☕ Paso 4: Generar y Mover los Modelos

Este paso es idéntico al de Spring.

1. **Ejecutar Maven:** Abre una terminal en la raíz de tu proyecto y ejecuta:

    ```bash
    mvn clean compile
    ```

    (O usa la interfaz gráfica de tu IDE).

2. **Verificar Archivos Generados:** Los archivos aparecerán en: `target/generated-sources/openapi/src/main/java/com/ejemplo/api/model`

3. **Desactivar generación de modelos:** Comentar el plugin que permite generar los modelos.

4. **Mover los Modelos:**

    - Copia todos los archivos `.java` de ese directorio (`Product.java`, `ProductList.java`, `ApiError.java`, etc.).

    - Pégalos en tu paquete de código fuente: `src/main/java/com/ejemplo/api/model`

Ahora tu proyecto Quarkus reconoce las clases del modelo.

---

## ➡️ Paso 5: Crear el Resource (Lógica del API)

En JAX-RS (Quarkus), los _Controllers_ se llaman _Resources_. Usan anotaciones diferentes a Spring.

Supongamos que tu OAS define `POST /products` y `GET /products/{id}`.

1. **Crear la Clase Resource:** En `com.ejemplo.api.resource`, crea una nueva clase Java, `ProductResource.java`.

2. **Añadir Anotaciones JAX-RS:**

    - `@Path("/api/v1")`: Define el prefijo base para todas las rutas en esta clase.

    - `@Produces(MediaType.APPLICATION_JSON)`: Indica que, por defecto, los métodos _devuelven_ JSON.

    - `@Consumes(MediaType.APPLICATION_JSON)`: Indica que, por defecto, los métodos _reciben_ JSON.

    - Importa `jakarta.ws.rs.*` para estas anotaciones.

    ```java
    package com.ejemplo.api.resource;

    import com.ejemplo.api.model.Category; // Importa el modelo generado para recibir datos
    import com.ejemplo.api.model.Product; // Importa el modelo generado para recibir datos
    import com.ejemplo.api.model.ProductResponse; // Importa el modelo generado para responder

    import jakarta.validation.Valid;
    import jakarta.ws.rs.Consumes;
    import jakarta.ws.rs.GET;
    import jakarta.ws.rs.POST;
    import jakarta.ws.rs.Path;
    import jakarta.ws.rs.PathParam;
    import jakarta.ws.rs.Produces;
    import jakarta.ws.rs.core.MediaType;
    import jakarta.ws.rs.core.Response;

    @Path("/api/v1") // Prefijo base de la API
    @Produces(MediaType.APPLICATION_JSON)
    @Consumes(MediaType.APPLICATION_JSON)
    public class ProductResource {

        // ... aquí irán los métodos
    }
    ```

3. **Implementar los Endpoints (Métodos):**

    - Usamos `@POST` y `@GET`.

    - Usamos `@Path` en el método para la sub-ruta.

    - `@Valid`: Activa la validación (igual que en Spring).

    - `@PathParam`: Se usa para capturar variables de la URL (en lugar de `@PathVariable`).

    - **Importante:** En JAX-RS, no se necesita `@RequestBody`. Si un método POST/PUT recibe un POJO, Quarkus automáticamente intenta deserializarlo desde el cuerpo.

    - **Retorno:** El estándar de JAX-RS usa `Response` para tener control total del código HTTP.

    ```java
        // ... dentro de la clase ProductResource ...
        
        @POST
        @Path("/products")
        public Response createProduct(@Valid Product productRequest)
        {
            // Por ahora, solo simularemos que lo guardamos
            System.out.println("Resource - Product recibido: " + productRequest.getName());

            // Simulamos que la DB le persiste la información
            ProductResponse productResponse = new ProductResponse();
            productResponse.setId("prod-12345");
            productResponse.setName(productRequest.getName());
            productResponse.setDescription(productRequest.getDescription());
            productResponse.setPrice(productRequest.getPrice());
            productResponse.setCategory(productRequest.getCategory());
            productResponse.setInStock(true);
            productResponse.setSku("LAP-GAM-001");
            productResponse.setCreatedAt(java.time.OffsetDateTime.now());
            productResponse.setUpdatedAt(java.time.OffsetDateTime.now());

            System.out.println("Resource - Product creado: " + productResponse.getName());

            // Devolvemos la respuesta de confirmación con código 201 (CREATED)
            // La sintaxis de JAX-RS es un poco diferente
            return Response.status(Response.Status.CREATED).entity(productResponse).build();
        }
        
        @GET
        @Path("/products/{productId}")
        public Response getProductById(@PathParam("productId") Integer productId) // <-- Nota el @PathParam
        {
            System.out.println("Resource - Buscando Product con ID: " + productId);

            // Validación básica del ID
            if (productId == null || productId < 1 || productId > 999999) {
                return Response.status(Response.Status.NOT_FOUND).build();
            }

            // Simulamos buscar la reserva en la base de datos
            // En un caso real, aquí harías: productService.findById(productId)

            // Simulamos que encontramos la reserva
            ProductResponse productResponse = new ProductResponse();
            productResponse.setId("prod-12345");
            productResponse.setName("Laptop Gamer");
            productResponse.setDescription("Una laptop para gaming");
            productResponse.setPrice(1500.00);
            productResponse.setCategory(Category.ELECTRONICS);
            productResponse.setInStock(true);
            productResponse.setSku("LAP-GAM-001");
            productResponse.setCreatedAt(null);
            productResponse.setUpdatedAt(null);
        
            // Devolvemos el reservation con código 200 (OK)
            return Response.ok(productResponse).build();
        }
    ```

---

## 🛠️ Paso 6: Añadir Capa de Servicio

La lógica de negocio debe estar separada. En Quarkus, esto se hace con CDI (Contexts and Dependency Injection).

1. **Crear `ProductService`:** En `com.ejemplo.api.service`, crea `ProductService.java`.

2. **Anotar con `@ApplicationScoped`:** Esta es la anotación estándar de CDI (equivalente a `@Service` en Spring) para crear un "bean" que vive durante toda la aplicación.

    ```java
    package com.ejemplo.api.service;

    import java.time.OffsetDateTime;
    import java.util.UUID;

    import com.ejemplo.api.model.Category;
    import com.ejemplo.api.model.Product;
    import com.ejemplo.api.model.ProductResponse;

    import jakarta.enterprise.context.ApplicationScoped; // <-- Importante

    @ApplicationScoped // Le dice a Quarkus que gestione esta clase como un servicio
    public class ProductService {

        public ProductResponse createProduct(Product product)
        {
            System.out.println("Service - Product recibido: " + product.getName());

            // Simulamos la persistencia y generación de datos del sistema
            ProductResponse response = new ProductResponse();
            
            // Mapeo de campos desde el Request
            response.setName(product.getName());
            response.setPrice(product.getPrice());
            response.setCategory(product.getCategory());
            response.setDescription(product.getDescription());
            response.setInStock(product.getInStock());

            // Datos generados por el servidor (conforme al OAS)
            response.setId("prod-" + System.currentTimeMillis());
            response.setSku("SKU-" + UUID.randomUUID().toString().substring(0, 8).toUpperCase());
            response.setCreatedAt(OffsetDateTime.now());
            response.setUpdatedAt(OffsetDateTime.now());

            return response;
        }

        public ProductResponse getProductById(String productId) 
        {
            System.out.println("Service - Buscando Product con ID: " + productId);

            // Simulación de búsqueda en base de datos
            ProductResponse response = new ProductResponse();
            response.setId(productId);
            response.setName("Producto de Ejemplo");
            response.setPrice(99.99);
            response.setCategory(Category.ELECTRONICS);
            response.setSku("LAP-GAM-001");
            response.setCreatedAt(OffsetDateTime.now());
            response.setInStock(true);
            
            return response;
        }
    }
    ```

3. **Usar el Service en el Resource:** Modifica tu `ProductResource` para "inyectar" el servicio.

    - En CDI (Quarkus), usamos `@Inject` (de `jakarta.inject.Inject`) en lugar de `@Autowired`.

    ```java
    package com.ejemplo.api.resource;

    import java.time.OffsetDateTime;
    import java.util.HashMap;
    import java.util.Map;

    import com.ejemplo.api.model.ApiError;
    import com.ejemplo.api.model.Category; // Importa el modelo generado para recibir datos
    import com.ejemplo.api.model.Product; // Importa el modelo generado para recibir datos
    import com.ejemplo.api.model.ProductResponse; // Importa el modelo generado para responder
    import com.ejemplo.api.service.ProductService;

    import jakarta.inject.Inject;
    import jakarta.validation.Valid;
    import jakarta.ws.rs.Consumes;
    import jakarta.ws.rs.GET;
    import jakarta.ws.rs.POST;
    import jakarta.ws.rs.Path;
    import jakarta.ws.rs.PathParam;
    import jakarta.ws.rs.Produces;
    import jakarta.ws.rs.core.MediaType;
    import jakarta.ws.rs.core.Response;

    @Path("/api/v1") // Prefijo base de la API
    @Produces(MediaType.APPLICATION_JSON)
    @Consumes(MediaType.APPLICATION_JSON)
    public class ProductResource {

        // Inyección de dependencias con CDI
        @Inject
        ProductService productService; // <-- Inyecta el servicio
        
        @POST
        @Path("/products")
        public Response createProduct(@Valid Product productRequest)
        {
            // Por ahora, solo simularemos que lo guardamos
            System.out.println("Resource - Product recibido: " + productRequest.getName());

            // El resource delega la lógica al service
            ProductResponse productResponse = productService.createProduct(productRequest);

            // Devolvemos la respuesta de confirmación con código 201 (CREATED)
            // La sintaxis de JAX-RS es un poco diferente
            return Response.status(Response.Status.CREATED).entity(productResponse).build();
        }

        @GET
        @Path("/products/{productId}")
        public Response getProductById(@PathParam("productId") Integer productId) // <-- Nota el @PathParam
        {
            System.out.println("Resource - Buscando Product con ID: " + productId);

            // Validación básica del ID
            if (productId == null || productId < 1 || productId > 999999) {
                ApiError errorResponse = new ApiError();
                errorResponse.setCode(ApiError.CodeEnum.INVALID_INPUT);
                errorResponse.setMessage("Invalid product ID");
                errorResponse.setTimestamp(OffsetDateTime.now());
                errorResponse.setPath("/products/{productId}");

                Map<String, Object> details = new HashMap<>();
                details.put("info", "El valor proporcionado no es correcto, debe estar entre 1 y 999999");
                errorResponse.setDetails(details);
                
                return Response.status(Response.Status.BAD_REQUEST).entity(errorResponse).build();
            }

            // El resource delega la lógica al service
            ProductResponse productResponse = productService.getProductById(productId.toString()); 
            
            // Devolvemos el reservation con código 200 (OK)
            return Response.ok(productResponse).build();
        }
    }
    ```

---

## 🛠️ Paso 7: Configuración de Rendimiento y Observabilidad

Agrega estas dependencias en tu `pom.xml` dentro de la sección `<dependencies>`:

    ```xml
            <dependency>
                <groupId>io.quarkus</groupId>
                <artifactId>quarkus-smallrye-health</artifactId>
            </dependency>
            <dependency>
                <groupId>io.quarkus</groupId>
                <artifactId>quarkus-micrometer-registry-prometheus</artifactId>
            </dependency>
    ```

En `src/main/resources/application.properties` configura la observabilidad y algunos parámetros básicos del servidor.

    ```properties
    # Observabilidad: Health checks y métricas en Quarkus
    quarkus.smallrye-health.enabled=true
    quarkus.smallrye-health.root-path=/q/health
    quarkus.micrometer.enabled=true
    quarkus.micrometer.export.prometheus.enabled=true
    quarkus.micrometer.export.prometheus.path=/metrics

    # Parámetros básicos del servidor
    quarkus.http.host=0.0.0.0
    quarkus.http.port=8080

    # Establecer el tiempo de espera de inactividad a 30 segundos
    quarkus.http.idle-timeout=30S
    ```

Ahora puedes revisar el estado del servicio y las métricas:

- Health: `curl http://localhost:8080/q/health`
- Métricas: `curl http://localhost:8080/metrics`

Estas rutas son el equivalente Quarkus de los endpoints de Spring Boot Actuator y te permiten validar que la aplicación está en línea y qué métricas básicas tiene.

---

## 🧪 Paso 8: Probar con Postman

Quarkus brilla por su _live reload_.

1. **Ejecutar la Aplicación (Modo Desarrollo):** Abre una terminal en la raíz del proyecto y ejecuta:

    ```bash
    mvn quarkus:dev
    ```

    Verás el logo de Quarkus. ¡No cierres esta terminal! Quarkus recargará automáticamente los cambios que hagas en el código.

2. **Abrir Postman.**

3. **Probar el `POST /products`:**

    - **Método:** `POST`

    - **URL:** `http://localhost:8080/api/v1/products` (Quarkus usa el puerto 8080 por defecto).

    - **Pestaña "Body"**:

        - Selecciona `raw` y `JSON`.

        - Escribe el JSON de tu reservation (¡los nombres deben coincidir con tu modelo!).

        ```json
        {
            "name": "Laptop Gaming",
            "price": 1299.99,
            "category": "BOOKS",
            "description": "Laptop de alto rendimiento para gaming",
            "inStock": true
        }
        ```

    - **¡Enviar!** Debes recibir una respuesta `201 Created` con el JSON de respuesta.

        ```json
        {
            "name": "Laptop Gaming",
            "price": 1299.99,
            "category": "BOOKS",
            "inStock": true,
            "id": "prod-1774315603200",
            "sku": "SKU-4920627E",
            "createdAt": "2026-03-23T19:26:43.202419-06:00",
            "description": "Laptop de alto rendimiento para gaming",
            "updatedAt": "2026-03-23T19:26:43.202465-06:00"
        }
        ```

5. **Probar el `GET /products/{id}`:**

    - **Método:** `GET`

    - **URL:** `http://localhost:8080/api/v1/products/1` (o el ID que quieras probar).

    - **¡Enviar!** Deberías recibir una respuesta `200 OK` con el JSON de respuesta.
        ```json
        {
            "name": "Producto de Ejemplo",
            "price": 99.99,
            "category": "ELECTRONICS",
            "inStock": true,
            "id": "1",
            "sku": "LAP-GAM-001",
            "createdAt": "2026-03-23T19:30:36.518198-06:00",
            "description": null,
            "updatedAt": null
        }
        ```
