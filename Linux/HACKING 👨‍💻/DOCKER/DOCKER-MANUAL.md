------
- Tags: #Linux #Docker 
------
Docker es una herramienta que nos permite virtualizar un entorno de manera rápida y eficiente. A diferencia de una máquina virtual docker virtualiza solo partes necesarias para generar un contenedor. Esto permite ahorrar recursos y mejorar el rendimiento. Lo hace perfecto para desarrollar programas y aplicaciones en distintos entornos, garantiza que los programas se ejecutarán de manera correcta en cualquier máquina ya que todas las dependecias y demás han sido contempladas en el propio contenedor.

## Comandos

### Listar imágenes y contenedores

Ver contenedores activos
```
docker ps 
```

Ver todos los contenedores existentes, tanto activos como inactivos.
```bash
docker ps -a 
```

Ver las imágenes
```bash
docker images
```

Ver imágenes corruptas con nombre \<none>
```bash
docker images --filter='dangling=true'
```

Ver los identificadores de los contenedores o las imágenes
```bash
docker ps -q
docker ps -a -q
docker images -q
```


## Contenedores
### Crear un contenedor
Un contenedor necesita apuntar a una imagen, la imagen es el sistema operativo que quieres virtualizar. 
Descargarse una imagen 
```bash
docker pull ubuntu
docke pull debian
```

Crear el contenedor
```bash
docker run -dit --name Micontenedor ubuntu
```

- -dit> es una combinación de parámetros que indican los siguiente:
	1. d: sirve para dejar el proceso en segundo plano (deamon)
	2. it: sirve para indicar que quieres que el contenedor sea interactivo para que podamos luego acceder al mismo desde una terminal
- --name> indicar el nombre que quieres ponerle al contenedor
- ubuntu> es el nombre de la imagen que he descargado, para crear un contenedor se necesita especificar una imagen al final del comando.

### Acceder desde una bash al contenedor
```bash
docker exec -it Micontenedor bash
```
Con docker exec podemos indicarle al contenedor que comando queremos que nos ejecute, en este caso le estamos indicando que nos proporcione una bash.

> También podemos ejecutar un contenedor directamente otorgándonos una bash
```bash
docker run -it --name contenedor ubuntu /bin/bash
```

Hay que tener en cuenta que si queremos ejecutar una bash nada más lanzar el contenedor tenemos que poner -it para que no lance el contenedor en segundo plano, sino que nos otorgue una bash interactiva al momento.

### Crear un contenedor temporal
```bash
docker run -it --rm --name contenedor ubuntu /bin/bash
```

--rm: este parámetro sirve para que cuando nos salgamos del contenedor este se borre automáticamente.


### CREAR UN CONTENEDOR PRIVILEGIADO 
```bash
docker run -dit --privileged --network=host --name contenedor ubuntu
```

--privileged: permite ejecutar un contenedor con privilegios extendidos, otorgándole acceso completo y sin restricciones a todos los dispositivos y recursos del sistema host. Al utilizar esta opción, se eliminan muchas de las restricciones de seguridad y aislamiento típicas de Docker.
--network=host: permite asignar las mismas interfaces con las mismas ips de la máquina host al contenedor 


### Borrar contenedores
Para borrar un contenedor podemos hacerlo proporcionando el nombre del mismo o con su identificador
```bash
docker rm Micontenedor
docker rm 7h6asdf1234

```

Forzar a borrar contenedores aunque estén activos
```bash
docker rm Micontenedor --force
```

## Networks
### Borrar interfaces de red docker
A medida que vamos creando contenedores se van asignando nuevas interfaces y aveces puede saturar cuando hacemos un ifconfig, para borrar todas estas interfaces hacemos lo siguiente:
```bash
docker network ls
docker network rm $(docker network ls -q) #Borra todas las interfaces que no sean necesarias y deja una que es la que viene por defecto
```
### Ver las interfaces que hay creadas en docker
```bash
docker network ls
```

### Inspeccionar las redes que han sido creadas y las interfaces activas
```bash
docker network inspect
```
>podemos ver más opciones poniendo simplemente docker network

### MACVLAN
Este método en Docker que se utiliza para asignar una dirección MAC a un contenedor determinado, haciendo que este aparezca como si fuera un dispositivo físico en su red.
Para ello tenemos que crear primero una macvlan especificando la subnet de nuestra casa y el gateway
```bash

```


## Imágenes
### Borrar imágenes
Para las imágenes es lo mismo pero añadiendo una i al final.
```bash
docker rmi Micontenedor
docker rmi 1f6ddc1b2547
```

### Borrar imágenes corruptas
Aveces cuando instalamos una imagen por lo que sea no se completa con éxito, esto quiere decir que se ha quedado colgando (dangling). Para borrar esta imagen en concreto:
```bash
docker rmi $(docker images --filter='dangling=true' -q)
```

### Borrar todo, contenedores o imágenes, de un plumazo
Podemos combinar dos simples comandos para ahorrarnos tener que ir uno por uno. 
```bash
docker rm $(docker ps -a -q) --force
docker rmi $(docker images -q)
```


### Borrar volúmenes
Los volúmenes son utilizados para garantizar la persistencia de los datos generados o utilizados por los contenedores, ya que los sistemas de archivos dentro de los contenedores son efímeros y se eliminan una vez que el contenedor se detiene o se reinicia. Al utilizar volúmenes, los datos se mantienen incluso si el contenedor es destruido o reemplazado.
```bash
docker volume rm $(docker volume ls -q)
```

### Port forwarding
Al crear un contenedor podemos especificar un puerto de nuestro máquina para que sea el puerto de la máquina virtual, por ejemplo:
```bash
docker run -dit -p 80:8080 --name Micontenedor imagen
```

Aquí lo que le estamos indicando es que nuestro puerto 80 será el puerto 8080 de la máquina de manera que toda la información que corra por nuestro puerto 80 será redirigida al puerto 8080 de  la máquina y viceversa.

> Podemos comprobar que efectivamente el puerto ochenta de nuestra máquina está siendo utilizada por la máquina virtual de la siguiente manera:

```bash
lsof -i:80
docker port contenedor
```



### Crear un contenedor con una montura (CARPETA COMPARTIDA)
Podemos montar un directorio de nuestra máquina real en la máquina virtual, solo tenemos que especificarle la ruta del directorio que queremos y luego la ruta en la que se va a montar
```bash
docker run -dit --name mi-contenedor -v /home/valen/carpeta:/home/ ubuntu
```


### Dockerfile
Podemos establecer en un archivo todo las características que queramos que contenga nuestro contenedor al ser desplegado. Al crear un contenedor este te viene casi desnudo, por lo que tienes que instalar tu mismo las herramientas que necesites. Con el dockerfile podemos declarlo todo a la primera, y prender el contenedor con todas las herramientas que necesitemos instaladas. Ejemplo:
```bash
FROM ubuntu:latest
MAINTAINER valentino

ENV DEBIAN_FRONTEND noninteractive

RUN apt update && apt install -y git \
nano \ 
net-tools \ 
iputils-ping \
apache2 \
php

EXPOSE 80
ENTRYPOINT service apache2 start && /bin/bash
```

- FROM > indicamos cuál es el sistema operativo 
- ENV> (enviroment)esto sirve para indicar como quieres que sea el proceso de la instalación, en este caso indicamos que no sea interactivo, es decir, cuando una aplicación nos pida algún dato cuando se esté instalando, ignore esa parte y se configure con los valores por defecto. De esta manera no nos saldrá ninguna pregunta de configuración ni nada en el proceso de instalación. 
- RUN > podemos ejecutar comandos en el sistema para instalar una serie de herramientas en el proceso de construcción
- EXPOSE> exponer un puerto para luego poder hacer port forwarding
- ENTRYPOINT> podemos indicar que nos inicie un comando de entrada nada más se ejecute el contenedor, en este caso le indicamos que inicie el servicio de apache y establezca una /bin/bash

### Ejecutar el dockerfile
Una vez que hayamos creado nuestro dockerfile podemos ejecutarlo para que nos construya la imagen correspondiente
```bash
docker build -t nueva_imagen .
```

- build> indicamos que contruya nuestro dockerfile en una imagen
- -t> (taged) indica un nombre a la imagen que vamos a crear
- .> el punto simboliza el directorio actual de trabajo donde es encuetre el dockerfile, debe ser un directorio vacío o con pocos elementos para que detecte más rápidamente el dockerfile.

### Docker-compose
El comando "docker-compose up" se utiliza para ejecutar los servicios definidos en un archivo de configuración llamado docker-compose.yml. Inicia contenedores Docker interrelacionados, creando un entorno de aplicaciones multi-contenedor de manera rápida y sencilla.
De la misma manera "docker-compose down"  detiene y elimina todos los recursos creados por el comando "docker-compose up" o "docker-compose start". Esto puede incluir la detención y eliminación de los contenedores en ejecución, la eliminación de las redes creadas y la limpieza de los volúmenes utilizados por los servicios definidos en el archivo docker-compose.yml. Es útil cuando se quiere desmontar y limpiar completamente una aplicación ejecutada con Docker Compose.
Y por último con "docker-compose stop" simplemente paramos la máquina.

