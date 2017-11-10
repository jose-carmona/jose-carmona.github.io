---
layout: post
title:  "Inyección de dependencias"
---
Un patrón de diseño es una forma de no complicarte la vida ni complicársela a tus colaboradores. Aplicar un patrón de diseño es aplicar una fórmula estandar, probada y conocida universalmente.

En Drupal, es esencial el patrón [Inyección de dependencias](https://en.wikipedia.org/wiki/Dependency_injection). Tal vez la mejor explicación del patrón sea la que oí en una sesión de [@husseinweb](https://twitter.com/jose_carmona/status/845611303100186624) en Drupal Developers Days de Sevilla en marzo de 2017.

![dependency-injection-and-paella.png]({{ site.baseurl }}/images/dependency-injection-and-paella.png)

Hussein usó el siguiente símil: inyección de dependencias es cuando tu pides a un cocinero que te haga paella entregándole los ingrediente concretos que debe usar.

Si entras un poco más en detalle en el patrón, te das cuenta que la idea es separar conceptualmente receta, cocinero e ingredientes y unirlos físicamente en el momento inicial. Esta independencia te permite variar ingredientes según necesidades (¡vaya! hoy no tengo marisco, pues hacemos [paella con carne](https://www.google.es/search?q=receta+paella+de+carne)) o experimentar (¡vamos a probar una [paella con trigo](https://www.google.es/search?q=receta+paella+de+trigo) en vez de arroz!).

Usando este patrón conseguirás que tu código esté desacoplado y sea, por tanto, más fácilmente reutilizable. Además, te será más sencillo crear tus tests.

### Drupal e Inyección de Dependencias

En Drupal, la inyección de Dependencias es el método recomendado para acceder y consumir servicios. Cuando declaras un servicio, en el correspondiente fichero YAML también puedes especificar aquellos servicios de los que depende con la etiqueta "arguments". El contenedor se encarga de instanciar esos servicios de los que depende y pasarlos como parámetros al constructor de la clase.

Bien, para servicios está claro. Pero, ¿qué pasa cuando Drupal instancia por ti un objeto y no hay configuración para especificar la Inyección de dependencias? Hay una convención en la comunidad Drupal para usar un método factory llamado "create". Entonces, es suficiente con incluir en la clase un método estático que recibirá el contenedor de inyección de dependencias como primer parámetro. La idea es extraer del contenedor los servicios y, a continuación, llamar al constructor. Algo así:

``` php
class MiClase {
  …

  public function __construct($servicio1, $servicio2, ...) {
    // Guarda los servicios en propiedades de la clase
  }

  public static function create(ContainerInterface $container) {
    // new static() significa "llama al constructor de la clase"
    return new static(
      $container.get('servicio1'),
      $container.get('servicio2'),
      …
    );
  }

}
```

Sencillo, ¿no?

¿No te ha convencido mi explicación? A ver que te parecen estos enlaces:

* [Drupal Documentation - Services and dependency injection in Drupal 8](https://www.drupal.org/node/2133171)
* [Drupal API - Services and Dependency Injection Container](https://api.drupal.org/api/drupal/core%21core.api.php/group/container/8.4.x)
* [Acquia - Lesson 8.3 - Dependency injection](https://docs.acquia.com/article/lesson-83-dependency-injection)
* [Lullabot - Injecting services in your D8 plugins](https://www.lullabot.com/articles/injecting-services-in-your-d8-plugins)
* [Chromatic - Dependency Injection in Drupal 8 Plugins](https://chromatichq.com/blog/dependency-injection-drupal-8-plugins)
