## Contenedor creado a partir de una imagen de ubuntu

Creamos un fichero de docker con la siguiente información: (01_UbuntuWithWget)

Dockerfile:

```dockerfile
FROM ubuntu:latest
RUN  apt-get update \
  && apt-get install -y wget \
  && rm -rf /var/lib/apt/lists/* 
```

Creamos una imagen:

```bash
docker build -t my-ubuntu . 
```

Creamos un contenedor a partir de la imagen my-ubuntu y a accedemos a la shell

```bash
docker run --name UbuntuWithWget -it my-ubuntu
```

Puede salir de la shell con exit.

Para iniciar el contenedor si esta detenido

```bash
docker start UbuntuWithWget

docker restart UbuntuWithWget
```

Para parar el contenedor si esta en ejecución

```bash
docker stop UbuntuWithWget
```

Para ver las imagenes en el Docker Host:

```bash
docker images
```

Para ver los contenedores en el Docker Host:

```
docker container ls -a
```

Accedemos a la shell del contenedor:

```
docker container exec -i -t UbuntuWithWget /bin/sh
```

