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

De esta forma se destaga mongo con el tag (versión) latets.

En los resultados de la búsqueda veremos además que se listan diferentes tags (o versiones de la imagen que se han subido). Si deseamos descargar alguna que no sea la oficial previamente descargada de la misma forma ejecutamos:

```markdown
  docker pull nombre_imagen:nombre_tag
```



## Imagenes Docker

##### Listar imágenes

```
 sudo docker images
```

Si deseamos listar por todas las imágenes de un tipo que hemos descargado, por ejemplo las imágenes de mongo escribimos


```
sudo docker images | grep mongo
```




**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)

`

### Rafael Gamez Diaz
2021
