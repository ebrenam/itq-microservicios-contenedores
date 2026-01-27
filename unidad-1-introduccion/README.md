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

### 📚 [Recursos complementarios](04-recursos/README.md)

Material de apoyo y referencias:
- **Bibliografía especializada** - Newman, Richardson, Fowler
- **Blogs técnicos oficiales** - Netflix, Uber, Amazon
- **Herramientas de diagramado** - Miro, Lucidchart, Draw.io
- **Plantillas y templates** - Análisis, mapas conceptuales

---

## 🎯 Conexión con el proyecto final

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

**Siguiente:** [Unidad 2: Diseño y Modelado de Microservicios →](../unidad-2-diseno/README.md)

---

*Esta unidad está diseñada para ser la base sólida sobre la cual construiremos progresivamente las competencias técnicas necesarias para el desarrollo de sistemas distribuidos modernos.*
