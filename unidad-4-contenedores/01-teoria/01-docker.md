# 🐳 Docker: Desde Cero hasta Producción

- [🐳 Docker: Desde Cero hasta Producción](#-docker-desde-cero-hasta-producción)
- [1. "Mi primer contenedor"](#1-mi-primer-contenedor)
  - [Objetivo: Ver en acción un contenedor y la magia detrás de ello](#objetivo-ver-en-acción-un-contenedor-y-la-magia-detrás-de-ello)
    - [🎯 ¿Qué aprenderemos?](#-qué-aprenderemos)
    - [🚀 Desafío inicial](#-desafío-inicial)
    - [💡 Primer concepto](#-primer-concepto)
    - [✅ Comparación: Virtual Machine vs Container](#-comparación-virtual-machine-vs-container)
    - [📺 Caso de estudio: Netflix y la abstracción de infraestructura con Titus](#-caso-de-estudio-netflix-y-la-abstracción-de-infraestructura-con-titus)
    - [✅ Checkpoint](#-checkpoint)
    - [🎓 Teoría consolidada: Contenedores y aislamiento](#-teoría-consolidada-contenedores-y-aislamiento)
- [2. "Imágenes vs Contenedores"](#2-imágenes-vs-contenedores)
  - [Objetivo: Entender la diferencia fundamental](#objetivo-entender-la-diferencia-fundamental)
    - [🎮 Analogía: El videojuego (Cartucho vs. Partida)](#-analogía-el-videojuego-cartucho-vs-partida)
    - [💡 Comparativa rápida](#-comparativa-rápida)
    - [🔧 Experimento práctico](#-experimento-práctico)
    - [💾 Las capas (simplificado)](#-las-capas-simplificado)
    - [✅ Checkpoint](#-checkpoint-1)
    - [🎓 Teoría consolidada: Imágenes, capas y templates](#-teoría-consolidada-imágenes-capas-y-templates)
- [3. "Crea tu propia aplicación en Docker"](#3-crea-tu-propia-aplicación-en-docker)
  - [Objetivo: Escribir un Dockerfile y entender cómo se construyen imágenes](#objetivo-escribir-un-dockerfile-y-entender-cómo-se-construyen-imágenes)
    - [🎯 Proyecto: Tu primer microservicio](#-proyecto-tu-primer-microservicio)
    - [💡 Conceptos introducidos (en contexto real)](#-conceptos-introducidos-en-contexto-real)
    - [🎓 Lectura comprensiva: ¿Por qué esto es revolucionario?](#-lectura-comprensiva-por-qué-esto-es-revolucionario)
    - [✅ Checkpoint 3: Experimenta por ti mismo](#-checkpoint-3-experimenta-por-ti-mismo)
    - [🎓 Teoría Consolidada: Dockerfile y Construcción de Imágenes](#-teoría-consolidada-dockerfile-y-construcción-de-imágenes)
- [4. "Múltiples contenedores que hablan entre sí"](#4-múltiples-contenedores-que-hablan-entre-sí)
  - [Objetivo: Entender redes y cómo los servicios se comunican](#objetivo-entender-redes-y-cómo-los-servicios-se-comunican)
    - [🎯 Problema real: Tu app necesita una base de datos](#-problema-real-tu-app-necesita-una-base-de-datos)
    - [💡 La magia de DNS dentro de Docker](#-la-magia-de-dns-dentro-de-docker)
    - [🎓 Los 4 tipos de redes (explicación simple)](#-los-4-tipos-de-redes-explicación-simple)
    - [✅ Checkpoint 4: Experimenta](#-checkpoint-4-experimenta)
    - [🎓 Teoría Consolidada: Redes y DNS](#-teoría-consolidada-redes-y-dns)
- [5. "Automatiza TODO con Docker Compose"](#5-automatiza-todo-con-docker-compose)
  - [Objetivo: Una sola herramienta para orquestar múltiples contenedores](#objetivo-una-sola-herramienta-para-orquestar-múltiples-contenedores)
    - [🎯 El problema de escribir comandos largos](#-el-problema-de-escribir-comandos-largos)
    - [✨ La solución: `docker-compose.yml`](#-la-solución-docker-composeyml)
    - [🎯 Ahora TODO es simple:](#-ahora-todo-es-simple)
    - [💡 Estructura de docker-compose.yml explicada](#-estructura-de-docker-composeyml-explicada)
    - [🎓 Caso de uso real: Stack MERN (MongoDB + Express + React + Node)](#-caso-de-uso-real-stack-mern-mongodb--express--react--node)
    - [✅ Checkpoint 5: Tu turno](#-checkpoint-5-tu-turno)
    - [🎓 Teoría Consolidada: Orquestación con Compose](#-teoría-consolidada-orquestación-con-compose)

# 1. "Mi primer contenedor"

## Objetivo: Ver en acción un contenedor y la magia detrás de ello

### 🎯 ¿Qué aprenderemos?

- Ejecutar el primer contenedor
- Ver los beneficios inmediatos
- Entender por qué Docker existe

### 🚀 Desafío inicial

```bash
# Paso 1: Ejecuta esto en tu terminal
docker run --rm -it ubuntu bash

# Ahora estás DENTRO de un contenedor Linux nuevo y limpio
# Escribe algunos comandos
ls -la
whoami
pwd

# Escribe "exit" para salir
exit

# ¡El contenedor desapareció! ✨
```

- Acabas de crear un entorno Linux limpio en 2 segundos
- Ejecutaste comandos como si fuera tu máquina
- Cuando saliste, no dejaste rastro alguno
- **Tu máquina host está intacta**

### 💡 Primer concepto

**Docker es como máquinas virtuales EXPRESS:**

![vm-container](images/docker-containers-vs-vm.png)

**A más detalle**

![vm-container](images/docker-containers-vs-vm-details.png)

> Las máquinas virtuales emulan hardware completo y ejecutan un kernel independiente, lo que requiere más recursos y tiempo de arranque. Docker, en cambio, comparte el kernel Linux del host pero aísla procesos usando **namespaces** (PID, network, filesystem). 
> 
> El resultado: toda la velocidad de un proceso nativo con la seguridad de estar completamente aislado. Es como tener varias aplicaciones en la misma casa pero en habitaciones completamente separadas con cerraduras.

### ✅ Comparación: Virtual Machine vs Container

| Aspecto | VM Tradicional | Docker Container |
|---------|---|---|
| **Tiempo arranque** | ⏰ 2-5 minutos | ⚡ Milisegundos |
| **Peso** | 📦 10-20 GB | 🪶 50-500 MB |
| **Cantidad por servidor** | 🖥️ ~10 máquinas | 🌊 Cientos |
| **Aislamiento** | 🔒 Total (2 kernels) | 🔐 Suficiente (1 kernel compartido) |
| **Consumo RAM** | ❌ Cada VM = 512MB-2GB mínimo | ✅ Cada container = 10-50MB |
| **Densidad de apps** | ❌ Baja (~10 apps) | ✅ Alta (~1000 apps) |

### 📺 Caso de estudio: Netflix y la abstracción de infraestructura con Titus

Netflix transformó su operación al evolucionar de un modelo basado puramente en **Máquinas Virtuales (AWS EC2)** hacia una arquitectura de **contenedores Docker** gestionada por su propia plataforma, **Titus**. En este ecosistema, las VMs actúan como la base sólida de cómputo, mientras que Docker permite que más de **700 equipos** desplieguen microservicios de forma independiente y masiva.

**Realidad técnica y resultados:**

- **Capas de abstracción:** Las aplicaciones ya no se empaquetan como imágenes de VM (AMIs), sino como contenedores. Esto permite que el software sea agnóstico al hardware emulado, facilitando la portabilidad y la consistencia entre entornos.
    
- **Velocidad de iteración:** El tiempo de despliegue se redujo de **decenas de minutos** (tiempo de arranque de una VM completa) a **pocos segundos**, acelerando drásticamente el ciclo de vida del desarrollo.
    
- **Densidad y eficiencia:** Gracias al _bin-packing_, Netflix ejecuta múltiples contenedores aislados dentro de una misma VM de gran tamaño, optimizando el uso de CPU y memoria hasta en un **60%** en comparación con el uso de una VM por servicio.
    
- **Resiliencia a escala:** La combinación de Docker y Titus permite soportar **billones de horas de streaming** mensuales, manteniendo una disponibilidad superior al **99.9%** mediante la recuperación inmediata de contenedores ante fallos.

**Nota:**

Es fundamental notar que **Netflix no eliminó las VMs**. En su lugar, las desplazó hacia la capa de infraestructura. El desarrollador interactúa con el contenedor (agilidad), mientras que el equipo de plataforma gestiona las VMs (estabilidad). Esta "separación de preocupaciones" es la que permite escalar a nivel global.

### ✅ Checkpoint

**Pregunta:** 
¿Qué diferencia ves entre estos dos comandos?

```bash
docker run ubuntu echo "Hola Mundo"   # ¿Qué pasa después?
docker run -it ubuntu bash            # ¿Y aquí?
```

**Respuesta:**
En la primera instrucción se crea un container, ejecuta el comando y termina.
En la segundo se crea un container y se da acceso interactivo a bash.

### 🎓 Teoría consolidada: Contenedores y aislamiento

![vm-container](./images/docker-container.png)

**Definición formal:**
> Un **contenedor Docker** es una unidad de software ligera, autosuficiente y aislada que incluye todo lo necesario para ejecutar una aplicación: código, runtime, dependencias del sistema y variables de entorno. Los contenedores garantizan que "si funciona en mi máquina, funcionará en cualquier lugar".

**¿Qué vimos en la práctica?**
Creaste un ambiente Linux limpio en segundos, ejecutaste comandos y desaparecieron sin dejar rastro. Esto es **aislamiento en acción**.

**La teoría detrás:**
Docker usa **namespaces** del kernel Linux para aislar procesos:

| Namespace | Qué aísla | Ejemplo |
|-----------|-----------|----------|
| **PID** | IDs de procesos | Cada container cree ser el proceso #1 |
| **Network** | Interfaces de red | Cada container tiene su IP virtual |
| **Filesystem** | Sistema de archivos | Cada container ve su propio `/` |
| **IPC** | Comunicación entre procesos | Cada container aislado de otros |
| **User** | UIDs/GIDs | Container puede creer que es root |
| **Cgroup** | Límites de recursos | CPU y memoria limitados por container |

Cuando ejecutas `docker run`, Docker:
1. Crea nuevos namespaces para el contenedor
2. El contenedor "cree" que es la única cosa ejecutándose
3. El kernel Linux gestiona la ilusión compartiendo recursos reales

**Diferencia conceptual:**

| Aspecto | VM | Container |
|--------|-----|----------|
| **Emulación** | ❌ Emula hardware completo | ✅ Comparte kernel Linux |
| **Kernels** | ❌ Linux + Windows = 2 kernels | ✅ 100 contenedores = 1 kernel |
| **Densidad** | ❌ ~10 VMs por servidor | ✅ ~1000 containers por servidor |

**¿Por qué importa?**

- ✅ Contenedores = Arranque en **milisegundos** vs ⏰ VMs = minutos
- ✅ Contenedores = **50-500 MB** vs 📦 VMs = 10+ GB
- ✅ Permite arquitecturas de **microservicios a escala**

---

# 2. "Imágenes vs Contenedores"

## Objetivo: Entender la diferencia fundamental

### 🎮 Analogía: El videojuego (Cartucho vs. Partida)

Imagina que tienes un juego clásico de **Super Mario**:

![image-container](./images/docker-image-vs-container.png)

> **🔍 Explicación del diagrama:**
>
> - **La Imagen (El cartucho):** Es el archivo que contiene todo lo necesario para que el juego funcione. Es **inmutable**: no importa cuánto juegues, no puedes cambiar el código que está grabado dentro del cartucho.
>
> - **El Contenedor (La partida):** Es el juego "en ejecución". Cada jugador tiene su propio progreso, vidas y posición en el mapa. Si el Jugador 3 pierde todas las vidas (el contenedor falla), el cartucho (la imagen) sigue perfecto para empezar una partida nueva desde cero.
>

---

### 💡 Comparativa rápida

| **Característica** | **Imagen (Docker Image)**                  | **Contenedor (Docker Container)**               |
| ------------------ | ------------------------------------------ | ----------------------------------------------- |
| **Estado**         | Estática (en reposo)                       | Dinámica (en ejecución)                         |
| **Mutabilidad**    | **Inmutable** (No cambia)                  | **Mutable** (Escribe datos en su capa temporal) |
| **Componentes**    | Sistema operativo base, librerías, código. | La imagen + procesos de CPU + memoria RAM.      |
| **Analogía**       | El plano de una casa.                      | La casa construida y habitada.                  |

**Diferencia crítica:**
- **Imagen**: Plantilla read-only, inmutable, reutilizable
- **Contenedor**: Instancia en ejecución, mutable, desechable

### 🔧 Experimento práctico

```bash
# Paso 1: Obtén una imagen
docker pull nginx:latest

# Paso 2: Crea dos contenedores de la misma imagen
docker run -d --name web1 nginx
docker run -d --name web2 nginx

# Paso 3: Verifica que ambos existen
docker ps

# Paso 4: Ahora modifica cada uno de los contenedores
docker exec web1 bash -c "echo 'Hola desde web1' > /usr/share/nginx/html/index.html"
docker exec web2 bash -c "echo 'Hola desde web2' > /usr/share/nginx/html/index.html"

# Paso 5: Verifica que son diferentes
docker exec web1 curl localhost
docker exec web2 curl localhost

# Paso 6: Elimina los contenedores
docker stop web1 web2
docker rm web1 web2

# Paso 7: Crea dos nuevos
docker run -d --name web3 nginx
docker run -d --name web4 nginx

# Paso 8: Verifica
docker exec web3 curl localhost  # ¡De nuevo a lo original!
```

**¿Qué aprendiste?**

- La imagen es un **molde inmutable** (Template)
- Los contenedores son **instancias desechables** (Instances)
- Cada contenedor es completamente **independiente**

### 💾 Las capas (simplificado)

![layers](./images/docker-layers.png)

> Una imagen Docker es una **pila de capas read-only**. Cada línea del Dockerfile crea una capa con su propio SHA (hash único). 
>
> Cuando ejecutas `docker run`, Docker agrega una **capa writable** encima. Los cambios en el contenedor ocurren SOLO en esa capa writable; la imagen permanece intacta. Esto permite que 3 contenedores ejecutándose desde la misma imagen compartan las capas base (ahorro de espacio) pero tengan datos independientes (seguridad).

**Ventaja estratégica de las capas:**
- Si solo cambió la Capa 3, Docker descarga SOLO esa capa (no las primeras)
- Múltiples imágenes puede compartir capas base = 60% ahorro de espacio en promedio
- Los cambios en un contenedor NO afectan la imagen (aislamiento perfecto)

### ✅ Checkpoint

**Preguntas:**
1. ¿Si tengo 10 contenedores nginx, tengo 10 copias diferentes de nginx?
2. ¿Si borro un contenedor, la imagen también se borra?
3. ¿Puedo modificar una imagen después de crear contenedores?

**Respuestas:**
1. Falso, todos los contenedores usan la misma imagen.
2. Falso, la imagen permanece si un contenedor se elimina.
3. Falso, las imágenes son inmutables.

### 🎓 Teoría consolidada: Imágenes, capas y templates

**¿Qué vimos en la práctica?**
Tuviste varios contenedores nginx idénticos que no se afectaban entre sí. Las imágenes fueron el "molde" que permitió eso.

**La teoría detrás:**
Una imagen Docker es una **pila de capas read-only**. Cada línea del Dockerfile crea una capa:

```text
Capa 1: Base (ubuntu) - SHA: abc123
Capa 2: Dependencias - SHA: def456
Capa 3: Configuración - SHA: ghi789
```

Cuando creas un contenedor, Docker agrega una capa **writable** encima. Los cambios en el contenedor NO afectan la imagen (son independientes).

**Ventaja de las capas:**

- Docker cachea capas inmutables
- Si cambia solo la capa 3, descarga solo esa (no las anteriores)
- Múltiples imágenes pueden compartir capas base = ahorro de espacio

**Aplicación práctica:**

- Cuando hiciste `docker run nginx` 2 veces, los 2 compartían LA MISMA imagen en disco
- Los cambios en un contenedor NO afectaban a los otros (capas escritura separadas)

---

# 3. "Crea tu propia aplicación en Docker"

## Objetivo: Escribir un Dockerfile y entender cómo se construyen imágenes

### 🎯 Proyecto: Tu primer microservicio

Vamos a crear una aplicación Node.js simple que te muestre por qué Docker es transformador.

**Paso 1: Crea los archivos de tu aplicación**

Archivo: `app.js`
```javascript
const express = require('express');
const app = express();

app.get('/', (req, res) => {
    res.send(`
        <!DOCTYPE html>
        <html>
        <head><title>Mi App en Docker</title></head>
        <body>
            <h1>🎉 ¡Funciona en un container!</h1>
            <p>Hostname: ${require('os').hostname()}</p>
            <p>Timestamp: ${new Date().toISOString()}</p>
        </body>
        </html>
    `);
});

app.listen(3000, () => {
    console.log('✅ Servidor escuchando en puerto 3000');
});
```

Archivo: `package.json`
```json
{
    "name": "mi-app-docker",
    "version": "1.0.0",
    "main": "app.js",
    "scripts": {
        "start": "node app.js"
    },
    "dependencies": {
        "express": "4.18.2"
    }
}
```

**Paso 2: Escribe el Dockerfile (la "receta")**

Archivo: `Dockerfile`
```dockerfile
# Paso 1: Comienza con una imagen base que tenga Node.js instalado
FROM node:18-alpine

# Paso 2: Crea un directorio de trabajo dentro del container
WORKDIR /app

# Paso 3: Copia el archivo package.json
COPY package.json .

# Paso 4: Instala las dependencias
RUN npm install

# Paso 5: Copia el resto del código
COPY app.js .

# Paso 6: Documenta qué puerto usará (solo información)
EXPOSE 3000

# Paso 7: Comando para ejecutar cuando se inicie el container
CMD ["npm", "start"]
```

**Paso 3: Construye tu imagen**

```bash
docker build -t mi-app:1.0 .
```

¿Qué pasó?
- Docker leyó cada línea del Dockerfile
- Ejecutó cada instrucción (capa por capa)
- Creó una imagen final llamada `mi-app:1.0`

**Paso 4: Ejecuta tu contenedor**

```bash
docker run -d -p 3000:3000 --name mi-contenedor mi-app:1.0
```

**¿Qué significa `-p 3000:3000`?**
```
Tu máquina       Container
  :3000    ←→     :3000
 (acceso)        (aplicación)
```

**Paso 5: Abre tu navegador**

```
http://localhost:3000
```

### 💡 Conceptos introducidos (en contexto real)

| Comando | Analogía | Lo que hace |
|---------|----------|-------------|
| `FROM` | "Comenzar con una base sólida" | Selecciona imagen padre |
| `WORKDIR` | "Definir mi área de trabajo" | Crea carpeta en el container |
| `COPY` | "Traer mis cosas" | Copia archivos desde tu PC |
| `RUN` | "Hacer instalaciones" | Ejecuta comandos durante construcción |
| `EXPOSE` | "Publicar qué puerto uso" | Documentación (no abre puertos) |
| `CMD` | "Qué hacer al iniciar" | Comando por defecto |

### 🎓 Lectura comprensiva: ¿Por qué esto es revolucionario?

**El problema tradicional sin Docker:**

![without-docker](./images/docker-traditional-problem.png)

> **🔍 Problema identificado:**  
> Sin Docker, cada ambiente (desarrollo, QA, producción) tiene configuraciones diferentes. El código que funciona en tu Mac no funciona en Windows porque faltan dependencias, hay conflictos de versiones, o diferencias en el sistema operativo. Resultado: "¡Funciona en mi máquina pero no en el cliente!" es el meme más viejo de la ingeniería de software.

**Con Docker: La solución**

![witt-docker](./images/docker-solution.png)

> **🔍 Solución con Docker:**  
> Un único Dockerfile especifica EXACTAMENTE qué versiones de qué dependencias se necesitan. Ese Dockerfile genera una imagen Docker que es **idéntica en Mac, Windows, Linux y servidores de producción**. No hay "funciona en mi máquina": o funciona en la imagen (y funciona en todas partes) o no funciona en ningún lado.

**Impacto real:**
- ✅ Eliminación del 80% de "problemas de ambiente"
- ✅ Onboarding de nuevos desarrolladores en **minutos** en lugar de días
- ✅ Reducción de bugs relacionados con dependencias
- ✅ Certificación: Si pasó tests en Docker, pasará en producción

### ✅ Checkpoint 3: Experimenta por ti mismo

**Desafío:** Modifica tu app
1. Edita `app.js`: Cambia el mensaje "¡Funciona en un container!"
2. Reconstruye: `docker build -t mi-app:2.0 .`
3. Ejecuta: `docker run -d -p 3001:3000 mi-app:2.0`
4. Verifica: http://localhost:3001

**Pregunta:** ¿Por qué creaste la versión 2.0 en lugar de sobrescribir 1.0?
**Respuesta esperada:** Para poder volver a la versión anterior si algo falla (rollback)

### 🎓 Teoría Consolidada: Dockerfile y Construcción de Imágenes

**¿Qué vimos en la práctica?**
Escribiste instrucciones en un archivo (Dockerfile) y Docker las ejecutó automáticamente, creando una imagen reproducible.

**La teoría detrás:**
El Dockerfile es un **DSL (lenguaje específico de dominio)** que automatiza la creación de imágenes. Cada línea es una instrucción:

| Instrucción | Nivel | Propósito |
|-------------|-------|----------|
| `FROM` | Base | Define imagen padre |
| `RUN` | Build | Ejecuta comandos (instala herramientas) |
| `COPY` | Build | Copia archivos desde host |
| `ENV` | Config | Variables de entorno |
| `EXPOSE` | Meta | Documenta puertos (NO abre) |
| `CMD` | Runtime | Comando por defecto |
| `ENTRYPOINT` | Runtime | Ejecutable principal |

**Orden de ejecución:**

1. **Build time** (docker build): FROM, RUN, COPY, ENV (crea capas)
2. **Runtime** (docker run): CMD, ENTRYPOINT (qué hacer al iniciar)

**¿Por qué importa?**

- Reproducibilidad: El mismo Dockerfile = la misma imagen siempre
- Automatización: No más "instala esto manualmente"
- Versionado: Cada versión del código = versión diferente de imagen

**Aplicación práctica:**
Tu `docker build -t mi-app:2.0 .` no reescribió la 1.0 porque Docker guarda capas por SHA. Si cambia contenido, SHA diferente = imagen diferente.

---

# 4. "Múltiples contenedores que hablan entre sí"

## Objetivo: Entender redes y cómo los servicios se comunican

### 🎯 Problema real: Tu app necesita una base de datos

**Escenario:** Tienes una app web que necesita guardar datos. ¿Cómo hacerlo con Docker?

**Solución "mala" (la que novatos hacen):**
```bash
docker run -d -p 3000:3000 mi-app   # App en puerto 3000
docker run -d -p 5432:5432 postgres # DB en puerto 5432
```

**Problema:** 

- Los contenedores no se "encuentran" entre sí automáticamente
- Tienes que resolver IPs manualmente
- Es frágil y no escala

**Solución "buena" (la profesional):**

**Paso 1: Crea una red personalizada**

```bash
docker network create mi-app-network
```

**¿Por qué?** Los contenedores en la misma red se ven por nombre.

**Paso 2: Ejecuta ambos contenedores EN LA MISMA RED**

```bash
# Base de datos
docker run -d \
  --name postgres-db \
  --network mi-app-network \
  -e POSTGRES_PASSWORD=secreto \
  postgres:15

# Aplicación
docker run -d \
  --name mi-app \
  --network mi-app-network \
  -p 3000:3000 \
  -e DATABASE_URL=postgresql://postgres:secreto@postgres-db:5432/midb \
  mi-app:1.0
```

### 💡 La magia de DNS dentro de Docker

```text
Tu app ejecuta: curl postgres-db
                      ↓
Docker automáticamente lo traduce a:
curl 172.18.0.2  ← IP del contenedor postgres
                      ↓
                   ¡Conexión establecida!
```

**Sin Docker**, tendrías que:
1. Obtener la IP del contenedor: `docker inspect postgres-db`
2. Codificar hardcoded en tu app
3. Si la IP cambia, tu app se rompe

**Con Docker**, simplemente usas el nombre y funciona. ✨

### 🎓 Los 4 tipos de redes (explicación simple)

```text
Tu vecindario tiene 4 tipos de casas:

1️⃣ bridge (default)
   - Vecinos NO tienen directorio telefónico
   - Se llaman por IP nada más
   - Uso: Contenedores aislados

2️⃣ custom bridge (RECOMENDADO)
   - ✅ Vecinos TIENEN directorio (DNS automático)
   - ✅ Se llaman por nombre
   - Uso: Aplicaciones multi-contenedor (Docker Compose)

3️⃣ host
   - Todos comparten la misma dirección de la casa
   - ⚠️ Sin aislamiento, máxima velocidad
   - Uso: Casos especiales (monitoring)

4️⃣ none
   - Casa completamente aislada, sin teléfono
   - Uso: Trabajos batch que no necesitan red
```

### ✅ Checkpoint 4: Experimenta

**Desafío práctico:**
1. Crea una red: `docker network create test-net`
2. Corre dos contenedores en esa red
3. Desde uno, haz ping al otro por nombre

```bash
# Contenedor 1
docker run -it --name server1 --network test-net ubuntu bash
# Dentro ejecuta: apt-get update && apt-get install -y iputils-ping
#                ping server2

# Contenedor 2 (en otra terminal)
docker run -d --name server2 --network test-net nginx

# El ping debería funcionar ✅
```

### 🎓 Teoría Consolidada: Redes y DNS

**¿Qué vimos en la práctica?**
Dos contenedores en la misma red se encontraron automáticamente por nombre, sin necesidad de IPs.

**La teoría detrás:**
Docker maneja **dos capas de red**:

1. **Bridge Network (default)**: Basada en Linux bridge
   - Contenedores en bridge diferente NO se ven (aisladas)
   - Contenedores en el mismo bridge se ven por IP (sin DNS)
   - Puerto 3000 en el host mapea al puerto 3000 del contenedor

2. **User-Defined Network (custom)**: Incluye DNS interno
   - Contenedores se resuelven por NOMBRE (DNS)
   - Mejor aislamiento y control
   - RECOMENDADO para producción

**Cómo funciona internamente:**

```text
Cuando haces: docker run --network mi-red --name web1 app
          ↓
Docker crea una entrada DNS: web1 → 172.18.0.2
          ↓
Otro contenedor hace: curl web1
          ↓
El DNS interno resuelve: web1 → 172.18.0.2
          ↓
¡Conexión establecida!
```

**¿Por qué importa?**
- Sin DNS: Tienes que codificar IPs (frágil, cambia al reiniciar)
- Con DNS: Usas nombres (robusto, predecible)

---

# 5. "Automatiza TODO con Docker Compose"

## Objetivo: Una sola herramienta para orquestar múltiples contenedores

### 🎯 El problema de escribir comandos largos

```bash
# ¡Imagínate escribir ESTO cada vez que quieres levantar tu app!

docker network create myapp-network

docker run -d \
  --name postgres \
  --network myapp-network \
  -e POSTGRES_PASSWORD=secret123 \
  -v pgdata:/var/lib/postgresql/data \
  postgres:15

docker run -d \
  --name redis-cache \
  --network myapp-network \
  redis:7

docker run -d \
  --name web-app \
  --network myapp-network \
  -p 3000:3000 \
  -e DB_HOST=postgres \
  -e REDIS_HOST=redis-cache \
  mi-app:1.0

# Y para bajarlo todo:
docker stop postgres redis-cache web-app
docker rm postgres redis-cache web-app
docker network rm myapp-network
```

😱 **¡Hay que recordar demasiado!**

### ✨ La solución: `docker-compose.yml`

Crea un archivo `docker-compose.yml`:

```yaml
version: '3.9'

services:
  # Servicio 1: Base de datos
  postgres:
    image: postgres:15
    environment:
      POSTGRES_PASSWORD: secret123
    volumes:
      - pgdata:/var/lib/postgresql/data
    networks:
      - app-network

  # Servicio 2: Cache
  redis:
    image: redis:7
    networks:
      - app-network

  # Servicio 3: Aplicación web
  web:
    image: mi-app:1.0
    ports:
      - "3000:3000"
    environment:
      DB_HOST: postgres
      DB_PASSWORD: secret123
      REDIS_HOST: redis
    depends_on:
      - postgres
      - redis
    networks:
      - app-network

volumes:
  pgdata:

networks:
  app-network:
```

### 🎯 Ahora TODO es simple:

```bash
# LEVANTAR todo con 1 comando
docker-compose up -d

# VER logs de todo
docker-compose logs -f

# PARAR todo limpiamente
docker-compose down
```

**¿Qué pasó mágicamente?**
- ✅ Se creó la red automáticamente
- ✅ Se ejecutaron los 3 servicios en orden correcto
- ✅ Se conectan por nombre automáticamente
- ✅ Los volúmenes se gestionan automáticamente

### 💡 Estructura de docker-compose.yml explicada

```yaml
version: '3.9'  # Versión del formato (ignora, solo ponlo)

services:      # Aquí listaremos todos los contenedores
  servicio1:
    image: ...        # Qué imagen usar
    ports: [...]      # Qué puertos exponer (máquina:contenedor)
    environment: ...  # Variables de entorno
    volumes: [...]    # Almacenamiento persistente
    depends_on: ...   # Esperar a que otros servicios arranquen primero
    networks: [...]   # Qué redes usar

  servicio2:
    ...

volumes:        # Define volúmenes nombrados
  mi-volumen:

networks:       # Define redes personalizadas
  mi-red:
```

### 🎓 Caso de uso real: Stack MERN (MongoDB + Express + React + Node)

```yaml
version: '3.9'

services:
  mongodb:
    image: mongo:6.0
    environment:
      MONGO_INITDB_ROOT_USERNAME: admin
      MONGO_INITDB_ROOT_PASSWORD: password
    volumes:
      - mongodb_data:/data/db
    networks:
      - mern-network

  backend:
    image: mi-backend:1.0
    ports:
      - "5000:5000"
    environment:
      MONGODB_URI: mongodb://admin:password@mongodb:27017/mydb
    depends_on:
      - mongodb
    networks:
      - mern-network

  frontend:
    image: mi-frontend:1.0
    ports:
      - "3000:3000"
    depends_on:
      - backend
    networks:
      - mern-network

volumes:
  mongodb_data:

networks:
  mern-network:
```

¡Una aplicación MERN completa lista con 1 comando! 🚀

### ✅ Checkpoint 5: Tu turno

**Desafío:** Crea un docker-compose.yml con:
- Una app nginx (imagen oficial)
- Una base de datos postgres
- Ambas en la misma red

```bash
# Levanta
docker-compose up -d

# Verifica
docker-compose ps

# Baja
docker-compose down
```

### 🎓 Teoría Consolidada: Orquestación con Compose

**¿Qué vimos en la práctica?**
Un archivo YAML describió múltiples servicios, y con `docker-compose up` todo se levantó coordinado automáticamente.

**La teoría detrás:**
Docker Compose es una **herramienta de orquestación local** que:

1. **Parsea un YAML**: Define servicios, redes, volúmenes
2. **Crea una red**: Todos los servicios en la misma red automáticamente
3. **Levanta servicios en orden**: Respeta `depends_on`
4. **Expone puertos**: Mapea host:container
5. **Gestiona ciclo de vida**: `up`, `down`, `restart`

**Estructura conceptual:**

```text
 docker-compose.yml (Declarativo)
        ↓
 Compose Parser
        ↓
 1. Crea red
 2. Crea volúmenes
 3. Lanza servicios en orden
 4. Conecta automáticamente
```

**¿Por qué importa?**
- **Reproducibilidad**: El mismo YAML = idéntico comportamiento
- **Documentación viva**: El archivo es tu documentación
- **Desarrollo ≈ Producción**: Misma estructura en ambos (aunque escala diferente)

**Limitación importante:**
Compose es para **UNA máquina**. Para múltiples máquinas → Docker Swarm o Kubernetes.
