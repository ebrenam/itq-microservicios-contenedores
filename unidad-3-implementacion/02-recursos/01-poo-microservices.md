# 🎓 POO para Microservicios

Este documento es una guía de nivelación para asegurar que todos comprendamos cómo los objetos de Java se transforman en los bloques de construcción de un sistema distribuido.

---

## Módulo 1: Abstracción y Encapsulamiento (La "Caja Negra")

### 1.1 ¿Qué es la Abstracción?

No es más que **ignorar los detalles irrelevantes**.

- **En POO:** Si creas una clase `Coche`, no programas cada tornillo. Solo defines `acelerar()` y `frenar()`.
    
- **En Microservicios:** Un servicio de "Pagos" es una abstracción. Al servicio de "Pedidos" no le importa si el pago se procesa con Visa, Stripe o PayPal; solo le importa que el resultado sea `EXITOSO`.
    

### 1.2 Encapsulamiento: El muro de seguridad

El encapsulamiento consiste en ocultar el estado interno (atributos) y solo permitir el acceso a través de métodos públicos.

Java

```
// Ejemplo de mal encapsulamiento (Todos tocan todo)
public class Cuenta {
    public double saldo; // MAL: Cualquiera puede poner saldo = -1000
}

// Ejemplo de buen encapsulamiento (Control total)
public class Cuenta {
    private double saldo; // PRIVADO

    public void depositar(double monto) {
        if (monto > 0) {
            this.saldo += monto;
        }
    }
}
```

**Conexión con Microservicios:** En una arquitectura de microservicios, **la base de datos es privada**. Ningún servicio externo puede hacer un `SELECT` o `UPDATE` a la tabla de otro servicio. Debe usar el API (el método público).

---

## Módulo 2: Interfaces y Polimorfismo (El "Contrato")

### 2.1 La Interfaz como Contrato

Una interfaz es una lista de promesas. Dice **qué** se hace, pero no **cómo**.

Java

```
public interface Notificador {
    void enviarMensaje(String mensaje);
}
```

### 2.2 Polimorfismo: Muchas formas

El polimorfismo permite que nuestro código sea flexible. Podemos probar el sistema con un `ServicioFake` antes de conectar el `ServicioReal` de producción.

**¿Para qué sirve en Spring Boot?** Cuando defines un `Service` en Spring, solemos usar interfaces. Esto nos permite cambiar la lógica del negocio (por ejemplo, cambiar de un proveedor de SMS a otro) **sin cambiar una sola línea de código** en el controlador que lo usa.

---

## Módulo 3: Relaciones (Composición sobre Herencia)

### 3.1 El problema de la Herencia (`is-a`)

La herencia crea una relación muy rígida. Si la clase "Padre" cambia, el "Hijo" puede romperse.

> **Regla de oro:** Si puedes usar composición, no uses herencia.

### 3.2 Composición (`has-a`)

En lugar de que un `Microservicio` herede de una clase `BaseDatos`, el `Microservicio` **tiene** una instancia de una base de datos.

Java

```
// Composición: El servicio "TIENE" un repositorio
public class OrdenService {
    private final OrdenRepository repository; 

    public OrdenService(OrdenRepository repository) {
        this.repository = repository;
    }
}
```

**En Microservicios:** Los sistemas se construyen "componiendo" pequeñas piezas independientes que se comunican entre sí. La autonomía es la clave.

---

## Módulo 4: Inyección de Dependencias (El "Pegamento")

Este es el punto donde dejamos de programar "scripts" y empezamos a programar "componentes".

### 4.1 El problema: El acoplamiento por `new`

Cuando escribes `Servicio s = new Servicio();` dentro de un Controlador, está "soldando" las dos piezas. Si el `Servicio` cambia, el `Controlador` se rompe. Además, es imposible hacer pruebas unitarias porque no puedes sustituir el servicio por un simulacro (Mock).

### 4.2 La Solución: Inversión de Control (IoC)

En lugar de que tú (el programador) controles la creación de objetos, le entregas las llaves a un **Contenedor** (Spring).

- **Antes:** "Yo fabrico mis herramientas conforme las necesito".
    
- **Con IoC:** "Yo le doy a Spring una lista de herramientas que sé fabricar (Beans) y le pido que me las entregue cuando las necesite".
    

### 4.3 Inyección de Dependencias (DI): ¿Cómo me llega el objeto?

Hay tres formas principales de recibir un objeto en Spring Boot, pero la más limpia y recomendada es la **Inyección por Constructor**:

Java

```
@Service
public class AlumnoService {
    // Definimos la dependencia pero NO la instanciamos
    private final AlumnoRepository repository;

    // Spring ve este constructor y busca un "Bean" de tipo AlumnoRepository
    // para "inyectarlo" automáticamente.
    public AlumnoService(AlumnoRepository repository) {
        this.repository = repository;
    }
}
```

### 4.4 El Ciclo de Vida de un "Bean"

Es vital entender que en Spring, los objetos no mueren al terminar un método.

- **Singleton (por defecto):** Spring crea **una sola instancia** de tu servicio para toda la aplicación. Esto ahorra memoria y es ideal para microservicios que procesan miles de peticiones.
    

### 4.5 DTOs: Los mensajeros del Microservicio

En POO usábamos clases para representar tablas de BD. En Microservicios, usamos **DTOs (Data Transfer Objects)**.

- **¿Por qué?** Seguridad y Eficiencia. No quieres enviar el `password` o el `ID_interno` de la base de datos en una respuesta JSON. El DTO es un "filtro" de seguridad.
    

---

### Resumen

1. **¿Quién crea los objetos en Spring?** El contenedor de IoC (ApplicationContext).
    
2. **¿Qué es un Bean?** Un objeto gestionado por Spring.
    
3. **¿Por qué usar interfaces en los servicios?** Para permitir polimorfismo y facilitar las pruebas.
    
4. **¿Qué hace `@Autowired` o la inyección por constructor?** Pide a Spring que busque y entregue una instancia de una clase necesaria.

