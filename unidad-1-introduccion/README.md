# Unidad 1: Introducción a los microservicios y arquitecturas evolutivas

## 📋 Información general

- **Código:** CDD-2601-U1
- **Duración:** 2 semanas (10 horas académicas)
- **Modalidad:** 2h teoría + 3h práctica + 5h trabajo independiente
- **Peso en curso:** 20% de la evaluación total

---

## 🎯 Objetivos de aprendizaje

Al finalizar esta unidad, el estudiante será capaz de:

1. **Comprender** el contexto histórico que origina los microservicios
2. **Diferenciar** entre arquitecturas monolíticas, SOA y microservicios  
3. **Identificar** ventajas, riesgos y casos de uso apropiados
4. **Analizar** transformaciones arquitectónicas reales de la industria
5. **Evaluar** criterios para toma de decisiones arquitectónicas

---

## 📚 Estructura del contenido

```
unidad-1-introduccion/
├── teoria/           # Material conceptual y fundamentos
├── actividades/      # Ejercicios de consolidación
├── practicas/        # Laboratorios prácticos evaluados
└── recursos/         # Material complementario y referencias
```

### 📖 [Teoría](teoria/README.md)
Fundamentos conceptuales organizados en tres módulos:

#### 1.1 Contexto histórico y evolución
- Arquitectura Monolítica: ventajas y el "Monolito Intolerable"
- Service-Oriented Architecture (SOA): principios y diferencias
- Transición a Microservicios: definición y filosofía

#### 1.2 Principios fundamentales  
- Desacoplamiento, Cohesión y Modularidad
- Autonomía de equipos y base de datos por servicio
- Trade-offs del estilo Microservicios

#### 1.3 Casos de estudio y adopción
- Análisis de Netflix, Uber y Amazon
- Criterios de decisión para migración
- Ley de Conway y estructura organizacional

### 🎯 [Actividades de aprendizaje](actividades/README.md)
Ejercicios de consolidación conceptual:

1. **Cuadro Comparativo** - Análisis sistemático de estilos arquitectónicos
2. **Mapa Conceptual** - Visualización de componentes fundamentales  
3. **Análisis de Casos** - Investigación de transformaciones reales

### 🔬 [Prácticas de laboratorio](practicas/README.md)
Dos prácticas evaluadas que preparan para el proyecto final:

#### [Práctica 1.1: Análisis comparativo](practicas/practica-1-1.md)
- **Duración:** 2 horas | **Modalidad:** Individual
- **Objetivo:** Desarrollar criterio técnico para selección arquitectónica
- **Entregables:** Matriz comparativa + análisis de casos + matriz de decisión

#### [Práctica 1.2: Estudio de caso](practicas/practica-1-2.md)  
- **Duración:** 3 horas | **Modalidad:** Equipos 2-3 personas
- **Objetivo:** Analizar desacoplamiento real y crear mapa conceptual
- **Entregables:** Análisis completo + mapa interactivo + aplicación al proyecto

### 📚 [Recursos Complementarios](recursos/README.md)
Material de apoyo y referencias:

- **Bibliografía especializada** - Newman, Richardson, Fowler
- **Blogs técnicos oficiales** - Netflix, Uber, Amazon  
- **Herramientas de diagramado** - Miro, Lucidchart, Draw.io
- **Plantillas y templates** - Análisis, mapas conceptuales

---

## 📅 Cronograma detallado

### Semana 1: Fundamentos y principios

| Día                       | Actividad                                               | Duración | Modalidad   |
| ------------------------- | ------------------------------------------------------- | -------- | ----------- |
| Lunes                     | **Teoría:** Contexto histórico y SOA vs Microservicios  | 2h       | Presencial  |
| Miércoles                 | **Práctica 1.1:** Análisis comparativo de arquitecturas | 2h       | Laboratorio |
| Viernes                   | **Actividades:** Cuadro comparativo + Mapa conceptual   | 1h       | Presencial  |
| **Trabajo Independiente** | Lectura Newman Cap. 1-3 + Fowler article                | 5h       | Autónomo    |

### Semana 2: Casos de Estudio y Aplicación

| Día                       | Actividad                                               | Duración | Modalidad   |
| ------------------------- | ------------------------------------------------------- | -------- | ----------- |
| Lunes                     | **Teoría:** Casos Netflix, Uber, Amazon + Ley de Conway | 2h       | Presencial  |
| Miércoles                 | **Práctica 1.2:** Análisis de transformación (Parte 1)  | 1.5h     | Laboratorio |
| Viernes                   | **Práctica 1.2:** Mapa conceptual + Presentaciones      | 1.5h     | Laboratorio |
| **Trabajo Independiente** | Investigación de caso + preparación presentación        | 5h       | Autónomo    |

---

## 📊 Evaluación

### Distribución de Puntos
- **Práctica 1.1:** 8 puntos (40% de prácticas U1)
- **Práctica 1.2:** 12 puntos (60% de prácticas U1)
- **Actividades:** Formativas (no calificadas, pero obligatorias)

### Criterios Transversales
1. **Rigor técnico** (30%) - Precisión conceptual y terminología correcta
2. **Pensamiento crítico** (25%) - Análisis de trade-offs y justificaciones  
3. **Aplicación práctica** (25%) - Conexión con escenarios reales
4. **Comunicación** (20%) - Claridad en documentación y presentación

---

## 🎯 Competencias Desarrolladas

### Competencias Específicas del Programa
- **C1:** Comprender arquitecturas distribuidas y sus principios de diseño
- **C2:** Analizar casos reales de sistemas de gran escala  
- **C3:** Evaluar decisiones técnicas considerando contexto organizacional

### Competencias Transversales
- **Pensamiento crítico:** Análisis de trade-offs arquitectónicos
- **Comunicación técnica:** Documentación y presentación de análisis
- **Trabajo colaborativo:** Desarrollo de casos de estudio en equipos

---

## 🔗 Conexión con el Proyecto Final

Esta unidad sienta las bases conceptuales para el **Proyecto Final: Plataforma de Ingesta y Procesamiento de Datos**:

### Fundamentos Transferibles
1. **Justificación arquitectónica** → Por qué microservicios para este dominio
2. **Bounded contexts** → Identificación de servicios independientes (3-5)
3. **Patrones de comunicación** → Event-driven architecture
4. **Criterios de decisión** → Selección de tecnologías (Spring Boot + Quarkus)

### Casos de Referencia
- **Netflix:** Patrones de resiliencia (Circuit Breaker, API Gateway)
- **Uber:** Arquitectura orientada a eventos y procesamiento de datos
- **Amazon:** Principios de service ownership y observabilidad

---

## ✅ Checklist de Finalización

### Para Estudiantes
Al finalizar la Unidad 1, deberías poder:

- [ ] **Explicar** las diferencias entre monolito, SOA y microservicios
- [ ] **Justificar** la selección arquitectónica para un caso específico  
- [ ] **Identificar** patrones de desacoplamiento en casos reales
- [ ] **Aplicar** criterios de decisión a tu proyecto final
- [ ] **Comunicar** análisis técnicos de forma clara y estructurada

### Para Docentes
- [ ] **Evaluar** comprensión conceptual mediante rúbricas específicas
- [ ] **Retroalimentar** análisis de casos y mapas conceptuales
- [ ] **Conectar** aprendizajes con unidades siguientes
- [ ] **Documentar** mejores prácticas de estudiantes para futuros cursos

---

## 🔄 Mejora Continua

### Feedback de Estudiantes
- **Claridad conceptual:** ¿Los fundamentos quedaron claros?
- **Relevancia práctica:** ¿Los casos de estudio fueron útiles?
- **Carga de trabajo:** ¿El balance teoría/práctica fue apropiado?
- **Preparación para U2:** ¿Te sientes preparado para diseño de APIs?

### Actualizaciones Semestrales
- **Nuevos casos de estudio** de empresas emergentes
- **Herramientas actualizadas** para diagramado y análisis
- **Métricas de industria** actualizadas
- **Feedback de empleadores** sobre competencias requeridas

---

## 📚 Recursos de Inicio Rápido

### Lectura Esencial (1 hora)
1. [Fowler, M. "Microservices"](https://martinfowler.com/articles/microservices.html)
2. Newman, S. "Building Microservices" - Chapter 1

### Videos Introductorios (30 minutos)
1. "Microservices Explained" - Tech Primers (15 min)
2. "Netflix Microservices Architecture" - InfoQ (15 min)

### Preparación de Herramientas (15 minutos)
1. Cuenta en Miro o Lucidchart
2. Editor Markdown (Typora, Mark Text, o VS Code)
3. Acceso a Netflix Tech Blog y Uber Engineering

---

**Siguiente:** [Unidad 2: Diseño y Modelado de Microservicios →](../unidad-2-diseno/README.md)

---

*Esta unidad está diseñada para ser la base sólida sobre la cual construiremos progresivamente las competencias técnicas necesarias para el desarrollo de sistemas distribuidos modernos.*