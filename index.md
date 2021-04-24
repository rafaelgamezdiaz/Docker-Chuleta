## Introducción 

No soy un experto en Docker, aquí tan solo dejo unas notas y comandos que pueden servir como consultas rápidas o como recordatorio. Estaré doblemente complacido si pueden ser de utilidad para otros.



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

De esta forma se descarga mongo con el tag (versión) latest.

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

Se generan cuando intentamos descargar una imagen previamente descargada y que tiene el mismo nombre. En ese caso al descargarse, la versión más vieja se le cambia el nombre del tag a \< none \>, que lo más probable es que tendrá el mismo peso que la nueva imagen.



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
 sudo docker build --tag mongo-img .
```

En este caso en el final del comnado se colocó un punto, Esto es para indicarle a docker que el Dockerfile se encuentra en la carpeta actual.


##### Ver las capas de la imagen que se crearon 

```
 sudo docker history -H mongo-img
```


#### Correr el contenedor 

``` 
 sudo docker run mongo-img
```  
De esta formal el contenedor va a morir una vez que se levanta. Es por eso que se deben especificar algunos comandos más que veremos a continuación.

Sigamos ejemplificando con el caso de un contenedor de Mongo. Por default para Mongo utiliza el puerto 27017. Ese el el puerto que en principio se utulizará dentro del contenedor para conectarse a Mongo. Sin embargo fuera de la instancia del contenedor debemos especificar el puerto a través del cual nos vamos a conectar. Para eso se utiliza el tag **-p #puerto**. Podemos utilizar el mismo puerto 27017 para conectarnos externamente o como en este ejemplo que mostramos estamos utilizando otrs puerto para la conexión.

Además podemos colocarle un nombre al contenedor utilizando el tag **--name**.
```
 sudo docker run -p 27117:27017 --name myDatabase mongo-img
```

Ya con esto debería estar ejecutandose la instancia de docker donde se está ejecutando mongo.

Sin embargo de esta forma el contenedor se queda corriendo en la terminal y si cerramos la terminar se detendría la ejecución del mismo. Para hacer que se siga ejecutando en segundo plano debemos agregar el tag **-d** 

```
 sudo docker run -d -p 27117:27017 --name myDatabase mongo-img
```



#### Listar los contenedores que se están ejecutando

```
 sudo docker ps
```


#### Listar todos los contenedores que han sido ejecutados en elgún momento

```
 sudo docker ps -a
```


#### Ver los Logs del contenedor

```
 sudo docker logs nombre_contenedor
```



#### Conectándonos a través de un puerto (ejemplo de contenedor de Mongo en ejecución)

Si ya se está ejecutando una instancia de del contenedor, como en este ejemplo un contendor de mongo

```
 mongo localhost:27117
```

Automáticamente con ese comando deberíamos estar dentro de la base de datos.




#### Detener la ejecución de un contenedor

Para detener la ejecución de un contenedor podemos pasarle el __id__ del contenedor (completo o los 3 primeros caracteres), o el __nombre del contenedor__

``` 
 sudo docker stop id_contenedor
```

Si queremos por otra parte detener la ejecución de todos los contenedores que se estén ejecutando

```
 sudo docker stop $(sudo docker ps -aq)
```



#### Eliminar un contenedor

Para eliminar un contendor primero debemos cerciorarnos de que el mismo no se está ejecutando. Una vez comprobemos que es así procedemos a ejecutar el comando

```
 sudo docker rm $(sudo docker ps -aq)
```










`

### Rafael Gamez Diaz
2021
