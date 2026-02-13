# Nombrado de campos en Base de Datos

No existe un estándar único y universal para nombrar campos en una base de datos, pero sí hay convenciones muy extendidas y mejores prácticas que te ayudarán a mantener tu esquema limpio, legible y fácil de mantener.

La elección correcta depende principalmente de tres factores:

1. El **motor de base de datos** que usas (PostgreSQL, MySQL, SQL Server, etc.).
    
2. El **lenguaje de programación** o framework con el que interactuarás (Python/Django, Ruby/Rails, C#/.NET).
    
3. Las **guías de estilo** de tu equipo de trabajo.
    

A continuación, te explico los formatos más comunes y te doy una recomendación general.

---

## 📝 Estilos de nomenclatura comunes

Aquí están los principales "sabores" que mencionaste, con sus pros y contras.

### 1. `snake_case` (con guion bajo)

Este es el formato **más recomendado y extendido** en el mundo de las bases de datos, especialmente en entornos de PostgreSQL, Oracle y MySQL.

- **Formato:** Todas las letras en minúscula, separando las palabras con un guion bajo (`_`).
    
- **Ejemplos:** `nombre_cliente`, `fecha_de_creacion`, `id_usuario`.
    
- **Ventajas:**
    
    - ✅ **Máxima legibilidad:** Es muy fácil de leer y entender.
        
    - ✅ **Compatibilidad:** Funciona sin problemas en prácticamente todos los motores de base de datos y lenguajes. Evita por completo los problemas de sensibilidad a mayúsculas/minúsculas.
        
    - ✅ **Estándar de facto:** Muchos frameworks populares (como Ruby on Rails y Django) lo usan por defecto.
        
- **Desventajas:**
    
    - ❌ Puede ser un poco más largo de escribir que otras opciones.
        

### 2. `PascalCase` o `CamelCase` (con mayúsculas)

Este estilo es muy popular en el mundo de Microsoft, especialmente con **SQL Server** y el ecosistema .NET.

- **Formato:**
    
    - `PascalCase`: Cada palabra comienza con mayúscula (`NombreCliente`).
        
    - `camelCase`: La primera palabra en minúscula, las siguientes con mayúscula inicial (`nombreCliente`).
        
- **Ejemplos:** `NombreCliente`, `FechaCreacion`, `IdUsuario`.
    
- **Ventajas:**
    
    - ✅ **Integración:** Se alinea perfectamente con las convenciones de lenguajes como C# y Java.
        
- **Desventajas:**
    
    - ❌ **Sensibilidad de mayúsculas (Case Sensitivity):** Este es el mayor problema. Algunos motores de bases de datos no distinguen entre mayúsculas y minúsculas por defecto (como SQL Server en Windows), mientras que otros sí (como PostgreSQL). Esto puede causar errores y confusiones si migras de un sistema a otro. Para forzar la distinción, a menudo necesitas usar comillas dobles (ej. `SELECT "NombreCliente" FROM ...`), lo cual es muy tedioso.
        

### 3. `kebab-case` (con guion medio)

Este formato debe **evitarse siempre** en el nombramiento de tablas y columnas.

- **Formato:** Palabras en minúscula separadas por un guion medio (`-`).
    
- **Ejemplos:** `nombre-cliente`.
    
- **Por qué es una mala idea:**
    
    - ❌ **Conflicto con SQL:** El guion medio es el operador de resta en SQL. Si nombras un campo `nombre-cliente`, una consulta como `SELECT nombre-cliente FROM ...` intentará restar el valor del campo `cliente` al del campo `nombre`, causando un error.
        
    - ❌ **Requiere comillas:** La única forma de usarlo es encerrando siempre el nombre entre comillas especiales (ej. `SELECT "nombre-cliente" ...`), lo cual es impráctico y propenso a errores.
        

---

## 🏆 Mejores prácticas y recomendación final

Más allá del estilo, sigue estas reglas para un diseño de base de datos robusto:

1. **Sé descriptivo pero conciso:** El nombre debe explicar claramente qué dato contiene. Usa `correo_electronico` en lugar de `email` o `mail`, y definitivamente no uses abreviaturas como `crr_elec`.
    
2. **Usa nombres en inglés:** Aunque tu equipo hable español, usar inglés es la convención global en programación. Facilita la contratación de talento internacional, el uso de librerías de terceros y la portabilidad del código.
    
3. **Usa sustantivos en singular para las tablas:** Nombra la tabla según la entidad que representa. Por ejemplo, una tabla para guardar usuarios debería llamarse `user` (o `usuario`), no `users` (o `usuarios`). La tabla es el molde para un "usuario", aunque contenga muchos.
    
4. **Evita palabras reservadas:** Nunca uses palabras que son comandos de SQL como `user`, `order`, `group`, `table`, `select`. Si necesitas usarlas, añade un prefijo o sufijo, como `app_user` o `customer_order`.
    
5. **Define un estándar para claves:**
    
    - **Clave primaria (PK):** Simplemente `id`. Es simple y funciona bien con la mayoría de los ORM (Object-Relational Mapping).
        
    - **Clave foránea (FK):** Usa el nombre de la tabla en singular seguido de `_id`. Por ejemplo, en la tabla `pedido`, la clave foránea que apunta a la tabla `cliente` se llamaría `cliente_id`.
        
6. **Sé consistente:** ¡Esta es la regla más importante! Elige una convención y **aplícala en toda la base de datos**. La consistencia hace que el esquema sea predecible y fácil de entender para cualquiera que trabaje con él.
    

---

### Resumen y recomendación

Si estás empezando un proyecto nuevo y tienes la libertad de elegir, la recomendación más segura y moderna es:

> **Usa `snake_case` con nombres en inglés y sustantivos en singular para las tablas.**

**Ejemplo de un esquema bien nombrado:**

- Tabla `customer`
    
    - `id` (PK)
        
    - `first_name`
        
    - `last_name`
        
    - `email_address`
        
    - `created_at`
        
- Tabla `product_order`
    
    - `id` (PK)
        
    - `customer_id` (FK a `customer`)
        
    - `order_date`
        
    - `total_amount`
        

Este enfoque te dará la mayor compatibilidad, legibilidad y evitará problemas a largo plazo, sin importar qué tecnología uses en el futuro.

## 📝 DB2 en Sistemas AS/400

Las bases de datos DB2 en sistemas AS/400 (ahora llamados **IBM i**) tienen su propio conjunto de reglas y convenciones, influenciadas por décadas de historia y retrocompatibilidad. Aunque comparten principios de SQL con otros sistemas, su entorno es único.

Lo que mencioné anteriormente sobre `snake_case` y otros estilos aplica a bases de datos más modernas, pero en el mundo del AS/400, las reglas son más estrictas y tienen un sabor particular.

Aquí te explico las claves para nombrar campos en DB2 para i.

---

## 💾 El "Doble Estándar": Nombres de Sistema vs. Nombres SQL

Lo primero que debes entender es que en DB2 para i existen dos tipos de nombres para el mismo objeto (tabla o campo):

1. **Nombre de Sistema (System Name):** Es el nombre "real" del objeto a nivel del sistema operativo. Está sujeto a las reglas más antiguas y restrictivas.
    
    - **Límite de 10 caracteres.**
        
    - No puede contener guiones bajos (`_`).
        
    - Generalmente en **MAYÚSCULAS**.
        
    - Este es el nombre que verás si interactúas con la base de datos usando herramientas tradicionales o lenguajes como RPG o COBOL.
        
2. **Nombre SQL (Long Name):** Es un alias o nombre "largo" que se usa principalmente en el contexto de SQL. Ofrece más flexibilidad.
    
    - **Límite mucho más amplio** (hasta 128 caracteres para tablas y 30 para columnas).
        
    - **Permite guiones bajos (`_`)**.
        
    - Puede ser más descriptivo.
        

Cuando creas una tabla con un nombre SQL largo, el sistema genera automáticamente un Nombre de Sistema de 10 caracteres (a menudo truncando el nombre largo y añadiendo un sufijo numérico).

**¿Por qué es importante?** Si solo vas a usar SQL, puedes usar los nombres largos sin preocuparte. Pero si tu base deatos debe ser compatible con aplicaciones RPG o COBOL existentes, **debes respetar las limitaciones del Nombre de Sistema de 10 caracteres**.

---

## 📜 Reglas y convenciones para DB2 en AS/400

Dada esa dualidad, las convenciones más seguras y extendidas en este entorno son:

### 1. Estilo de nomenclatura: `MAYUSCULAS_CON_PREFIJOS` (o estilo RPG/COBOL)

Debido a la historia de la plataforma, la convención más arraigada no es `snake_case` en minúsculas, sino una variante en mayúsculas, a menudo usando prefijos para agrupar campos relacionados.

- **Formato:** Palabras en mayúsculas, a veces abreviadas para cumplir el límite de 10 caracteres. Se usan prefijos de 2 o 3 letras para indicar a qué entidad pertenecen.
    
- **Ejemplos:**
    
    - Tabla de Clientes: `CUSMST` (Customer Master)
        
    - Campos en la tabla de clientes:
        
        - `CUSID` (ID de Cliente)
            
        - `CUSNAM` (Nombre de Cliente)
            
        - `CUSADR` (Dirección de Cliente)
            
        - `CUSSTS` (Estatus de Cliente)
            

### 2. Sensibilidad a mayúsculas (case sensitivity)

Por defecto, **DB2 en AS/400 no es sensible a mayúsculas y convierte todos los nombres no citados a mayúsculas**. Por ejemplo, si escribes `CREATE TABLE Clientes`, el sistema lo interpretará y creará como `CLIENTES`. Para forzar minúsculas o un `CamelCase`, tendrías que usar comillas dobles (`"Clientes"`), pero esto es muy poco común y no se recomienda en este entorno porque rompe con las convenciones y dificulta el trabajo con herramientas nativas.

### 3. Caracteres permitidos

Los nombres deben empezar con una letra. Pueden contener letras (A-Z), números (0-9) y algunos símbolos especiales como (`$`, `#`, `@`). Como mencioné, el guion bajo (`_`) solo es válido para los nombres largos de SQL.

---

### Recomendación práctica

- **Para proyectos nuevos (solo SQL):** Si estás seguro de que nunca interactuarás con programas RPG/COBOL, puedes usar un estilo `snake_case` en minúsculas (ej. `customer_address`) o mayúsculas (`CUSTOMER_ADDRESS`). El sistema lo manejará bien. Sin embargo, sigue siendo una buena práctica mantener los nombres relativamente cortos.
    
- **Para entornos mixtos o de mantenimiento (la norma general):**
    
    > **Adopta el estilo tradicional de 10 caracteres en mayúsculas con prefijos.** Es la forma más segura y compatible de trabajar en un AS/400.
    

**Ejemplo de una tabla `PEDIDOS` (ORDERS):**

|Campo Lógico|Nombre Físico (10 car.)|Descripción|
|---|---|---|
|ID de Pedido|`ORDIDO`|ID del Pedido|
|ID de Cliente|`ORDIDC`|ID del Cliente (FK)|
|Fecha de Pedido|`ORDDAT`|Fecha del Pedido|
|Monto Total|`ORDAMT`|Monto Total|
|Estatus|`ORDSTS`|Estatus del Pedido|

Este estilo puede parecer anticuado, pero garantiza que tus tablas y campos sean accesibles y manejables desde cualquier herramienta o lenguaje en el ecosistema IBM i, evitando sorpresas y problemas de compatibilidad.