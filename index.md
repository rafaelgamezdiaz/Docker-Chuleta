## Introducción 

No soy un experto en Docker, aquí tan solo dejo unas notas y comandos que escribo para mi mismo como recordatorio y que además estaré doblemente complacido si pueden ser de utilidad para otros.



## Dockerhub

Dockerhub es el sitio oficial donde se almacenan las imágenes de Docker. Allí puedes encontrar imágenes oficiales y no oficiales. Incluso tu mismo puedes subir tus imágenes docker.

[Dockerhub](https://hub.docker.com/)


### Descargar imagen de Dockerhub

Buscamos en el sitio de [Dockerhub](https://hub.docker.com/) el nombre de la imagen que necesitamos. Al mostrarse los resultados veremos que ala derecha aparecerá el comando para descargar la imagen. 

```markdown
 docker pull nombre_imagen
```

Por ejemplo si buscamos la image de mongo, a la derecha se nos mostrará el comando:

```markdown
 docker pull mongo
```

De esta forma se destaga mongo con el tag (versión) latest.

En los resultados de la búsqueda veremos además que se listan diferentes tags (o versiones de la imagen que se han subido). Si deseamos descargar alguna que no sea la oficial previamente descargada de la misma forma ejecutamos:

```markdown
  docker pull nombre_imagen:nombre_tag
```

Notemos que si intentamos descargar una imagen que previamente hemos descargado se te notificará en la consola que ya la hemos descargado. Se descargaran solamente aquellas capas de la imagen que no se han descargado.



## Imagenes Docker

##### Listar imágenes

```
 sudo docker images
```

Si deseamos listar por todas las imágenes de un tipo que hemos descargado, por ejemplo las imágenes de mongo escribimos


```
 sudo docker images | grep mongo
```


##### Imágenes colgadas

Se generan cuando intentamos descargar una imagen previamente descargada y que tiene el mismo nombre. En ese caso al descargarse, la versión más vieja se le cambia el nombre del tag a <none>, que lo más probable es que tendrá el mismo peso que la nueva imagen.



##### Creando nuestras propias imágenes (Dockerfile)

En una imagen personalizada podemos incluir diferentes imágenes. Para esto lo primero que tenemos que hacer es crear un **DockerFile**. Veamos la estructura básica de un Dockerfile.

```
 FROM ubuntu
 
 RUN sudo apt-get update | sudo apt-get install -y mongodb
 
```

Este **Dockerfile** contiene las instrucciones para 

 1. Descargar la imagen de ununtu
 2. Actualizar el repositorio de ubuntu dentro del contenedor
 3. Instalar mongodb


##### Construir imagen

Para construr una imagen tomando como referencia un ***Dockerfile***

```
 docker build --tag mongo-img .
```

En este caso en el final del comnado se colocó un punto, Esto es para indicarle a docker que el Dockerfile se encuentra en la carpeta actual.

















`

### Rafael Gamez Diaz
2021
