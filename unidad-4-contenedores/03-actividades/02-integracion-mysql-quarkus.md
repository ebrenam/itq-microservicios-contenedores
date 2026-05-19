# Integración de Base de Datos MySQL con Quarkus

Este documento continúa desde donde dejamos en la **"Creación de Proyecto OAS - Quarkus"** de la **Unidad 3** y te guiará paso a paso para agregar persistencia con MySQL y completar las operaciones CRUD.

---

## 📋 Requisitos previos

- Tener completado el proyecto del documento anterior
- MySQL Server instalado y ejecutándose
- Conocimientos básicos de SQL

---

## 🗄️ Paso 1: Validación de la configuración MySQL y Base de Datos

Primero, necesitamos preparar nuestra base de datos.

### 1.1 Conectar a MySQL

Se puede realizar la conexión de diferentes formas, en este punto se recomienda utilizar un cliente como `MySQL Workbench` o `DBeaver` que presentan una interfaz gráfica.

Abre el cliente de tu elección y conecta con los siguientes datos:

| Dato     | Valor              |
| -------- | ------------------ |
| Server   | localhost          |
| Port     | 3306               |
| Database | reservation_system |
| Username | quarkus_user       |
| Password | quarkus_password   |

> Si no cuentas con una Base de Datos ya creada, necesitas realizar los pasos del punto `8.4 Configuración con Volúmenes Docker (Recomendado para producción)` del documento **Configuración de Base de Datos MySQL con Docker**.

## 📦 Paso 2: Agregar dependencias de Base de Datos al `pom.xml`

Abre tu archivo `pom.xml` y agrega las siguientes dependencias dentro de la sección `<dependencies>`:

```xml
        <!-- Dependencias para MySQL y Hibernate ORM -->
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-hibernate-orm</artifactId>
        </dependency>

        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-jdbc-mysql</artifactId>
        </dependency>

        <!-- Dependencia para Hibernate ORM con Panache (simplifica JPA) -->
        <dependency>
            <groupId>io.quarkus</groupId>
            <artifactId>quarkus-hibernate-orm-panache</artifactId>
        </dependency>
```

**💡 Explicación:**

- `quarkus-hibernate-orm`: Proporciona JPA/Hibernate para el mapeo objeto-relacional
- `quarkus-jdbc-mysql`: Driver JDBC específico para MySQL
- `quarkus-hibernate-orm-panache`: Simplifica las operaciones de base de datos con un patrón Active Record

---

## ⚙️ Paso 3: Configurar la conexión a la Base de Datos

Abre el archivo `src/main/resources/application.properties` y agrega la configuración de la base de datos:

```properties
# Configuración de la base de datos MySQL
quarkus.datasource.db-kind=mysql
quarkus.datasource.username=quarkus_user
quarkus.datasource.password=quarkus_password
quarkus.datasource.jdbc.url=jdbc:mysql://localhost:3306/reservation_system

# Configuración de Hibernate
quarkus.hibernate-orm.log.sql=true
```

💡 **Explicación de las propiedades:**
- `db-kind`: Tipo de base de datos
- `username/password`: Credenciales de acceso
- `jdbc.url`: URL de conexión a MySQL
- `database.generation=validate`: Validar que la estructura de la BD coincida con las entidades
- `log.sql=true`: Mostrar las consultas SQL en los logs (útil para desarrollo)

## 🏗️ Paso 4: Crear la entidad JPA

En lugar de usar solo el modelo generado por OpenAPI, crearemos una entidad JPA que mapee directamente a nuestra tabla de base de datos.

### 4.1 Crear el paquete Entity

Crea un nuevo paquete: `src/main/java/com/ejemplo/api/entity`

### 4.2 Crear la entidad ReservationEntity

Crea el archivo `ReservationEntity.java` en el paquete `entity`:

```java
package com.ejemplo.api.entity;

import io.quarkus.hibernate.orm.panache.PanacheEntity;
import jakarta.persistence.*;
import java.math.BigDecimal;
import java.time.LocalDateTime;

@Entity
@Table(name = "reservations")
public class ReservationEntity extends PanacheEntity {

    @Column(name = "id_client", nullable = false)
    public String idClient;

    @Column(name = "activity", nullable = false)
    public String activity;

    @Column(name = "day_of_week", nullable = false)
    public String dayOfWeek;

    @Column(name = "time", nullable = false)
    public String time;

    @Column(name = "id_room")
    public Integer idRoom;

    @Column(name = "instructor", length = 100)
    public String instructor;

    @Column(name = "discount", precision = 5, scale = 2)
    public BigDecimal discount;

    @Column(name = "created_at", updatable = false)
    public LocalDateTime createdAt;

    @Column(name = "updated_at")
    public LocalDateTime updatedAt;

    // Métodos de ciclo de vida de JPA
    @PrePersist
    protected void onCreate() {
        createdAt = LocalDateTime.now();
        updatedAt = LocalDateTime.now();
    }

    @PreUpdate
    protected void onUpdate() {
        updatedAt = LocalDateTime.now();
    }

    // Método toString para debugging
    @Override
    public String toString() {
        return "ReservationEntity{" +
                "id=" + id +
                ", idClient='" + idClient + '\'' +
                ", activity='" + activity + '\'' +
                ", dayOfWeek='" + dayOfWeek + '\'' +
                ", time='" + time + '\'' +
                ", idRoom=" + idRoom +
                ", instructor='" + instructor + '\'' +
                ", discount=" + discount +
                ", createdAt=" + createdAt +
                ", updatedAt=" + updatedAt +
                '}';
    }
}
```

💡 **Explicación:**
- Extendemos `PanacheEntity` que nos da un campo `id` automático y métodos CRUD básicos
- `@PrePersist` y `@PreUpdate` manejan automáticamente las fechas de creación y actualización
- Los campos son públicos (patrón de Panache) para simplificar el acceso

## 🔄 Paso 5: Crear el mapper para conversión de datos

En una aplicación con arquitectura en capas, necesitamos **separar los modelos de datos**. Tenemos dos tipos principales:

1. **Modelos OpenAPI**: Representan la estructura de datos que intercambiamos con el cliente (JSON)
2. **Entidades JPA**: Representan la estructura de datos en la base de datos

El **Mapper** es el responsable de convertir entre estos dos modelos. Esto nos permite:

- **Mantener independencia** entre la API y la base de datos
- **Evolucionar cada capa** sin afectar las otras
- **Aplicar transformaciones** específicas de cada contexto
- **Manejar diferentes formatos** (ej: String vs Enum, BigDecimal vs Double)

Necesitamos convertir entre nuestros modelos OpenAPI y las entidades JPA.

### 5.1 Crear el paquete Mapper

Crea el paquete: `src/main/java/com/ejemplo/api/mapper`

### 5.2 Crear ReservationMapper

Crea el archivo `ReservationMapper.java`:

```java
package com.ejemplo.api.mapper;

import com.ejemplo.api.entity.ReservationEntity;
import com.ejemplo.api.model.Confirmation;
import com.ejemplo.api.model.Reservation;
import jakarta.enterprise.context.ApplicationScoped;

@ApplicationScoped
public class ReservationMapper {

    /**
     * Convierte de modelo OpenAPI a entidad JPA
     */
    public ReservationEntity toEntity(Reservation reservation)
    {
        if (reservation == null) {
            return null;
        }

        ReservationEntity entity = new ReservationEntity();
        entity.idClient = reservation.getIdClient();
        entity.activity = reservation.getActivity();
        entity.dayOfWeek = reservation.getDayOfWeek() != null ? reservation.getDayOfWeek().toString() : null;
        entity.time = reservation.getTime();

        // Asignar valores por defecto para simplificar
        entity.idRoom = 1; // Sala por defecto
        entity.instructor = "Instructor Asignado"; // Instructor por defecto
        entity.discount = java.math.BigDecimal.valueOf(0.0); // Sin descuento por defecto

        return entity;
    }

    /**
     * Convierte de entidad JPA a modelo de confirmación
     */
    public Confirmation toConfirmation(ReservationEntity entity)
    {
        if (entity == null) {
            return null;
        }

        Confirmation confirmation = new Confirmation();
        confirmation.setIdReservation(entity.id.intValue()); // PanacheEntity usa Long, convertimos a Integer
        confirmation.setIdRoom(entity.idRoom);
        confirmation.setInstructor(entity.instructor);
        
        // Convertir BigDecimal a Double si no es null
        if (entity.discount != null) {
            confirmation.setDiscount(entity.discount.doubleValue());
        }

        return confirmation;
    }

    /**
     * Convierte de entidad JPA a modelo Reservation
     */
    public Reservation toReservation(ReservationEntity entity)
    {
        if (entity == null) {
            return null;
        }

        Reservation reservation = new Reservation();
        reservation.setIdClient(entity.idClient);
        reservation.setActivity(entity.activity);
        reservation.setTime(entity.time);
        
        // Convertir string a enum
        if (entity.dayOfWeek != null) {
            try {
                reservation.setDayOfWeek(Reservation.DayOfWeekEnum.valueOf(entity.dayOfWeek.toUpperCase()));
            } catch (IllegalArgumentException e) {
                reservation.setDayOfWeek(Reservation.DayOfWeekEnum.LUN); // Valor por defecto
            }
        }

        return reservation;
    }
}
```

### **🎯 Resumen del Mapper:**

**Función Principal:**

- Convierte entre modelos OpenAPI (JSON) y entidades JPA (Base de datos)
- Actúa como adaptador entre capas para mantener independencia

**Métodos Implementados:**

- `toEntity()`: JSON → Base de datos (para crear/actualizar)
- `toConfirmation()`: Base de datos → JSON respuesta (para consultas)
- `toReservation()`: Base de datos → JSON completo (para operaciones completas)

**Transformaciones Clave:**

- Enum ↔ String (DayOfWeekEnum ↔ "Lun", "Mar", etc.)
- Long ↔ Integer (PanacheEntity.id ↔ API IDs)
- BigDecimal ↔ Double (Precisión BD ↔ Simplicidad API)

**Beneficios:**

- **Desacoplamiento**: Cambios en BD no afectan API y viceversa
- **Seguridad**: Manejo de nulls y conversiones fallidas
- **Mantenibilidad**: Punto único de transformación de datos
- **Flexibilidad**: Permite diferentes representaciones del mismo dato

El mapper es esencial para una arquitectura limpia y mantenible. 🚀
## 💼 Paso 6: Actualizar el service con operaciones CRUD completas

Ahora actualizaremos nuestro `ReservationService` para usar la base de datos real.

```java
package com.ejemplo.api.service;

import com.ejemplo.api.entity.ReservationEntity;
import com.ejemplo.api.mapper.ReservationMapper;
import com.ejemplo.api.model.CancelConfirmation;
import com.ejemplo.api.model.Confirmation;
import com.ejemplo.api.model.ConfirmationList;
import com.ejemplo.api.model.Reservation;
import com.ejemplo.api.model.ReservationPatch;

import jakarta.enterprise.context.ApplicationScoped;
import jakarta.inject.Inject;
import jakarta.transaction.Transactional;
import java.time.OffsetDateTime;
import java.util.List;

@ApplicationScoped
public class ReservationService {

    @Inject
    ReservationMapper reservationMapper;

    /**
     * Crear una nueva reservación
     */
    @Transactional
    public Confirmation createReservation(Reservation reservation)
    {
        System.out.println("Service - Creando reservación para cliente: " + reservation.getIdClient());
        
        // Convertir el modelo OpenAPI a entidad JPA
        ReservationEntity entity = reservationMapper.toEntity(reservation);
        
        // Persistir en la base de datos
        entity.persist();
        
        // Convertir la entidad guardada a modelo de confirmación
        Confirmation confirmation = reservationMapper.toConfirmation(entity);
        
        System.out.println("Service - Reservación creada con ID: " + entity.id);
        return confirmation;
    }

    /**
     * Obtener todas las reservaciones
     */
    public ConfirmationList getReservations(String idClient, String activity, String dayOfWeek, String time)
    {
        System.out.println("Service - Obteniendo todas las reservaciones");
        
        List<ReservationEntity> entities = ReservationEntity.listAll();
        
        List<Confirmation> confirmations = entities.stream()
                .map(reservationMapper::toConfirmation)
                .toList();
                
        ConfirmationList confirmationList = new ConfirmationList();
        confirmationList.setConfirmations(confirmations);
        confirmationList.setTotal(confirmations.size());
        
        return confirmationList;
    }

    /**
     * Obtener reservación por ID
     */
    public Confirmation getReservationById(Integer reservationId)
    {
        System.out.println("Service - Buscando reservación con ID: " + reservationId);
        
        ReservationEntity entity = ReservationEntity.findById(reservationId.longValue());
        
        if (entity != null) {
            System.out.println("Service - Reservación encontrada: " + entity.toString());
            return reservationMapper.toConfirmation(entity);
        } else {
            System.out.println("Service - Reservación no encontrada con ID: " + reservationId);
            return null;
        }
    }

    /**
     * Actualizar una reservación existente
     */
    @Transactional
    public Confirmation updateReservation(Integer reservationId, Reservation reservation)
    {
        System.out.println("Service - Actualizando reservación con ID: " + reservationId);
        
        ReservationEntity entity = ReservationEntity.findById(reservationId.longValue());
        
        if (entity != null) {
            // Actualizar los campos
            entity.idClient = reservation.getIdClient();
            entity.activity = reservation.getActivity();
            entity.dayOfWeek = reservation.getDayOfWeek().toString();
            entity.time = reservation.getTime();
            
            // Panache automáticamente detecta cambios y los persiste
            System.out.println("Service - Reservación actualizada: " + entity.toString());
            return reservationMapper.toConfirmation(entity);
        } else {
            System.out.println("Service - No se puede actualizar. Reservación no encontrada con ID: " + reservationId);
            return null;
        }
    }

    /**
     * Actualizar parcialmente una reservación existente (PATCH)
     */
    @Transactional
    public Confirmation patchReservation(Integer reservationId, ReservationPatch reservationPatch)
    {
        System.out.println("Service - Actualizando parcialmente reservación con ID: " + reservationId);
        
        ReservationEntity entity = ReservationEntity.findById(reservationId.longValue());
        
        if (entity != null) {
            // Actualizar solo los campos que no son nulos (actualización parcial)
            if (reservationPatch.getIdClient() != null) {
                entity.idClient = reservationPatch.getIdClient();
            }
            if (reservationPatch.getActivity() != null) {
                entity.activity = reservationPatch.getActivity();
            }
            if (reservationPatch.getDayOfWeek() != null) {
                entity.dayOfWeek = reservationPatch.getDayOfWeek().toString();
            }
            if (reservationPatch.getTime() != null) {
                entity.time = reservationPatch.getTime();
            }
            
            // Panache automáticamente detecta cambios y los persiste
            System.out.println("Service - Reservación actualizada parcialmente: " + entity.toString());
            return reservationMapper.toConfirmation(entity);
        } else {
            System.out.println("Service - No se puede actualizar. Reservación no encontrada con ID: " + reservationId);
            return null;
        }
    }

    /**
     * Eliminar una reservación
     */
    @Transactional
    public CancelConfirmation cancelReservation(Integer reservationId)
    {
        System.out.println("Service - Eliminando reservación con ID: " + reservationId);
        
        boolean deleted = ReservationEntity.deleteById(reservationId.longValue());
        
        CancelConfirmation cancelConfirmation = new CancelConfirmation();
        cancelConfirmation.setIdReservation(reservationId);
        
        if (deleted) {
            System.out.println("Service - Reservación eliminada exitosamente");
            cancelConfirmation.setStatus(CancelConfirmation.StatusEnum.CANCELLED);
            cancelConfirmation.setMessage("Reserva cancelada exitosamente");
        } else {
            System.out.println("Service - No se pudo eliminar. Reservación no encontrada con ID: " + reservationId);
            cancelConfirmation.setStatus(CancelConfirmation.StatusEnum.FAILED);
            cancelConfirmation.setMessage("No se pudo cancelar. Reservación no encontrada");
        }
        
        cancelConfirmation.setCancelledAt(OffsetDateTime.now());
        return cancelConfirmation;
    }
}
```

💡 **Explicación:**
- `@Transactional` es necesario para operaciones que modifican la base de datos
- Usamos el mapper para convertir entre modelos OpenAPI y entidades JPA
- Manejamos casos donde la reservación no existe retornando `null` o `false`

## 🧪 Paso 7: Compilar y probar la aplicación

### 7.1 Compilar el proyecto

```bash
mvn clean compile
```

### 7.2 Ejecutar en modo desarrollo

```bash
mvn quarkus:dev
```

### 7.3 Verificar la conexión a la Base de Datos

En los logs, deberías ver algo como:

```text
2025-11-30 17:04:19,573 INFO  [io.quarkus] (Quarkus Main Thread) oas-api-rest 1.0.0-SNAPSHOT on JVM (powered by Quarkus 3.29.0) started in 2.487s. Listening on: http://localhost:8080
2025-11-30 17:04:19,574 INFO  [io.quarkus] (Quarkus Main Thread) Installed features: [agroal, cdi, hibernate-orm, hibernate-orm-panache, jdbc-mysql, rest, rest-jackson]
```

**Nota:** Si ves advertencias sobre `reservations_SEQ`, es normal - Hibernate la crea automáticamente para el manejo de IDs.

## 🔧 Paso 8: Probar con Postman - CRUD completo

### 8.1 CREATE - Crear reservación

- Método: `POST`
- URL: `http://localhost:8080/api/v1/reservations`
- Body (JSON):

```json
{
    "idClient": "BC-123",
    "activity": "Yoga",
    "dayOfWeek": "Lun",
    "time": "18:30"
}
```

Respuesta esperada: `201 Created`

```json
{
    "idReservation": 108,
    "idRoom": 1,
    "instructor": "Instructor Asignado",
    "discount": 0.0
}
```

### 8.2 READ - Obtener todas las reservaciones

- Método: `GET`
- URL: `http://localhost:8080/api/v1/reservations`

Respuesta esperada: `200 OK` con lista de todas las reservaciones

### 8.3 READ - Obtener reservación por ID

- Método: `GET`
- URL: `http://localhost:8080/api/v1/reservations/1`

Respuesta esperada: `200 OK` con los datos de la reservación:

```json
{
    "idReservation": 1,
    "idRoom": 1,
    "instructor": "María García",
    "discount": 5.0
}
```

### 8.4 UPDATE - Actualizar Reservación (PUT)

- Método: `PUT`
- URL: `http://localhost:8080/api/v1/reservations/1`
- Body (JSON):

```json
{
    "idClient": "BC-123",
    "activity": "Yoga Avanzado",
    "dayOfWeek": "Mar",
    "time": "10:30"
}
```

Respuesta esperada: `200 OK` con los datos actualizados:

```json
{
    "idReservation": 1,
    "idRoom": 1,
    "instructor": "María García",
    "discount": 5.0
}
```

💡 **Diferencia PUT vs PATCH:** PUT reemplaza completamente el recurso (requiere todos los campos), mientras que PATCH actualiza solo los campos enviados.

### 8.5 PATCH - Actualizar parcialmente reservación

- Método: `PATCH`
- URL: `http://localhost:8080/api/v1/reservations/1`
- Body (JSON) - Solo los campos que quieres cambiar:

```json
{
    "activity": "Pilates Avanzado"
}
```

O cambiar múltiples campos:

```json
{
    "activity": "Zumba",
    "time": "19:00"
}
```

Respuesta esperada: `200 OK` con los datos actualizados:

```json
{
    "idReservation": 1,
    "idRoom": 1,
    "instructor": "María García",
    "discount": 5.0
}
```

💡 **Ventaja del PATCH:** Solo necesitas enviar los campos que quieres actualizar, el resto se mantiene igual.

**Ejemplo práctico de la diferencia:**

| Operación | PUT (Reemplaza todo) | PATCH (Actualiza parcial) |
|-----------|---------------------|----------------------------|
| **Body requerido** | Todos los campos | Solo campos a cambiar |
| **Campos omitidos** | Se pierden/null | Se mantienen igual |
| **Uso típico** | Actualización completa | Cambios pequeños |

### 8.6 DELETE - Eliminar reservación

- Método: `DELETE`
- URL: `http://localhost:8080/api/v1/reservations/1`

Respuesta esperada: `200 OK` con confirmación de cancelación:

```json
{
    "idReservation": 1,
    "status": "CANCELLED",
    "message": "Reserva cancelada exitosamente",
    "cancelledAt": "2025-11-30T23:45:00Z"
}
```

## 📊 Paso 9: Verificación en la Base de Datos

Puedes verificar los cambios directamente en MySQL usando Docker:

```bash
# Conectar al contenedor MySQL
docker exec mysql-quarkus-volumes mysql -u quarkus_user -pquarkus_password reservation_system
```

```sql
-- Ver todas las reservaciones
SELECT * FROM reservations ORDER BY created_at DESC;

-- Ver reservaciones por cliente
SELECT * FROM reservations WHERE id_client = 'BC-123';

-- Ver reservaciones por actividad
SELECT * FROM reservations WHERE activity LIKE '%Yoga%';

-- Ver cambios después de PATCH (verificar que solo algunos campos cambiaron)
SELECT id, activity, day_of_week, time, updated_at 
FROM reservations 
WHERE id = 1;

-- Ver estructura de las tablas
DESCRIBE reservations;
DESCRIBE reservations_SEQ;
```

**Nota:** La tabla `reservations_SEQ` es creada automáticamente por Hibernate para manejar la generación de IDs con la estrategia de secuencias.

## 🎯 Resumen de lo aprendido

1. Configuración de MySQL con Quarkus usando `application.properties`
2. Entidades JPA con Panache para mapeo objeto-relacional
3. Patrón Mapper para conversión entre modelos OpenAPI y entidades JPA
4. Transacciones con `@Transactional` para operaciones que modifican datos
5. CRUD completo con manejo de errores básico
6. Uso de Panache para simplificar las operaciones de base de datos
7. **Diferencia entre PUT y PATCH:**
   - **PUT**: Reemplaza completamente el recurso (requiere todos los campos)
   - **PATCH**: Actualiza solo los campos enviados (actualización parcial)
8. Validación condicional en PATCH (solo actualizar campos no nulos)

## 🚀 Próximos pasos

- Agregar validaciones de negocio más complejas
- Implementar manejo de excepciones personalizado
- Agregar logging estructurado
- Configurar profiles para diferentes ambientes (dev, test, prod)
- Implementar tests unitarios e integración

¡Has completado exitosamente la integración de Quarkus con MySQL y tienes un API REST completamente funcional con operaciones CRUD!
