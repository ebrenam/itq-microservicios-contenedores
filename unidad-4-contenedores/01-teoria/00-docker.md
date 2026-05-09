# El contenedor de un solo archivo

**Objetivo:** Crear una imagen personalizada con **un solo archivo** de código y **3 líneas** de Dockerfile.

## Paso 1: Crea tu página (index.html)

No necesitamos programar un servidor; usaremos un archivo HTML simple.

```html
<!DOCTYPE html>
<html>
<head><title>Hola Docker</title></head>
<body>
    <h1>Mi primera imagen personalizada</h1>
    <p>Esta página vive dentro de un contenedor.</p>
</body>
</html>
```

## Paso 2: Escribe el Dockerfile

Este es el "minimalismo" puro. Vamos a usar Python solo para que nos sirva el archivo HTML.

```Dockerfile
# 1. Usamos una versión ligera de Python
FROM python:3.10-alpine

# 2. Copiamos nuestro archivo al contenedor
COPY index.html .

# 3. Ejecutamos un servidor web instantáneo en el puerto 8000
CMD ["python", "-m", "http.server", "8000"]
```

### Pao 3: Construcción y ejecución

Solo dos comandos para que los alumnos vean la magia:

1. **Construir:**

    `docker build -t mi-web-simple .`

2. **Correr:**

    `docker run -d -p 8080:8000 mi-web-simple`


> **Explicación:** "Estamos mapeando el puerto **8080** de nuestra computadora al **8000** del contenedor".
