---
layout: post
title:  "BDD en Javascript con NodeJS y Mocha"
date:   2015-07-19 23:00:00
categories: node BDD ES6 Mocha
tags: opinion
image: /assets/article_images/cover-bdd.jpg
comments: true
---

### Behavior Driven Development

La primera vez que oí hablar sobre cómo testear código de forma automatizada; es decir, escribiendo más código con una sintaxis específica etc.. , me pareció que se añadía una capa de complejidad que difícilmente se vería compensada. Una vez que lo pruebas te das cuenta de la importancia que tiene *apuntalar* nuestro código con una batería de test automáticos que nos garanticen que cada función va hacer lo que teníamos pensado que hiciera. 

Las ventajas de usar BDD no sólo afectan a la estabilidad del código en sí. Además nos va a permitir **conceptualizar y diseñar** de forma más eficiente cada una de las funcionalidades de nuestra aplicación.

### Mocha
Lo primero que haremos es *setear* un entorno de testing. En este post os hablaré de [Mocha](http://mochajs.org) corriendo sobre NodeJS, de modo que entiendo que tenéis NodeJS instalado.
Para empezar podéis crear una carpeta vacía con el terminal y dentro inicializamos un paquete de node:

```
$ mkdir myProject
$ cd myProject
npm init
```
De esta forma NodeJS nos crea un archivo llamado `package.json`con las características iniciales de nuestro proyecto.
A continuación instalamos Mocha con el flag `--save-dev`:

```
$ npm install mocha --save-dev
```
De esta forma indicamos a NodeJS que **no** nos incluya este paquete en producción.

Ahora si abrimos la carpeta `node_modules`nos aparecerá la sub-carpeta de mocha.
Además del entorno de testeo recomiendo instalar un par de paquetes más:

- [Babel](https://babeljs.io/): Transpiler JS que nos permite utilizar sintaxis de ECMAScript 6.
- [Expect](https://www.npmjs.com/package/expect): Librería de aserciones que nos permite redactar test BDD del tipo: `expect(object).toBe(value, [message])`

Para instalarlos como dependencias de desarrollo haremos:

```
$npm install babel expect --save-dev
```

Una vez instalados estos paquetes configuraremos nuestro entorno con un script que nos permita lanzar todos nuestros test escribiendo:

```
$npm test
```

Para crearlo editamos el archivo `package.json`y añadimos la siguiente declaración:

```
"scripts": {
    "test": "mocha --compilers js:babel/register"
  },
```
Ok! Ya tenemos *seteado* el entorno. Ahora vamos a crear la estructura de carpetas necesaria para separar nuestros test del código que vamos a testear.
Se trata de crear una carpeta `test`y otra `src`y decirle a la una que testee los scripts contenidos en la otra. Lo haremos de la siguiente forma:

```
├── package.json
├── src
│   ├── numbers_01.js
│   ├── numbers_02.js
│   └── [...]
└── test
    └── numbers_test.js
```









<div class="referencias">
  <p><strong>Bibliografía:</strong></p>
  
  <p>BDD for JS: <br />
  <a href="https://jaxenter.com/behaviour-driven-development-for-javascript-part-one-107588.html">It's not about testing</a></p>
  
</div>