# 🚀 Curso Express: UML para Microservicios y Contenedores

## 🎯 Objetivo

Guía condensada de los diagramas UML esenciales para el diseño, desarrollo y despliegue de microservicios que serán containerizados en Docker/Kubernetes.

## 📋 Prerequisitos

- Conocimientos básicos de arquitectura de software
- Conceptos de microservicios (Unidad 1)
- Domain-Driven Design básico (Unidad 2) 

---

## 🧭 Roadmap UML para microservicios

```mermaid
flowchart TD
    A[📋 Casos de Uso] --> B[🏗️ Clases de Dominio]
    B --> C[🔄 Diagramas de Secuencia]
    C --> D[🚀 Despliegue]
    
    A --> E[Definir límites<br/>de contexto]
    B --> F[Identificar<br/>agregados]
    C --> G[Patrones de<br/>comunicación]
    D --> H[Infraestructura<br/>K8s/Docker]

    style A fill:#e1f5fe
    style B fill:#f3e5f5
    style C fill:#e8f5e8
    style D fill:#fff3e0
```

---

## 1. 📋 Casos de uso: Definiendo fronteras de microservicios

### 🎯 ¿Por qué son críticos?

Los casos de uso nos ayudan a:
- **Identificar Bounded Contexts** (base para microservicios)
- **Definir APIs** que expondrán los servicios
- **Establecer contratos** entre servicios

### 🛠️ Ejemplo:

```mermaid
flowchart TD
    Cliente(("Cliente"))
    SistemaPagos["Sistema Pagos"]
    SistemaNotificaciones["Sistema Notificaciones"]
    
    subgraph "E-Commerce Microservices"
        RealizarPedido(["Realizar Pedido"])
        ProcesarPago(["Procesar Pago"])
        GestionarInventario(["Gestionar Inventario"])
        EnviarConfirmacion(["Enviar Confirmación"])
    end
    
    Cliente --> RealizarPedido
    RealizarPedido --> ProcesarPago
    ProcesarPago --> SistemaPagos
    RealizarPedido --> GestionarInventario
    RealizarPedido --> EnviarConfirmacion
    EnviarConfirmacion --> SistemaNotificaciones
    
    classDef microservice fill:#e6f7ff,stroke:#1890ff
    classDef external fill:#f6ffed,stroke:#52c41a
    
    class RealizarPedido,ProcesarPago,GestionarInventario,EnviarConfirmacion microservice
    class SistemaPagos,SistemaNotificaciones external
```

> 📝 **Notas del diagrama:**
> - **Realizar Pedido**: Orquesta el proceso completo del pedido
> - **Procesar Pago**: Maneja transacciones monetarias  
> - **Gestionar Inventario**: Controla disponibilidad de productos

### 🔥 Tips:

1. **Un caso de uso = Un microservicio potencial**
2. **Actores externos = Integraciones que diseñar**
3. **Dependencias entre casos de uso = Comunicación entre servicios**

### 📐 Criterios de separación

| ✅ **Separar en microservicio** | ❌ **Mantener junto** |
|-----------------------------|--------------------|
| Diferentes dominios de negocio | Misma transacción ACID requerida |
| Escalado independiente requerido | Comunicación muy frecuente |
| Equipos diferentes | Datos altamente relacionados |
| Evolución de negocio independiente | Cambios siempre coordinados |

---

## 2. 🏗️ Clases de Dominio: Del DDD al código

### 🎯 ¿Por qué son esenciales?

- **Traducen conceptos** de DDD a estructuras de código
- **Definen agregados** (transaccional boundaries)
- **Establecen DTOs/APIs** entre servicios

### 🛠️ Ejemplo:

```mermaid
classDiagram
    class Order {
        <<AggregateRoot>>
        -OrderId id
        -CustomerId customerId
        -OrderStatus status
        -LocalDateTime orderDate
        -List~OrderItem~ items
        +placeOrder()
        +cancelOrder()
        +addItem(item OrderItem)
    }
    
    class OrderItem {
        <<Entity>>
        -ProductId productId
        -Integer quantity
        -BigDecimal unitPrice
        +calculateSubTotal() BigDecimal
    }
    
    class OrderStatus {
        <<ValueObject>>
        -String value
        +isPending() boolean
        +isCompleted() boolean
    }
    
    class Payment {
        <<AggregateRoot>>
        -PaymentId id
        -OrderId orderId
        -BigDecimal amount
        -PaymentStatus status
        +processPayment() PaymentResult
    }
    
    class OrderDTO {
        -String orderId
        -String customerId
        -BigDecimal totalAmount
    }
    
    class PaymentRequest {
        -String orderId
        -BigDecimal amount
        -String currency
    }
    
    Order *-- OrderItem : contains
    Order --> OrderStatus : has
    Order ..> OrderDTO : creates
    Payment ..> PaymentRequest : uses
    OrderDTO ..> PaymentRequest : maps to
```

> 📝 **Notas del diagrama:**
> - **Order**: Aggregate Root para transacciones de orden (Order Service)
> - **Payment**: Microservicio separado para pagos (Payment Service)
> - **OrderDTO**: DTO para comunicación entre microservicios

### 🔥 Tips:

1. **Aggregate Root** → Microservice boundary
2. **Value Objects** → Inmutables, compartibles
3. **DTOs** → Contratos de API entre servicios
4. **Entities** dentro del mismo agregado → Mismo microservicio

### 📄 Mapeo DDD → Microservicios

| **Concepto DDD** | **Implementación** | **Docker/K8s**   |
| ---------------- | ------------------ | ---------------- |
| Bounded Context  | Microservice       | Pod/Deployment   |
| Aggregate Root   | Service Class      | Container        |
| Repository       | Data Access Layer  | ConfigMap/Secret |
| Domain Event     | Message/Event      | Message Queue    |

---

## 3. 🔄 Diagramas de Secuencia: Comunicación entre servicios

### 🎯 ¿Por qué son críticos?

- **Diseñan la comunicación** entre microservicios
- **Identifican patrones** (Saga, CQRS, Event Sourcing)
- **Definen APIs** y contratos de integración

### 🛠️ Ejemplo: Patrón Saga

```mermaid
sequenceDiagram
    participant Client
    participant OS as Order Service
    participant PS as Payment Service
    participant IS as Inventory Service
    participant MQ as Message Queue
    
    Note over Client,MQ: 🟢 Proceso Feliz
    
    Client->>+OS: POST /orders
    OS->>OS: validateOrder()
    OS->>MQ: PublishEvent(OrderCreated)
    OS-->>-Client: 201 Created {orderId}
    
    MQ->>+IS: OrderCreated Event
    IS->>IS: reserveInventory()
    IS->>MQ: PublishEvent(InventoryReserved)
    IS-->>-MQ: 
    
    MQ->>+PS: InventoryReserved Event
    PS->>PS: processPayment()
    PS->>MQ: PublishEvent(PaymentCompleted)
    PS-->>-MQ: 
    
    MQ->>+OS: PaymentCompleted Event
    OS->>OS: completeOrder()
    OS->>MQ: PublishEvent(OrderCompleted)
    OS-->>-MQ: 
    
    Note over Client,MQ: 🔴 Proceso de Compensación
    Note over MQ: Si falla el pago...
    
    MQ->>+PS: PaymentFailed Event
    PS->>MQ: PublishEvent(PaymentFailed)
    PS-->>-MQ: 
    
    MQ->>+IS: PaymentFailed Event
    IS->>IS: releaseInventory()
    IS->>MQ: PublishEvent(InventoryReleased)
    IS-->>-MQ: 
    
    MQ->>+OS: InventoryReleased Event
    OS->>OS: cancelOrder()
    OS-->>-MQ: 
```

### 🛠️ Ejemplo: Patrón API Gateway

```mermaid
sequenceDiagram
    participant MA as Mobile App
    participant WA as Web App
    participant AG as API Gateway
    participant AS as Auth Service
    participant OS as Order Service
    participant US as User Service
    
    Note over MA,US: 🔐 Autenticación y Routing
    
    MA->>+AG: GET /api/orders
    AG->>AS: validateToken()
    AS-->>AG: 200 OK {userId}
    
    AG->>+OS: GET /orders?userId={userId}
    OS-->>-AG: 200 OK {orders[]}
    
    AG-->>-MA: 200 OK {orders[]}
    
    Note over MA,US: 📊 Composición de Datos
    
    WA->>+AG: GET /api/dashboard
    
    par Llamadas paralelas
        AG->>OS: GET /orders?userId={userId}
    and
        AG->>US: GET /user-profile/{userId}
    end
    
    OS-->>AG: orders data
    US-->>AG: profile data
    
    AG->>AG: composeResponse()
    AG-->>-WA: 200 OK {dashboard}
```

> 📝 **Funcionalidades del API Gateway:**
> - **Autenticación/Autorización**: Validación centralizada de tokens
> - **Rate Limiting**: Control de límites de solicitudes
> - **Load Balancing**: Distribución de carga entre instancias
> - **Response Composition**: Agregación de datos de múltiples servicios

### 🔥 Tips:

1. **Síncronos** → REST APIs (para queries simples)
2. **Asíncronos** → Events/Messages (para procesos complejos)
3. **Gateway** → Punto único de entrada
4. **Timeouts** y **Circuit Breakers** → Resiliencia

### 📋 Checklist de comunicación

- [ ] **¿Transacción distribuida?** → Consider Saga Pattern
- [ ] **¿Query complejo?** → Consider CQRS  
- [ ] **¿Necesita auditabilidad?** → Consider Event Sourcing
- [ ] **¿Cliente externo?** → Use API Gateway
- [ ] **¿Comunicación real-time?** → WebSockets/SSE

---

## 4. 🚀 Diagramas de Despliegue: Docker + Kubernetes

### 🎯 ¿Por qué son esenciales?

- **Visualizan la infraestructura** de containers
- **Identifican dependencias** entre servicios
- **Planifican recursos** y escalado
- **Documentan configuración** de producción

### 🛠️ Ejemplo: Arquitectura completa

```mermaid
flowchart TD
    subgraph k8s["Kubernetes Cluster"]
        
        subgraph ingress["Ingress Layer"]
            nginx["NGINX Ingress<br/>LoadBalancer"]
        end
        
        subgraph gateway_ns["API Gateway Namespace"]
            gateway["API Gateway<br/>Pod"]
            cache[("Redis Cache<br/>StatefulSet")]
            gateway --> cache
        end
        
        subgraph microservices["Microservices Namespace"]
            order["Order Service<br/>Deployment"]
            payment["Payment Service<br/>Deployment"]
            inventory["Inventory Service<br/>Deployment"]
            user["User Service<br/>Deployment"]
            
            orderdb[("Order DB<br/>StatefulSet")]
            paymentdb[("Payment DB<br/>StatefulSet")]
            inventorydb[("Inventory DB<br/>StatefulSet")]
            userdb[("User DB<br/>StatefulSet")]
            
            order --> orderdb
            payment --> paymentdb
            inventory --> inventorydb
            user --> userdb
        end
        
        subgraph infrastructure["Infrastructure Namespace"]
            mq["Message Queue<br/>(RabbitMQ)<br/>StatefulSet"]
            monitor["Monitoring<br/>(Prometheus)<br/>DaemonSet"]
            logging["Logging<br/>(Fluentd)<br/>DaemonSet"]
        end
        
    end
    
    subgraph external["External Services"]
        external_pay["Payment Gateway<br/>(Stripe/PayPal)"]
        external_email["Email Service<br/>(SendGrid)"]
    end
    
    nginx --> gateway
    gateway --> order
    gateway --> payment
    gateway --> inventory
    gateway --> user
    
    order --> mq
    payment --> mq
    inventory --> mq
    
    payment --> external_pay
    user --> external_email
    
    monitor -.-> order
    monitor -.-> payment
    monitor -.-> inventory
    monitor -.-> user
    
    logging -.-> order
    logging -.-> payment
    logging -.-> inventory
    logging -.-> user
    
    classDef ingressStyle fill:#e1f5fe,stroke:#0277bd,stroke-width:2px
    classDef gatewayStyle fill:#f3e5f5,stroke:#7b1fa2,stroke-width:2px
    classDef serviceStyle fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef databaseStyle fill:#fff3e0,stroke:#ef6c00,stroke-width:2px
    classDef infraStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    classDef externalStyle fill:#f1f8e9,stroke:#558b2f,stroke-width:2px
    
    class nginx ingressStyle
    class gateway,cache gatewayStyle
    class order,payment,inventory,user serviceStyle
    class orderdb,paymentdb,inventorydb,userdb databaseStyle
    class mq,monitor,logging infraStyle
    class external_pay,external_email externalStyle
```

> 📝 **Notas de la arquitectura:**
> - **NGINX Ingress**: Entry point - 443 HTTPS
> - **API Gateway**: Authentication, Rate Limiting, Load Balancing
> - **Message Queue**: Asynchronous Communication
> - **Payment Gateway**: PCI Compliance Required

### 🛠️ Ejemplo: Configuración de servicios

```mermaid
flowchart TD
    subgraph pod["Order Service Pod"]
        api["order-api:1.2.3<br/>Container"]
        db["postgres:13<br/>Sidecar"]
    end
    
    subgraph config_section["Configuration"]
        config["ConfigMap<br/>📄<br/>DATABASE_URL<br/>RABBITMQ_URL<br/>JWT_SECRET_KEY"]
        secret["Secret<br/>🔐<br/>DB_PASSWORD<br/>RABBITMQ_PASSWORD"]
        storage["PVC<br/>💾<br/>Storage: 10Gi<br/>ReadWriteOnce"]
    end
    
    config -.->|env vars| api
    secret -.->|env vars| api
    storage -.->|mount /var/lib/postgresql| db
    
    classDef containerStyle fill:#e3f2fd,stroke:#1976d2,stroke-width:2px
    classDef configStyle fill:#f1f8e9,stroke:#689f38,stroke-width:2px
    classDef secretStyle fill:#fce4ec,stroke:#c2185b,stroke-width:2px
    classDef storageStyle fill:#fff3e0,stroke:#f57c00,stroke-width:2px
    
    class api,db containerStyle
    class config configStyle
    class secret secretStyle
    class storage storageStyle
```

> 📝 **Tipos de configuración:**
> - **ConfigMap**: Non-sensitive configuration
> - **Secret**: Encrypted storage
> - **PVC**: Persistent data

### 🔥 Tips:

1. **Un microservicio** → Un Deployment en K8s
2. **Datos stateful** → StatefulSet + PVC
3. **Configuración** → ConfigMaps y Secrets
4. **Comunicación** → Services + Ingress
5. **Observabilidad** → Sidecar containers

### 📊 Mapeo: Microservicio → Kubernetes

| **Concepto** | **Kubernetes** | **Docker** |
|-------------|---------------|-----------|
| Microservice | Deployment | Container |
| Database | StatefulSet | Volume |
| Configuration | ConfigMap | ENV vars |
| Secrets | Secret | ENV vars |
| Load Balancer | Service | Port mapping |
| API Gateway | Ingress | Nginx container |

---

## 🎯 Metodología de aplicación

### Paso 1: Análisis de dominio
1. **Casos de Uso** → Identificar Bounded Contexts
2. **Separación de responsabilidades** → Definir microservicios

### Paso 2: Diseño detallado  
1. **Clases de Dominio** → Definir agregados y APIs
2. **Secuencias** → Diseñar comunicación entre servicios

### Paso 3: Preparación para implementación
1. **Despliegue** → Planificar infraestructura K8s
2. **APIs OpenAPI** → Documentar contratos

### 🔄 Iteración continua

```mermaid
graph LR
    A[Casos de Uso] --> B[Clases]
    B --> C[Secuencias]  
    C --> D[Despliegue]
    D --> E[OpenAPI]
    E --> F[Código]
    F --> A
    
    style E fill:#e1f5fe
    style F fill:#f3e5f5
```

---

### 🛠️ Tools recomendadas

- **Mermaid** → Diagramas como código (nativo en GitHub) ⭐
- **Draw.io** → Diagramas visuales rápidos
- **PlantUML** → Para casos específicos avanzados
- **Kubernetes Dashboard** → Visualización de despliegue en tiempo real

---

## 📚 Conexión con OpenAPI

Los DTOs de tus diagramas de clase se convertirán directamente en:

```yaml
components:
  schemas:
    OrderDTO:
      type: object
      properties:
        orderId:
          type: string
        customerId:
          type: string  
        totalAmount:
          type: number
          format: double
```

### 🔄 Flujo completo: UML → OpenAPI → Código

1. **Casos de Uso** → Definir endpoints REST
2. **Clases/DTOs** → OpenAPI schemas 
3. **Secuencias** → OpenAPI operations
4. **Despliegue** → OpenAPI servers

¡Listo para modelar APIs y construir código! 🚀