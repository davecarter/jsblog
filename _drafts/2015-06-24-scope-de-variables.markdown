---
layout: post
title:  "Scope de variables, hoisting y closures"
date:   2015-06-28 23:00:00
categories: variables feature
tags: opinion
image: /assets/article_images/2015-06-24-scope-de-variables/cover.jpg
comments: true
---

### Variables en JS

Una variable es un contenedor de datos. A diferencia de otros lenguajes de programación fuertemente tipados como el C, una variable en JS no necesita ningún tipo de identificador que especifique el tipo de dato que contiene. 

Podemos usar prácticamente cualquier nombre o caracter unicode para *identificar* o darle nombre a una variable. Algunos ejemplos de nombres de variables válidos son:

```
> var π = Math.PI;
> var ლ_ಠ益ಠ_ლ = 42;
```
Más información en [esta página](https://mathiasbynens.be/notes/javascript-identifiers#examples).
Puedes comprobar la validez del identificador de una variable con [esta herramienta](https://mothereff.in/js-variables#%E0%B2%A0%5f%E0%B2%A0).

Cuando digo *prácticamente cualquier nombre* me refiero a que hay una lista de palabras reservadas o *keywords* que no pueden utilizarse como identificadores de variables. Puedes consultarlos en esta lista de [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar).

Esta arbitrariedad a la hora de crear variables no implica que sea buena idea hacerlo. Se recomienda utilizar convenciones de nombres para maximizar la legibilidad de tu código y hacerlo así más fácil de mantener. Por ejemplo un buen nombre de variable:

- Empieza por minúscula.
- No contiene caracteres especiales (ñ, ç, %) ni acentos...
- Utiliza [camelCase](https://es.wikipedia.org/wiki/CamelCase).
- Las variables globales y las constantes se escriben todo en MAYÚSCULAS.
- No contienen un guión (-).

Las convenciones de nombres no sólo se usan para las variables sino que son útiles como guías comunes para aplicar a todo el código en sí. Si quieres más información al respecto puedes consultar el [siguiente enlace](http://javascript.crockford.com/code.html). Además hay herramientas de *linting* que te van haciendo sugerencias a medida que escribes tu código. Una de ellas es [ESlint](http://eslint.org/).

#### Declarar una variable

A la acción de crear una variable se le conoce como **declaración**. La sintaxis es:

```
> var miVariable;
```
Las variables son **sensibles a las mayúsculas** de modo que `miVariable`y `mivariable` son diferentes.
Algo que debemos de tener en cuenta a la hora de crear una variable es que lo que realmente estamos haciendo es reservar un espacio de memoria para almacenar un dato cualquiera. Esto convierte a JS en un lenguaje de programación poco eficiente en lo que a gestión de recursos se refiere. De modo que tendremos que evitar siempre que nos sea posible crear variables globales para no consumir más recursos de los necesarios. Más abajo comentaré como hacerlo.

Llamamos *asignación* a la acción de guardar un valor en una variable. Utilizamos el símbolo =:

```
> var miVariable = 5;
```

En JS hay dos tipos de *valores* de datos diferentes: Primitivas y objetos.
Una primitiva es un valor que al compararse consigo mismo retorna `true`. Por ejemplo una string, un numeral, un boolean, undefined o null son primitivas.

```
> var num1 = 100;
> var num2 = 100;
> num1 === num2
true
```

Si hacemos lo mismo con un objeto nos retornará `false` ya que los objetos en JS sólo son iguales intrínsicamente a sí mismos. (Esto lo sueltas en una reunión y quedas genial).

```
> var obj1 = {'one','two'};
> var obj2 = {'one','two'};
> obj1 === obj2
false
```
Sin embargo...

```
> var obj1 = {'one','two'};
> var obj2 = {'one','two'};
> obj1 === obj1
true
```

<div class="protip">
  Existen dos tipos de comparación de igualdad: <strong>normal (==)</strong> y <strong>estricta (===)</strong>. La normal se utiliza cuando comparas valores de un mismo tipo de datos, objeto con objeto, string con string... Si los valores <strong>undefined</strong> y <strong>null</strong> pueden aparecer en la comparación utiliza siembre la igualdad estricta y evitarás sorpresas.
</div>

### Scope de variables

Llamamos *scope* al ámbito de actuación de una variable. Puede ser local, es decir, si la declaramos dentro de una función sólo podremos acceder a su contenido desde una instrucción situada dentro de ese bloque.

Esto que en principio puede sonar restrictivo es algo realmente bueno. Nos interesa tener controlado quien tiene acceso a nuestras variables para que no nos las modifiquen de forma inesperada. No lo es tanto para el rendimiento de nuestra aplicación; Crear bloques con referencias a variables hacen que el sistema encargado de decidir si puede o no liberarlas de memoria no las borre por si acaso la estamos usando. A esta liberación de memoria se le conoce como *garbage collection*. Cada navegador en el que ejecutemos nuestro código JS tiene su propio sistema. En definitiva, para intentar que este sistema sea lo más eficiente posible hemos de tener controlados en todo momento estos encapsulamientos conocidos como *closures*.

Sin embargo, la nueva especificación de JS conocida como ECMAScript6 (ES6) trae consigo un nuevo *scoping* de variables:

```
let myES6var = 'I'm cool';
```
