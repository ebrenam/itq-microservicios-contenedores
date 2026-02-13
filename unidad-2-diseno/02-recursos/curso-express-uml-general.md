# 📐 Curso UML Express: Guía completa de diagramas

## 🎯 Objetivo

Guía condensada de **todos los diagramas UML** con ejemplos prácticos y criterios claros para saber **cuándo usar cada uno** en el desarrollo de software.

## 📋 Prerequisitos

- Programación orientada a objetos básica
- Conceptos básicos de ingeniería de software

---

## 📊 UML en perspectiva

```mermaid
mindmap
  root((UML 2.5))
    Diagramas Estructurales
      Clases
      Objetos
      Componentes
      Despliegue
      Paquetes
      Estructura Compuesta
    Diagramas de Comportamiento
      Casos de Uso
      Actividades
      Estados
      Secuencia
      Comunicación
      Temporización
    Diagramas de Interacción
      Secuencia
      Comunicación
      Vista General
      Temporización
```

## 🗂️ Categorías principales

### **🏗️ Diagramas estructurales**
Muestran la **estructura estática** del sistema - qué elementos existen y cómo se relacionan.

### **🔄 Diagramas de comportamiento**  
Muestran el **comportamiento dinámico** del sistema - qué hace y cómo lo hace.

### **💬 Diagramas de interacción** (subset de comportamiento)
Muestran el **flujo de control y datos** entre objetos.

---

# 🏗️ DIAGRAMAS ESTRUCTURALES

## 1. 📋 Diagrama de clases

### 🎯 ¿Cuándo usarlo?

- ✅ **Diseño de arquitectura** de software
- ✅ **Modelado de datos** y relaciones
- ✅ **Documentación de APIs** y librerías
- ✅ **Análisis de dominio** (DDD)

### 🛠️ Ejemplo:

```mermaid
classDiagram
    class Vehicle {
        <<abstract>>
        -String brand
        -String model
        -int year
        +start() void
        +stop() void
        +getInfo() String
    }
    
    class Car {
        -int doors
        -String fuelType
        +openDoors() void
    }
    
    class Motorcycle {
        -boolean hasSidecar
        +wheelie() void
    }
    
    class Engine {
        -int horsepower
        -String type
        +ignite() void
    }
    
    class Driver {
        -String name
        -String license
        +drive(vehicle: Vehicle) void
    }
    
    Vehicle <|-- Car : inherits
    Vehicle <|-- Motorcycle : inherits
    Vehicle *-- Engine : contains
    Driver --> Vehicle : drives
```

### 🔥 Tips:

- **Clases abstractas**: `<<abstract>>`
- **Interfaces**: `<<interface>>`
- **Herencia**: `<|--` 
- **Composición**: `*--` (no puede existir independiente)
- **Agregación**: `o--` (puede existir independiente)
- **Asociación**: `-->` (usa o conoce)

---

## 2. 🎭 Diagrama de objetos

### 🎯 ¿Cuándo usarlo?

- ✅ **Snapshot de instancias** en un momento específico
- ✅ **Ejemplos concretos** de clases abstractas
- ✅ **Testing y debugging** - estados específicos
- ✅ **Documentar configuraciones** complejas

### 🛠️ Ejemplo:

```mermaid
classDiagram
    class car1 {
        <<Car>>
        brand: "Toyota"
        model: "Camry"
        year: 2023
        doors: 4
        fuelType: "Hybrid"
    }
    
    class engine1 {
        <<Engine>>
        horsepower: 203
        type: "Hybrid V6"
    }
    
    class driver1 {
        <<Driver>>
        name: "Juan Pérez"
        license: "A-12345"
    }
    
    car1 *-- engine1 : contains
    driver1 --> car1 : drives
```

### 🔥 Tips:

- Muestra **valores reales** de atributos
- Útil para **casos de prueba**
- Complementa diagramas de clases con **ejemplos concretos**

---

## 3. 📦 Diagrama de componentes

### 🎯 ¿Cuándo usarlo?

- ✅ **Arquitectura de sistemas** grandes
- ✅ **Microservicios** y modularización
- ✅ **Interfaces y dependencias** entre módulos
- ✅ **Deployment** y organización de código

### 🛠️ Ejemplo:

```mermaid
flowchart TD
    subgraph "E-Commerce System"
        subgraph "Frontend Tier"
            UI[Web UI Component]
            API_Client[API Client Component]
        end
        
        subgraph "Backend Tier"
            AuthService[Authentication Service]
            OrderService[Order Service]
            PaymentService[Payment Service]
            InventoryService[Inventory Service]
        end
        
        subgraph "Data Tier"
            UserDB[(User Database)]
            OrderDB[(Order Database)]
            PaymentDB[(Payment Database)]
        end
    end
    
    subgraph "External Systems"
        PaymentGateway[Payment Gateway]
        EmailService[Email Service]
    end
    
    UI --> API_Client
    API_Client --> AuthService
    API_Client --> OrderService
    
    OrderService --> PaymentService
    OrderService --> InventoryService
    
    AuthService --> UserDB
    OrderService --> OrderDB
    PaymentService --> PaymentDB
    
    PaymentService --> PaymentGateway
    OrderService --> EmailService
    
    classDef frontend fill:#e1f5fe,stroke:#0277bd
    classDef backend fill:#e8f5e8,stroke:#2e7d32
    classDef database fill:#fff3e0,stroke:#ef6c00
    classDef external fill:#fce4ec,stroke:#c2185b
    
    class UI,API_Client frontend
    class AuthService,OrderService,PaymentService,InventoryService backend
    class UserDB,OrderDB,PaymentDB database
    class PaymentGateway,EmailService external
```

### 🔥 Tips:

- **Componentes**: Unidades desplegables independientes
- **Interfaces**: Contratos entre componentes
- **Dependencias**: Quién necesita qué
- **Capas**: Organización lógica del sistema

---

## 4. 🚀 Diagrama de despliegue

### 🎯 ¿Cuándo usarlo?

- ✅ **Infraestructura de producción**
- ✅ **Docker/Kubernetes** deployments
- ✅ **Network topology** y comunicación
- ✅ **Hardware requirements** y scaling

### 🛠️ Ejemplo:

```mermaid
flowchart TD
    subgraph Internet["🌐 Internet"]
        Users[Users/Clients]
    end
    
    subgraph Cloud["☁️ AWS Cloud"]
        subgraph LoadBalancer["⚖️ Load Balancer"]
            ALB[Application Load Balancer]
        end
        
        subgraph WebTier["🖥️ Web Tier (Auto Scaling)"]
            Web1[Web Server 1<br/>t3.medium]
            Web2[Web Server 2<br/>t3.medium] 
            Web3[Web Server N<br/>t3.medium]
        end
        
        subgraph AppTier["⚙️ Application Tier"]
            App1[App Server 1<br/>t3.large<br/>8GB RAM]
            App2[App Server 2<br/>t3.large<br/>8GB RAM]
        end
        
        subgraph DatabaseTier["🗃️ Database Tier"]
            Primary[(Primary DB<br/>RDS PostgreSQL<br/>r5.xlarge)]
            Replica[(Read Replica<br/>RDS PostgreSQL<br/>r5.large)]
        end
        
        subgraph Cache["⚡ Cache Layer"]
            Redis[(Redis Cluster<br/>r6g.large)]
        end
    end
    
    Users --> ALB
    ALB --> Web1
    ALB --> Web2
    ALB --> Web3
    
    Web1 --> App1
    Web2 --> App2
    Web3 --> App1
    
    App1 --> Primary
    App2 --> Primary
    App1 --> Replica
    App2 --> Replica
    
    App1 --> Redis
    App2 --> Redis
    
    Primary -.->|replication| Replica
    
    classDef internet fill:#e3f2fd,stroke:#1976d2
    classDef loadbalancer fill:#f1f8e9,stroke:#689f38
    classDef web fill:#fff3e0,stroke:#f57c00
    classDef app fill:#e8f5e8,stroke:#388e3c
    classDef database fill:#fce4ec,stroke:#c2185b
    classDef cache fill:#f3e5f5,stroke:#7b1fa2
    
    class Users internet
    class ALB loadbalancer
    class Web1,Web2,Web3 web
    class App1,App2 app
    class Primary,Replica database
    class Redis cache
```

### 🔥 Tips:

- **Nodos**: Dispositivos físicos o máquinas virtuales
- **Artefactos**: Software desplegado (WAR, JAR, containers)
- **Conexiones**: Protocolos de comunicación
- **Restricciones**: CPU, RAM, storage

---

## 5. 📁 Diagrama de paquetes

### 🎯 ¿Cuándo usarlo?

- ✅ **Organización de código** en grandes proyectos
- ✅ **Arquitectura por capas**
- ✅ **Dependencias entre módulos**
- ✅ **Refactoring** y reestructuración

### 🛠️ Ejemplo:

```mermaid
flowchart TD
    subgraph "com.example.ecommerce"
        subgraph "presentation"
            Controllers[controllers]
            DTOs[dto]
            Views[views]
        end
        
        subgraph "business"
            Services[services]
            Models[models]
            Interfaces[interfaces]
        end
        
        subgraph "persistence"
            Repositories[repositories]
            Entities[entities]
            Config[config]
        end
        
        subgraph "infrastructure" 
            Utils[utils]
            Security[security]
            Messaging[messaging]
        end
    end
    
    Controllers --> Services
    Controllers --> DTOs
    Services --> Models
    Services --> Interfaces
    Services --> Repositories
    Repositories --> Entities
    Repositories --> Config
    
    Services --> Utils
    Controllers --> Security
    Services --> Messaging
    
    classDef presentation fill:#e1f5fe,stroke:#0277bd
    classDef business fill:#e8f5e8,stroke:#2e7d32
    classDef persistence fill:#fff3e0,stroke:#ef6c00
    classDef infrastructure fill:#f3e5f5,stroke:#7b1fa2
    
    class Controllers,DTOs,Views presentation
    class Services,Models,Interfaces business
    class Repositories,Entities,Config persistence
    class Utils,Security,Messaging infrastructure
```

### 🔥 Tips:

- **Packages**: Agrupación lógica de clases relacionadas
- **Dependencies**: `-->` indica "usa" o "importa"
- **Layers**: Organización en capas arquitectónicas
- **Visibility**: public (+), private (-), protected (#)

---

# 🔄 DIAGRAMAS DE COMPORTAMIENTO

## 6. 🎭 Casos de uso

### 🎯 ¿Cuándo usarlo?

- ✅ **Requerimientos funcionales**
- ✅ **Interacciones usuario-sistema**
- ✅ **Alcance del proyecto**
- ✅ **Comunicación con stakeholders**

### 🛠️ Ejemplo:

```mermaid
flowchart TD
    Customer((Customer))
    Admin((Administrator))
    PaymentSystem((Payment System))
    
    subgraph "E-Commerce System"
        Browse[Browse Products]
        Search[Search Products]
        AddCart[Add to Cart]
        Checkout[Checkout]
        Payment[Process Payment]
        ManageProducts[Manage Products]
        ViewReports[View Sales Reports]
        ManageUsers[Manage Users]
    end
    
    Customer --> Browse
    Customer --> Search
    Customer --> AddCart
    Customer --> Checkout
    
    Checkout --> Payment
    Payment --> PaymentSystem
    
    Admin --> ManageProducts
    Admin --> ViewReports
    Admin --> ManageUsers
    
    classDef actor fill:#e3f2fd,stroke:#1976d2
    classDef usecase fill:#e8f5e8,stroke:#2e7d32
    classDef system fill:#fff3e0,stroke:#ef6c00
    
    class Customer,Admin,PaymentSystem actor
    class Browse,Search,AddCart,Checkout,Payment,ManageProducts,ViewReports,ManageUsers usecase
```

### 🔥 Tips:

- **Actores**: Usuarios o sistemas externos
- **Casos de uso**: Funcionalidades del sistema
- **Include**: `<<include>>` funcionalidad reutilizable
- **Extend**: `<<extend>>` funcionalidad opcional

---

## 7. 🔄 Diagrama de actividades

### 🎯 ¿Cuándo usarlo?

- ✅ **Procesos de negocio**
- ✅ **Workflows** complejos
- ✅ **Algoritmos** paso a paso
- ✅ **Procesos paralelos**

### 🛠️ Ejemplo:

```mermaid
flowchart TD
    Start([Start Order Process])
    CheckInventory{Inventory Available?}
    ReserveItems[Reserve Items]
    ProcessPayment[Process Payment]
    PaymentSuccess{Payment Successful?}
    
    subgraph Parallel["Parallel Activities"]
        SendConfirmation[Send Confirmation Email]
        UpdateInventory[Update Inventory]
        GenerateInvoice[Generate Invoice]
    end
    
    ShipOrder[Ship Order]
    ReleaseInventory[Release Reserved Items]
    NotifyFailure[Notify Payment Failure]
    End([End Process])
    
    Start --> CheckInventory
    CheckInventory -->|Yes| ReserveItems
    CheckInventory -->|No| NotifyFailure
    ReserveItems --> ProcessPayment
    ProcessPayment --> PaymentSuccess
    
    PaymentSuccess -->|Success| SendConfirmation
    PaymentSuccess -->|Success| UpdateInventory  
    PaymentSuccess -->|Success| GenerateInvoice
    PaymentSuccess -->|Failure| ReleaseInventory
    
    SendConfirmation --> ShipOrder
    UpdateInventory --> ShipOrder
    GenerateInvoice --> ShipOrder
    
    ShipOrder --> End
    ReleaseInventory --> NotifyFailure
    NotifyFailure --> End
    
    classDef startEnd fill:#e8f5e8,stroke:#2e7d32,stroke-width:2px
    classDef process fill:#e3f2fd,stroke:#1976d2
    classDef decision fill:#fff3e0,stroke:#ef6c00
    classDef parallel fill:#f3e5f5,stroke:#7b1fa2
    
    class Start,End startEnd
    class ReserveItems,ProcessPayment,SendConfirmation,UpdateInventory,GenerateInvoice,ShipOrder,ReleaseInventory,NotifyFailure process
    class CheckInventory,PaymentSuccess decision
```

### 🔥 Tips:

- **Start/End**: Círculos con bordes gruesos
- **Activities**: Rectángulos
- **Decisions**: Diamantes con preguntas
- **Fork/Join**: Barras para actividades paralelas

---

## 8. 🔀 Diagrama de estados

### 🎯 ¿Cuándo usarlo?

- ✅ **Objetos con estados** complejos
- ✅ **State machines**
- ✅ **Protocolos** de comunicación
- ✅ **Ciclo de vida** de entidades

### 🛠️ Ejemplo:

```mermaid
stateDiagram-v2
    [*] --> Draft
    
    Draft --> InReview : submit()
    Draft --> Cancelled : cancel()
    
    InReview --> Approved : approve()
    InReview --> Rejected : reject()
    InReview --> Draft : return_to_draft()
    
    Approved --> Published : publish()
    Approved --> Cancelled : cancel()
    
    Rejected --> Draft : revise()
    Rejected --> Cancelled : cancel()
    
    Published --> Archived : archive()
    
    Cancelled --> [*]
    Archived --> [*]
    
    note right of Draft : Author can edit content
    note right of InReview : Awaiting reviewer feedback
    note right of Published : Live content, read-only
```

### 🔥 Tips:

- **Estados**: Situación actual del objeto
- **Transiciones**: Eventos que cambian el estado
- **Guardas**: `[condición]` para transiciones condicionales
- **Acciones**: `/acción` ejecutada durante transición

---

# 💬 DIAGRAMAS DE INTERACCIÓN

## 9. 📞 Diagrama de secuencia

### 🎯 ¿Cuándo usarlo?

- ✅ **Flujo temporal** de mensajes
- ✅ **APIs** y protocolos
- ✅ **Debugging** de interacciones
- ✅ **Documentación técnica**

### 🛠️ Ejemplo:

```mermaid
sequenceDiagram
    participant C as Client
    participant G as API Gateway
    participant A as Auth Service
    participant O as Order Service
    participant P as Payment Service
    participant D as Database
    
    Note over C,D: Order Creation Flow
    
    C->>+G: POST /api/orders
    G->>+A: validateToken(token)
    A->>A: verifyJWT()
    A-->>-G: userInfo
    
    G->>+O: createOrder(userInfo, orderData)
    O->>O: validateOrder()
    
    alt valid order
        O->>+P: processPayment(paymentInfo)
        P->>P: chargeCard()
        P-->>-O: paymentResult
        
        alt payment successful
            O->>+D: saveOrder(order)
            D-->>-O: orderId
            O->>G: orderCreated(orderId)
            G-->>C: 201 Created
        else payment failed
            O->>G: paymentError
            G-->>C: 400 Bad Request
        end
    else invalid order
        O->>G: validationError
        G-->>C: 400 Bad Request
    end
    
    deactivate O
    deactivate G
```

### 🔥 Tips:

- **Lifelines**: Objetos participantes
- **Messages**: `->` síncronos, `->>` asíncronos
- **Activation**: `+/-` cuándo está "activo"
- **Alt/Opt**: Condicionales y opcionales

---

## 10. 📡 Diagrama de comunicación

### 🎯 ¿Cuándo usarlo?

- ✅ **Estructura de comunicación** entre objetos
- ✅ **Arquitectura de colaboración**
- ✅ **Overview rápido** de interacciones
- ✅ **Alternativa** a diagramas de secuencia

### 🛠️ Ejemplo:

```mermaid
flowchart LR
    Client[Client]
    Controller[OrderController]
    Service[OrderService]
    Repository[OrderRepository]
    Database[(Database)]
    
    Client -->|"1: createOrder()"| Controller
    Controller -->|"2: processOrder()"| Service
    Service -->|"3: saveOrder()"| Repository
    Repository -->|"4: INSERT"| Database
    Database -->|"5: orderId"| Repository
    Repository -->|"6: order"| Service
    Service -->|"7: orderDTO"| Controller
    Controller -->|"8: 201 Created"| Client
    
    classDef client fill:#e3f2fd,stroke:#1976d2
    classDef controller fill:#e8f5e8,stroke:#2e7d32
    classDef service fill:#fff3e0,stroke:#ef6c00
    classDef repository fill:#f3e5f5,stroke:#7b1fa2
    classDef database fill:#fce4ec,stroke:#c2185b
    
    class Client client
    class Controller controller
    class Service service
    class Repository repository
    class Database database
```

### 🔥 Tips:

- **Objetos**: Participantes en la colaboración
- **Links**: Relaciones entre objetos
- **Messages**: Numerados en orden temporal
- **Focus**: En la estructura más que en el tiempo

---

# 🎯 Guía de decisión: ¿cuál diagrama usar?

## 🤔 Por propósito

### **📋 Análisis de requisitos**
- **Casos de Uso** → Funcionalidades del sistema
- **Actividades** → Procesos de negocio
- **Estados** → Ciclo de vida de entidades

### **🏗️ Diseño de arquitectura**
- **Componentes** → Módulos y sus interfaces
- **Paquetes** → Organización del código
- **Despliegue** → Infraestructura y hardware

### **💻 Diseño detallado**
- **Clases** → Estructura de datos y métodos
- **Objetos** → Instancias específicas
- **Secuencia** → Flujo de mensajes temporales

### **📞 Comunicación**
- **Casos de Uso** → Con stakeholders no técnicos
- **Componentes** → Con arquitectos
- **Secuencia** → Con desarrolladores

## ⚡ ¿Cómo elegir el modelo a diseñar?

```mermaid
flowchart TD
    Start{¿Qué quieres modelar?}
    
    Start -->|Estructura estática| Structure{¿Qué nivel?}
    Start -->|Comportamiento dinámico| Behavior{¿Qué aspecto?}
    
    Structure -->|Classes y objetos| ClassDiag[Diagrama de Clases]
    Structure -->|Módulos y capas| ComponentDiag[Diagrama de Componentes]
    Structure -->|Infraestructura| DeploymentDiag[Diagrama de Despliegue]
    Structure -->|Organización código| PackageDiag[Diagrama de Paquetes]
    
    Behavior -->|Funcionalidades| UseCaseDiag[Casos de Uso]
    Behavior -->|Procesos/workflows| ActivityDiag[Diagrama de Actividades]
    Behavior -->|Estados/ciclo vida| StateDiag[Diagrama de Estados]
    Behavior -->|Interacciones| Interaction{¿Enfoque?}
    
    Interaction -->|Temporal| SequenceDiag[Diagrama de Secuencia]
    Interaction -->|Estructural| CommunicationDiag[Diagrama de Comunicación]
    
    classDef question fill:#fff3e0,stroke:#ef6c00
    classDef structural fill:#e1f5fe,stroke:#0277bd
    classDef behavioral fill:#e8f5e8,stroke:#2e7d32
    classDef interaction fill:#f3e5f5,stroke:#7b1fa2
    
    class Start,Structure,Behavior,Interaction question
    class ClassDiag,ComponentDiag,DeploymentDiag,PackageDiag structural
    class UseCaseDiag,ActivityDiag,StateDiag behavioral
    class SequenceDiag,CommunicationDiag interaction
```

## 📄 Matriz de uso por fase del proyecto

| **Fase** | **Diagramas Principales** | **Diagramas Secundarios** |
|----------|-------------------------|--------------------------|
| **Análisis** | Casos de Uso, Actividades | Estados, Objetos |
| **Diseño Arquitectónico** | Componentes, Paquetes | Despliegue |
| **Diseño Detallado** | Clases, Secuencia | Comunicación, Estados |
| **Implementación** | Clases, Objetos | Secuencia |
| **Despliegue** | Despliegue, Componentes | Paquetes |
| **Mantenimiento** | Clases, Componentes | Todos según necesidad |

---

## 🛠️ Tools y Best practices

### **🎨 Herramientas recomendadas**

- **Mermaid** ⭐ → Diagramas como código, nativo en GitHub
- **PlantUML** → Potente para diagramas complejos
- **Draw.io** → Visual, fácil colaboración
- **Lucidchart** → Profesional, templates
- **Enterprise Architect** → Completo para grandes proyectos

### **✅ Best practices**

1. **Keep it Simple** → Solo incluir elementos necesarios
2. **Consistent Naming** → Mismos nombres en todos los diagramas
3. **Right Level of Detail** → Apropiado para la audiencia
4. **Update Regularly** → Mantener sincronizado con código
5. **Version Control** → Tratar diagramas como código

### **🚫 Errores comunes**

- ❌ **Over-modeling** → Demasiados diagramas sin valor
- ❌ **Under-modeling** → Falta de documentación clave
- ❌ **Inconsistency** → Nombres diferentes entre diagramas
- ❌ **Outdated diagrams** → No actualizar con cambios
- ❌ **Wrong audience** → Nivel de detalle incorrecto

---

## 📚 Conexión con microservicios

Este curso general **complementa** el [Curso UML Ultra Express para Microservicios](curso-express-uml-microservicios.md):

### **🔗 Flujo recomendado**

1. **Curso General** → Entender todos los tipos de diagramas
2. **Curso Microservicios** → Aplicar específicamente a arquitecturas distribuidas
3. **Práctica** → Usar ambos según el contexto del proyecto

### **🎯 Cuándo usar cada curso**

- **General** ✅ → Proyectos monolíticos, librerías, sistemas tradicionales
- **Microservicios** ✅ → Arquitecturas distribuidas, containers, cloud-native

¡Ahora tienes la base completa de UML! 🎉