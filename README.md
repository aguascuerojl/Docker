# Docker Cheat Sheet

## Conceptos Básicos

* **Imagen:** Una plantilla de solo lectura con instrucciones para crear un contenedor Docker.
* **Contenedor:** Una instancia ejecutable de una imagen. Es ligero y portable.
* **Volumen:** Un mecanismo para persistir datos generados por un contenedor.
* **Red:** Permite la comunicación entre contenedores y con el mundo exterior.
* **Dockerfile:** Un archivo de texto que contiene las instrucciones para construir una imagen Docker.
* **Docker Compose:** Una herramienta para definir y ejecutar aplicaciones Docker de múltiples contenedores.

## Comandos Principales

### Gestión de Contenedores

* **`docker run [OPTIONS] IMAGE [COMMAND] [ARG...]`**: Crea y ejecuta un nuevo contenedor a partir de una imagen.
    * `-d`: Ejecutar en modo "detached" (segundo plano).
    * `-p HOST_PORT:CONTAINER_PORT`: Mapea un puerto del host a un puerto del contenedor.
    * `-v HOST_PATH:CONTAINER_PATH`: Mapea un volumen del host a un volumen del contenedor.
    * `--name NAME`: Asigna un nombre al contenedor.
    * `--rm`: Elimina automáticamente el contenedor cuando se detiene.
    * `-it`: Asigna un pseudo-TTY y mantiene STDIN abierto (para interactuar con el contenedor).
* **`docker ps [OPTIONS]`**: Lista los contenedores en ejecución.
    * `-a`: Muestra todos los contenedores (incluidos los detenidos).
* **`docker start [CONTAINER]`**: Inicia uno o más contenedores detenidos.
* **`docker stop [CONTAINER]`**: Detiene uno o más contenedores en ejecución.
* **`docker restart [CONTAINER]`**: Reinicia uno o más contenedores.
* **`docker rm [OPTIONS] CONTAINER [CONTAINER...]`**: Elimina uno o más contenedores.
    * `-f`: Fuerza la eliminación de un contenedor en ejecución.
* **`docker exec [OPTIONS] CONTAINER COMMAND [ARG...]`**: Ejecuta un comando dentro de un contenedor en ejecución.
    * `-it`: Para interactuar con el comando (ej: `docker exec -it my_container bash`).
* **`docker logs [OPTIONS] CONTAINER`**: Muestra los logs de un contenedor.
    * `-f`: Sigue los logs en tiempo real.

### Gestión de Imágenes

* **`docker build [OPTIONS] PATH | URL`**: Construye una imagen Docker a partir de un Dockerfile.
    * `-t NAME[:TAG]`: Asigna un nombre y opcionalmente una etiqueta a la imagen.
    * `.`: Indica que el Dockerfile se encuentra en el directorio actual.
* **`docker images [OPTIONS]`**: Lista las imágenes Docker disponibles.
* **`docker pull NAME[:TAG]`**: Descarga una imagen de un registro (ej: Docker Hub).
* **`docker push NAME[:TAG]`**: Sube una imagen a un registro.
* **`docker rmi [OPTIONS] IMAGE [IMAGE...]`**: Elimina una o más imágenes.
    * `-f`: Fuerza la eliminación de una imagen.
* **`docker history IMAGE`**: Muestra el historial de capas de una imagen.

### Gestión de Volúmenes

* **`docker volume create [OPTIONS] VOLUME`**: Crea un volumen.
* **`docker volume ls [OPTIONS]`**: Lista los volúmenes.
* **`docker volume inspect VOLUME`**: Muestra información detallada de un volumen.
* **`docker volume rm [VOLUME...]`**: Elimina uno o más volúmenes.

### Gestión de Redes

* **`docker network create [OPTIONS] NETWORK`**: Crea una red.
* **`docker network ls [OPTIONS]`**: Lista las redes.
* **`docker network inspect NETWORK`**: Muestra información detallada de una red.
* **`docker network rm [NETWORK...]`**: Elimina una o más redes.
* **`docker network connect NETWORK CONTAINER`**: Conecta un contenedor a una red.
* **`docker network disconnect NETWORK CONTAINER`**: Desconecta un contenedor de una red.

### Información y Limpieza

* **`docker info`**: Muestra información del sistema Docker.
* **`docker version`**: Muestra la versión de Docker.
* **`docker system prune [OPTIONS]`**: Elimina datos no utilizados (contenedores detenidos, imágenes sin usar, volúmenes sin uso, etc.).
    * `-a`: Elimina todos los objetos no utilizados (incluyendo imágenes sin usar).
    * `--volumes`: También elimina los volúmenes no utilizados.

## Dockerfile Básico

```dockerfile
# Usa una imagen base
FROM ubuntu:latest

# Establece el directorio de trabajo dentro del contenedor
WORKDIR /app

# Copia los archivos de la aplicación al contenedor
COPY . /app

# Instala dependencias
RUN apt-get update && apt-get install -y nginx

# Expone el puerto que la aplicación escucha
EXPOSE 80

# Comando para ejecutar cuando el contenedor se inicie
CMD ["nginx", "-g", "daemon off;"]
