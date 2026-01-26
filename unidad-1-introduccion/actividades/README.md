# Actividades de Aprendizaje - Unidad 1

## 📋 Información General

**Objetivo:** Consolidar los conceptos fundamentales a través de análisis comparativo y casos de estudio reales.

---

## 🎯 Actividad 1: Cuadro Comparativo de Estilos Arquitectónicos

### Descripción
Elaborar un cuadro comparativo detallado que contraste las características principales de tres estilos arquitectónicos: Monolito, SOA y Microservicios.

### Instrucciones

1. **Investigación**
   - Revisar material teórico de la unidad
   - Consultar al menos 2 fuentes adicionales
   - Tomar notas sobre cada arquitectura

2. **Elaboración del Cuadro**
   - Utilizar la plantilla proporcionada
   - Completar cada celda con información precisa y concisa
   - Incluir ejemplos específicos donde corresponda

3. **Análisis Crítico**
   - Agregar una columna de "Casos de Uso Ideales"
   - Justificar cada recomendación

### Plantilla del Cuadro Comparativo

| Aspecto                          | Monolito | SOA | Microservicios |
| -------------------------------- | -------- | --- | -------------- |
| **Definición**                   |          |     |                |
| **Unidad de Despliegue**         |          |     |                |
| **Base de Datos**                |          |     |                |
| **Comunicación**                 |          |     |                |
| **Tecnología**                   |          |     |                |
| **Escalabilidad**                |          |     |                |
| **Complejidad de Desarrollo**    |          |     |                |
| **Complejidad Operacional**      |          |     |                |
| **Tamaño de Equipo Ideal**       |          |     |                |
| **Tiempo de Desarrollo Inicial** |          |     |                |
| **Facilidad de Testing**         |          |     |                |
| **Manejo de Fallos**             |          |     |                |
| **Casos de Uso Ideales**         |          |     |                |

### Criterios de Evaluación

- **Precisión técnica** (40%): Información correcta y actualizada
- **Análisis comparativo** (30%): Identificación clara de diferencias
- **Casos de uso** (20%): Justificación apropiada de recomendaciones
- **Presentación** (10%): Claridad y organización

### Entregable
- Documento en formato Markdown o PDF
- Máximo 3 páginas
- **Fecha límite:** Fin de la semana 1

---

## 🧠 Actividad 2: Mapa Conceptual de Microservicios

### Descripción
Crear un mapa conceptual que visualice los componentes fundamentales de un microservicio y sus interrelaciones.

### Instrucciones

1. **Identificación de Conceptos**
   - Listar todos los componentes mencionados en la teoría
   - Identificar las relaciones entre conceptos
   - Priorizar por importancia y frecuencia de uso

2. **Construcción del Mapa**
   - Utilizar herramienta digital (Miro, Lucidchart, draw.io)
   - Organizar conceptos jerárquicamente
   - Conectar con líneas etiquetadas que expliquen relaciones

3. **Validación y Refinamiento**
   - Revisar completitud del mapa
   - Verificar coherencia de las conexiones
   - Añadir ejemplos concretos donde sea útil

### Conceptos Clave a Incluir

**Conceptos Centrales:**
- Microservicio
- Bounded Context
- API
- Base de Datos Independiente

**Principios:**
- Desacoplamiento
- Cohesión
- Autonomía
- Modularidad

**Características Técnicas:**
- Comunicación HTTP/REST
- Event-Driven Architecture
- Circuit Breaker
- Service Discovery

**Aspectos Organizacionales:**
- Equipo Autónomo
- DevOps
- Continuous Deployment

### Ejemplo de Estructura Sugerida

```
                    MICROSERVICIO
                         |
            +------------+------------+
            |                        |
       PRINCIPIOS                IMPLEMENTACIÓN
            |                        |
    +-------+-------+        +-------+-------+
    |       |       |        |       |       |
Cohesión Autonomía Desac.   API    BD     Deploy
```

### Criterios de Evaluación

- **Completitud** (35%): Incluye todos los conceptos fundamentales
- **Relaciones** (30%): Conexiones lógicas y bien etiquetadas
- **Organización** (20%): Estructura jerárquica clara
- **Creatividad** (15%): Uso efectivo de elementos visuales

### Entregable
- Imagen del mapa conceptual (PNG/JPG)
- Breve explicación escrita (máximo 1 página)
- **Fecha límite:** Fin de la semana 1

---

## 🔍 Actividad 3: Análisis de Casos de Estudio

### Descripción
Investigar y analizar en detalle la transformación arquitectónica de una empresa real (Netflix, Uber, o Amazon).

### Opciones de Casos de Estudio

#### Opción A: Netflix - La Revolución del Streaming
- **Contexto:** De DVDs por correo a streaming global
- **Desafío:** Escalar de miles a millones de usuarios
- **Solución:** Arquitectura cloud-native con microservicios

#### Opción B: Uber - Conectando el Mundo
- **Contexto:** Plataforma global de transporte
- **Desafío:** Latencia geográfica y consistencia de datos
- **Solución:** Microservicios distribuidos geográficamente

#### Opción C: Amazon - De Libro a Todo
- **Contexto:** Evolución de librería online a marketplace global
- **Desafío:** Múltiples líneas de negocio en una plataforma
- **Solución:** Service-oriented organization

### Estructura del Análisis

#### 1. Contexto Histórico (25%)
- Situación inicial de la empresa
- Problemas específicos que enfrentaban
- Arquitectura original (monolítica)

#### 2. Proceso de Transformación (30%)
- Estrategia de migración adoptada
- Desafíos técnicos y organizacionales
- Timeline y fases de implementación

#### 3. Arquitectura Resultante (25%)
- Número y tipos de microservicios
- Patrones arquitectónicos implementados
- Tecnologías y herramientas utilizadas

#### 4. Resultados e Impacto (20%)
- Métricas de éxito (performance, escalabilidad)
- Beneficios organizacionales alcanzados
- Lecciones aprendidas y mejores prácticas

### Metodología de Investigación

1. **Fuentes Primarias**
   - Blogs técnicos oficiales de la empresa
   - Presentaciones en conferencias (QCon, AWS re:Invent)
   - Papers y case studies publicados

2. **Fuentes Secundarias**
   - Artículos de análisis en medios especializados
   - Libros de arquitectura que mencionen el caso
   - Entrevistas con ingenieros de la empresa

3. **Documentación Técnica**
   - Arquitectura de microservicios específicos
   - Patrones y herramientas open source derivados
   - Métricas de rendimiento publicadas

### Criterios de Evaluación

- **Investigación** (30%): Calidad y variedad de fuentes
- **Análisis técnico** (25%): Comprensión de la arquitectura
- **Análisis organizacional** (20%): Impacto en equipos y procesos
- **Conclusiones** (15%): Lecciones aprendidas aplicables
- **Presentación** (10%): Claridad y estructura del documento

### Entregable
- Documento de análisis (4-6 páginas)
- Presentación ejecutiva (10-15 slides)
- **Fecha límite:** Fin de la semana 2

---

## 📅 Cronograma de Actividades

| Semana | Actividad          | Modalidad      |
| ------ | ------------------ | -------------- |
| 1      | Cuadro Comparativo | Individual     |
| 1      | Mapa Conceptual    | Individual     |
| 2      | Caso de Estudio    | Equipos de 2-3 |
| 2      | Presentaciones     | Grupal         |

---

## 🎯 Preparación para Siguientes Unidades

Estas actividades sientan las bases conceptuales para:

- **Unidad 2:** Aplicación de DDD y diseño de bounded contexts
- **Unidad 3:** Selección de frameworks y tecnologías apropiadas  
- **Proyecto Final:** Justificación arquitectónica de decisiones de diseño

---

## 📚 Recursos de Apoyo

### Herramientas Sugeridas
- **Mapas Conceptuales:** Miro, Lucidchart, draw.io
- **Documentación:** Notion, GitHub Wiki, Markdown
- **Presentaciones:** Canva, Google Slides, PowerPoint

### Enlaces Útiles
- [Netflix Tech Blog](https://netflixtechblog.com/)
- [Uber Engineering](https://eng.uber.com/)
- [AWS Architecture Blog](https://aws.amazon.com/blogs/architecture/)
- [Microservices.io](https://microservices.io/)