# Ley de Conway

La **Ley de Conway** es un principio de la ingeniería de software y la gestión empresarial que establece que el diseño de los sistemas técnicos de una organización estará inevitablemente limitado por las estructuras de comunicación de dicha organización.

Fue formulada en 1967 por el programador **Melvin Conway**, quien la resumió de la siguiente manera:

> "Las organizaciones que diseñan sistemas... están limitadas a producir diseños que son copias de las estructuras de comunicación de estas organizaciones".

---

### ¿Cómo funciona en la práctica?

Imagina que tienes una empresa con tres equipos de desarrollo separados trabajando en un mismo software. Según la Ley de Conway, es casi seguro que el software resultante terminará teniendo **tres módulos principales** o capas distintas, simplemente porque así es como se comunican las personas que lo crearon.

#### Ejemplo clásico:

- Si tienes **4 equipos** trabajando en un compilador, obtendrás un compilador de **4 fases**.

- Si los equipos de "Base de Datos" y "Frontend" nunca hablan entre sí, el sistema tendrá una separación técnica muy marcada y difícil de integrar entre esos dos puntos.

---

### ¿Por qué es importante hoy en día?

Este concepto ha cobrado mucha relevancia con el auge de los **Microservicios**. Muchas empresas ahora aplican lo que se conoce como la **"Maniobra de Conway Inversa"**:

1. Primero, diseñan la arquitectura técnica que desean (por ejemplo, microservicios independientes).

2. Luego, **organizan a sus equipos** para que reflejen esa estructura.

3. Si quieres un sistema desacoplado, debes tener equipos independientes y autónomos.

### Resumen de implicaciones

| **Factor**        | **Efecto de la Ley de Conway**                                                       |
| ----------------- | ------------------------------------------------------------------------------------ |
| **Arquitectura**  | El software "hereda" la forma del organigrama.                                       |
| **Comunicación**  | Los silos de información en la oficina crean cuellos de botella en el código.        |
| **Escalabilidad** | Si la organización es un caos, el sistema técnico será caótico y difícil de escalar. |