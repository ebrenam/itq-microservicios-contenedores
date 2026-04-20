# Prácticas de laboratorio - Unidad 3

## 📋 Información General

Las prácticas de la Unidad 3 están diseñadas para que los estudiantes implementen los microservicios diseñados en la Unidad 2, utilizando dos de los frameworks más importantes del ecosistema Java: Spring Boot y Quarkus. El objetivo es aplicar un enfoque API-First, generar código a partir de una especificación OpenAPI y comparar las diferencias en desarrollo, rendimiento y experiencia entre ambos frameworks.

---

## 🎯 Objetivos de las prácticas

1.  **Implementar microservicios** con Spring Boot y Quarkus siguiendo un enfoque API-First.
2.  **Generar código** (modelos) a partir de una especificación OpenAPI.
3.  **Comparar la arquitectura** y las anotaciones entre Spring Web MVC y JAX-RS (Quarkus).
4.  **Evaluar diferencias** en la experiencia de desarrollo, como el "live reload" de Quarkus.
5.  **Construir los componentes técnicos** que servirán de base para las siguientes unidades del proyecto final.

---

## 📚 Lista de prácticas

### [Práctica 3.1: Implementación con Spring Boot](01-creacion-proyecto-spring-boot.md)

-   **Objetivo:** Desarrollar un microservicio RESTful para el catálogo de productos utilizando **Spring Boot** y el enfoque API-First.
-   **Entregables:**
    -   Proyecto Spring Boot completo con el código generado desde OpenAPI.
    -   Controladores REST (`@RestController`) con validación de entradas.
    -   Capa de servicio (`@Service`) para la lógica de negocio.
    -   Documentación interactiva con Swagger UI.

### [Práctica 3.2: Implementación con Quarkus](02-creacion-proyecto-quarkus.md)

-   **Objetivo:** Reimplementar el mismo microservicio de catálogo de productos utilizando **Quarkus** para comparar el desarrollo, rendimiento y características Cloud-Native.
-   **Entregables:**
    -   Proyecto Quarkus completo con el código generado desde OpenAPI.
    -   Recursos JAX-RS (`@Path`) con inyección de dependencias (CDI).
    -   Capa de servicio (`@ApplicationScoped`).
    -   Análisis comparativo de la experiencia de desarrollo vs. Spring Boot.
