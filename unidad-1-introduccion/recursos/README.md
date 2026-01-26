# Recursos Complementarios - Unidad 1

## 📚 Material de Referencia

### Libros Fundamentales

#### 📖 Lectura Obligatoria
1. **Newman, S. (2021). "Building Microservices" (2nd ed.)**
   - Capítulos 1-3: Fundamentos y conceptos
   - Enfoque: Práctico y basado en experiencia real
   - **Por qué es esencial:** Considerado el estándar de la industria

2. **Fowler, M. (2014). "Microservices" - martinfowler.com**
   - Artículo fundacional del término
   - Define las características principales
   - **Disponible:** [https://martinfowler.com/articles/microservices.html](https://martinfowler.com/articles/microservices.html)

#### 📚 Lectura Complementaria
1. **Richardson, C. (2018). "Microservices Patterns"**
   - Capítulo 1: Escaping monolithic hell
   - Enfoque: Patrones de diseño específicos

2. **Kleppmann, M. (2017). "Designing Data-Intensive Applications"**
   - Capítulo 1: Reliable, Scalable, and Maintainable Applications
   - Perspectiva: Arquitectura de datos distribuidos

---

## 🌐 Recursos Web y Blogs

### Blogs Técnicos Oficiales

#### Netflix Tech Blog
- **URL:** [https://netflixtechblog.com/](https://netflixtechblog.com/)
- **Artículos clave:**
  - "Microservices at Netflix Scale"
  - "The Netflix Simian Army"
  - "Fault Tolerance in a High Volume Distributed System"

#### Uber Engineering
- **URL:** [https://eng.uber.com/](https://eng.uber.com/)
- **Artículos clave:**
  - "Introducing Domain-Oriented Microservice Architecture"
  - "Scaling Uber's Real-time Market Platform"
  - "Microservice Architecture at Uber"

#### Amazon Architecture Center
- **URL:** [https://aws.amazon.com/architecture/](https://aws.amazon.com/architecture/)
- **Recursos clave:**
  - Well-Architected Framework
  - Microservices on AWS
  - Case studies and reference architectures

### Recursos Especializados

#### Microservices.io
- **URL:** [https://microservices.io/](https://microservices.io/)
- **Contenido:** Patrones, anti-patrones, y mejores prácticas
- **Autor:** Chris Richardson

#### High Scalability
- **URL:** [http://highscalability.com/](http://highscalability.com/)
- **Contenido:** Casos de estudio de arquitectura de grandes sistemas

---

## 🎥 Videos y Conferencias

### Conferencias Técnicas Recomendadas

#### QCon Presentations
1. **"Microservices at Netflix Scale" - Adrian Cockcroft**
   - Enfoque: Lecciones aprendidas en transformación

2. **"From Monolith to Microservices at Uber" - Matt Ranney**
   - Enfoque: Desafíos de escalabilidad global

#### AWS re:Invent Sessions
1. **"Microservices: Decomposing Applications for Deployability"**
   - Nivel: 300 (Intermediate)
   - Enfoque: Estrategias prácticas de descomposición

### Cursos Online Complementarios

#### Coursera - "Microservices Architecture"
- **Universidad:** University of Alberta
- **Enfoque:** Fundamentos teóricos y prácticos

#### edX - "Microservices Development"
- **Universidad:** IBM
- **Enfoque:** Implementación práctica con contenedores

---

## 🛠️ Herramientas de Apoyo

### Diagramado y Visualización

#### Miro
- **Tipo:** Herramienta colaborativa online
- **Uso:** Mapas conceptuales, diagramas de arquitectura
- **Ventajas:** Colaboración en tiempo real, templates
- **Plan gratuito:** Disponible con limitaciones

#### Lucidchart
- **Tipo:** Herramienta de diagramas profesional
- **Uso:** Arquitectura de sistemas, flowcharts
- **Ventajas:** Integración con Google/Microsoft Office
- **Plan educativo:** Descuentos disponibles

#### Draw.io (diagrams.net)
- **Tipo:** Herramienta gratuita online/offline
- **Uso:** Todo tipo de diagramas técnicos
- **Ventajas:** Completamente gratuito, integración con GitHub

### Gestión de Documentación

#### Notion
- **Uso:** Documentación colaborativa, bases de conocimiento
- **Ventajas:** Multimedia, templates, colaboración
- **Plan educativo:** Gratuito para estudiantes

#### GitBook
- **Uso:** Documentación técnica estructurada
- **Ventajas:** Integración con Git, búsqueda potente
- **Plan gratuito:** Disponible con limitaciones

---

## 📊 Datasets y Casos de Estudio

### Casos Reales Documentados

#### 1. Migración de Monolito a Microservicios
```markdown
**Empresa:** SoundCloud
**Período:** 2012-2014
**Contexto:** 
- Monolito Ruby on Rails
- 40M usuarios registrados
- Problemas de escalabilidad

**Estrategia:**
- Strangler Fig Pattern
- Descomposición por dominio
- Event-driven architecture

**Resultados:**
- 20+ microservicios
- Mejora en time-to-market
- Equipos autónomos

**Fuentes:**
- SoundCloud Tech Blog
- QCon London 2014 presentation
```

#### 2. Arquitectura Cloud-Native desde Cero
```markdown
**Empresa:** Spotify
**Período:** 2008-presente
**Contexto:**
- Startup de streaming musical
- Crecimiento exponencial
- Arquitectura distribuida desde día 1

**Arquitectura:**
- Squad/Tribe organization
- 800+ microservicios
- Event-driven communication

**Lecciones:**
- Importancia de cultura organizacional
- Autonomía vs. coherencia
- Observabilidad desde el diseño

**Fuentes:**
- Spotify Engineering Culture videos
- "Spotify Model" documentation
```

### Métricas de Referencia

#### Benchmarks de la Industria
```markdown
**Tiempo de Despliegue:**
- Monolito tradicional: 2-4 semanas
- Microservicios maduros: Múltiples veces al día

**Mean Time to Recovery (MTTR):**
- Monolito: 2-4 horas
- Microservicios con circuit breakers: 5-15 minutos

**Tamaño de Equipos:**
- Monolito: 8-20 desarrolladores
- Microservicio: 2-8 desarrolladores (2 pizza teams)

**Frequency of Deployment:**
- Monolito: Weekly/Monthly
- Microservicios: Daily/Multiple daily
```

---

## 📋 Plantillas y Templates

### Plantilla de Análisis Arquitectónico

```markdown
# Análisis Arquitectónico: [Nombre del Sistema]

## Contexto
- **Dominio de negocio:**
- **Tamaño de organización:**
- **Volumen de usuarios/transacciones:**
- **Criticidad del sistema:**

## Arquitectura Actual
- **Estilo arquitectónico:**
- **Tecnologías principales:**
- **Número de equipos:**
- **Frecuencia de despliegue:**

## Problemas Identificados
### Técnicos
- 
### Organizacionales
- 
### De negocio
- 

## Recomendación
### Arquitectura sugerida:
### Justificación:
### Riesgos identificados:
### Plan de migración:
```

### Template de Mapa Conceptual

```
Elementos requeridos:
1. Concepto central
2. Conceptos secundarios (máximo 8)
3. Relaciones etiquetadas
4. Ejemplos concretos
5. Código de colores por categoría

Categorías sugeridas:
- Principios (azul)
- Componentes técnicos (verde)
- Aspectos organizacionales (naranja)
- Beneficios (verde claro)
- Desafíos (rojo claro)
```

---

## 🔍 Checklist de Investigación

### Antes de Analizar un Caso
- [ ] Identificar fuentes primarias (blogs oficiales, presentaciones)
- [ ] Verificar fechas de publicación (preferir < 2 años)
- [ ] Buscar múltiples perspectivas del mismo caso
- [ ] Identificar métricas cuantitativas cuando sea posible

### Durante el Análisis
- [ ] Documentar fuentes consultadas
- [ ] Distinguir entre hechos y opiniones
- [ ] Identificar el contexto temporal de cada decisión
- [ ] Buscar lecciones aprendidas explícitas

### Validación del Análisis
- [ ] Contrastar con otros casos similares
- [ ] Verificar coherencia técnica de las soluciones
- [ ] Evaluar aplicabilidad al contexto actual
- [ ] Identificar gaps de información

---

## 🎯 Rúbrica de Autoevaluación

### Comprensión Conceptual

| Nivel            | Criterio                                                                    |
| ---------------- | --------------------------------------------------------------------------- |
| **Principiante** | Puedo definir microservicios y listar sus características                   |
| **Competente**   | Puedo comparar estilos arquitectónicos y justificar selecciones             |
| **Avanzado**     | Puedo analizar casos reales y extraer patrones aplicables                   |
| **Experto**      | Puedo diseñar estrategias de migración considerando contexto organizacional |

### Pensamiento Crítico

| Nivel            | Criterio                                                  |
| ---------------- | --------------------------------------------------------- |
| **Principiante** | Identifico ventajas y desventajas básicas                 |
| **Competente**   | Analizo trade-offs en contextos específicos               |
| **Avanzado**     | Evalúo decisiones arquitectónicas con criterios múltiples |
| **Experto**      | Anticipo consecuencias y propongo mitigaciones            |

---

## 📚 Bibliografía Extendida

### Artículos Académicos

1. **Balalaie, A., Heydarnoori, A., & Jamshidi, P. (2016).** "Microservices Architecture Enables DevOps: Migration to a Cloud-Native Architecture." *IEEE Software*, 33(3), 42-52.

2. **Taibi, D., Lenarduzzi, V., & Pahl, C. (2017).** "Processes, Motivations, and Issues for Migrating to Microservices Architectures: An Empirical Investigation." *IEEE Cloud Computing*, 4(5), 22-32.

### Informes de Industria

1. **O'Reilly. (2021).** "Microservices Adoption in 2021" - Survey Report
2. **Gartner. (2021).** "Market Guide for Microservices Infrastructure"
3. **ThoughtWorks Technology Radar** - Continuous updates on microservices tools and techniques

---

**Siguiente:** [Unidad 2: Diseño y Modelado →](../../unidad-2-diseno/README.md)