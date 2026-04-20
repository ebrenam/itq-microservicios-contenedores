# Unidad 3: Implementación de microservicios con Spring Boot y Quarkus

## 🎯 Objetivos de aprendizaje

Al completar esta unidad, el estudiante será capaz de:

### **1. Implementación con Spring Boot**

- **Crear proyectos** de microservicios con Spring Boot usando enfoque API-First
- **Generar código** a partir de especificaciones OpenAPI/Swagger
- **Implementar controladores REST** siguiendo las mejores prácticas de Spring
- **Configurar validación** y manejo de errores robusto

### **2. Implementación con Quarkus**

- **Desarrollar microservicios** con Quarkus para aplicaciones nativas en la nube
- **Utilizar JAX-RS** y CDI para arquitecturas reactivas y eficientes
- **Optimizar tiempo de arranque** y consumo de memoria
- **Comparar rendimiento** entre diferentes frameworks

### **3. Integración y Testing**

- **Implementar testing** de APIs con herramientas automatizadas
- **Configurar observabilidad** con métricas, logs y trazas distribuidas
- **Documentar APIs** interactivas con Swagger UI

---

## 📚 Estructura del contenido

```text
unidad-3-implementacion/
├── 01-teoria/             # Fundamentos teóricos
│   ├── 01-microservices.md    # Fundamentos y arquitectura
│   ├── 02-spring-boot.md      # Teoría Spring Boot
│   └── 03-quarkus.md          # Teoría Quarkus
├── 02-recursos/           # Material complementario
│   ├── 00-docker.md
│   ├── 01-poo-microservices.md
│   ├── 02-annotations.md
│   ├── 03-beans.md
│   ├── 04-java-bean.md
│   ├── 05-pojo-java-bean-spring-bean.md
│   ├── 06-slf4j-java-util-logging.md
│   ├── 07-maven.md
│   ├── 08-maven-vs-gradle.md
│   ├── maven.png
│   ├── oas-ecommerce-complete.yaml
│   └── oas-ecommerce-product.yaml
├── 03-actividades/        # Ejercicios prácticos
│   ├── 01-creacion-proyecto-spring-boot.md
│   ├── 02-creacion-proyecto-quarkus.md
│   └── README.md
└── README.md                 # Esta vista general
```

---

### 📖 Teoría

### [Tema 3.1: Fundamentos de implementación](01-teoria/01-microservices.md)

- **Enfoque API-First vs Code-First** - Ventajas y desventajas
- **Generación de código** desde OpenAPI - Automatización y consistencia
- **Arquitectura de capas** en microservicios - Controller, Service, Repository
- **Inyección de dependencias** - Spring vs CDI

### [Tema 3.2: Spring Boot para microservicios](01-teoria/02-spring-boot.md)

- **Spring Boot Starters** para microservicios - Web, Validation, Data
- **Spring Web MVC** - Controladores REST y anotaciones
- **Spring Boot Actuator** - Health checks, métricas y monitoreo
- **Configuration management** - application.properties y profiles

### [Tema 3.3: Quarkus para cloud-native](01-teoria/03-quarkus.md)

- **Quarkus fundamentals** - supersonic, subatomic Java
- **JAX-RS vs Spring MVC** - Comparación de enfoques
- **CDI (Contexts and Dependency Injection)** - Gestión de beans
- **Native compilation** - GraalVM y optimización de recursos

### **Tema 3.4: Testing y observabilidad**

- **Testing de APIs** - unit, integration y contract testing
- **OpenAPI testing** - automatización con especificaciones
- **Logging estructurado** - JSON logging y correlación de trazas
- **Métricas de aplicación** - Prometheus, Micrometer


---

## 🛠️ Prácticas de laboratorio

### **[Práctica 3.1: Product Catalog API con Spring Boot](03-actividades/01-creacion-proyecto-spring-boot.md)**

**Objetivo:** Implementar sistema de catálogo de productos usando Spring Boot API-First

**Entregables:**

- Proyecto Spring Boot completo con OpenAPI
- Controladores REST con validación
- Capa de servicio y manejo de errores

### **[Práctica 3.2: Product Catalog API con Quarkus](03-actividades/02-creacion-proyecto-quarkus.md)**

**Objetivo:** Reimplementar el mismo sistema de catálogo de productos usando Quarkus y JAX-RS

- Proyecto Quarkus con generación de código OpenAPI
- Resources JAX-RS con CDI

---

## 🔗 Conexión con otras unidades

### **Prerrequisitos (Unidades 1-2)**

- ✅ Conceptos de microservicios y arquitecturas distribuidas
- ✅ Domain-Driven Design y modelado de dominios
- ✅ Diseño de APIs REST y especificaciones OpenAPI
- ✅ Patrones de integración entre servicios

## 🔗 Conexión con el proyecto final

Esta unidad proporciona la **implementación técnica** de los microservicios diseñados en unidades anteriores:

### **Preparación para Unidad 4 (Resiliencia y Observabilidad)**

- 🎯 **Servicios implementados** listos para patrones de resiliencia
- 🎯 **Métricas y observabilidad** base para circuit breakers
- 🎯 **Testing automatizado** para validar comportamientos resilientes
- 🎯 **Múltiples frameworks** para comparar estrategias de fault tolerance

### **Contribución al proyecto final**

- 🚀 **Implementación de microservicios** para plataforma de ingesta de datos
- 🚀 **APIs REST** para recepción y procesamiento de datos
- 🚀 **Selección de Framework** basado en análisis de rendimiento
- 🚀 **Estrategias de pruebas** para garantizar calidad en producción

---

## 🚀 Tecnologías y herramientas

### **Frameworks principales**

- **Spring Boot 3.2+** - Framework empresarial maduro
- **Quarkus 3.6+** - Framework cloud-native optimizado

### **Herramientas de desarrollo**

- **Maven/Gradle** - Build tools y dependency management
- **OpenAPI Generator** - Generación automática de código
- **Swagger UI** - Documentación interactiva de APIs
- **JUnit 5** - Testing framework

### **Observabilidad y testing**

- **Spring Boot Actuator** / **Quarkus Micrometer** - Métricas
- **Postman/Newman** - API testing automatizado
- **JMeter** - Performance testing
- **SLF4J/Logback** - Logging estructurado

### **Herramientas de productividad**

- **IntelliJ IDEA** / **VS Code** - IDEs con soporte completo
- **Docker** - Containerización para desarrollo
- **Git** - Control de versiones y colaboración

---

## � Material de Apoyo y Referencias

### **Libros Recomendados**

#### **Spring Boot**
1. **"Spring Boot in Action"** - Craig Walls (2016)
   - Referencia completa de Spring Boot con ejemplos prácticos
   - Cobertura de integración, testing y deployment
   - Disponible en Amazon, O'Reilly, editorial Prentice Hall

2. **"Spring Microservices in Action"** - John Carnell & Illary Huaylupo (2ª edición, 2021)
   - Patrones y prácticas para microservicios con Spring Boot
   - Incluye Service Discovery, Load Balancing, Configuration
   - Editorial Manning

3. **"Mastering Spring Cloud"** - Piotr Mińkowski (2ª edición, 2019)
   - Spring Cloud para arquitecturas distribuidas
   - Cloud-native patterns con Spring
   - Editorial Packt Publishing

#### **Quarkus**
1. **"Quarkus in Action"** - Jason Porter & Daniel Oh (2023)
   - Guía completa de Quarkus desde lo básico
   - Cloud-native Java applications
   - Editorial Manning

2. **"Building Microservices with Quarkus"** - Alex Soto & Jason Porter (2023)
   - Patrones específicos para Quarkus
   - Performance optimization y native compilation
   - O'Reilly

#### **APIs REST y OpenAPI**
1. **"RESTful API Design Rulebook"** - Mark Masse (2011)
   - Principios fundamentales de diseño REST
   - Mejores prácticas y anti-patterns
   - Editorial O'Reilly

2. **"Designing APIs with Swagger and OpenAPI"** - Josh Ponelat & Lukas Rosenstock (2020)
   - Especificación OpenAPI 3.0
   - Tools y generación de código
   - Editorial Manning

### **Cursos en Línea Recomendados**

#### **Spring Boot (Video tutoriales)**
- **Udemy**: "Spring Boot Microservices" - Bharath Thippireddy
  - Tiempo: 15+ horas | Nivel: Intermedio | Lenguaje: Inglés
  - URL: https://www.udemy.com/course/microservices-with-spring-boot-and-spring-cloud/

- **Coursera**: "Microservices Architecture" - IBM
  - Tiempo: 10 horas | Nivel: Intermedio | Acceso: Auditoria gratuita disponible
  - URL: https://www.coursera.org/learn/microservices-architecture

- **YouTube**: "Spring Boot Tutorial" - telusko
  - Playlist completa de Spring Boot
  - URL: https://www.youtube.com/playlist?list=PLsyeobzWxl7rJFbKPrFsPREMqxME0sI7b

#### **Quarkus (Video tutoriales)**
- **Red Hat Developers**: "Getting Started with Quarkus" (Official)
  - Contenido oficial en YouTube
  - URL: https://www.youtube.com/watch?v=DXNfRr3lJYo

- **YouTube**: "Quarkus Framework Tutorial" - Code Decode
  - Introducción práctica a Quarkus
  - URL: https://www.youtube.com/watch?v=iHFUIqj_A7o

- **Linux Academy / A Cloud Guru**: "Quarkus Mastery"
  - Nivel: Intermedio a Avanzado
  - Con laboratorios prácticos

#### **API-First Development**
- **Postman Learning Center**: "API Fundamentals"
  - Acceso gratuito, tutoriales interactivos
  - URL: https://learning.postman.com/docs/getting-started/introduction/

- **OpenAPI Initiative**: "OpenAPI Documentation"
  - Documentación oficial y ejemplos
  - URL: https://www.openapis.org/

### **Documentación Oficial**

#### **Spring Boot**
- [Spring Boot Official Documentation](https://spring.io/projects/spring-boot)
- [Spring Web MVC Documentation](https://docs.spring.io/spring-framework/reference/web/webmvc.html)
- [Spring Boot Actuator](https://spring.io/guides/gs/actuator-service/)

#### **Quarkus**
- [Quarkus Official Guide](https://quarkus.io/guides/)
- [Quarkus API Reference](https://quarkus.io/api/)
- [JAX-RS with Quarkus](https://quarkus.io/guides/rest-json)

#### **OpenAPI y Swagger**
- [OpenAPI 3.0 Specification](https://spec.openapis.org/oas/v3.0.3)
- [Swagger Editor](https://editor.swagger.io/)
- [OpenAPI Generator](https://openapi-generator.tech/)

### **Herramientas Online**

1. **Swagger Editor** - https://editor.swagger.io/
   - Editor visual para especificaciones OpenAPI
   - Preview en tiempo real

2. **OpenAPI Generator** - https://start.openapi-generator.tech/
   - Generador de código desde especificaciones

3. **Postman** - https://www.postman.com/
   - Testing de APIs
   - Colecciones de ejemplos

4. **GitHub Copilot** - https://github.com/features/copilot
   - Asistencia en codificación
   - Sugerencias contextuales

### **Blogs y Artículos Técnicos**

- **Spring Blog**: https://spring.io/blog
- **Baeldung** (Spring & Java): https://www.baeldung.com/
- **DZone** (Microservices): https://dzone.com/
- **RedHat Developer** (Quarkus): https://developers.redhat.com/products/quarkus

### **Repositorios de Referencia en GitHub**

- **Spring Boot Examples**: https://github.com/spring-projects/spring-boot/tree/main/spring-boot-samples
- **Quarkus Examples**: https://github.com/quarkusio/quarkus-quickstarts
- **OpenAPI Generator Examples**: https://github.com/OpenAPITools/openapi-generator/tree/master/samples

### **Comunidades y Foros**

- **Stack Overflow**
  - Tags: `spring-boot`, `quarkus`, `openapi`, `java-microservices`
  
- **Reddit**
  - r/java, r/springframework, r/microservices
  
- **Spring Community** - https://spring.io/community
  
- **Quarkus Community** - https://quarkus.io/community/

---

**Anterior:** [← Unidad 2: Diseño](../unidad-2-diseno/README.md) | **Siguiente:** [Unidad 4: Contenedores →](../unidad-4-contenedores/README.md)
