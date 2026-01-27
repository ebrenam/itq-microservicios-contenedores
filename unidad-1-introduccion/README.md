# Unidad 1: Introducción a los microservicios y arquitecturas evolutivas

## 🎯 Objetivos de aprendizaje

Al finalizar esta unidad, el estudiante será capaz de:

1. **Comprender** el contexto histórico que origina los microservicios
2. **Diferenciar** entre arquitecturas monolíticas, SOA y microservicios
3. **Identificar** ventajas, riesgos y casos de uso apropiados
4. **Analizar** transformaciones arquitectónicas reales de la industria
5. **Evaluar** criterios para toma de decisiones arquitectónicas

---

## 📚 Estructura del contenido

```text
unidad-1-introduccion/
├── 01-teoria/        # Material teórico completo con diagramas
├── 02-actividades/   # Ejercicios de consolidación
├── 03-practicas/     # Laboratorios prácticos evaluados
└── 04-recursos/      # Material complementario y referencias
```

### 📖 [Teoría](01-teoria/README.md)

#### 1.1 Contexto histórico y evolución
- Arquitectura Monolítica: ventajas y el "Monolito Intolerable"
- Service-Oriented Architecture (SOA): principios y diferencias
- Transición a Microservicios: definición y filosofía

#### 1.2 Principios fundamentales
- Desacoplamiento, Cohesión y Modularidad
- Autonomía de equipos y base de datos por servicio
- Trade-offs del estilo Microservicios

#### 1.3 Casos de estudio y adopción
- Análisis detallado de Netflix, Uber y Amazon
- Criterios de decisión para migración
- Ley de Conway y estructura organizacional

### 🎯 [Actividades de consolidación](02-actividades/README.md)

Ejercicios para reforzar los conceptos:

1. **Cuadro Comparativo** - Análisis sistemático de estilos arquitectónicos
2. **Mapa Conceptual** - Visualización de componentes fundamentales  
3. **Análisis de Casos** - Investigación de transformaciones reales

### 🔬 [Prácticas de laboratorio](03-practicas/README.md)

Dos prácticas evaluadas que preparan para el proyecto final:

#### [Práctica 1.1: Análisis comparativo](03-practicas/practica-1-1.md)
- **Modalidad:** Individual
- **Objetivo:** Desarrollar criterio técnico para selección arquitectónica
- **Entregables:** Matriz comparativa + análisis de casos + matriz de decisión

#### [Práctica 1.2: Estudio de caso](03-practicas/practica-1-2.md)
- **Modalidad:** Equipos 2-3 personas
- **Objetivo:** Analizar desacoplamiento real y crear mapa conceptual
- **Entregables:** Análisis completo + mapa interactivo + aplicación al proyecto

### 📚 [Recursos complementarios](04-recursos/README.md)

Material de apoyo y referencias:
- **Bibliografía especializada** - Newman, Richardson, Fowler
- **Blogs técnicos oficiales** - Netflix, Uber, Amazon
- **Herramientas de diagramado** - Miro, Lucidchart, Draw.io
- **Plantillas y templates** - Análisis, mapas conceptuales

---

## 📅 Cronograma detallado

### **Semana 1: Fundamentos y principios**

| Tipo | Actividad |
|------|----------|
| Teoría | Contexto histórico y SOA vs Microservicios |
| Práctica | Análisis comparativo de arquitecturas |
| Actividades | Cuadro comparativo + Mapa conceptual |
| Trabajo Independiente | Lectura Newman Cap. 1-3 + Fowler article |

### **Semana 2: Casos de estudio y aplicación**

| Tipo | Actividad |
|------|----------|
| Teoría | Casos Netflix, Uber, Amazon + Ley de Conway |
| Práctica | Análisis de transformación (Parte 1) |
| Práctica | Mapa conceptual + Presentaciones |
| Trabajo Independiente | Investigación de caso + preparación presentación |

---

##  Conexión con el proyecto final

Esta unidad sienta las bases conceptuales para el **Proyecto Final: Plataforma de Ingesta y Procesamiento de Datos**:

### **Fundamentos transferibles**
1. **Justificación arquitectónica** → Por qué microservicios para este dominio
2. **Bounded contexts** → Identificación de servicios independientes (3-5)
3. **Patrones de comunicación** → Event-driven architecture
4. **Criterios de decisión** → Selección de tecnologías (Spring Boot + Quarkus)

### **Casos de referencia**
- **Netflix:** Patrones de resiliencia (Circuit Breaker, API Gateway)
- **Uber:** Arquitectura orientada a eventos y procesamiento de datos
- **Amazon:** Principios de service ownership y observabilidad

---

## ✅ Checklist de finalización

### **Para estudiantes**
Al finalizar la Unidad 1, deberías poder:
- [ ] **Explicar** las diferencias entre monolito, SOA y microservicios
- [ ] **Justificar** la selección arquitectónica para un caso específico
- [ ] **Identificar** patrones de desacoplamiento en casos reales
- [ ] **Aplicar** criterios de decisión a tu proyecto final
- [ ] **Comunicar** análisis técnicos de forma clara y estructurada

### **Para docentes**
- [ ] **Evaluar** comprensión conceptual mediante rúbricas específicas
- [ ] **Retroalimentar** análisis de casos y mapas conceptuales
- [ ] **Conectar** aprendizajes con unidades siguientes
- [ ] **Documentar** mejores prácticas de estudiantes para futuros cursos

---

**Siguiente:** [Unidad 2: Diseño y Modelado de Microservicios →](../unidad-2-diseno/README.md)

---

*Esta unidad está diseñada para ser la base sólida sobre la cual construiremos progresivamente las competencias técnicas necesarias para el desarrollo de sistemas distribuidos modernos.*
