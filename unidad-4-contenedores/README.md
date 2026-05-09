# **Unidad 4: Contenerización y orquestación de microservicios**

> **"Los contenedores son el puente entre el desarrollo y la producción, transformando código en servicios distribuibles y escalables"**

---

## 🎯 **Objetivos de aprendizaje**

Al finalizar esta unidad, los estudiantes serán capaces de:

- ✅ **Dominar** los fundamentos de Docker para microservicios
- ✅ **Crear** imágenes optimizadas y multi-stage builds
- ✅ **Implementar** estrategias de distribución y registro
- ✅ **Configurar** orquestación básica con Docker Compose

---

## 📚 **Estructura del contenido**

### **🐳 Fundamentos de contenerización**

- Arquitectura de contenedores vs virtualización
- Docker engine y runtime components
- Imágenes, capas y filesystem
- Networking y storage en contenedores
- Security y best practices

### **📦 Construcción y optimización**

- Dockerfile optimization
- Multi-stage builds
- Base images selection
- Layer caching strategies
- Image scanning y vulnerabilities

### **🚀 Distribución y orquestación**

- Registry strategies (Docker Hub, ECR, Harbor)
- Docker Compose para desarrollo
- Service discovery y load balancing
- Health checks y monitoring
- CI/CD integration

---

## 🏗️ **Estructura de la unidad**

```text
unidad-4-contenedores/
├── 01-teoria/                  # Fundamentos teóricos
│   ├── 00-docker.md            # Ejemplo básico de contenedores
│   ├── 01-docker.md            # Teoría y práctica de Docker
│   └── 02-docker-advanced.md   # Teoría y práctica de Docker
├── 03-actividades/             # Ejercicios prácticos
│   ├── 01-configuracion-mysql-docker.md
│   └── 02-integracion-mysql-quarkus.md
└── README.md
```

---

## 🚀 **Flujo de aprendizaje recomendado**

1. **📖 Teoría Fundamental**
   - Leer [Docker: Desde Cero hasta Producción](01-teoria/01-docker.md)
   - Comprender los conceptos de imágenes, contenedores, redes y volúmenes

2. **🎯 Actividades Prácticas**
   - Completar [Configuración de Base de Datos MySQL con Docker](03-actividades/01-configuracion-mysql-docker.md)
   - Completar [Integración de Base de Datos MySQL con Quarkus](03-actividades/02-integracion-mysql-quarkus.md)

3. **📚 Recursos complementarios**
   - Revisar [Conceptos fundamentales](02-recursos/01-conceptos-fundamentales.md)
   - Consultar [Docker Sign-In](02-recursos/02-docker-sign-in.md)
   - Estudiar [Vulnerabilidades en Docker](02-recursos/03-docker-vulnerabilities.md)

4. **🔧 Ejemplos visuales**
   - Analizar [diagrama del ciclo de vida Docker](01-teoria/images/docker-lifecycle-complete.jpeg)
   - Comparar [contenedores vs máquinas virtuales](01-teoria/images/docker-containers-vs-vm-details.png)

5. **💻 Desarrollo e integración**
   - Aplica los conceptos en tus proyectos Quarkus
   - Usa Docker Compose y volúmenes para bases de datos persistentes

---


## 🔗 **Conexión con el proyecto final**

Esta unidad **completa el ciclo de desarrollo** llevando los microservicios desde implementación hasta distribución:

### **Aplicación Directa al Proyecto**
- 🎯 **Contenerización completa** de la plataforma
- 🎯 **Imágenes optimizadas** para diferentes entornos
- 🎯 **Pipeline de distribución** automatizado
- 🎯 **Preparación para Kubernetes** y cloud deployment

### **Entrega Final del Proyecto**
- 🚀 **Microservicios completamente operacionales**
- 🚀 **Infraestructura como código** con Docker Compose
- 🚀 **Distribución automatizada** en registry
- 🚀 **Documentación de despliegue** completa

---

## 📚 **Material de Apoyo y Referencias**

### **Libros Recomendados**

#### **Docker Fundamentals**
1. **"Docker in Action"** - Jeff Nickoloff & Stephen Kuenzli (2ª edición, 2019)
   - Guía práctica desde conceptos básicos hasta producción
   - Ejemplos reales con microservicios
   - Editorial Manning

2. **"The Docker Book"** - James Turnbull (2016)
   - Introducción completa a Docker
   - Casos de uso en producción
   - Buenas prácticas y patrones

3. **"Using Docker"** - Adrian Mouat (2015)
   - Construcción y despliegue de aplicaciones en contenedores
   - Orquestación y clustering
   - Editorial O'Reilly

#### **Docker Avanzado y Producción**
1. **"Kubernetes in Action"** - Marko Lukša (2018)
   - Orquestación de contenedores con Kubernetes
   - Deployment patterns para producción
   - Editorial Manning

2. **"Docker Deep Dive"** - Nigel Poulton (2ª edición, 2019)
   - Análisis profundo de Docker internals
   - Performance tuning y optimización
   - Best practices para escala

### **Cursos en Línea Recomendados**

#### **Docker Fundamentals (Video Tutoriales)**
- **Udemy**: "Docker and Kubernetes: The Complete Guide" - Stephen Grider
  - Tiempo: 22+ horas | Nivel: Intermedio | Lenguaje: Inglés
  - URL: https://www.udemy.com/course/docker-and-kubernetes-the-complete-guide/

- **Coursera**: "Introduction to Containers w/ Docker, Kubernetes & OpenShift" - IBM
  - Tiempo: 15 horas | Nivel: Beginner | Acceso: Auditoría gratuita disponible
  - URL: https://www.coursera.org/learn/ibm-containers-docker-kubernetes-openshift

- **YouTube**: "Docker Tutorial for Beginners" - Amigoscode
  - Playlist completa desde cero
  - URL: https://www.youtube.com/watch?v=17Bl31rlnRM

#### **Docker Avanzado**
- **Linux Academy / A Cloud Guru**: "Docker Certified Associate (DCA) Exam Prep"
  - Nivel: Avanzado | Laboratorios prácticos incluidos
  - Certificación reconocida en la industria

- **YouTube**: "Docker Advanced Tutorial" - TechWorld with Nana
  - Docker Compose, Swarm, y orquestación
  - URL: https://www.youtube.com/playlist?list=PLy_6D98if0UiiG2BYEf8uqSqP3zVHMXk4

#### **Docker Compose y Orquestación**
- **Udemy**: "Docker Compose & Kubernetes for Beginners" - Praveen Gupta
  - Enfoque práctico en herramientas de orquestación
  - Ejemplos reales con microservicios

### **Documentación Oficial**

#### **Docker**
- [Docker Official Documentation](https://docs.docker.com/)
- [Dockerfile Reference](https://docs.docker.com/engine/reference/builder/)
- [Docker Compose File Reference](https://docs.docker.com/compose/compose-file/)
- [Docker Best Practices](https://docs.docker.com/develop/dev-best-practices/)

#### **Docker Hub**
- [Docker Official Images](https://hub.docker.com/search?image_filter=official)
- [Publishing Images](https://docs.docker.com/docker-hub/publish/)
- [Security and Access Control](https://docs.docker.com/docker-hub/access-tokens/)

#### **Kubernetes (Próxima etapa)**
- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [Kubernetes Concepts](https://kubernetes.io/docs/concepts/)
- [kubectl Reference](https://kubernetes.io/docs/reference/kubectl/)

### **Herramientas Online**

1. **Docker Hub** - https://hub.docker.com/
   - Repositorio oficial de imágenes Docker
   - Almacenar y compartir tus imágenes

2. **Play with Docker** - https://labs.play-with-docker.com/
   - Laboratorio Docker gratuito en línea
   - Sin instalación requerida

3. **Docker Playground** - https://www.katacoda.com/courses/docker
   - Escenarios interactivos de aprendizaje
   - Hands-on practice

4. **Dockerfile Linter - Hadolint** - https://www.hadolint.net/
   - Validador online de Dockerfiles
   - Mejores prácticas automáticas

5. **Container Structure Tests** - https://github.com/GoogleContainerTools/container-structure-test
   - Testing para imágenes Docker
   - Validación de estructura

### **Blogs y Artículos Técnicos**

- **Docker Blog**: https://www.docker.com/blog/
- **The New Stack**: https://thenewstack.io/ (artículos sobre containers y DevOps)
- **Medium** (Docker tag): https://medium.com/tag/docker
- **Dev.to**: https://dev.to/ (búsqueda: Docker)
- **Nigel Poulton's Blog**: https://nigelpoulton.com/

### **Repositorios de Referencia en GitHub**

- **Docker Official Images**: https://github.com/docker-library
- **Awesome Docker**: https://github.com/veggiemonk/awesome-docker
- **Docker Samples**: https://github.com/docker/samples
- **Compose Examples**: https://github.com/docker/compose/tree/master/docs/samples

### **Comunidades y Foros**

- **Stack Overflow**
  - Tags: `docker`, `docker-compose`, `dockerfile`, `containerization`
  
- **Reddit**
  - r/docker, r/devops, r/kubernetes
  
- **Docker Community**
  - https://www.docker.com/community
  - Slack, Forums y Meetups
  
- **CNCF (Cloud Native Computing Foundation)**
  - https://www.cncf.io/
  - Eventos y recursos sobre containers

### **Herramientas Complementarias**

- **Docker Compose** - Orquestación local
- **Docker Swarm** - Clustering nativo de Docker
- **Portainer** - UI para gestión de Docker
- **ctop** - Monitoreo de contenedores en tiempo real
- **Dive** - Análisis de capas de imágenes Docker

---

**Anterior:** [← Unidad 3: Implementación](../unidad-3-implementacion/README.md) | **Siguiente:** [Unidad 5: Resiliencia →](../unidad-5-resiliencia/README.md)
