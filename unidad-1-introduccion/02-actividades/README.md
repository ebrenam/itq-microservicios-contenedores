# Actividad Guiada Única: Descifrando la Transformación de Netflix

## 🎯 Información general

**Objetivo:** Consolidar TODOS los conceptos teóricos de microservicios analizando paso a paso la transformación real de Netflix, desde su monolito inicial hasta su arquitectura actual de 700+ microservicios.

**Modalidad:** Clase dirigida con análisis colaborativo guiado por el profesor

**Duración:** 90 minutos (sesión única optimizada)

**Producto final:** Comprensión completa de por qué y cómo Netflix hizo la transición, aplicando todos los conceptos teóricos de la unidad

---

## 🎬 ACTIVIDAD GUIADA: "De Monolito a 700 Microservicios - El Caso Netflix"

### 📚 Preparación (profesor presenta contexto - 10 min)

**Como profesor, inicio explicando:**

> "Estudiantes, vamos a vivir la transformación más famosa de la industria tech. Netflix no nació como la plataforma de streaming que conocen hoy. Empezó como una empresa de DVDs por correo con UN SOLO SISTEMA. Hoy tienen más de 700 microservicios. ¿Cómo y por qué pasaron de 1 a 700? Eso es lo que vamos a descubrir aplicando todo lo que han estudiado."

**Contexto que presento:**
- **2007**: Netflix = DVDs por correo + un monolito Rails
- **2024**: Netflix = Streaming global + 700+ microservicios independientes  
- **Desafío**: Entender esta transformación aplicando los conceptos teóricos

---

### 🕵️ PASO 1: Diagnosticando el "Monolito Intolerable" de Netflix (20 min)

**Como profesor, guío el análisis:**

> "Imaginen que son consultores arquitectónicos en 2008. Netflix nos contrata porque su sistema está colapsando. Vamos a aplicar lo que saben de arquitecturas monolíticas para diagnosticar qué estaba pasando."

#### 🔍 Actividad dirigida: Síntomas del monolito Netflix

**Presento los síntomas reales (los estudiantes identifican los conceptos):**

| Síntoma Real de Netflix 2008 | **Estudiantes: ¿Qué concepto teórico aplica?** |
|------------------------------|-------------------------------------------|
| "Un bug en recomendaciones tumba todo el sitio" | *[Estudiantes responden: Acoplamiento fuerte]* |
| "Deployments toman 6 horas y fallan frecuentemente" | *[Estudiantes: Riesgo de deployment monolítico]* |
| "El equipo de DVDs no puede trabajar sin el equipo de Streaming" | *[Estudiantes: Dependencias de equipos]* |
| "Escalar DVDs significa escalar innecesariamente Streaming" | *[Estudiantes: Escalamiento monolítico]* |
| "Cambiar la recomendación requiere deployment completo" | *[Estudiantes: Modularidad limitada]* |

**Mi rol como profesor:**
- Presento cada síntoma real
- Pregunto: "¿Qué concepto de monolitos explica este problema?"
- Confirmo y refuerzo: "Exacto, eso es acoplamiento fuerte porque..."
- Conecto con teoría: "Recuerdan que en teoría vimos que los monolitos..."

#### 📊 Síntesis dirigida: El diagnóstico

**Guío la consolidación:**
> "Perfecto, han identificado todos los problemas teóricos del monolito. Netflix tenía acoplamiento fuerte, riesgo de deployment, dependencias organizacionales y escalamiento ineficiente. Ahora, ¿cuál era la solución teórica que estudiamos?"

**Respuesta esperada:** Microservicios para lograr desacoplamiento, autonomía, escalamiento independiente.

---

### ⚖️ PASO 2: La decisión arquitectónica - Trade-offs en acción (25 min)

**Como profesor, presento el dilema real:**

> "Netflix en 2009 está en una encrucijada. Pueden seguir con el monolito, migrar a SOA, o apostar por microservicios. Vamos a aplicar el análisis de trade-offs que estudiamos para entender su decisión."

#### 🎯 Actividad: Matriz de decisión colaborativa

**Proyecto en pantalla y completamos juntos:**

| Criterio (estudiantes proponen peso) | Monolito | SOA | **Microservicios** |
|--------------------------------------|----------|-----|-------------------|
| **Velocidad de desarrollo** (25%) | 1 | 3 | **5** ← *Netflix eligió* |
| **Escalamiento independiente** (30%) | 1 | 3 | **5** ← *Crítico para streaming* |
| **Tolerancia a fallos** (20%) | 1 | 3 | **5** ← *No podían tener downtime* |
| **Complejidad operacional** (15%) | 5 | 3 | **1** ← *Asumieron esta complejidad* |
| **Costo inicial** (10%) | 5 | 3 | **1** ← *Invirtieron fuerte* |

**Mi proceso de facilitación:**
1. **Pregunto:** "¿Qué criterios creen que eran críticos para Netflix?"
2. **Explico:** "Streaming requería escalamiento independiente porque..."
3. **Calculamos:** "Si microservicios gana en velocidad (5×25%), escalamiento (5×30%)..."
4. **Concluimos:** "La matriz muestra por qué eligieron microservicios a pesar de la complejidad"

#### 💡 Conexión con Ley de Conway

**Explico el factor organizacional:**
> "Pero había un factor clave que estudiamos: la Ley de Conway. Netflix tenía que reorganizar sus equipos también. ¿Recuerdan qué dice esta ley?"

**Guío la reflexión:**
- **Ley de Conway**: Las arquitecturas reflejan la comunicación organizacional
- **Aplicación Netflix**: 1 monolito = 1 equipo grande vs 700 microservicios = 700 equipos pequeños
- **Resultado**: Cada equipo Netflix es dueño de sus microservicios (autonomía total)

---

### 🏗️ PASO 3: La arquitectura resultante - Principios en práctica (25 min)

**Como profesor, muestro la arquitectura actual:**

> "Ahora vamos a ver cómo Netflix aplicó TODOS los principios de microservicios que estudiamos. Cada principio teórico tiene una manifestación concreta en su arquitectura."

#### 🎯 Actividad: Mapeo de principios a implementación

**Presento la arquitectura real y pregunto:**

```
🎬 Netflix Architecture (2024)
├── User Service (perfiles, autenticación)
├── Video Service (streaming, transcoding)  
├── Recommendation Service (ML, algoritmos)
├── Billing Service (pagos, suscripciones)
├── Content Service (metadatos, catálogo)
└── ... 695 microservicios más
```

| Principio Teórico | **¿Cómo lo ven aplicado en Netflix?** | Implementación Real |
|-------------------|--------------------------------------|---------------------|
| **Base de datos por servicio** | *[Estudiantes observan]* | User Service → User DB, Video Service → Video DB |
| **Desacoplamiento** | *[¿Qué evidencia ven?]* | APIs REST independientes, fallos aislados |
| **Cohesión funcional** | *[¿Dónde lo identifican?]* | Cada servicio = una responsabilidad específica |
| **Autonomía de equipos** | *[¿Cómo se manifiesta?]* | Cada equipo despliega independientemente |
| **Escalamiento independiente** | *[¿Por qué es crucial aquí?]* | Video Service escala diferente que Billing |

**Mi rol:**
- Muestro cada parte de la arquitectura
- Pregunto cómo se conecta con la teoría
- Confirmo y amplío sus respuestas
- Hago conexiones: "Exactly, eso es cohesión funcional porque el Video Service solo se encarga de..."

#### 🔧 Patrones identificados

**Explico los patrones clave que implementaron:**
- **API Gateway**: Un punto de entrada que distribuye requests
- **Circuit Breaker**: Si Recommendations falla, el streaming continúa  
- **Service Discovery**: Los 700 servicios se encuentran automáticamente
- **Event-driven**: Los servicios se comunican por eventos (user watches → update recommendations)

---

### 🚀 PASO 4: Lecciones aprendidas y aplicabilidad (10 min)

**Como profesor, cierro con reflexión aplicada:**

> "Netflix nos enseña que los microservicios no son solo teoría. Hay decisiones reales, trade-offs concretos y resultados medibles. ¿Qué lecciones extraemos para aplicar a otros contextos?"

#### 🎓 Síntesis final dirigida

**Pregunto y guío las respuestas:**

1. **¿Cuándo SÍ microservicios?**
   - Alta escala (millones de usuarios)
   - Equipos múltiples (50+ desarrolladores)  
   - Dominios bien definidos (streaming ≠ billing)
   - Tolerancia a complejidad operacional

2. **¿Cuándo NO microservicios?**
   - Equipos pequeños (< 10 personas)
   - Producto en MVP
   - Dominios poco claros
   - Presupuesto limitado

3. **¿Qué principio fue más crítico para Netflix?**
   - Respuesta esperada: Escalamiento independiente + autonomía de equipos

**Pregunta final para aplicar:**
> "Si tuvieran que diseñar una plataforma de e-learning (como Coursera), ¿aplicarían la estrategia de Netflix? ¿Por qué sí o no?"

---

## 📊 Evaluación de la actividad

### Criterios de evaluación

| Aspecto | Peso | Descripción | Evidencias |
|---------|------|-------------|------------|
| **Identificación de conceptos** | 40% | Capacidad de conectar síntomas reales con teoría estudiada | Respuestas correctas en matriz, identificación de principios |
| **Análisis de trade-offs** | 30% | Comprensión de por qué Netflix eligió microservicios | Justificación en matriz de decisión, entendimiento de costos/beneficios |
| **Aplicación de principios** | 20% | Reconocimiento de principios teóricos en arquitectura real | Mapeo correcto de principios a implementación |
| **Síntesis y aplicabilidad** | 10% | Capacidad de extraer lecciones para otros contextos | Reflexión final sobre cuándo aplicar microservicios |

### Modalidad de evaluación

- **Participación durante clase**: Respuestas a preguntas dirigidas
- **Completitud de matriz**: Contribución a análisis colaborativo
- **Reflexión final**: Aplicación de lecciones aprendidas
- **No hay entregables individuales**: Todo se trabaja en clase

### Evidencias de aprendizaje logrado

**Excelente comprensión:**
- Identifica todos los síntomas monolíticos en Netflix
- Justifica la decisión arquitectónica con trade-offs claros
- Reconoce la implementación de principios teóricos
- Aplica lecciones a nuevos contextos

**Comprensión satisfactoria:**
- Identifica la mayoría de conceptos teóricos
- Entiende las razones principales de la migración
- Reconoce algunos principios en la arquitectura
- Extrae lecciones básicas

---

## 🧰 Recursos para el profesor

### Material de apoyo preparado

**Slides clave:**
1. Timeline Netflix 2007-2024 (evolución visual)
2. Arquitectura monolítica vs microservicios (comparación lado a lado)
3. Tabla de síntomas reales (para análisis colaborativo)
4. Matriz de decisión (template para completar en clase)
5. Arquitectura actual Netflix (diagrama completo)
6. Patrones implementados (circuit breaker, API gateway, etc.)

### Preguntas guía para facilitar

**Para diagnosticar monolito:**
- "¿Qué concepto teórico explica que un bug en recomendaciones tumbe todo el sitio?"
- "Si escalar DVDs significa escalar streaming innecesariamente, ¿qué principio se está violando?"

**Para análisis de decisión:**
- "Para una empresa de streaming global, ¿qué criterios serían más importantes?"
- "¿Por qué Netflix aceptó la complejidad operacional de microservicios?"

**Para arquitectura:**
- "¿Dónde ven aplicado el principio de 'base de datos por servicio'?"
- "¿Cómo logra Netflix que el fallo de un servicio no afecte a los demás?"

**Para síntesis:**
- "¿Qué factores determinan si microservicios son apropiados para un contexto?"
- "¿Cómo aplicarían estas lecciones a un proyecto diferente?"

### Conexión con teoría estudiada

**Refuerza directamente:**
- Características del monolito intolerable (Sección 1.1)
- Principios fundamentales de microservicios (Sección 1.2)  
- Trade-offs y decisiones arquitectónicas (Sección 1.2)
- Ley de Conway y organización (Sección 1.3)
- Casos de adopción exitosa (Sección 1.3)

**Prepara para:**
- Unidad 2: Diseño y descomposición (bounded contexts identificados en Netflix)
- Unidad 3: Implementación (patrones técnicos aplicados)
- Proyecto final: Metodología de análisis y decisión arquitectónica

---

## ✅ Checklist para el profesor

### Preparación de clase (5 min antes)
- [ ] Slides de Netflix listos (timeline, arquitectura, matriz)
- [ ] Proyector configurado para trabajo colaborativo  
- [ ] Matriz de decisión en documento compartido
- [ ] Ejemplos de síntomas preparados para presentar

### Durante la actividad (90 min)
- [ ] **Paso 1**: Presentar contexto y síntomas, guiar identificación de conceptos
- [ ] **Paso 2**: Facilitar matriz de decisión, explicar trade-offs
- [ ] **Paso 3**: Mostrar arquitectura, conectar con principios teóricos
- [ ] **Paso 4**: Dirigir síntesis y aplicabilidad a otros contextos

### Cierre de clase
- [ ] Confirmar que todos identificaron los conceptos clave
- [ ] Verificar comprensión de por qué Netflix eligió microservicios
- [ ] Asegurar conexión con teoría estudiada
- [ ] Preparar transición a siguiente unidad

---

**Siguiente:** [Prácticas de Laboratorio →](../03-practicas/README.md)
