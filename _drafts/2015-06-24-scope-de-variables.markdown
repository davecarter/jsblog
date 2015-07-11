---
layout: post
title:  "Scope de variables y hoisting"
date:   2015-07-12 23:00:00
categories: variables ES5
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

Actualmente la versión de JS que interpretan los navegadores de forma nativa es ECMAScript 5 de finales del 2009. El borrador final de ECMAScript 6 tiene fecha de abril de este año 2015, así que mientras que los navegadores no la tengan completamente implementada tendremos que utilizar *transpilers*, aplicaciones que traducen ES6 a ES5 como por ejemplo <a href="https://babeljs.io/">Babel</a>.

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
Como podemos observar únicamente cuando comparamos un objeto consigo mismo retorna `true`.

<div class="protip">
  Existen dos tipos de comparación de igualdad: <strong>normal (==)</strong> y <strong>estricta (===)</strong>. La normal se utiliza cuando comparas valores de un mismo tipo de datos, objeto con objeto, string con string... Si los valores <strong>undefined</strong> y <strong>null</strong> pueden aparecer en la comparación utiliza siembre la igualdad estricta y evitarás sorpresas conocidas como <a href="http://robertnyman.com/2008/05/16/how-to-avoid-automatic-type-conversion-in-javascript/">type coercion</a>.
</div>

### Scope de variables

Llamamos *scope* al ámbito de actuación de una variable. Puede ser local, es decir, si la declaramos dentro de una función sólo podremos acceder a su contenido desde una instrucción que se ejecuta dentro de esa misma función. A esto se le llama *function-scoped*.

La nueva especificación de JS conocida como **ECMAScript6 (ES6)** trae consigo dos nuevos tipos de declaración de variables que además afectan al *scoping*:

```
let myES6var = 'I'm cool';
cons myES6constant = 3,1415;
```
`let` y `const` en ES6 vienen a reemplazar a `var`.

Hasta ahora, las declaraciones realizadas mediante `var` se consideraban como *function-scoped*, es decir. Existen dentro de una función. Las nuevas declaraciones de ES6 son *block-scoped*, de modo que su ámbito de actuación se limita exclusivamente al bloque en el que han sido declaradas:

```
function currentStatus() {
    if (initialStatus === 0) {
        let counter = 0;
    }
    console.log(counter); // ReferenceError: counter is not defined
}
```
La variable *counter* declarada con `let` sólo existe en el bloque creado por la instrucción `if`. En el caso de haberla declarado mediante `var` `console.log(counter)` retornaría el valor 0 ya que se encuentra dentro de la función en la que ha sido declarada.

<div class="referencias">
  <p><strong>Bibliografía:</strong></p>
  
  <p>Variables and assignments: <br />
  <a href="http://speakingjs.com/es5/ch01.html#_variables_and_assignment">SpeakingJS</a></p>
  
  <p>Variables and scoping<br />
  <a href="https://leanpub.com/exploring-es6/read#leanpub-auto-variables-and-scoping">Exploring ES6</a>
  <a href="http://people.mozilla.org/~jorendorff/es6-draft.html#sec-let-and-const-declarations">Let, Consts and declarations</a>
  
  <p>Type coercion<br />
  <a href="http://robertnyman.com/2008/05/16/how-to-avoid-automatic-type-conversion-in-javascript/">How to avoid automatic type conversion</a></p>
</div>