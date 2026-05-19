# ¿Qué es un Java Bean?

Un **Java Bean** es una clase Java que cumple ciertas reglas y se utiliza principalmente para encapsular datos de manera estándar y facilitar su manipulación en frameworks, bibliotecas y herramientas Java.

## Características de un Java Bean

- **Constructor público sin argumentos** (por defecto).
- **Propiedades privadas** (campos privados).
- **Métodos públicos getter y setter** para acceder y modificar las propiedades.
- **Serializable** (opcional, pero común para Java Beans).

## Ejemplo de Java Bean

```java
public class Persona implements java.io.Serializable {
    private String nombre;
    private int edad;

    public Persona() {
        // Constructor sin argumentos
    }

    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        this.edad = edad;
    }
}
```

## ¿Para qué se usan?

- Transferencia de datos entre capas de una aplicación (DTOs).
- Integración con frameworks como JavaServer Faces (JSF), JSP, Spring, etc.
- Serialización y deserialización de objetos.
- Manipulación automática de propiedades en herramientas visuales.

**Resumen:**  
Un Java Bean es una clase Java simple y estructurada para encapsular datos, siguiendo reglas estándar de Java.

[[Conceptos Java]]
