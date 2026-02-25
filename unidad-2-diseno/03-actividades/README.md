# Actividades de aprendizaje - Unidad 2

## 📋 Información general

**Objetivo:** Dominar la creación de especificaciones OpenAPI (OAS) desde cero, integrando conceptos de DDD, diseño de APIs RESTful y patrones arquitectónicos para microservicios.

## 🚀 Material de apoyo requerido

**ANTES de comenzar la actividad, consulta:**
- 📖 [Curso UML Express General](../02-recursos/curso-express-uml-general.md) - Base completa de diagramas UML
- 🚀 [Curso UML para Microservicios](../02-recursos/curso-ultraexpress-uml-microservicios.md) - Específico para arquitecturas distribuidas
- 🛠️ [Proceso de Desarrollo](../02-recursos/proceso-desarrollo.md) - Flujo completo desde análisis hasta despliegue
- 🔤 [Convenciones de Nomenclatura](../02-recursos/diseno-api-db-url.md) - API vs DB vs URL
- 🗃️ [Guía de Nomenclatura para BD](../02-recursos/nombrado-campos-db.md) - Best practices para bases de datos

---

## 🎯 Actividad: construcción completa de API Specification

### Descripción

Crear una **especificación OpenAPI completa** desde cero, aplicando principios de Domain-Driven Design, patrones RESTful y mejores prácticas de diseño de APIs para un sistema de catálogo de productos de e-commerce.

### 📚 Material base

Para completar esta actividad, sigue paso a paso el documento:
📋 **[Guía Completa: Creación de OpenAPI Specification](creacion-openapi-specification.md)**
### 📝 Archivo de referencia completo

Puedes consultar un ejemplo completo de OpenAPI Specification para e-commerce:
📝 **[Ejemplo Completo: EcommerceAPI.yaml](EcommerceAPI.yaml)** - Especificación completa con todos los elementos implementados
### 🏗️ Estructura de la actividad

#### **Fase 1: modelado del dominio**

**Objetivos:**
- Identificar Bounded Contexts del dominio "E-commerce"
- Modelar entidades principales usando UML
- Definir lenguaje ubicuo del dominio

**Deliverables:**
1. **Diagrama de Casos de Uso** usando sintaxis Mermaid
2. **Diagrama de Clases del Dominio** con agregados identificados
3. **Definición de Bounded Contexts** documentada

**Plantilla de Bounded Contexts:**

```markdown
# Bounded Contexts - Sistema de E-commerce

## Context: Catálogo de Productos

**Responsabilidades:**
- Crear nuevos productos
- Buscar productos existentes
- Actualizar productos
- Eliminar productos

**Entidades Principales:**
- **Product** (Aggregate Root)
- **Category** (Entity)
- **Price** (Value Object)
- **Inventory** (Value Object)

**Lenguaje Ubicuo:**
- **Product**: Ítem que puede ser vendido en la plataforma
- **Category**: Clasificación de productos (Electronics, Clothing, etc.)
- **Price**: Valor monetario del producto
- **Inventory**: Cantidad disponible en stock
```

#### **Fase 2: diseño de API RESTful**

**Objetivos:**
- Aplicar Richardson Maturity Model (Niveles 1-2)
- Diseñar endpoints siguiendo convenciones REST
- Planificar operaciones CRUD completas

**Actividades:**
1. **Identificar Recursos:** De entidades del dominio a recursos REST
2. **Diseñar URLs:** Aplicar convenciones de nomenclatura
3. **Mapear Operaciones:** CRUD + operaciones de negocio específicas
4. **Planificar Responses:** Códigos HTTP y estrutura de respuestas

#### **Fase 3: construcción de OpenAPI Specification**

**Objetivos:**
- Construir especificación OpenAPI 3.0.4 completa
- Implementar validaciones robustas
- Crear documentación auto-descriptiva

**Sigue la guía paso a paso:**
📋 [Creación de OpenAPI Specification](creacion-openapi-specification.md)

**Elementos Requeridos:**

1. **Estructura Básica**
   - openapi version 3.0.4
   - info completo con metadatos
   - servers (desarrollo y producción)
   - tags para organización

2. **Operaciones Completas**
   - `POST /products` - Crear producto
   - `GET /products` - Buscar productos (con filtros)
   - `GET /products/{id}` - Obtener producto específico
   - `PUT /products/{id}` - Actualizar producto completo
   - `PATCH /products/{id}` - Actualizar producto parcial
   - `DELETE /products/{id}` - Eliminar producto

3. **Schemas Completos**
   - `Product` - Datos de entrada
   - `ProductPatch` - Actualización parcial
   - `ProductResponse` - Respuesta de éxito
   - `ProductList` - Lista de productos
   - `DeleteConfirmation` - Confirmación de eliminación
   - `ApiError` - Manejo de errores

4. **Validaciones Avanzadas**
   - Pattern matching para IDs de producto
   - Enums para categorías
   - Rangos para valores monetarios
   - Formatos específicos (decimal, date-time)

#### **Fase 4: Testing y validación**

**Objetivos:**
- Validar especificación usando herramientas
- Generar documentación interactiva
- Verificar completitud de la API

**Actividades:**
1. **Validación técnica** en Swagger Editor
2. **Review de documentación** generada
3. **Testing de ejemplos** en Swagger UI
4. **Verificación de checklist** de completitud

**Herramientas Requeridas:**
- [Swagger Editor Online](https://editor.swagger.io/)
- Postman o Insomnia (para importar spec)
- VS Code con extensión OpenAPI

### 🛠️ Herramientas y recursos

#### **Herramientas de desarrollo**
- **Swagger Editor**: https://editor.swagger.io/
- **VS Code**: Extensión "OpenAPI (Swagger) Editor"
- **Postman**: Para testing de APIs
- **Mermaid Live Editor**: Para diagramas UML

#### **Referencias técnicas**
- **OpenAPI 3.0.4 Specification**: https://swagger.io/specification/
- **HTTP Status Codes**: https://developer.mozilla.org/en-US/docs/Web/HTTP/Status
- **REST API Best Practices**: Documentos en recursos

#### **Validadores de OpenAPI**
- Swagger Editor (online)
- Spectral (CLI linter)
- OpenAPI Validator plugins


### 🔗 Conexión con unidades siguientes

Esta actividad establece la base para:

- **Unidad 3 - Implementación:** El archivo OpenAPI será la base para generar código servidor
- **Unidad 4 - Resiliencia:** Los endpoints diseñados incorporarán patrones de Circuit Breaker y timeout
- **Unidad 5 - Contenedores:** La API será desplegada en contenedores Docker/Kubernetes
- **Proyecto Final:** Integración en la plataforma completa de microservicios

