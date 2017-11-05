---
layout: post
title:  "Preparando el blog"
---
Aquí tienes mi blog técnico. Me permite compartir con el mundo información y conocimientos técnicos. Aunque parezca un gesto altruista, en realidad se trata de un acto de puro egoísmo. Persigo:

* Obligarme a organizar las ideas. Atribuyen a Albert Einstein la frase "si no lo puedes explicar de forma sencilla, es que no lo has entendido". Pues eso, intentaré explicar de forma sencilla aquello que intento entender.
* Obtener feedback, ese valioso tesoro.

No esperes publicaciones todos los días. Recuerda que este es un blog egoísta sin más pretensiones.

### Qué he usado

Poco. Muy poco. [GitHub pages](https://pages.github.com) me parece un sistema sencillo y poco intrusivo que no genera anuncios al lector. Además, para un blog técnico, la cercanía al código es un aliciente más. Lo único que necesito es un repositorio en GitHub y un par de herramientas de andar por casa: un editor y Docker.

GitHub pages usa [Jekyll](https://jekyllrb.com) para renderizar las páginas a partir de ficheros Markdown en un repositorio determinado del usuario. ¡Sencillo y simple!

Por otro lado, en vez de empezar desde cero, se puede empezar clonando alguno de los repositorios que existen con todo lo necesario para que Jekyll se comporte como un blog. Yo, concretamente, he clonado [Jekyll-now](http://www.jekyllnow.com) porque es muy, muy sencillo.

Como editor uso [Atom](https://atom.io) que es flexible y potente, aunque a veces sea un poco abusivo en el uso de CPU y memoria. Atom con el paquete "Markdown preview" te da una idea muy aproximada del resultado final del post.

Sin embargo, no tiene demasiado sentido tener que hacer commit en master del repositorio para ver el resultado final ya en producción, en vivo y en directo. Aquí es donde [Docker](https://www.docker.com) vuelve a convertirse en un aliado perfecto. Basándome en éste [post de @kristofclaes](https://kristofclaes.github.io/2016/06/19/running-jekyll-locally-with-docker/) he creado el correspondiente fichero `docker-compose.yml` que me permite usar Jekyll sobre docker en mi Mac. Es suficiente con abrir un terminal y ...:

```sh
cd <directorio-del-repositorio>
docker-compose up
```

Puedes acceder al resultado en `http://127.0.0.1:4000`. ¡Sencillo!
