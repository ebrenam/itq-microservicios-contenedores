# 📖 Teoría: Fundamentos de Docker y Contenerización

> **"Aprender Docker es aprender a empacar y distribuir software de manera confiable"**

Bienvenido a la sección teórica de Contenerización. Aquí aprenderás los fundamentos y conceptos avanzados de Docker para microservicios.

---

## 🎯 Objetivos de Aprendizaje

Al completar esta sección teórica, serás capaz de:

- ✅ Entender qué son contenedores y por qué son revolucionarios
- ✅ Diferenciar entre imágenes Docker y contenedores
- ✅ Construir imágenes Docker optimizadas
- ✅ Configurar redes y volúmenes
- ✅ Orquestar múltiples contenedores con Docker Compose
- ✅ Aplicar mejores prácticas de producción

---

## 📚 Contenido de la Sección

### **[Tema 4.1: Docker: Desde Cero hasta Producción](01-docker.md)**

Introducción completa a Docker con enfoque hands-on.

**Contenidos:**
- Concepto de contenedores vs máquinas virtuales
- Mi primer contenedor
- Imágenes vs Contenedores
- Crear tu propia aplicación en Docker
- Múltiples contenedores que hablan entre sí (redes)
- Automatización con Docker Compose
- Almacenamiento persistente (volúmenes)
- Escalado: Docker Swarm
- Arquitectura en producción
- DevOps: El ciclo de vida completo

**Nivel:** 🟢 Beginner → 🟡 Intermediate

---

### **[Tema 4.2: Docker Avanzado: Optimización y Producción](02-docker-advanced.md)**

Técnicas avanzadas para entornos de producción.

**Contenidos:**
- Optimización de imágenes Docker
- Multi-stage builds
- Seguridad en contenedores
- Performance tuning
- Estrategias de logging y monitoreo
- Integración con CI/CD
- Orquestación avanzada

**Nivel:** 🟠 Advanced → 🔴 Expert

---

## 🎓 Tabla de Progresión

| Nivel | Sección | Herramienta | Objetivo |
|-------|---------|-------------|----------|
| 🟢 Beginner | 01-docker: 1-3 | `docker` | Ejecutar y construir contenedores simples |
| 🟡 Intermediate | 01-docker: 4-5 | `docker-compose` | Múltiples contenedores, desarrollo local |
| 🟠 Advanced | 02-docker-advanced: 6-7 | `docker stack` | Escalado, múltiples máquinas |
| 🔴 Expert | 02-docker-advanced: 8-9 | Kubernetes / Swarm | Arquitectura empresarial, CI/CD |

---

## 📚 Material de Referencia Rápida

### Comandos Esenciales

```bash
# Imágenes
docker build -t nombre:tag .           # Construir imagen
docker run -d -p 8080:8080 nombre      # Ejecutar contenedor
docker image ls                        # Listar imágenes
docker image rm nombre                 # Eliminar imagen

# Contenedores
docker container ls                    # Ver activos
docker container ls -a                 # Ver todos
docker container stop nombre           # Detener
docker container rm nombre             # Eliminar
docker container logs nombre           # Ver logs

# Redes
docker network create mi-red           # Crear red
docker network ls                      # Listar redes
docker run --network mi-red imagen     # Usar red

# Volúmenes
docker volume create datos             # Crear volumen
docker volume ls                       # Listar volúmenes
docker run -v datos:/data imagen       # Usar volumen

# Docker Compose
docker-compose up -d                   # Levantar servicios
docker-compose down                    # Bajar servicios
docker-compose logs -f                 # Logs en vivo
```

### Glosario de Términos

- **Image**: Template inmutable que contiene aplicación + dependencias
- **Container**: Instancia ejecutable de una imagen
- **Volume**: Almacenamiento persistente fuera del contenedor
- **Network**: Comunicación segura entre contenedores
- **Service**: Definición de cómo ejecutar un contenedor en Swarm
- **Swarm**: Cluster de máquinas Docker trabajando juntas
- **Stack**: Aplicación completa (múltiples servicios)
- **Registry**: Repositorio de imágenes (Docker Hub, etc.)
- **Dockerfile**: Script para construir imágenes
- **docker-compose.yml**: Especificación para orquestar contenedores
