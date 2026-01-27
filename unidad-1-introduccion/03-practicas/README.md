# Práctica de Laboratorio: Especificando Microservicios estilo Netflix

## 🎯 Información general

**Enfoque:** Práctica técnica aplicando los conocimientos consolidados en la actividad guiada de Netflix

**Modalidad:** Laboratorio dirigido donde especificaremos microservicios usando la metodología Netflix

**Duración:** 90 minutos (complementa la actividad guiada)

**Producto:** Especificación técnica de 3 microservicios siguiendo el modelo Netflix

---

## 🏗️ PRÁCTICA: "Diseñando Microservicios como Netflix"

### 📋 Contexto de la práctica

**Basándose en todo lo aprendido sobre Netflix, ahora van a aplicar su metodología para especificar microservicios de un dominio diferente.**

**Escenario:** Diseñar la arquitectura de microservicios para "EduStream", una plataforma de cursos online que quiere seguir el modelo Netflix.

**Requisitos del sistema:**
- Usuarios: estudiantes, instructores, administradores
- Funcionalidades: cursos, videos, evaluaciones, certificados, pagos
- Escala objetivo: 100k usuarios concurrentes

---

## 🔬 EJERCICIO PRÁCTICO (90 min total)

### 🟢 FASE 1: Identificación de bounded contexts (30 min)

**Siguiendo el método Netflix, identificar los servicios principales:**

#### Actividad dirigida:
1. **Análisis funcional** (15 min)
   - Listar todas las funcionalidades de EduStream
   - Agrupar por responsabilidades cohesivas
   - Identificar entidades clave y sus relaciones

2. **Aplicar principios Netflix** (15 min)
   - Una responsabilidad = un microservicio
   - Equipos autónomos = servicios independientes
   - Datos no compartidos entre servicios

#### Template a completar:

```
📚 EduStream - Bounded Contexts Identificados:

[  ] User Service
    Responsabilidad: _____________
    Entidades: ___________________
    Operaciones: ________________

[  ] Course Service  
    Responsabilidad: _____________
    Entidades: ___________________
    Operaciones: ________________

[  ] Video Service
    Responsabilidad: _____________
    Entidades: ___________________
    Operaciones: ________________

[  ] Assessment Service
    Responsabilidad: _____________
    Entidades: ___________________
    Operaciones: ________________

[  ] Payment Service
    Responsabilidad: _____________
    Entidades: ___________________
    Operaciones: ________________
```

---

### 🟡 FASE 2: Especificación técnica de APIs (40 min)

**Diseñar las APIs REST siguiendo estándares Netflix:**

#### 2.1 User Service API (15 min)

```http
### Endpoints a diseñar ###

POST /users
GET /users/{userId}  
PUT /users/{userId}
GET /users/{userId}/enrollments
POST /users/{userId}/enroll/{courseId}

### Especificar contratos ###
POST /users
{
  "email": "student@example.com",
  "name": "John Doe",
  "role": "student" // student, instructor, admin
}

Response:
{
  "userId": "uuid",
  "email": "student@example.com", 
  "name": "John Doe",
  "role": "student",
  "createdAt": "2024-01-26T10:00:00Z"
}
```

#### 2.2 Course Service API (15 min)

```http
### Diseñar endpoints ###

POST /courses
GET /courses
GET /courses/{courseId}
PUT /courses/{courseId}
POST /courses/{courseId}/modules
GET /courses/{courseId}/modules

### Ejemplo de contrato ###
POST /courses
{
  "title": "Microservices Architecture",
  "description": "Learn microservices with real examples",
  "instructorId": "uuid",
  "price": 99.99,
  "duration": 40 // hours
}
```

#### 2.3 Video Service API (10 min)

```http
### Endpoints críticos (estilo Netflix streaming) ###

GET /videos/{videoId}/stream
POST /videos/{videoId}/progress
GET /videos/{videoId}/analytics

### Consideraciones técnicas ###
- Streaming adaptativo (como Netflix)
- Progress tracking por usuario
- Analytics de visualización
```

---

### 🟠 FASE 3: Definir integraciones y comunicación (20 min)

**Especificar cómo se comunican los servicios (patrón Netflix):**

#### 3.1 Comunicación síncrona (REST)

```
User enrolls in course:
Frontend → User Service → Course Service (validate course exists)
                       → Payment Service (process payment)  
                       → User Service (confirm enrollment)
```

#### 3.2 Comunicación asíncrona (Events)

```
Course completed event:
User Service publishes: CourseCompleted {userId, courseId, completedAt}

Subscribers:
- Certificate Service → generates certificate
- Analytics Service → updates metrics  
- Recommendation Service → updates ML model
```

#### 3.3 Patrones de resiliencia (estilo Netflix)

```
Circuit Breaker examples:
- User Service → Payment Service (timeout: 5s, fallback: pending payment)
- Course Service → Video Service (fallback: placeholder video)

API Gateway routing:
/api/users/* → User Service
/api/courses/* → Course Service  
/api/videos/* → Video Service
```

---

## 📊 Entregables de la práctica

### Especificación técnica completa

1. **Bounded Contexts Document**
   - 5 microservicios identificados con responsabilidades claras
   - Justificación de la descomposición (principios Netflix aplicados)

2. **API Specifications** 
   - Endpoints REST para cada servicio
   - Contratos de request/response con ejemplos
   - Status codes y manejo de errores

3. **Integration Map**
   - Diagrama de comunicación entre servicios
   - Identificación de llamadas síncronas vs asíncronas
   - Eventos y subscribers definidos

4. **Resilience Patterns**
   - Circuit breakers especificados
   - Fallback strategies por servicio
   - API Gateway configuration

---

## 🔍 Criterios de evaluación

| Aspecto | Peso | Descripción |
|---------|------|-------------|
| **Bounded contexts apropiados** | 30% | Servicios con responsabilidades cohesivas y bien desacoplados |
| **APIs bien diseñadas** | 25% | Endpoints RESTful, contratos claros, manejo de errores |
| **Comunicación efectiva** | 25% | Integración sync/async apropiada, eventos bien definidos |
| **Patrones de resiliencia** | 20% | Circuit breakers, fallbacks y API Gateway correctos |

### Rubrica detallada

**Excelente (90-100):**
- Bounded contexts reflejan principios Netflix perfectamente aplicados
- APIs siguen estándares REST con contratos completos
- Comunicación optimizada (sync para consistency, async para performance)
- Patrones de resiliencia apropiados para cada interacción

**Bueno (80-89):**
- Servicios bien identificados con minor overlaps
- APIs funcionales con la mayoría de contratos especificados
- Comunicación adecuada con algunas optimizaciones faltantes
- Patrones básicos de resiliencia aplicados

**Satisfactorio (70-79):**
- Servicios identificados pero con algunas responsabilidades poco claras
- APIs básicas pero funcionales
- Comunicación funcional pero no optimizada
- Patrones de resiliencia mínimos

---

## 🧰 Recursos de apoyo

### Templates proporcionados

**Bounded Context Template:**
```
Service Name: ___________
Responsibility: ___________  
Data Owned: ___________
Operations: ___________
Team Size: _____ people
Dependencies: ___________
```

**API Endpoint Template:**
```
Method: POST/GET/PUT/DELETE
Path: /resource/{id}
Purpose: ___________
Request Body: {...}  
Response: {...}
Error Codes: 400, 401, 404, 500
```

**Integration Template:**
```
From: Service A
To: Service B  
Type: Sync/Async
Purpose: ___________
Fallback: ___________
```

### Herramientas recomendadas

- **API Design**: Swagger/OpenAPI Editor
- **Diagramas**: Draw.io, Lucidchart
- **Collaboration**: Miro para integrations map

### Referencias técnicas

**Netflix Architecture Patterns:**
- API Gateway: Kong, Zuul patterns
- Service Discovery: Eureka patterns  
- Circuit Breaker: Hystrix patterns
- Event Streaming: Kafka patterns

**REST API Best Practices:**
- Resource naming conventions
- HTTP status codes usage
- Error response formats
- Pagination and filtering

---

## 🎯 Conexión con actividad guiada

**Esta práctica aplica directamente lo aprendido:**

1. **Principios Netflix** → Aplicados a EduStream bounded contexts
2. **Trade-offs analysis** → Decisiones sync vs async communication  
3. **Resilience patterns** → Circuit breakers y fallbacks especificados
4. **Scalability** → API design for 100k concurrent users

**Prepara para unidades siguientes:**
- **Unidad 2**: Implementación técnica de los microservicios especificados
- **Unidad 3**: Despliegue y containerización de la arquitectura
- **Proyecto Final**: Metodología completa aplicable a cualquier dominio

---

## ✅ Checklist de completitud

### Durante la práctica
- [ ] **Fase 1**: Identificar 5 bounded contexts con responsabilidades claras
- [ ] **Fase 2**: Especificar APIs REST con contratos completos
- [ ] **Fase 3**: Definir integraciones y patrones de resiliencia

### Entregables finales
- [ ] Documento de bounded contexts justificados
- [ ] Especificaciones de API con ejemplos
- [ ] Mapa de integraciones entre servicios
- [ ] Patrones de resiliencia especificados

### Auto-evaluación
- [ ] ¿Los servicios siguen principios Netflix (cohesión + desacoplamiento)?
- [ ] ¿Las APIs son RESTful y están bien documentadas?
- [ ] ¿La comunicación está optimizada (sync vs async apropiado)?
- [ ] ¿Los patrones de resiliencia cubren los puntos de falla principales?

---

**Siguiente:** [Recursos y Referencias →](../04-recursos/README.md)
