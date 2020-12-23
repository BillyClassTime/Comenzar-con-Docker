# Creando un contenedor desde BusyBox

Creamos un fichero Dockerfile:

```dockerfile
FROM busybox:latest
CMD ["echo", "Welcome to Docker"]
```

Creamos la imagen:

```dockerfile
docker build -t mytest:latest .
```

Creamos el contenedor desde la imagen:

```
docker run -t mytest:latest 
```

