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

### Template literals
Los template literals nos permiten evaluar variables dentro de una cadena de texto. Para poder crearlos necesitamos iniciar y cerrar el string con las comillas invertidas: `` `string` ``

- En lugar de usar el signo `+` para concatenar usaremos el siguiente placeholder:

```
`string ${moneyLeft} string`
```
- El ejemplo anterior de la función `myWallet` quedaría finalmente así:

```
const myWallet = (currentMoney, expenses) => {
  let moneyLeft = currentMoney - expenses;
  let msg = `You have ${moneyLeft} $ remaining in you wallet`;
    return msg;
};
```

### Modulos
Hasta ahora había que recurrir a CommonJS/RequireJS para poder usar JS modular. Con ES6 disponemos de `import` y `export` de forma nativa.