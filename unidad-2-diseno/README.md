# Unidad 2: Diseño y modelado de microservicios

## 🎯 Objetivos de aprendizaje

Al finalizar esta unidad, el estudiante será capaz de:

1. **Aplicar** domain-driven design (DDD) para definir bounded contexts
2. **Diseñar** APIs RESTful siguiendo principios de madurez y especificarlas con OpenAPI
3. **Identificar** y aplicar patrones arquitectónicos: API Gateway, Saga, CQRS, Event Sourcing
4. **Modelar** la comunicación entre microservicios usando context mapping
5. **Preparar** el diseño base para la plataforma de ingesta y procesamiento de datos

---

## 📚 Estructura del contenido

```text
unidad-2-diseno/
├── 01-teoria/        # Conceptos de DDD, APIs y patrones
├── 02-recursos/      # Material complementario y herramientas
└── 03-actividades/   # Ejercicios de modelado y análisis
```

### 📖 [Teoría](01-teoria/README.md)

Conceptos fundamentales organizados en tres módulos principales:

#### 2.1 Domain-driven design (DDD) y contextos

- **Conceptos centrales:** Dominio, Modelo, Lenguaje Ubicuo
- **Bounded Contexts:** Delimitación de responsabilidades
- **Context Mapping:** Patrones de colaboración entre contextos

#### 2.2 Diseño de APIs y contratos

- **Richardson Maturity Model:** Niveles 0-3 de madurez RESTful
- **OpenAPI/Swagger:** Especificación completa de contratos de API
- **Versionado y documentación:** Estrategias de evolución de APIs

#### 2.3 Patrones arquitectónicos de integración

- **API Gateway:** Punto de entrada único y funcionalidades transversales
- **Saga Pattern:** Transacciones distribuidas con compensación
- **CQRS y Event Sourcing:** Separación de responsabilidades y auditabilidad

---

## 🔗 Conexión con el proyecto final

Esta unidad establece el **diseño arquitectónico base** para el proyecto final:

### Bounded contexts del proyecto

Aplicando DDD al **"Sistema de Ingesta y Procesamiento de Datos"**:

1. **Ingesta Context** - Recepción y validación inicial de datos
   - Entidades: DataSource, IngestionJob, ValidationRule
   - APIs: Ingestion API, Source Management API

2. **Processing Context** - Transformación y enriquecimiento
   - Entidades: Pipeline, Transformation, ProcessingJob
   - APIs: Pipeline Control API, Job Status API

3. **Storage Context** - Persistencia y consulta
   - Entidades: Dataset, Query, StoragePolicy
   - APIs: Query API, Metadata API

4. **Monitoring Context** - Observabilidad y métricas
   - Entidades: Metric, Alert, Dashboard
   - APIs: Metrics API, Health Check API

### Patrones arquitectónicos aplicables

- **API Gateway:** Punto de entrada único para todas las APIs del sistema
- **Saga Pattern:** Coordinación de pipelines de procesamiento multi-etapa
- **CQRS:** Separación de APIs de ingesta (write) vs consulta (read)
- **Event Sourcing:** Auditabilidad completa del procesamiento de datos

---

**Anterior:** [← Unidad 1: Introducción](../unidad-1-introduccion/README.md) | **Siguiente:** [Unidad 3: Implementación →](../unidad-3-implementacion/README.md)

---

*Esta unidad transforma los conceptos fundamentales de la Unidad 1 en diseños arquitectónicos concretos, preparando la implementación práctica que comenzará en la Unidad 3.*
