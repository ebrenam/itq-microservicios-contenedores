# Práctica 1.1: Análisis Comparativo de Estilos Arquitectónicos

## 🎯 Objetivo
Elaborar un cuadro comparativo detallado que contraste Monolitos, SOA y Microservicios, identificando ventajas, riesgos y casos de uso mediante análisis de escenarios reales.

---

## 📋 Información General

- **Modalidad:** Individual con discusión grupal
- **Prerrequisitos:** Lectura de material teórico de la Unidad 1
- **Herramientas:** Editor de texto, navegador web

---

## 🔧 Preparación del Entorno

### Recursos Necesarios
1. **Plantilla de análisis** (proporcionada)
2. **Casos de estudio** preparados
3. **Acceso a internet** para investigación adicional
4. **Editor Markdown** o procesador de texto

### Casos de Estudio Preparados
- **Caso A:** Sistema de E-commerce tradicional (100K usuarios)
- **Caso B:** Plataforma de streaming de video (10M usuarios)  
- **Caso C:** Sistema bancario core (regulaciones estrictas)
- **Caso D:** Startup de delivery de comida (crecimiento rápido)

---

## 📚 Parte 1: Análisis Teórico Comparativo

### Instrucciones

1. **Completar la matriz comparativa** utilizando la plantilla proporcionada
2. **Investigar** al menos 2 fuentes adicionales por cada arquitectura
3. **Documentar** ejemplos específicos de cada característica

### Plantilla Extendida de Análisis

```markdown
# Matriz Comparativa de Estilos Arquitectónicos

## 1. Características Técnicas

| Aspecto | Monolito | SOA | Microservicios |
|---------|----------|-----|----------------|
| **Unidad de Despliegue** | | | |
| **Estrategia de Base de Datos** | | | |
| **Protocolo de Comunicación** | | | |
| **Gestión de Transacciones** | | | |
| **Estrategia de Escalado** | | | |
| **Manejo de Fallos** | | | |

## 2. Aspectos de Desarrollo

| Aspecto | Monolito | SOA | Microservicios |
|---------|----------|-----|----------------|
| **Complejidad Inicial** | | | |
| **Curva de Aprendizaje** | | | |
| **Tiempo hasta Producción** | | | |
| **Facilidad de Testing** | | | |
| **Gestión de Dependencias** | | | |
| **Refactoring** | | | |

## 3. Aspectos Operacionales

| Aspecto | Monolito | SOA | Microservicios |
|---------|----------|-----|----------------|
| **Complejidad de Despliegue** | | | |
| **Monitoreo y Observabilidad** | | | |
| **Gestión de Configuración** | | | |
| **Backup y Recovery** | | | |
| **Seguridad** | | | |
| **Costos de Infraestructura** | | | |

## 4. Aspectos Organizacionales

| Aspecto | Monolito | SOA | Microservicios |
|---------|----------|-----|----------------|
| **Tamaño de Equipo Ideal** | | | |
| **Estructura Organizacional** | | | |
| **Ownership de Código** | | | |
| **Ciclo de Release** | | | |
| **Coordinación entre Equipos** | | | |
| **Especialización Técnica** | | | |
```

### Guía de Completado

**Para cada celda, incluir:**
- Descripción concisa de la característica
- Ventaja/desventaja principal
- Ejemplo específico o métrica cuando sea posible

**Fuentes sugeridas:**
- Martin Fowler - Microservices vs SOA
- Netflix Engineering Blog
- ThoughtWorks Technology Radar
- Amazon Architecture Guidelines

---

## 🎯 Parte 2: Aplicación a Casos Reales

### Actividad: Recomendación Arquitectónica

Para cada caso de estudio, determinar el estilo arquitectónico más apropiado y justificar la decisión.

#### Caso A: E-commerce Tradicional
**Contexto:**
- 100,000 usuarios registrados
- 10,000 pedidos/mes
- Equipo de 8 desarrolladores
- Presupuesto limitado
- Tiempo al mercado: 6 meses

**Tu análisis:**
```
Arquitectura recomendada: _______________

Justificación:
1. Factor decisivo principal: 
2. Ventajas específicas para este caso:
3. Riesgos mitigables:
4. Plan de evolución futura:
```

#### Caso B: Plataforma de Streaming
**Contexto:**
- 10 millones de usuarios activos
- Picos de tráfico impredecibles
- Múltiples tipos de contenido (video, audio, texto)
- Equipos distribuidos globalmente
- Regulaciones por país

**Tu análisis:**
```
Arquitectura recomendada: _______________

Justificación:
1. Factor decisivo principal: 
2. Ventajas específicas para este caso:
3. Riesgos mitigables:
4. Plan de evolución futura:
```

#### Caso C: Sistema Bancario Core
**Contexto:**
- Regulaciones financieras estrictas
- Requerimientos de auditoria completa
- Transacciones de alta criticidad
- Uptime 99.99% requerido
- Integración con sistemas legacy

**Tu análisis:**
```
Arquitectura recomendada: _______________

Justificación:
1. Factor decisivo principal: 
2. Ventajas específicas para este caso:
3. Riesgos mitigables:
4. Plan de evolución futura:
```

#### Caso D: Startup de Delivery
**Contexto:**
- Crecimiento exponencial esperado
- Múltiples ciudades en 6 meses
- Equipo técnico de 4 personas
- Integración con múltiples APIs externas
- Inversión Series A conseguida

**Tu análisis:**
```
Arquitectura recomendada: _______________

Justificación:
1. Factor decisivo principal: 
2. Ventajas específicas para este caso:
3. Riesgos mitigables:
4. Plan de evolución futura:
```

---

## 🧠 Parte 3: Síntesis y Reflexión

### Actividad de Cierre

1. **Completar matriz de decisión:**

| Criterio | Peso | Monolito Score | SOA Score | Microservicios Score |
|----------|------|----------------|-----------|----------------------|
| Complejidad Técnica | 20% | | | |
| Tiempo al Mercado | 15% | | | |
| Escalabilidad | 25% | | | |
| Tamaño de Equipo | 15% | | | |
| Presupuesto | 15% | | | |
| Mantenibilidad | 10% | | | |

2. **Reflexión personal:**
   - ¿Cuál fue el caso más desafiante de analizar? ¿Por qué?
   - ¿Qué factor consideras más importante al tomar decisiones arquitectónicas?
   - ¿Cómo cambiarían tus recomendaciones si tuvieras que implementarlas en tu contexto laboral actual?

---

## 📝 Entregables

### 1. Documento de Análisis
- **Formato:** Markdown o PDF
- **Contenido:** 
  - Matriz comparativa completa
  - Análisis de 4 casos de estudio
  - Matriz de decisión con puntuaciones
  - Reflexión personal (máximo 500 palabras)

### 2. Presentación Ejecutiva
- **Contenido:**
  - 3 hallazgos principales del análisis
  - 1 recomendación general para toma de decisiones
  - 1 caso de estudio más interesante y por qué

---

## ✅ Criterios de Evaluación

| Criterio | Peso | Excelente (5) | Bueno (4) | Satisfactorio (3) | Insuficiente (1-2) |
|----------|------|---------------|-----------|-------------------|-------------------|
| **Completitud de Matriz** | 30% | Todas las celdas con información precisa y ejemplos | Mayoría completa con información correcta | Matriz básicamente completa | Información incompleta o incorrecta |
| **Análisis de Casos** | 35% | Justificación sólida basada en criterios técnicos | Análisis correcto con justificación básica | Recomendaciones apropiadas sin profundizar | Recomendaciones incorrectas |
| **Matriz de Decisión** | 20% | Pesos bien justificados y puntuaciones coherentes | Criterios apropiados con puntuaciones consistentes | Matriz completa pero sin justificación | Criterios o puntuaciones inconsistentes |
| **Reflexión Personal** | 15% | Insights profundos y conexión con experiencia | Reflexión thoughtful y bien articulada | Reflexión básica pero coherente | Reflexión superficial |

---

## 🔗 Conexión con el Proyecto Final

Esta práctica sienta las bases para:

1. **Justificación arquitectónica** del proyecto final
2. **Criterios de decisión** para selección de patrones
3. **Análisis de trade-offs** en diseño de microservicios
4. **Documentación de decisiones** técnicas

Los casos analizados aquí se retomarán al diseñar la "Plataforma de Ingesta y Procesamiento de Datos" del proyecto final.

---

## 📚 Recursos Adicionales

### Lecturas Complementarias
- Richardson, C. "Microservices Patterns" - Chapter 1
- Fowler, M. "Microservices Trade-Offs"
- AWS Well-Architected Framework

### Herramientas de Apoyo  
- [Architecture Decision Records (ADR)](https://github.com/joelparkerhenderson/architecture_decision_record)
- [C4 Model for Software Architecture](https://c4model.com/)
- [ThoughtWorks Technology Radar](https://www.thoughtworks.com/radar)