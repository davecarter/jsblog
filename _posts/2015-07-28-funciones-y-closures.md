---
layout: post
title:  "Funciones y Closures en Javascript"
date:   2015-07-28 23:00:00
categories: functions
tags: opinion
image: /assets/article_images/cover-functions.jpg
comments: true
---

### Funciones en Javascript

La función de una función (toma! empezamos bien!) es la de reutilizar un bloque de código que resuelve un problema específico. Para ello, consta de diferentes partes:

-  Entrada > Llamados también *argumentos*. Permiten a la función obtener los datos con los que va a operar.
-  Bloque > lineas de código contenidas entre `{ ... }`- Una de las características principales de este *bloque* es que las variables definidas dentro de una función mediante `var`**no** existen fuera de ella.
-  Salida > Resultado de la operación realizada en el bloque entre los atributos de entrada. Extraemos el resultado mediante `return`.

Este sería una estructura típica de una **declaración de función:**

```
function square(parameter){
   return parameter*parameter;
}

```
Lo más destacado de una **declaración de una función** es que existe en todo el código desde el momento en el que es declarada. Esto significa que si la declaramos en la línea 100 de nuestro código y la invocamos en la 50 funcionará correctamente.

De forma que el siguiente código es válido:

```
// Invocamos a la función square aquí:
square(4);

// ...
//  más código super limpio..
// ... 

// Declaramos la función square más abajo:
function square(parameter){
   return parameter*parameter;
}
```

### Expresiones con Funciones

Otra forma de declarar una función es **asignándola a una variable**. De esta forma creamos una *function expression*. A diferencia del método anterior **no** podemos referenciarla antes de dicha asignación ya que si la variable que la contiene no existe nos retornará `undefined`

```
var square = function (parameter){
   return parameter*parameter;
};
```

Observad que en el ejemplo asignamos a la variable `square` una función *anónima*. El motivo por el cual se omite el nombre es porque al estar definiendo un *scope* sólo podríamos acceder a esta función por su nombre **dentro** de sí misma. Lo cual carece de sentido.

```
// Asignamos la función getSquareOf a la variable square
var square = function getSquareOf(number){
   return typeOf getSquareOf;
};

//getSquareOf no es visible fuera de su propio scope
typeOf getSquareOf;		// > undefined
typeOf square;			// > function
```

> Las **declaraciones de funciones** no se finalizan en `;`mientras que las **expresiones con funciones** sí que se requiere (como todas las expresiones) acabar en `;`

### Cuando usar un tipo u otro




### Conclusiones

El TDD es una herramienta importante a la hora de crear código estable y de calidad. Te puede gustar más un sistema u otro pero es indudable que como humanos que cometemos fallos con facilidad podamos acotarlos de alguna manera e incluso llegar a eliminarlos por completo.

Si te ha gustado esta entrada y la has encontrado útil, puedes dejar un comentario o ayudarme a difundirlo.


<div class="referencias">
  <p><strong>Bibliografía:</strong></p>

  <p>Koalite: <br />
  <a href="http://blog.koalite.com/2011/10/javascript-diferencias-entre-declaracion-de-funcion-y-expresion-con-funcion/">Diferencias entre declaración de función y expresión con función</a></p>
  
  <p>TDD for JS: <br />
  <a href="https://jaxenter.com/behaviour-driven-development-for-javascript-part-one-107588.html">It's not about testing</a></p>
  
</div>