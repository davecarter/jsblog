---
layout: post
title:  "Funciones en Javascript"
date:   2015-07-28 23:00:00
categories: functions
tags: opinion
image: /assets/article_images/cover-functions.jpg
comments: true
---

### Definición de una función

La función de una función (toma! empezamos bien!) es la de reutilizar un bloque de código que resuelve un problema específico. Para ello, consta de diferentes partes:

-  Entrada > Llamados también *argumentos*. Permiten a la función obtener los datos con los que va a operar.
-  Bloque > lineas de código contenidas entre `{ ... }`- Una de las características principales de este *bloque* es que las variables definidas dentro de una función mediante `var`**no** existen fuera de ella.
-  Salida > Resultado de la operación realizada en el bloque entre los atributos de entrada. Extraemos el resultado mediante `return`.

Este es la estructura de una **declaración de función:**

```
function square(number){
   return number*number;
}

```

En el ejemplo vemos como declaramos una función con el nombre *square* a la que le pasamos el parámetro de entrada *number*. La función retorna el resultado de multiplicar el parámetro de entrada por sí mismo mediante *return*.

Lo más destacado de una **declaración de una función** es que existe en todo el código desde el momento en el que la creamos (o es declarada). Esto significa que si la declaramos en la línea 100 de nuestro código y la invocamos en la 50 funcionará correctamente.

De forma que el siguiente código, aunque no es una buena práctica hacerlo de esta forma ya que induce a errores y hace difícil su depuración, es válido:

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

// La función square existe en todo el bloque 
// en el que ha sido declarada
```

### Expresiones con Funciones

Otra forma de declarar una función es **asignándola a una variable**. De esta forma creamos una *function expression*. A diferencia del método anterior **no** podemos referenciarla antes de dicha asignación ya que si la variable que la contiene no existe nos retornará `undefined`

```
var square = function (parameter){
   return parameter*parameter;
};
```

Observad que en el ejemplo asignamos a la variable `square` una función *anónima*. El motivo por el cual se omite el nombre es porque al crear una función estamos definiendo un *scope* de modo que sólo podríamos acceder a esta función por su nombre **dentro** de sí misma. Lo cual carece de sentido.

```
// Asignamos la función getSquareOf a la variable square
var square = function getSquareOf(number){
   return typeOf getSquareOf;
};

//getSquareOf no es visible fuera de su propio scope
typeOf getSquareOf;		// > undefined
typeOf square;			// > function
```

> Las **declaraciones de funciones** no se finalizan en `;`mientras que las **expresiones con funciones** sí que es necesario (como todas las expresiones) acabar en `;`

### Funciones IIFEs

Las funciones del tipo IIFE (Immediately-invoked function expressions) son un tipo de declaración de funciones que se invocan a sí mismas.

Además, como hemos visto anteriormente, al crear una función estamos creando un nuevo contexto de modo que al crear este tipo de funciones dotamos de cierta privacidad a ciertas partes de código de su interior. A esta técnica se le conoce como *local scoping*.

```
(function(){
  // nuestro super-código
}());
```

Para invocar a una función lo hacemos con su nombre acabado en paréntesis:
`miFuncion()`

De modo que para llamar a una función anónima podríamos probar de hacer lo siguiente: 
```
function(){ 
	// nuestro código aquí 
}();
```

Si probamos este método veremos que nos lanza un error. Para poder auto-invocarse una función a sí misma necesitamos incluirla entre paréntesis para indicarle al *parser* de JS que se trata de una **expesión con función** y no de una **declaración de función**. Finalmente nuestra IIFE quedaría así:

```
(function(){ 
	// nuestro código aquí 
})();
```

Como comenté en la entrada anterior sobre [scope de variables](http://davecarter.me/scope-de-variables/), 


### Conclusiones

Usar un tipo u otro de definición de función va a depender del contexto en el que vayamos a crearla. Como hemos visto hay sutiles diferencias que nos van a permitir aportar mayor o menor visibilidad tanto a las funciones en sí como a los objetos u otras declaraciones que puedan haber en su interior según nos interese.

Si te ha gustado esta entrada y la has encontrado útil, puedes dejar un comentario o ayudarme a difundirlo.


<div class="referencias">
  <p><strong>Bibliografía:</strong></p>

  <p>Koalite: <br />
  <a href="http://blog.koalite.com/2011/10/javascript-diferencias-entre-declaracion-de-funcion-y-expresion-con-funcion/">Diferencias entre declaración de función y expresión con función</a></p>
  
  <p>Function expressions vs. Function declarations: <br />
  <a href="http://kangax.github.io/nfe/#named-expr">Named function expressions</a></p>

<p>IIFE<br />
  <a href="http://benalman.com/news/2010/11/immediately-invoked-function-expression/">Immediately-Invoked Function Expression</a></p>
  
</div>