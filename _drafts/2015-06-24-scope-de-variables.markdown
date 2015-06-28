---
layout: post
title:  "Scope de variables, hoisting y closures"
date:   2015-06-28 23:00:00
categories: variables feature
tags: opinion
image: /assets/article_images/2015-06-24-scope-de-variables/cover.jpg
comments: true
---

### Variables, scope y hoisting

Una variable es un contenedor de datos. A diferencia de otros lenguajes de programación fuertemente tipados como el C, una variable en JS no necesita ningún tipo de identificador que especifique el tipo de dato que contiene. 

Podemos usar prácticamente cualquier nombre o caracter unicode para *identificar* o darle nombre a una variable. Algunos ejemplos de nombres de variables válidos son:

```
> var π = Math.PI;
> var ლ_ಠ益ಠ_ლ = 42;
```
Más información en [esta página](https://mathiasbynens.be/notes/javascript-identifiers#examples).
Puedes comprobar la validez del identificador de una variable con [esta herramienta](https://mothereff.in/js-variables#%E0%B2%A0%5f%E0%B2%A0).

Cuando digo *prácticamente cualquier nombre* me refiero a que hay una lista de palabras reservadas o *keywords* que no pueden utilizarse como identificadores de variables que puedes consultar en [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar).

Esta arbitrariedad a la hora de crear variables no implica que sea buena idea hacerlo. Se recomienda utilizar convenciones de nombres para maximizar la legibilidad de tu código y lo hace más fácil de mantener. Por ejemplo un buen nombre de variable:

- Empieza por minúscula.
- No contiene caracteres especiales (ñ, ç, %) ni acentos...
- Utiliza [camelCase](https://es.wikipedia.org/wiki/CamelCase).
- Las variables globales y constantes se escriben todo en MAYÚSCULAS.
- No contienen un guión (-).

Las convenciones de nombres no sólo se usan para las variables sino que so útiles como guias comunes para aplicar a todo el código en sí. Si quieres más información al respecto puedes consultar el [siguiente enlace](http://javascript.crockford.com/code.html). Además hay herramientas de *linting* que te van haciendo sugerencias a medida que escribes tu código. Una de ellas es [ESlint](http://eslint.org/).

#### Declarar una variable

A la acción de crear una variable se le conoce como `declaración`. La sintaxis es:

```
> var miVariable;
```
Las variables son **sensibles a las mayúsculas** de modo que `miVariable`y `mivariable` son diferentes.
Llamamos `asignación` a la acción de guardar un valor en una variable. Utilizamos el símbolo `=`:

```
> var miVariable = 5;
```



En JS hay dos tipos de *valores* de datos diferentes: Primitivas y objetos.
Una primitiva es un valor que al compararse consigo mismo retorna `true`. Por ejemplo una string, un numeral, un boolean, undefined o null son primitivas.

```
> var num1 = 100;
> var num2 = 100;
num1 === num2
**true**
```