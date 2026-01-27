# Práctica 1.2: Estudio de Caso - Desacoplamiento de un Monolito

## 🎯 Objetivo

Analizar un caso de estudio real de transformación arquitectónica y elaborar un mapa conceptual que muestre los componentes fundamentales de un microservicio y la estrategia de desacoplamiento utilizada.

---

## 📋 Información General

- **Modalidad:** Equipos de 2-3 personas
- **Prerrequisitos:** Práctica 1.1 completada
- **Herramientas:** Miro/Lucidchart, navegador web, editor de texto

---

## 🏢 Casos de estudio disponibles

### Opción A: Netflix - De Monolito a Microservicios Cloud-Native

**Contexto histórico:**

- **2008:** Monolito Java desplegado en datacenter propio
- **2009:** Incidente mayor: corrupción de base de datos, 3 días sin servicio
- **2010-2016:** Migración gradual a AWS con arquitectura de microservicios
- **Actualidad:** 700+ microservicios atendiendo a 200M+ usuarios

### Opción B: Uber - Escalando la Plataforma Global de Movilidad

**Contexto histórico:**

- **2010:** Aplicación monolítica PHP ("Schemaless")
- **2013:** Problemas de escalabilidad con crecimiento exponencial
- **2014-2017:** Transición a microservicios con arquitectura SOA
- **Actualidad:** 4000+ microservicios en múltiples regiones

### Opción C: Amazon - La Transformación que Cambió la Industria

**Contexto histórico:**

- **1995-2001:** Monolito C++ para operaciones de librería
- **2002:** Memo de Bezos: "Service-Oriented Architecture"
- **2003-2006:** Descomposición gradual en servicios internos
- **Actualidad:** Miles de servicios, AWS nació de esta transformación

---

## 🔍 Parte 1: Investigación y análisis del caso

### Metodología de Investigación

#### 1. Recopilación de Información

**Fuentes primarias recomendadas:**

**Para Netflix:**

- Netflix Technology Blog
- QCon presentations by Netflix engineers
- "Microservices at Netflix Scale" - Adrian Cockcroft
- Netflix OSS GitHub repositories

**Para Uber:**

- Uber Engineering Blog
- "Microservice Architecture at Uber" - Matt Ranney
- Uber's Schemaless documentation
- High Scalability articles about Uber

**Para Amazon:**

- Amazon Architecture Center
- AWS re:Invent presentations
- "The Everything Store" - Brad Stone
- Werner Vogels' blog (Amazon CTO)

#### 2. Análisis Estructurado

Completar la siguiente plantilla de análisis:

```markdown
# Análisis del Caso: [Empresa Seleccionada]

## 1. Estado inicial (monolito)

### Arquitectura Original

- **Tecnología:**
- **Base de datos:**
- **Tamaño del equipo:**
- **Usuarios/transacciones:**

### Problemas Identificados

- **Técnicos:**
  -
- **Organizacionales:**
  -
- **De negocio:**
  -

### Evento Catalizador

- **¿Qué precipitó la transformación?**
- **¿Cuál fue el "último straw"?**

## 2. Proceso de Transformación

### Estrategia de Migración

- **Enfoque:** (Big Bang vs Strangler Fig vs ...)
- **Cronología:** (fases principales)
- **Herramientas/frameworks desarrollados:**

### Desafíos Enfrentados

- **Técnicos:**
- **Organizacionales:**
- **Culturales:**

### Patrones y Soluciones Aplicadas

- **Descomposición:**
- **Comunicación:**
- **Datos:**
- **Observabilidad:**

## 3. Estado Final (Microservicios)

### Arquitectura Resultante

- **Número de servicios:**
- **Tecnologías utilizadas:**
- **Patrones arquitectónicos:**

### Beneficios Alcanzados

- **Técnicos:**
- **Organizacionales:**
- **De negocio:**

### Lecciones Aprendidas

- **¿Qué harían diferente?**
- **¿Qué funcionó mejor de lo esperado?**
- **¿Qué fue más difícil de lo anticipado?**
```

---

## 🗺️ Parte 2: Creación del Mapa Conceptual

### Objetivo del Mapa

Visualizar la estrategia de desacoplamiento específica utilizada en el caso seleccionado, mostrando:

1. **Componentes del monolito original**
2. **Proceso de descomposición**
3. **Microservicios resultantes**
4. **Patrones de comunicación implementados**

### Estructura Sugerida del Mapa

#### Nivel 1: Vista General

```text
MONOLITO ORIGINAL
       ↓
PROCESO DE TRANSFORMACIÓN
       ↓
ARQUITECTURA DE MICROSERVICIOS
```

#### Nivel 2: Descomposición Detallada

Para cada empresa, incluir elementos específicos:

**Netflix:**

- Circuit Breaker (Hystrix)
- Service Discovery (Eureka)
- API Gateway (Zuul)
- Configuration Management (Archaius)

**Uber:**

- Domain-Oriented Microservices Architecture (DOMA)
- Request/Response vs Event-Driven patterns
- Schemaless → Service-specific databases

**Amazon:**

- Service-Oriented Organization
- "You build it, you run it" philosophy
- API-first design

### Herramientas Recomendadas

1. **Miro** - Colaboración en tiempo real
   - Templates de arquitectura disponibles
   - Iconos de tecnología integrados
   - Comentarios y feedback directo

2. **Lucidchart** - Diagramas profesionales
   - Integración con Google Drive
   - Templates de arquitectura de software
   - Export a múltiples formatos

3. **Draw.io** - Gratuito y potente
   - Integración con GitHub
   - Amplia biblioteca de símbolos
   - Colaboración básica

### Elementos Visuales a Incluir

#### Componentes Técnicos

- 🏢 Servicios/sistemas
- 🗄️ Bases de datos
- 🌐 APIs/interfaces
- ⚡ Mensajería/eventos
- 🔒 Seguridad/autenticación

#### Flujos y Procesos

- ➡️ Comunicación síncrona
- 📡 Comunicación asíncrona
- 🔄 Procesos de transformación
- Líneas de tiempo

#### Anotaciones

- 💡 Decisiones clave
- ⚠️ Desafíos identificados
- ✅ Beneficios obtenidos
- 📊 Métricas de impacto

---

## 📊 Parte 3: Análisis de Impacto y Métricas

### Métricas de Transformación

Documentar el impacto cuantitativo de la transformación:

#### Métricas Técnicas

- **Tiempo de despliegue:** Antes vs Después
- **Frecuencia de releases:** Releases por semana/mes
- **MTTR (Mean Time to Recovery):** Tiempo de recuperación de fallos
- **Escalabilidad:** Capacidad de manejo de usuarios/transacciones

#### Métricas Organizacionales

- **Velocidad de desarrollo:** Story points por sprint
- **Autonomía de equipos:** Dependencias entre equipos
- **Tiempo de onboarding:** Nuevos desarrolladores
- **Satisfacción del desarrollador:** Encuestas internas

#### Métricas de Negocio

- **Time to market:** Nuevas funcionalidades
- **Disponibilidad del servicio:** Uptime/SLA
- **Costos operacionales:** Infraestructura y personal
- **Innovación:** Nuevos productos/experimentos

### Plantilla de Métricas

```markdown
# Impacto Cuantitativo de la Transformación

| Métrica                  | Antes (Monolito) | Después (Microservicios) | Mejora |
| ------------------------ | ---------------- | ------------------------ | ------ |
| Tiempo de despliegue     |                  |                          |        |
| Releases por mes         |                  |                          |        |
| MTTR (minutos)           |                  |                          |        |
| Usuarios concurrentes    |                  |                          |        |
| Equipos de desarrollo    |                  |                          |        |
| Tiempo onboarding (días) |                  |                          |        |
| Uptime (%)               |                  |                          |        |
| Costo por transacción    |                  |                          |        |
```

---

## 🎯 Parte 4: Aplicación al Proyecto Final

### Conexión Estratégica

Basándose en el caso analizado, definir:

#### 1. Patrones Aplicables

¿Cuáles de los patrones identificados son relevantes para la "Plataforma de Ingesta y Procesamiento de Datos"?

#### 2. Estrategia de Descomposición

¿Cómo aplicarían la lógica de bounded contexts del caso estudiado?

#### 3. Tecnologías y Herramientas

¿Qué elementos del stack tecnológico podrían reutilizar?

#### 4. Riesgos Anticipados

¿Qué desafíos del caso estudiado podrían aparecer en el proyecto?

---

## 📝 Entregables

### 1. Documento de Análisis del Caso

- **Formato:** Markdown o PDF
- **Extensión:** 4-6 páginas
- **Contenido:**
  - Análisis completo según plantilla
  - Tabla de métricas con fuentes
  - Conclusiones y lecciones aprendidas

### 2. Mapa Conceptual Interactivo

- **Formato:** Miro, Lucidchart, o imagen de alta resolución
- **Contenido:**
  - Descomposición visual del monolito
  - Proceso de transformación
  - Arquitectura final
  - Patrones y componentes clave

### 3. Aplicación al Proyecto Final

- **Formato:** Documento complementario (2 páginas)
- **Contenido:**
  - Patrones seleccionados para reutilizar
  - Estrategia de descomposición propuesta
  - Riesgos identificados y mitigaciones

---

## ✅ Criterios de Evaluación

| Criterio | Peso | Excelente (5) | Bueno (4) | Satisfactorio (3) | Insuficiente (1-2) |
|----------|------|---------------|-----------|-------------------|-------------------|
| **Investigación** | 25% | Fuentes primarias diversas, información precisa y actualizada | Buenas fuentes, información mayormente correcta | Fuentes básicas, información general correcta | Fuentes limitadas o información incorrecta |
| **Análisis del Caso** | 30% | Comprensión profunda de motivaciones, proceso y resultados | Análisis sólido con buen entendimiento | Análisis básico pero correcto | Análisis superficial o con errores |
| **Mapa Conceptual** | 25% | Visualización clara, completa y bien organizada | Mapa bien estructurado con elementos clave | Mapa funcional pero básico | Mapa confuso o incompleto |
| **Conexión Proyecto** | 15% | Aplicación estratégica y bien justificada | Conexiones apropiadas con justificación | Conexiones básicas identificadas | Conexiones forzadas o incorrectas |
| **Presentación** | 5% | Documentos profesionales y bien organizados | Buena organización y claridad | Organización adecuada | Presentación descuidada |

---

## 🎤 Presentación Final

### Formato

- **Modalidad:** Todos los miembros del equipo participan
- **Herramientas:** Presentación + demo del mapa conceptual

### Estructura Sugerida

1. **Contexto del caso**
   - Situación inicial y problemas
   - Evento catalizador

2. **Proceso de transformación**
   - Estrategia de migración
   - Desafíos principales y soluciones
   - Demo del mapa conceptual

3. **Resultados e impacto**
   - Métricas de mejora
   - Beneficios alcanzados

4. **Aplicación al proyecto final**
   - Patrones seleccionados
   - Lecciones aplicables

---

## 🔗 Preparación para Unidad 2

Esta práctica prepara específicamente para:

1. **Domain-Driven Design:** Comprensión de bounded contexts en casos reales
2. **API Design:** Patrones de comunicación entre servicios
3. **Data Management:** Estrategias de separación de datos
4. **Architecture Patterns:** Circuit Breaker, API Gateway, Event Sourcing

Los insights de esta práctica se utilizarán directamente en el diseño de la arquitectura del proyecto final.

---

## 📚 Referencias Específicas por Caso

### Netflix

- [Netflix Technology Blog](https://netflixtechblog.com/)
- "Microservices at Netflix Scale" - Adrian Cockcroft
- Netflix OSS: Hystrix, Eureka, Zuul documentation

### Uber

- [Uber Engineering Blog](https://eng.uber.com/)
- "Scaling Uber's Real-time Market Platform" - Matt Ranney
- "Introducing Domain-Oriented Microservice Architecture"

### Amazon

- [Amazon Architecture Center](https://aws.amazon.com/architecture/)
- "Scaling up to your first 10 million users" - AWS
- Werner Vogels' "Eventually Consistent" paper
