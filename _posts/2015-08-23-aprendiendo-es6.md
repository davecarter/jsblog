---
layout: post
title:  "Aprendiendo ES6"
date:   2015-08-23 23:00:00
categories: ES6
tags: opinion
image: /assets/article_images/cover-es6.jpg
comments: true
---

### ECMA-262 Odyssey:
Se conoce como ECMAScript a la implementación del estandar ECMA-262. Este estandar ha sido revisado varias veces desde su creación. Javascript está basado en dicho estandar pero además añade nuevas funcionalidades que **no** están definidas en la especificación. De modo que cada revisión del estandar ECMA-262 afecta a las funcionalidades y/o a la sintaxis de Javascript.

Las revisiones de este estandar han sido por lo general difíciles. Para que os hagáis una idea, la versión 3 estuvo desde 1999 hasta el 2009. La versión 4 (Codenamed Harmony) fue desestimada porque aportaba *demasiados avances* y no tenía retro-compatibilidad con las versiones anteriores. Se retoma la versión 3, se añaden algunas mejoras sintácticas y se renombra 3.1. Finalmente, se lanza en Diciembre del 2009 como ECMAScript 5.

### ECMAScript 6
En Junio de este año 2015 se publica una revisión del estandar codenamed Harmony, es decir, el mismo que Brendan Eich (el creador de JS) intentó publicar como ES4 en el 2009 pero no le dejaron aunque esta vez renombrado como ES6 (Supongo que llamarlo ES4 y retroceder una versión no quedaba serio...)

De modo que finalmente ES6 pasa a ser **la mayor revisión** de esta especificación en más de 15 años ya que actualiza y mejora funcionalidades, sintaxis y semántica que Javascript lleva arrastrando desde su versión 3.

### Situación actual
Una actualización a gran escala como necesita soporte de los navegadores para que podamos empezar a usarlo. Navegadores actuales como Chrome, Firefox e incluso IE12 empiezan a incluir algunas de las novedades que aporta ES6. Consulta [esta tabla](https://kangax.github.io/compat-table/es6/) de compatibilidad para ver qué está disponible en cada uno de ellos.

### ES6 transpiling
Afortunadamente tenemos [BabelJS](https://babeljs.io/), un *transpiler* que traduce archivos JS con sintaxis ES6 a ES5 haciéndolo compatible en todos los navegadores y de forma totalmente transparente para nosotros. Así que ya **no tienes excusa para no empezar a usar ES6 hoy mismo**.

## Novedades de ES6
Esta lista no pretende ser ni mucho menos la más representativa de ES6. Se trata más bien de lo que personalmente estoy usando a día de hoy. Si crees que hay alguna funcionalidad más que te resulta útil y no está aquí puedes dejar una nota en los comentarios.

### Arrow functions
Se trata de un *syntactic sugar* para las funciones. Se elimina la palabra `function`, se pasan los parámetros de la función entre paréntesis y a continuación se añade `=>`:

```
// Funciones en ES5
var myWallet = function(currentMoney, expenses){
  return ('You have '+ (currentMoney - expenses) + '$ remaining in you wallet');
}

// Funciones en ES6
var myWallet = (currentMoney, expenses) => {
  return ('You have '+ (currentMoney - expenses) + '$ remaining in you wallet');
}
```
Inicialmente no me parece que aplique demasiado bien el concepto de syntactic sugar pero es cierto que te acabas acostumbrando.

### Variables de ámbito de bloque
Hasta ahora las variables en JS tenian un ámbito de función, es decir, existian en todo el ambito de la función en la que habían sido declaradas. Con la introducción de `let` ahora podemos crear un ámbito reducido a un bloque concreto definido por una expresión o una declaración. Ahora nuestras variables se mantienen locales sin necesidad de crear [IIFE](http://exploringjs.com/es6/ch_callables.html#sec_iifes-in-es6).

### Constantes
`const` nos permite crear estructuras de datos inmutables. De esta forma obtendremos resultados más predecibles y nos resultará más fácil *debuggar* errores. Puedes consultar mi entrada anterior en la que hablo más detalladamente sobre [Let y Const](http://davecarter.me/scope-de-variables/).

### Template strings
Los template strings nos permiten evaluar variables dentro de una cadena de texto. Para poder crearlos necesitamos iniciar y cerrar el string con las comillas invertidas: `` `string` ``

- En lugar de usar el signo `+` para concatenar usaremos el siguiente placeholder:

```
`string ${moneyLeft} string`
```
La variable `moneyLeft` se evalua y se concatena al resto de la cadena de texto. 

Los template strings no solo funcionan con variables. Permiten evaluar el resultado de cualquier cosa contenida entre las llaves `{}`, por ejemplo: Una operación aritmética entre dos variables.

- El ejemplo anterior de la función `myWallet` quedaría así utilizando arrow functions, las nuevas variables y los template strings:

```
const myWallet = (currentMoney, expenses) => {
  let moneyLeft = currentMoney - expenses;
  let msg = `You have ${moneyLeft} $ remaining in you wallet`;
    return msg;
};
```
Además son multi-línea sin necesidad de usar el backslash `\`, también podemos crear *tagged templates* que vienen a ser template strings encabezados con un nombre de función y para escapar código HTML de forma sencilla.

```
fn`Hello! My name is ${name}`
```

### Modulos

La gestión del código JS ha ido evolucionando. Hemos pasado de usar múltiples tags `<script>` en el header a minificar y concatenar diferentes archivos en uno sólo mediante *task runners* tipo [Grunt](http://gruntjs.com/) o [Gulp](http://gulpjs.com/).

Aquí os dejo un ejemplo de cómo gestiona Gulp sus dependencias:
![GulpJS](/assets/images/gulp.png)

De esta forma *modularizamos* nuestro código pero todavía nos queda pendiente la gestión de dependencias. Realmente no sabemos si una librería depende de otra o no.

CommonJS/RequireJS han ofrecido hasta ahora mayor control sobre dependencias para poder así crear JS modular. Con ES6 disponemos de los nuevos `import` y `export` que aportan esta funcionalidad de forma nativa.

**Export** nos permite gestionar qué partes de nuestro código queremos exponer:

```
// Si disponemos del siguiente código en el archivo message.js
// podremos exponerlo con export así:
export const message = 'Hello World';

// Y lo importaremos de la siguiente manera:
import {message} from './message';
console.log(message); // Hello World

// Podemos importar múltiples objetos separados por comas:
import {author, books} from './library';

// O el módulo completo usando el wildcard *
import * as library from './library';

// Para acceder a los objetos haríamos:
let author = library.author;
let books = library.books;

```
A esta forma de exportar módulos de ES6 se le llama *named exports*. Son útiles cuando conocemos el nombre del objeto que queremos importar/exportar.

Por otro lado, cuando queremos exportar una función completa o una clase podemos utilizar **default**

```
// Exportamos una función anónima del archivo app.js:
export default function () { ··· }

// La importamos y le aplicamos 
// el identificador myWallet:
import myWallet from './app';
myWallet();
``` 

Puntos a tener en cuenta cuando utilizamos módulos en ES6:

- Se ejecutan una vez cargados.
- Pueden contener declaraciones de variables, funciones, objetos, etc...
- El ámbito de las declaraciones que hacemos en un módulo permanecen locales a ese módulo. Las partes expuestas mediante export sufrirán un hoisting, es decir, estarán disponibles en cualquier parte del código una vez expuestas.
- Un módulo puede exportar todo o partes específicas de sí mismo.
- Un módulo puede importar a otro.

### Conclusión

Esta nueva versión de Javascript conocida como ES6 o ES2015 no es sólo un *restyling* sino una adaptación del lenguaje a las necesidades actuales de crear aplicaciones que corren tanto en el cliente como en el servidor.

Esta entrada no pretende ser una referencia en lo que a nivel de detalle se refiere sino más bien una recopilación de apuntes sobre las funcionalidades que personalmente más utilizo.

Si te ha gustado este artículo no dudes es difundirlo o dejar un comentario.


<div class="referencias">
  <p><strong>Bibliografía:</strong></p>

  <p>Google Developers: <br />
  <a href="https://developers.google.com/web/updates/2015/01/ES6-Template-Strings">Getting Literal With ES6 Template Strings</a></p>
  
  <p>Understanding ES6: <br />
  <a href="https://leanpub.com/understandinges6/read#leanpub-auto-multiline-strings">Multiline Strings</a></p>

  <p>Exploring ES6<br />
    <a href="http://exploringjs.com/es6/ch_modules.html#ch_modules">Modules</a></p>

  <p>Tower of Babel<br />
    <a href="https://github.com/yosuke-furukawa/tower-of-babel">A series of exercises that introduce you to ES6 features</a></p>
  
</div>