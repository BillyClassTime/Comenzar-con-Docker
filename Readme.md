# Descripción general de Docker

*Tiempo de lectura estimado: 10 minutos*

Docker es una plataforma abierta para desarrollar, enviar y ejecutar aplicaciones. Docker le permite separar sus aplicaciones de su infraestructura para que pueda desplegar software rápidamente. Con Docker, puede administrar su infraestructura de la misma manera que administra sus aplicaciones. Al aprovechar las metodologías de Docker para enviar, probar e implementar código rápidamente, puede reducir significativamente el retraso entre la escritura del código y su ejecución en producción.

## La plataforma Docker 

Docker proporciona la capacidad de empaquetar y ejecutar una aplicación en un entorno aislado llamado contenedor. El aislamiento y la seguridad le permiten ejecutar muchos contenedores simultáneamente en un host determinado. Los contenedores son livianos porque no necesitan la carga adicional de un hipervisor, sino que se ejecutan directamente dentro del kernel de la máquina host. Esto significa que puede ejecutar más contenedores en una combinación de hardware determinada que si estuviera utilizando máquinas virtuales. ¡Incluso puede ejecutar contenedores Docker dentro de máquinas host que en realidad son máquinas virtuales!

Docker proporciona herramientas y una plataforma para administrar el ciclo de vida de sus contenedores:

- Desarrolle su aplicación y sus componentes de soporte utilizando contenedores.
- El contenedor se convierte en la unidad para distribuir y probar su aplicación.
- Cuando esté listo, implemente su aplicación en su entorno de producción, como un contenedor o un servicio orquestado. Esto funciona igual si su entorno de producción es un centro de datos local, un proveedor de nube o un híbrido de los dos.

## Motor Docker 

*Docker Engine* es una aplicación cliente-servidor con estos componentes principales:

- Un servidor que es un tipo de programa de larga ejecución llamado proceso demonio (el `dockerd`comando).
- Una API REST que especifica interfaces que los programas pueden usar para hablar con el demonio e indicarle qué hacer.
- Un cliente de interfaz de línea de comandos (CLI) (el `docker`comando).

![](img/engine-components-flow.png)

La CLI utiliza la API REST de Docker para controlar o interactuar con el demonio de Docker a través de secuencias de comandos o comandos directos de la CLI. Muchas otras aplicaciones de Docker utilizan la API y la CLI subyacentes.

El daemon crea y administra *objetos* Docker , como imágenes, contenedores, redes y volúmenes.

> **Nota** : Docker tiene la licencia de código abierto Apache 2.0.

Para obtener más detalles, consulte **Arquitectura de Docker** mas adelante en este documento.

## ¿Para qué puedo usar Docker? 

**Despliegue rápido y consistente de sus aplicaciones**

Docker agiliza el ciclo de vida del desarrollo al permitir que los desarrolladores trabajen en entornos estandarizados utilizando contenedores locales que brindan sus aplicaciones y servicios. Los contenedores son excelentes para la integración continua y los flujos de trabajo de entrega continua (CI / CD).

Considere el siguiente escenario de ejemplo:

- Sus desarrolladores escriben código localmente y comparten su trabajo con sus colegas usando contenedores Docker.
- Usan Docker para desplegar sus aplicaciones a un entorno de prueba y ejecutar pruebas automáticas y manuales.
- Cuando los desarrolladores encuentran errores, pueden corregirlos en el entorno de desarrollo y volver a implementarlos en el entorno de prueba para realizar pruebas y validaciones.
- Una vez finalizada la prueba, hacer llegar la solución al cliente es tan simple como enviar la imagen actualizada al entorno de producción.

**Implementación receptiva y escalado**

La plataforma basada en contenedores de Docker permite cargas de trabajo altamente portátiles. Los contenedores Docker pueden ejecutarse en la computadora portátil local de un desarrollador, en máquinas físicas o virtuales en un centro de datos, en proveedores de nube o en una combinación de entornos.

La portabilidad y la ligereza de Docker también facilitan la administración dinámica de cargas de trabajo, ampliando o eliminando aplicaciones y servicios según lo dicten las necesidades comerciales, casi en tiempo real.

**Ejecutar más cargas de trabajo en el mismo hardware**

Docker es ligero y rápido. Proporciona una alternativa viable y rentable a las máquinas virtuales basadas en hipervisores, por lo que puede utilizar una mayor parte de su capacidad informática para lograr sus objetivos comerciales. Docker es perfecto para entornos de alta densidad y para implementaciones pequeñas y medianas donde necesita hacer más con menos recursos.

## Arquitectura de Docker 

Docker utiliza una arquitectura cliente-servidor. El *cliente de* Docker habla con el *demonio de* Docker , que hace el trabajo pesado de compilar, ejecutar y distribuir sus contenedores de Docker. El cliente y el demonio de Docker *pueden* ejecutarse en el mismo sistema, o puede conectar un cliente de Docker a un demonio de Docker remoto. El cliente y el demonio de Docker se comunican mediante una API REST, a través de sockets UNIX o una interfaz de red.

![](img/architecture.svg)

### El demonio de Docker 

El daemon de Docker ( `dockerd`) escucha las solicitudes de la API de Docker y administra objetos de Docker como imágenes, contenedores, redes y volúmenes. Un demonio también puede comunicarse con otros demonios para administrar los servicios de Docker.

### El cliente de Docker 

El cliente de Docker ( `docker`) es la forma principal en que muchos usuarios de Docker interactúan con Docker. Cuando utiliza comandos como `docker run`, el cliente envía estos comandos a `dockerd`, que los ejecuta. El `docker`comando usa la API de Docker. El cliente de Docker puede comunicarse con más de un demonio.

### Registros de Docker 

Un *registro de* Docker almacena imágenes de Docker. Docker Hub es un registro público que cualquiera puede usar y Docker está configurado para buscar imágenes en Docker Hub de forma predeterminada. Incluso puede ejecutar su propio registro privado.

Cuando usa los comandos `docker pull`o `docker run`, las imágenes requeridas se extraen de su registro configurado. Cuando usa el `docker push`comando, su imagen se envía a su registro configurado.

### Objetos Docker 

Cuando usa Docker, está creando y usando imágenes, contenedores, redes, volúmenes, complementos y otros objetos. Esta sección es una breve descripción general de algunos de esos objetos.

#### IMAGENES

Una *imagen* es una plantilla de solo lectura con instrucciones para crear un contenedor Docker. A menudo, una imagen se *basa en* otra imagen, con alguna personalización adicional. Por ejemplo, puede crear una imagen basada en la `ubuntu`imagen, pero instala el servidor web Apache y su aplicación, así como los detalles de configuración necesarios para ejecutar su aplicación.

Puede crear sus propias imágenes o puede usar solo las creadas por otros y publicadas en un registro. Para crear su propia imagen, cree un *Dockerfile* con una sintaxis simple para definir los pasos necesarios para crear la imagen y ejecutarla. Cada instrucción en un Dockerfile crea una capa en la imagen. Cuando cambia el Dockerfile y reconstruye la imagen, solo se reconstruyen las capas que han cambiado. Esto es parte de lo que hace que las imágenes sean tan ligeras, pequeñas y rápidas en comparación con otras tecnologías de virtualización.

#### CONTENEDORES

Un contenedor es una instancia ejecutable de una imagen. Puede crear, iniciar, detener, mover o eliminar un contenedor mediante la API de Docker o la CLI. Puede conectar un contenedor a una o más redes, adjuntarle almacenamiento o incluso crear una nueva imagen basada en su estado actual.

De forma predeterminada, un contenedor está relativamente bien aislado de otros contenedores y de su máquina host. Puede controlar qué tan aislados están la red, el almacenamiento u otros subsistemas subyacentes de un contenedor de otros contenedores o de la máquina host.

Un contenedor se define por su imagen, así como por las opciones de configuración que le proporcione cuando lo crea o lo inicia. Cuando se quita un contenedor, cualquier cambio en su estado que no esté almacenado en un almacenamiento persistente desaparece.

##### `docker run`Comando de ejemplo

El siguiente comando ejecuta un `ubuntu`contenedor, se adjunta de forma interactiva a su sesión de línea de comandos local y se ejecuta `/bin/bash`.

```
$ docker run -i -t ubuntu /bin/bash
```

Cuando ejecuta este comando, sucede lo siguiente (suponiendo que esté utilizando la configuración de registro predeterminada):

1. Si no tiene la `ubuntu`imagen localmente, Docker la extrae de su registro configurado, como si la hubiera ejecutado `docker pull ubuntu`manualmente.
2. Docker crea un nuevo contenedor, como si hubiera ejecutado un `docker container create`comando manualmente.
3. Docker asigna un sistema de archivos de lectura y escritura al contenedor, como su capa final. Esto permite que un contenedor en ejecución cree o modifique archivos y directorios en su sistema de archivos local.
4. Docker crea una interfaz de red para conectar el contenedor a la red predeterminada, ya que no especificó ninguna opción de red. Esto incluye asignar una dirección IP al contenedor. De forma predeterminada, los contenedores pueden conectarse a redes externas mediante la conexión de red de la máquina host.
5. Docker inicia el contenedor y lo ejecuta `/bin/bash`. Debido a que el contenedor se ejecuta de forma interactiva y está adjunto a su terminal (debido a las banderas `-i`y `-t`), puede proporcionar entrada usando su teclado mientras la salida se registra en su terminal.
6. Cuando escribe `exit`para terminar el `/bin/bash`comando, el contenedor se detiene pero no se elimina. Puede iniciarlo de nuevo o eliminarlo.

#### SERVICIOS

Los servicios le permiten escalar contenedores en varios demonios de Docker, que trabajan juntos como un *swarm (enjambre)* con varios *managers* y *workers* . Cada miembro de un swarm es un demonio de Docker y todos los demonios se comunican mediante la API de Docker. Un servicio le permite definir el estado deseado, como la cantidad de réplicas del servicio que deben estar disponibles en un momento dado. De forma predeterminada, el servicio tiene un equilibrio de carga en todos los nodos workers. Para el consumidor, el servicio Docker parece ser una sola aplicación. Docker Engine admite el modo de swarm en Docker 1.12 y versiones posteriores.

## La tecnología subyacente 

Docker está escrito en el [lenguaje de programación Go](https://translate.google.com/website?sl=auto&tl=es&u=https://golang.org/) y aprovecha varias características del kernel de Linux para ofrecer su funcionalidad.

### Espacios de nombres 

Docker usa una tecnología llamada `namespaces`para proporcionar el espacio de trabajo aislado llamado *contenedor* . Cuando ejecuta un contenedor, Docker crea un conjunto de *espacios* de *nombres* para ese contenedor.

Estos espacios de nombres proporcionan una capa de aislamiento. Cada aspecto de un contenedor se ejecuta en un espacio de nombres separado y su acceso está limitado a ese espacio de nombres.

Docker Engine usa espacios de nombres como los siguientes en Linux:

- **El `pid`espacio de nombres:** Aislamiento del proceso (PID: ID del proceso).
- **El `net`espacio de nombres:** Gestión de interfaces de red (NET: Networking).
- **El `ipc`espacio de nombres:** gestión del acceso a los recursos de IPC (IPC: comunicación entre procesos).
- **El `mnt`espacio de nombres:** Gestión de puntos de montaje del sistema de archivos (MNT: Mount).
- **El `uts`espacio de nombres:** aislar identificadores de kernel y versión. (UTS: Sistema de tiempo compartido Unix).

### Grupos de control 

Docker Engine en Linux también se basa en otra tecnología llamada *grupos de control* ( `cgroups`). Un cgroup limita una aplicación a un conjunto específico de recursos. Los grupos de control permiten a Docker Engine compartir los recursos de hardware disponibles con los contenedores y, opcionalmente, hacer cumplir los límites y restricciones. Por ejemplo, puede limitar la memoria disponible a un contenedor específico.

### Sistemas de archivos de unión 

Los sistemas de archivos Union, o UnionFS, son sistemas de archivos que operan creando capas, lo que los hace muy ligeros y rápidos. Docker Engine utiliza UnionFS para proporcionar los componentes básicos de los contenedores. Docker Engine puede usar múltiples variantes de UnionFS, incluidos AUFS, btrfs, vfs y DeviceMapper.

### Formato de contenedor 

Docker Engine combina los espacios de nombres, los grupos de control y UnionFS en un contenedor llamado formato contenedor. El formato de contenedor predeterminado es `libcontainer`. En el futuro, Docker puede admitir otros formatos de contenedor mediante la integración con tecnologías como BSD Jails o Solaris Zones.