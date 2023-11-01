# TALLER DE INTRODUCCIÓN A VIRTUALIZACIÓN Y PROG. DISTRIBUIDA

## Conceptos

### Docker
Docker es el software de TI, es una tecnología de creación de contenedores que permite la creación y el uso de contenedores de Linux®. Con docker, puede usar los contenedores como máquinas virtuales extremadamente livianas y modulares.


## Pre-requisitos

Debe tener instalado lo siguiente:

* [GIT](https://git-scm.com/book/es/v2/Inicio---Sobre-el-Control-de-Versiones-Instalación-de-Git)
* [JAVA 8](https://www.java.com/es/download/)
* [MAVEN](https://maven.apache.org)
* [DOCKER](https://www.docker.com/)
* **DOCKER-COMPOSE** - Viene incluido en Docker Desktop, sin embargo si no lo tiene, puede ver como instalarlo [AQUI](https://docs.docker.com/compose/install/).

## Compilación

* Para hacer una instalación limpia de las dependencias y plugins con maven

        mvn clean install

* Para compilar el codigo fuente únicamente.

        mvn compile

## Ejecución

**JAVA Linux**

        java -cp target/classes:target/dependency/* co.edu.escuelaing.sparkdockerdemolive.SparkWebServer

**JAVA Windows**

        java -cp target/classes;target/dependency/* co.edu.escuelaing.sparkdockerdemolive.SparkWebServer

Al acceder a la url http://localhost:4567/hello debería ver el siguiente mensaje.

![local-deploy.png](img/local-deploy.png)

### Ejecucion en Docker

**Docker**

La definición para la imagen donde se construye a partir de un [Dockerfile](Dockerfile). Un Dockerfile es un archivo de texto que contiene una serie de instrucciones para construir una imagen de Docker. Una vez que se construye la imagen, se puede utilizar para desplegar el servicio varias veces.
Como en este archivo se definió el puerto 6000 como variable de entorno el servicio se desplegara por el puerto 6000 dentro de cada contenedor que se construya a partir de la imagen.

* Construir la imagen.

        docker build --tag dockersparkprimer.

* Construir el contenedor, encender el contenedor y mapear el puerto 6000 del contenedor con el 34000 del equipo.

        docker run -d -p 34000:6000 --name firstdockercontainer dockersparkprimer

Al acceder a la url http://localhost:34000/hello debería ver el siguiente mensaje.

![docker-deploy.png](img/docker-deploy.png)


Podemos usar la imagen para construir multiples contenedores y desplegar los servicios en diferentes puertos.

    docker run -d -p 34001:6000 --name firstdockercontainer dockersparkprimer
    docker run -d -p 34002:6000 --name firstdockercontainer dockersparkprimer


Ejecutanto `Docker ps` debería ver algo similar a esto.

![docker-ps.png](img/docker-ps.png)


**Docker Compose**

        docker-compose build
        docker-compose up -d

En el [docker-compose.yml](docker-compose.yml) usamos el Dockerfile para construir una imagen y un contenedor con el tag web para el servicio de SparkWebServer junto con una imagen mongodb y contenedor llamado db.

Debería ver lo siguiente:

![docker-ps-2.png](img/docker-ps-2.png)


## Subir la imagen a DockerHub

1. Si no la tiene crear una cuenta de dockerhub.
2. Crear un repositorio llamado dockersparkprimer.
3. Crear una referencia a la imagen con el nombre del repositorio a donde se subirá.

        docker tag dockersparkprimer ricar8o/firstsprkwebapprepo

4. Revisar las imagenes y sus referencias.

        docker images

5. Autenticarse con la cuenta de Dockerhub.

        docker login

6. Enviar la imagen al repositorio en DockerHub.

        docker push ricar8o/firstsprkwebapprepo:latest

7. Al subirse debería verse la imagen cargada en la sección de tags.

    ![docker-ps-2.png](img/docker-hub-tags.png)


## Subir la imagen a DockerHub

## Autor

Andrés Ricardo Martínez Díaz - [Ricar8o](https://github.com/Ricar8o)