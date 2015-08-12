---
layout: post
title:  "Aprendiendo ES6"
date:   2015-08-09 23:00:00
categories: ES6
tags: opinion
image: /assets/article_images/cover-es6.jpg
comments: true
---

### ECMA-262 Odyssey:
Se conoce como ECMAScript a la implementación del estandar ECMA-262. Este estandar ha sido revisado varias veces desde su creación. Javascript está basado en dicho estandar pero además añade nuevas funcionalidades que **no** están definidas en la especificación. De modo que cada revisión del estandar ECMA-262 afecta a las funcionalidades y/o a la sintaxis de Javascript.

Las revisiones de este estandar han sido por lo general difíciles. Para que os hagáis una idea, la versión 3 estuvo desde 1999 hasta el 2009. La versión 4 (Codenamed Harmony) fue desestimada porque aportaba *demasiados avances* y no tenía retro-compatibilidad con las versiones anteriores. Se retoma la versión 3, se añaden algunas mejoras sintácticas y se renombra 3.1. Finalmente, se lanza en Diciembre del 2009 como ECMAScript 5.

### ECMAScript 6
En Junio de este año 2015 se publica una revisión del estandar codenamed Harmony, curiosamente el mismo que Brendan Eich, el creador de JS intentó publicar como ES4 en el 2009 pero no le dejaron aunque esta vez renombrado como ES6 (Hubiese sido la leche llamarlo ES4 y retroceder una versión...)

ES6 es la mayor revisión de esta especificación en más de 15 años ya que actualiza y mejora funcionalidades, sintaxis y semántica que Javascript lleva arrastrando desde su versión 3.

### Situación actual
Una actualización a gran escala como necesita soporte de los navegadores para que podamos empezar a usarlo. Navegadores actuales como Chrome, Firefox e incluso IE12 empiezan a incluir algunas de las novedades que aporta ES6. Consulta [esta tabla](https://kangax.github.io/compat-table/es6/) de compatibilidad para ver qué está disponible en cada navegador.

### ES6 transpiling
Afortunadamente tenemos [BabelJS](https://babeljs.io/), un *transpiler* JS que genera archivos JS ES5 compatibles en todos los navegadores partiendo de una sintaxis ES6. De forma que **no tienes excusa para no empezar a usar ES6 hoy mismo**.

### Arrow functions
Se trata de una nueva sintaxis para las funciones. Se elimina la palabra `function`, se pasan los parámetros de la función entre paréntesis y a continuación se añade `=>`:

```
// ES5
var myWallet = function(currentMoney, expenses){
  return ('You have '+ (currentMoney - expenses) + '$ remaining in you wallet');
}

// ES6
const myWallet = (currentMoney, expenses) => {
  return (`You have (${currentMoney} - ${expenses}) $ remaining in you wallet`);
}
```
Quizás no sea una forma muy *verbosa* de crear funciones pero te acabas acostumbrando rápido.

### Variables con ámbito de bloque
Hasta ahora las variables en JS tenian un ámbito de función, es decir, existian en todo el ambito de la función en la que habían sido declaradas. Con la introducción de `let` ahora podemos crear un ámbito reducido a un bloque concreto definido por una expresión o una declaración. Ahora nuestras variables se mantienen locales sin necesidad de crear [IIFE](http://exploringjs.com/es6/ch_callables.html#sec_iifes-in-es6).

### Constantes
`const` nos permite crear estructuras de datos inmutables. De esta forma obtendremos resultados más predecibles y nos resultará más fácil *debuggar* errores.

### Template literals
