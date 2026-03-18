# Beans

Un bean en el contexto de la programación y los frameworks de Java (especialmente en Spring) es un objeto que es instanciado, ensamblado y gestionado por un contenedor. Es esencialmente un componente fundamental de una aplicación.

---

## Concepto de un Bean

La idea principal es que no creas los objetos con la palabra clave `new` directamente. En su lugar, le dices al contenedor de Spring qué objetos necesitas. El contenedor se encarga de:

1. Instanciar el objeto.
2. Configurarlo (por ejemplo, inyectando otros beans de los que depende).
3. Gestionar su ciclo de vida, desde su creación hasta su destrucción.

Este enfoque se conoce como Inversión de Control (IoC). En lugar de que tu código controle la creación de los objetos, el contenedor de Spring es el que tiene el control.

# ¿Qué es un bean?

En el contexto de Java y frameworks como Spring, un **bean** es un objeto que es gestionado por el contenedor de inversión de control (IoC). Los beans son componentes clave en la arquitectura de aplicaciones Java modernas.

## Características principales

- **Instanciados, configurados y gestionados automáticamente** por el contenedor de Spring.
- Pueden representar servicios, repositorios, controladores, configuraciones, etc.
- Se definen usando anotaciones como `@Component`, `@Service`, `@Repository`, o mediante configuración en archivos XML (en versiones antiguas).

## Ejemplo básico

```java
import org.springframework.stereotype.Component;

@Component
public class MiServicio {
    public void saludar() {
        System.out.println("¡Hola desde un bean!");
    }
}
```

## ¿Cómo se usan?

- Spring detecta automáticamente las clases anotadas y las registra como beans.
- Puedes inyectar beans en otras clases usando `@Autowired` o constructor injection.

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MiControlador {
    private final MiServicio miServicio;

    @Autowired
    public MiControlador(MiServicio miServicio) {
        this.miServicio = miServicio;
    }
}
```

## Resumen

Un **bean** es cualquier objeto gestionado por el contenedor de Spring, facilitando la inyección de dependencias y la configuración automática de la aplicación.
