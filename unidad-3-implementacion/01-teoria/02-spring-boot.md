# Fundamentos teóricos para el desarrollo de microservicios REST con Spring Boot y Java

- [Fundamentos teóricos para el desarrollo de microservicios REST con Spring Boot y Java](#fundamentos-teóricos-para-el-desarrollo-de-microservicios-rest-con-spring-boot-y-java)
  - [📋 Introducción](#-introducción)
  - [1. 🌐 Ecosistema y Setup](#1--ecosistema-y-setup)
    - [¿Qué es Spring Boot?](#qué-es-spring-boot)
    - [El Rol de Maven como Gestor de Dependencias](#el-rol-de-maven-como-gestor-de-dependencias)
    - [Flujo Inicial con Spring Initializr](#flujo-inicial-con-spring-initializr)
  - [2. 🏗️ Arquitectura Multicapa (Teoría)](#2-️-arquitectura-multicapa-teoría)
    - [Capa de Presentación/API (Controller)](#capa-de-presentaciónapi-controller)
    - [Capa de Negocio (Service)](#capa-de-negocio-service)
    - [Capa de Persistencia (Model/Entity)](#capa-de-persistencia-modelentity)
  - [3. ☕ Java 25 y la Modernización del Lenguaje](#3--java-25-y-la-modernización-del-lenguaje)
    - [Clase Tradicional (POJO)](#clase-tradicional-pojo)
    - [Java Record (Estándar moderno en Java 25)](#java-record-estándar-moderno-en-java-25)
    - [Diferencias principales](#diferencias-principales)
    - [¿Por qué enfocarnos en clases tradicionales?](#por-qué-enfocarnos-en-clases-tradicionales)
  - [4. 💾 Persistencia con JPA](#4--persistencia-con-jpa)
    - [Concepto de ORM (Object-Relational Mapping)](#concepto-de-orm-object-relational-mapping)
    - [Spring Data JPA: Abstracción de Consultas](#spring-data-jpa-abstracción-de-consultas)
  - [5. 📋 Referencia de Anotaciones](#5--referencia-de-anotaciones)
  - [🎓 Conclusión](#-conclusión)

---

## 📋 Introducción

Este módulo teórico establece las bases conceptuales para comprender Spring Boot como herramienta principal en el desarrollo de microservicios REST. Nos enfocaremos en los principios arquitectónicos, la evolución de Java y las abstracciones que facilitan la persistencia de datos. El objetivo es proporcionar una comprensión sólida antes de pasar a la implementación práctica.

---

## 1. 🌐 Ecosistema y Setup

### ¿Qué es Spring Boot?

Spring Boot es un framework de Java que simplifica la creación de aplicaciones standalone y listas para producción. Forma parte del ecosistema Spring, pero elimina la configuración manual compleja mediante "convenciones sobre configuración". En el contexto de microservicios REST, Spring Boot permite desarrollar APIs web de manera rápida, con integración automática de componentes como servidores embebidos (Tomcat) y gestión de dependencias.

**Ventajas clave:**
- Configuración automática (Auto-configuration).
- Aplicaciones empaquetables como JARs ejecutables.
- Soporte nativo para microservicios y contenedores.

### El Rol de Maven como Gestor de Dependencias

Maven es una herramienta de gestión de proyectos y dependencias que utiliza un archivo `pom.xml` para declarar bibliotecas externas. En Spring Boot, Maven resuelve automáticamente las dependencias transitivas, compilando y empaquetando el proyecto.

**Flujo típico con Maven:**
1. Declarar dependencias en `pom.xml`.
2. Ejecutar `mvn clean install` para descargar y compilar.
3. Ejecutar `mvn spring-boot:run` para iniciar la aplicación.

**Nota:** Gradle es la alternativa moderna a Maven, con sintaxis más concisa (basada en Groovy/Kotlin) y mejor rendimiento en proyectos grandes. Sin embargo, Maven sigue siendo el estándar en muchos entornos empresariales.

### Flujo Inicial con Spring Initializr

Spring Initializr es una herramienta web (start.spring.io) que genera la estructura base de un proyecto Spring Boot. El proceso conceptual es:

```
Usuario selecciona:
├── Lenguaje: Java 25
├── Framework: Spring Boot 4.x
├── Dependencias: Spring Web, Spring Boot Actuator, Validation
└── Genera proyecto

Resultado:
├── Estructura de directorios estándar
├── Archivo pom.xml configurado
├── Clase principal @SpringBootApplication
└── application.properties listo
```

Este bootstrapping acelera el inicio, permitiendo enfocarse en la lógica de negocio desde el primer momento.

---

## 2. 🏗️ Arquitectura Multicapa (Teoría)

La arquitectura multicapa es un patrón de diseño que separa responsabilidades en capas lógicas, promoviendo mantenibilidad y escalabilidad. En microservicios REST con Spring Boot, utilizamos tres capas principales:

### Capa de Presentación/API (Controller)

- **Responsabilidad:** Actúa como punto de entrada de la aplicación, manejando requests HTTP y responses.
- **Funciones:** Validación inicial de datos, transformación de formatos (JSON), enrutamiento a la capa de negocio.
- **Principio:** Es la "interfaz" con el cliente externo; no contiene lógica de negocio.

**Diagrama conceptual:**
```
Cliente HTTP ── Request ──> Controller ── Delega ──> Service
                        │
                        └─ Response <── Service
```

### Capa de Negocio (Service)

- **Responsabilidad:** Contiene la lógica de negocio y reglas de aplicación.
- **Funciones:** Validaciones complejas, cálculos, coordinación entre entidades, manejo de transacciones.
- **Principio:** Independiente de la presentación y persistencia; puede ser reutilizada por múltiples controladores.

**Diagrama conceptual:**
```
Controller ── Datos ──> Service ── Reglas ──> Lógica Procesada
                        │
                        └─ Resultados <── Lógica
```

### Capa de Persistencia (Model/Entity)

- **Responsabilidad:** Representa y gestiona los datos de la aplicación.
- **Funciones:** Mapeo objeto-relacional, consultas a base de datos, definición de esquemas.
- **Principio:** Abstrae el acceso a datos; las entidades son objetos que reflejan tablas de BD.

**Diagrama conceptual:**
```
Service ── Consultas ──> Model/Entity ── SQL ──> Base de Datos
                        │
                        └─ Resultados <── Base de Datos
```

**Beneficios de la separación:**
- **Mantenibilidad:** Cambios en una capa no afectan otras.
- **Testabilidad:** Cada capa puede probarse independientemente.
- **Escalabilidad:** Facilita la distribución en microservicios.

---

## 3. ☕ Java 25 y la Modernización del Lenguaje

Java 25 consolida la era de la "programación concisa", donde el lenguaje elimina el ruido visual sin perder su esencia orientada a objetos. Aunque las versiones actuales ofrecen herramientas automáticas, en este curso nos centramos en las clases tradicionales para asegurar que comprendas los fundamentos de la POO (Programación Orientada a Objetos) antes de usar las simplificaciones modernas.

### Clase Tradicional (POJO)

Un **POJO** (_Plain Old Java Object_) es la base del diseño de software en Java. Representa una estructura donde tú, como desarrollador, tienes control total sobre cada componente:

```java
public class Product {
    // Atributos (Estado: representan la información del objeto)
    private String name;
    private Double price;
    
    // Constructor (Inicialización: define cómo nace el objeto)
    public Product(String name, Double price) {
        this.name = name;
        this.price = price;
    }
    
    // Constructor vacío (Requerido por frameworks de persistencia y serialización)
    public Product() {}
    
    // Métodos de acceso (Getters/Setters: implementan el encapsulamiento)
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    
    public Double getPrice() { return price; }
    public void setPrice(Double price) { this.price = price; }
}
```

**Elementos clave:**

- **Atributos:** Definen qué sabe el objeto.
- **Constructores:** Garantizan que el objeto se cree en un estado válido.
- **Encapsulamiento:** Protege los datos mediante modificadores de acceso (`private`) y métodos controlados.

### Java Record (Estándar moderno en Java 25)

Un Record es una clase especial para objetos inmutables, diseñada para datos que no cambian:

```java
public record ProductDTO(String name, Double price) {
    // El constructor canónico, los getters, equals, hashCode 
    // y toString se generan automáticamente en tiempo de compilación.
}
```

**Diferencias principales:**

### Diferencias principales

|**Aspecto**|**Clase Tradicional (POJO)**|**Java Record (Java 25)**|
|---|---|---|
|**Mutabilidad**|**Mutable:** Los datos pueden cambiar mediante setters.|**Inmutable:** Los datos son `final` y no pueden cambiar.|
|**Código Manual**|Alto (requiere getters, setters, toString, etc.).|Mínimo (una sola línea de declaración).|
|**Herencia**|Flexible: Puede extender otras clases.|Restringida: No puede extender otras clases (hereda de `Record`).|
|**Uso Ideal**|Entidades de Base de Datos y lógica de negocio compleja.|DTOs, respuestas de API y Value Objects.|

---
### ¿Por qué enfocarnos en clases tradicionales?

A pesar de que Java 25 permite escribir menos código, los estudiantes necesitan comprender explícitamente cómo funcionan los **atributos, constructores y el flujo de datos**.

Los **Records** son herramientas de productividad que "ocultan" la infraestructura del objeto. Si aprendes a usar Records sin entender las clases tradicionales, tendrás dificultades para trabajar con lógica personalizada o frameworks que aún dependen de la mutabilidad controlada. Recomendamos migrar a Records una vez que hayas dominado el ciclo de vida de un objeto tradicional.

---

## 4. 💾 Persistencia con JPA

### Concepto de ORM (Object-Relational Mapping)

ORM es una técnica que mapea objetos de Java a tablas de bases de datos relacionales, eliminando la necesidad de escribir SQL manual. JPA (Java Persistence API) es la especificación estándar de Java para ORM.

**Problema que resuelve:**
- **Impedancia objeto-relacional:** Objetos son jerárquicos; BD son tabulares.
- **SQL manual:** Propenso a errores, difícil de mantener.

**Cómo funciona:**
```
Objeto Java ── Mapeo ──> Tabla BD
Product p ────────────> products (id, name, price)
```

### Spring Data JPA: Abstracción de Consultas

Spring Data JPA extiende JPA, abstrayendo consultas SQL mediante interfaces. Define métodos por convención de nombres:

```java
public interface ProductRepository extends JpaRepository<Product, Long> {
    // findByName(String name) ── Genera: SELECT * FROM product WHERE name = ?
    // findByPriceGreaterThan(Double price) ── Genera: SELECT * FROM product WHERE price > ?
}
```

**Beneficios:**
- **Cero SQL:** Métodos CRUD automáticos (save, findById, findAll, delete).
- **Consultas derivadas:** Basadas en nombres de métodos.
- **Transacciones automáticas:** Gestionadas por Spring.

**Flujo conceptual:**
```
Service ── productRepository.save(product) ──> JPA ── INSERT INTO product...
Service ── productRepository.findAll() ────> JPA ── SELECT * FROM product
```

---

## 5. 📋 Referencia de Anotaciones

Las anotaciones son metadatos que configuran el comportamiento de Spring Boot. A continuación, una tabla resumen de las críticas:

| Anotación | Capa | Descripción | Ejemplo de Uso |
|-----------|------|-------------|----------------|
| `@SpringBootApplication` | Principal | Marca la clase principal; habilita auto-configuración, escaneo de componentes y configuración. | Clase main del proyecto |
| `@RestController` | Controller | Combina @Controller + @ResponseBody; expone endpoints REST. | Clases que manejan requests HTTP |
| `@Service` | Service | Marca componentes de lógica de negocio; candidatos para inyección. | Clases con reglas de negocio |
| `@Entity` | Model | Marca clases como entidades JPA; mapea a tablas BD. | Clases que representan datos persistentes |
| `@Id` | Model | Marca el atributo como clave primaria. | Campo único identificador |
| `@GeneratedValue` | Model | Genera automáticamente valores para claves primarias. | IDs auto-incrementales |

**Notas importantes:**
- Las anotaciones se procesan en tiempo de compilación/ejecución.
- Facilitan la configuración declarativa sobre programática.
- Spring Boot las detecta automáticamente mediante escaneo de paquetes.

---

## 🎓 Conclusión

Este contenido teórico proporciona los fundamentos necesarios para comprender Spring Boot como herramienta para microservicios REST. La arquitectura multicapa asegura separación de responsabilidades, mientras que JPA abstrae la complejidad de la persistencia. El enfoque en clases tradicionales fortalece las bases OOP antes de explorar características modernas como Records.

**Recomendaciones para el estudio:**
- Relee los diagramas conceptuales para internalizar los flujos.
- Relaciona cada anotación con su responsabilidad en la arquitectura.
- Practica identificando capas en aplicaciones existentes.

Con estos conceptos claros, estarás preparado para la implementación práctica. ¡El dominio teórico es la base del desarrollo efectivo!

---

*Este contenido está diseñado para lectura rápida y referencia continua durante el curso Express.*