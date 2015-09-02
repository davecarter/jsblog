---
layout: post
title:  "Constructores"
date:   2015-08-29 23:00:00
categories: constructores
tags: opinion
image: /assets/article_images/cover-constructors.jpg
comments: true
---

### Objetos

En JS todo son objetos. De esta forma puede parecer que se reduce complejidad o se limita en cierta manera el propio lenguaje. El hecho de que podamos crearlos de formas diferentes y que cada una tenga implícita una serie de condiciones es lo que me resulta más difícil de comprender.

### Creando objetos

Podemos crear un objeto vacío y asignarlo a una variable así:
```
var persona = {};
```
Al utilizar las *llaves* sin contenido estamos indicando a JS que cree una instancia de un objeto mediante el constructor predefinido `Object()`y nos asigne dicho elemento a una variable.

Otra forma de instanciar un objeto sería mediante el constructor `new`:
```
var persona = new Object();
```
Una *instancia* es una copia de un objeto que mantiene una relación con su 

Hay 9 tipos de constructores predefinidos en Javascript:

- Number();
- String();
- Boolean();
- Object();
- Array();
- Function();
- Date();
- RegExp();
- Error();



### Conclusión



Si te ha gustado este artículo no dudes es difundirlo o dejar un comentario.


<div class="referencias">
  <p><strong>Bibliografía:</strong></p>

  <p>Eric Elliott's JavaScript Blog: <br />
  <a href="http://ericleads.com/2012/09/stop-using-constructor-functions-in-javascript/">
Stop Using Constructor Functions In JavaScript</a></p>
  
</div>