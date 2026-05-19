# Swagger Editor Local

## Docker Image

- Descargar la `imagen de contenedor`.

```bash
docker pull docker.swagger.io/swaggerapi/swagger-editor
```

## Docker Container

Iniciar **Swagger Editor** por medio de un `contenedor docker`.

### Primer plano (foregroud o interactivo)

> Ejemplo 1

- Al contenedor se le define:
  - Puerto de ejecución (-p).

- El contenedor se inicia y pasa a un estado "corriendo" (`Up`).

    ```bash
    docker run -p 8080:80 docker.swagger.io/swaggerapi/swagger-editor
    ```

- Para detener (stop) el contenedor se presionan las teclas `ctrl + c`, este pasa a un estatus "salido/detenido" `Exited`.

> Ejemplo 2

- Al contenedor se le define:
  - Nombre del contenedor (--name).
  - Bandera la eliminar el contenedor cuando finaliza (--rm).
  - Puerto de ejecución (-p).

- El contenedor se inicia y pasa a un estado "corriendo" (`Up`).

    ```bash
    docker run --name swaggger --rm -p 8080:80 docker.swagger.io/swaggerapi/swagger-editor
    ```

- Al detener el contenedor (stop), este se "destruye".

### Segundo plano (detached o background)

- Al contenedor se le define:
  - Nombre del contenedor (--name) para identificarlo facilmente.
  - Bandera la eliminar el contenedor cuando finaliza (--rm).
  - Bandera para indicar modo detached (-d).
  - Puerto de ejecución (-p).

- El contenedor se inicia y pasa a un estado "corriendo" (`Up`) pero en segundo plano.

    ```bash
    docker run --name swaggger --rm -d -p 8080:80 docker.swagger.io/swaggerapi/swagger-editor
    ```
- Para eliminar el contenedor se requiere identificarlo y detenerlo.

    ```bash
    docker container ls
    ```

- Una vez identificado, se detiene y en automático se elimina.

    ```bash
    docker container stop swaggger
    ```
