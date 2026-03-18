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
- **Establecer CI/CD** básico para microservicios
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
│   ├── oas-ecommerce-complete.yaml
│   └── oas-ecommerce-product.yaml
├── 03-actividades/        # Ejercicios prácticos
│   ├── practica-3-1-spring-boot.md
│   ├── practica-3-2-quarkus.md
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

### **[Práctica 3.1: Product Catalog API con Spring Boot](03-actividades/practica-3-1-spring-boot.md)**

**Objetivo:** Implementar sistema de catálogo de productos usando Spring Boot API-First

**Entregables:**

- Proyecto Spring Boot completo con OpenAPI
- Controladores REST con validación
- Capa de servicio y manejo de errores
- Documentación interactiva con Swagger UI

**Evaluación:** Actividades formativas complementarias

### **[Práctica 3.2: Product Catalog API con Quarkus](03-actividades/practica-3-2-quarkus.md)**

**Objetivo:** Reimplementar el mismo sistema de catálogo de productos usando Quarkus y JAX-RS

**Entregables:**

- Proyecto Quarkus con generación de código OpenAPI
- Resources JAX-RS con CDI
- Testing automatizado y métricas
- Comparativo de rendimiento vs Spring Boot

**Evaluación:** Actividades formativas complementarias

---

## 🔗 Conexión con otras unidades

### **Prerrequisitos (Unidades 1-2)**

- ✅ Conceptos de microservicios y arquitecturas distribuidas
- ✅ Domain-Driven Design y modelado de dominios
- ✅ Diseño de APIs REST y especificaciones OpenAPI
- ✅ Patrones de integración entre servicios

## 🔗 Conexión con el proyecto final

Esta unidad proporciona la **implementación técnica** de los microservicios diseñados en unidades anteriores:

### **Preparación para Unidad 4 (Resiliencia)**

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

---

**Preparado por:** Profesor del Curso
**Fecha:** Diciembre 2025
**Versión:** 1.0

---

**Navegación:**

- ← [Unidad 2: Diseño y Modelado](../unidad-2-diseno/README.md)
- → [Unidad 4: Resiliencia y Fault Tolerance](../unidad-4-resiliencia/README.md)
- ↑ [Índice General del Curso](../README.md)
