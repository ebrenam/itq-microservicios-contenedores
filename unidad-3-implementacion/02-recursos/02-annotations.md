# Annotations

Las anotaciones de Spring Boot son una forma de metadatos que se añaden al código Java para proporcionar instrucciones a Spring. Piensa en ellas como etiquetas o marcadores que le dicen al framework cómo debe comportarse un componente, sin necesidad de escribir código XML o configuraciones complejas. Su propósito principal es simplificar el desarrollo, reducir la configuración y permitir a Spring Boot automatizar la creación de aplicaciones.

---

## ¿Cómo funcionan?

Las anotaciones de Spring Boot se basan en el concepto de "convención sobre configuración". Esto significa que el framework asume ciertos comportamientos por defecto, y solo necesitas usar anotaciones para desviarte de esa convención o para habilitar funcionalidades específicas.

# ¿Qué son las annotations?

**Annotations** (anotaciones) son una característica de lenguajes como Java que permiten agregar metadatos al código fuente. Se escriben usando el símbolo `@` seguido del nombre de la anotación y, opcionalmente, parámetros.

## ¿Para qué sirven?

- Proporcionan información adicional al compilador, frameworks o herramientas.
- Permiten modificar el comportamiento del código sin cambiar la lógica principal.
- Son ampliamente usadas en frameworks como Spring, Quarkus, JPA, etc.

## Ejemplos comunes en Java

```java
@Override
public String toString() {
    return "Ejemplo";
}

@Entity
public class Usuario {
    @Id
    private Long id;
}
```

- `@Override`: Indica que un método sobrescribe a uno de la superclase.
- `@Entity`, `@Id`: Usadas en JPA para mapear clases a tablas de base de datos.

## Ventajas

- Facilitan la configuración y automatización.
- Hacen el código más legible y mantenible.
- Permiten integración sencilla con frameworks modernos.

**Resumen:**

Las annotations son metadatos en el código que ayudan a los frameworks y herramientas a entender cómo debe comportarse una clase, método o campo.

