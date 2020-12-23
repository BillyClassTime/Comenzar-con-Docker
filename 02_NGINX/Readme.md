# Crear un contenedor con una imagen de NGINX

Creación de un contendor con NGINX

```
docker run -d --name nginx -p 8082:80 nginx:alpine
```

Navegar a este contenedor desde un browser http://localhost:8082

![image-20201223114413536](../img/image-20201223114413536.png)

Conectate al servidor nginx con el commando:

	docker container exec -i -t nginx /bin/sh
Cambia la página web de inicio: 

``` 
cd /usr/share/nginx/html 
editar index.html
```

![](../img/editingindexfile.png)

Abrir los puertos en el router:

![](../img/openports.png)

Deshabilitar el firewall mientras la prueba para comprobar que sale a internet

![image-20201223115604477](../img/image-20201223115604477.png)

Navegar a la ip publica con el puerto 8082

![](../img/image-20201223114413578.png)

Habilite el firewall nuevamente (También puede crear una regla de inbound para este puerto si desea mantener la conexión)

![](../img/image-20201223115604578.png)