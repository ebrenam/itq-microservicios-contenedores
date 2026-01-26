# **UNIDAD 1: Introducción a Microservicios**
## **Arquitecturas Evolutivas**
### CDD-2601 | Enero 2026

---

## 📋 **AGENDA DE LA UNIDAD**

### **🎯 Objetivos:**
- ✅ Comprender la evolución arquitectónica hacia microservicios
- ✅ Diferenciar Monolitos, SOA y Microservicios  
- ✅ Identificar ventajas, riesgos y casos de uso
- ✅ Analizar transformaciones reales de la industria

### 3 subtemas | 2 semanas

---

# **1.1 CONTEXTO HISTÓRICO Y EVOLUCIÓN**

---

## 🏢 **ARQUITECTURA MONOLÍTICA**

### **¿Qué es un Monolito?**
```
┌─────────────────────────────────────┐
│        APLICACIÓN MONOLÍTICA        │
├─────────────────────────────────────┤
│  UI Layer                          │
│  Business Logic Layer              │ 
│  Data Access Layer                 │
│  Database                          │
└─────────────────────────────────────┘
```

### **✅ Ventajas del Monolito:**
- **Simplicidad:** Una sola aplicación para desarrollar y desplegar
- **Testing:** Pruebas end-to-end más directas
- **Debugging:** Stack traces completos y fácil troubleshooting
- **Rendimiento:** Sin latencia de red entre componentes

---

## 😰 **EL "MONOLITO INTOLERABLE"**

### **❌ Problemas que surgen:**

#### **🚀 Escalabilidad:**
- Toda la aplicación debe escalarse junta
- No se puede escalar componentes específicos independientemente

#### **👥 Equipos:**
- Múltiples equipos trabajando en el mismo código base
- Conflictos de merge y dependencias entre equipos

#### **🔧 Tecnología:**
- Atado a una sola tecnología/framework
- Actualizaciones riesgosas afectan toda la aplicación

#### **📦 Despliegues:**
- Releases grandes y riesgosos
- Un bug puede tumbar todo el sistema

---

## 🌐 **SERVICE-ORIENTED ARCHITECTURE (SOA)**

### **Evolución hacia servicios:**
```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│   Service   │◄──►│   Service   │◄──►│   Service   │
│      A      │    │      B      │    │      C      │
└─────────────┘    └─────────────┘    └─────────────┘
       ▲                  ▲                  ▲
       └──────────────────┼──────────────────┘
                          ▼
              ┌─────────────────────┐
              │   Enterprise Bus    │
              │   (ESB)            │
              └─────────────────────┘
```

### **🎯 Principios SOA:**
- **Reutilización:** Servicios compartidos entre aplicaciones
- **Interoperabilidad:** Estándares como SOAP, WSDL
- **Gobernanza:** Control centralizado mediante ESB
- **Abstracción:** Servicios como cajas negras

---

## 🔄 **SOA vs MICROSERVICIOS**

| **Aspecto** | **SOA** | **Microservicios** |
|-------------|---------|-------------------|
| **Tamaño** | Servicios grandes | Servicios pequeños |
| **Comunicación** | ESB centralizado | HTTP/REST directo |
| **Datos** | Bases de datos compartidas | DB por servicio |
| **Despliegue** | Monolítico | Independiente |
| **Governance** | Centralizada | Descentralizada |
| **Tecnología** | Estándares pesados (SOAP) | Protocolos ligeros (REST) |

---

## 🚀 **TRANSICIÓN A MICROSERVICIOS**

### **📖 Definición:**
> *"Los microservicios son un enfoque arquitectónico para construir aplicaciones como un conjunto de servicios pequeños, autónomos que se comunican a través de APIs bien definidas."*

### **🔑 Características Clave:**
- **🎯 Una responsabilidad:** Cada servicio hace una cosa bien
- **🔄 Desarrollo independiente:** Equipos autónomos 
- **📦 Despliegue independiente:** Ciclos de release separados
- **💾 Datos independientes:** Base de datos por servicio
- **🌐 Comunicación ligera:** REST, messaging

---

# **1.2 PRINCIPIOS FUNDAMENTALES**

---

## 🔗 **DESACOPLAMIENTO (COUPLING)**

### **Alto Acoplamiento = Problemas:**
```
Service A ──┬── Service B ──┬── Service C
            │               │
            └── Service D ──┴── Service E
```
**❌ Cambio en uno afecta a todos**

### **Bajo Acoplamiento = Flexibilidad:**
```
Service A ──API──> Service B
Service C ──API──> Service D  
Service E ──API──> Service F
```
**✅ Servicios independientes**

### **🎯 Tipos de Desacoplamiento:**
- **Temporal:** No necesitan estar activos al mismo tiempo
- **Espacial:** No necesitan conocer ubicaciones específicas
- **Tecnológico:** Diferentes lenguajes y frameworks

---

## 🎯 **COHESIÓN**

### **Alta Cohesión Interna:**
```
┌─────────────────────────────────┐
│     USER SERVICE               │
├─────────────────────────────────┤
│ • getUserProfile()             │
│ • updateUserProfile()          │  ← Funciones relacionadas
│ • validateUserData()           │    juntas
│ • hashPassword()               │
└─────────────────────────────────┘
```

### **❌ Baja Cohesión - Evitar:**
```
┌─────────────────────────────────┐
│     MIXED SERVICE              │
├─────────────────────────────────┤
│ • getUserProfile()             │  ← Usuario
│ • processPayment()             │  ← Pago
│ • sendEmail()                  │  ← Email  
│ • generateReport()             │  ← Reportes
└─────────────────────────────────┘
```

---

## 📦 **MODULARIDAD**

### **Bounded Context (DDD):**
```
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│   USER CONTEXT  │  │  ORDER CONTEXT  │  │ PAYMENT CONTEXT │
├─────────────────┤  ├─────────────────┤  ├─────────────────┤
│ • User Entity   │  │ • Order Entity  │  │ • Payment Entity│
│ • User Service  │  │ • Order Service │  │ • Payment Service│
│ • User DB       │  │ • Order DB      │  │ • Payment DB    │
└─────────────────┘  └─────────────────┘  └─────────────────┘
```

### **🎯 Principios de Modularidad:**
- **Single Responsibility:** Una razón para cambiar
- **Interface Segregation:** APIs específicas por cliente
- **Dependency Inversion:** Depender de abstracciones

---

## 👥 **AUTONOMÍA DE EQUIPOS**

### **Estructura Tradicional:**
```
Frontend Team ──┐
                ├── Shared Database
Backend Team ───┘
```
**❌ Dependencias entre equipos**

### **Estructura Microservicios:**
```
Team A ──► Service A + DB A
Team B ──► Service B + DB B  
Team C ──► Service C + DB C
```
**✅ Equipos completamente autónomos**

### **🚀 Beneficios:**
- **Velocidad:** Sin esperar a otros equipos
- **Innovación:** Tecnologías propias por equipo
- **Responsabilidad:** Ownership completo del servicio

---

## 💾 **BASE DE DATOS POR SERVICIO**

### **❌ Antipatrón - DB Compartida:**
```
Service A ──┐
            ├──► [Shared Database]
Service B ──┘
```

### **✅ Patrón Correcto:**
```
Service A ──► [Database A]
Service B ──► [Database B]
Service C ──► [Database C]
```

### **🎯 Ventajas:**
- **Evolución independiente:** Cambios de schema sin coordinación
- **Tecnología apropiada:** SQL vs NoSQL según necesidad
- **Aislamiento de fallos:** Problema en una DB no afecta otras

---

# **1.3 CASOS DE ESTUDIO**

---

## 📺 **NETFLIX: De DVD a Streaming Global**

### **🎬 El Desafío:**
- **2008:** Servicio DVD por correo + streaming naciente
- **Problema:** Monolito no podía escalar para streaming masivo
- **Meta:** Soportar millones de usuarios simultáneos globalmente

### **🏗️ Transformación:**
```
ANTES (2008)              DESPUÉS (2015)
┌─────────────────┐      ┌─── User Service
│                 │      ├─── Video Service  
│   DVD Monolith  │  ──► ├─── Recommendation Service
│                 │      ├─── Billing Service
└─────────────────┘      └─── Analytics Service
                              ... +700 servicios
```

### **📊 Resultados:**
- **+700 microservicios** desplegados independientemente
- **Disponibilidad:** 99.99% uptime global
- **Escalabilidad:** Billions de horas de video al mes

---

## 🚗 **UBER: Escalando la Movilidad**

### **🚀 Crecimiento Explosivo:**
- **2010:** Startup simple de taxis
- **2015:** Operaciones globales complejas
- **Servicios:** UberEATS, UberFREIGHT, UberAIR

### **🏗️ Arquitectura Microservicios:**
```
┌─── Trip Service ────┐   ┌─── Driver Service ───┐
│ • Route planning    │   │ • Driver matching    │
│ • ETA calculation   │   │ • Driver tracking    │
└─────────────────────┘   └──────────────────────┘

┌─── Payment Service ─┐   ┌─── Notification ─────┐
│ • Payment processing│   │ • Push notifications │
│ • Pricing calculation   │ • SMS/Email         │
└─────────────────────┘   └──────────────────────┘
```

### **🎯 Lecciones Aprendidas:**
- **Domain-Driven Design** para definir servicios
- **Event-driven architecture** para comunicación
- **Circuit breakers** para resiliencia

---

## 🛒 **AMAZON: La Plataforma de Plataformas**

### **📈 Escala Masiva:**
- **Millones** de productos
- **Cientos de millones** de usuarios
- **Miles de desarrolladores** internos

### **🏗️ Estrategia "Two-Pizza Teams":**
```
┌─────────────────────────────────────────────────┐
│              AMAZON ECOSYSTEM                   │
├─────────────────────────────────────────────────┤
│ Product Service │ Cart Service │ Review Service │
├─────────────────────────────────────────────────┤
│ Payment Service │ Ship Service │ Track Service  │
├─────────────────────────────────────────────────┤
│    AWS Service  │ Alexa Service│  Prime Service │
└─────────────────────────────────────────────────┘
```

### **🔑 Principios Amazon:**
- **API First:** Todo servicio debe tener API
- **Decentralized:** Cada equipo = dueño de su servicio  
- **Scalable:** Diseñado para escalar horizontalmente

---

## 🤔 **¿CUÁNDO USAR MICROSERVICIOS?**

### **✅ Casos Apropiados:**
- **Equipos grandes** (>50 desarrolladores)
- **Dominios complejos** con múltiples bounded contexts
- **Escalabilidad diferenciada** por componentes
- **Innovación tecnológica** constante
- **Deployment independiente** crítico

### **❌ Casos NO Apropiados:**
- **Equipos pequeños** (<10 desarrolladores)
- **Dominios simples** bien definidos
- **Aplicaciones CRUD** básicas
- **Startups tempranas** buscando product-market fit
- **Sistemas con transacciones ACID** complejas

---

## ⚡ **TRADE-OFFS DE MICROSERVICIOS**

### **✅ VENTAJAS:**
| **Aspecto** | **Beneficio** |
|-------------|---------------|
| **🚀 Escalabilidad** | Escalar servicios independientemente |
| **🛠️ Tecnología** | Diversidad tecnológica por equipo |
| **⚡ Deployment** | Releases independientes y frecuentes |
| **🔒 Resiliencia** | Fault isolation entre servicios |
| **👥 Equipos** | Autonomía y ownership completo |

### **❌ DESAFÍOS:**
| **Aspecto** | **Reto** |
|-------------|----------|
| **🌐 Complejidad** | Distributed systems complexity |
| **🔄 Comunicación** | Network latency y timeouts |
| **🗃️ Datos** | Eventual consistency |
| **🐛 Debugging** | Trazas distribuidas complejas |
| **🚀 Deployment** | Orchestration y service discovery |

---

## 🎯 **ESTRUCTURA ORGANIZACIONAL**

### **⚖️ LEY DE CONWAY:**
> *"Las organizaciones que diseñan sistemas están constreñidas a producir diseños que copian las estructuras de comunicación de estas organizaciones."*

### **Tradicional vs Microservicios:**
```
TRADICIONAL                   MICROSERVICIOS
┌─────────────┐              ┌─── Team A ──► Service A
│ Monolithic  │              ├─── Team B ──► Service B
│ Team        │     VS       ├─── Team C ──► Service C
│             │              └─── Team D ──► Service D
└─────────────┘
```

### **🔄 "Inverse Conway Maneuver":**
1. **Diseñar** la arquitectura deseada
2. **Reorganizar** equipos según la arquitectura
3. **Resultado:** Sistema que refleja estructura organizacional

---

## 📋 **RESUMEN UNIDAD 1**

### **🎯 Conceptos Clave:**
- **Evolución:** Monolito → SOA → Microservicios
- **Principios:** Desacoplamiento, Cohesión, Autonomía
- **Trade-offs:** Ventajas vs Complejidad distribuida
- **Casos reales:** Netflix, Uber, Amazon

### **🤝 Próxima Unidad:**
**Diseño y Modelado** - Aprenderemos Domain-Driven Design y patrones arquitectónicos para estructurar microservicios efectivamente.

### **📚 Lecturas Recomendadas:**
- Newman, S. - "Building Microservices" Cap. 1-3
- Fowler, M. - "Microservices" article
- Richardson, C. - "Microservice Patterns" Cap. 1

---

## 🎓 **ACTIVIDADES DE APRENDIZAJE**

### **📊 Práctica 1.1: Análisis Comparativo**
- Matriz comparativa: Monolito vs SOA vs Microservicios
- Criterios de evaluación para migración
- Casos de uso específicos

### **📊 Práctica 1.2: Estudio de Caso**
- Análisis transformación Netflix/Uber/Amazon
- Mapa conceptual de componentes
- Aplicación al proyecto final

### **💡 Reflexión:**
*"¿Cuál sería tu estrategia para convencer a una empresa con monolito exitoso de migrar a microservicios?"*