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

El flujo para desarrollar software basado en **BDD** es el siguiente:

- Escribimos la especificación del test.
- Escribimos el código para que pase el test.
- Si falla, refactorizamos el código hasta que pase el test.

Podemos ver este proceso en la siguiente gráfica:

![BDD](/assets/images/bdd-cycle-around.png)

Más abajo os pongo un ejemplo práctico de cómo llevar a cabo este proceso.

### Mocha
Si queremos poner en práctica todo esto, lo primero que haremos es *setear* un entorno de testing. En este post os hablaré de [Mocha](http://mochajs.org) corriendo sobre NodeJS, de modo que entiendo que tenéis NodeJS instalado.

Mocha es una *Testing Suite* altamente configurable. Podemos especificar diferentes librerías de aserciones como por ejemplo [chai](http://chaijs.com/) o [expect.js](https://github.com/LearnBoost/expect.js). Estas librerías definen cómo vamos a escribir nuestros test. En este caso usaremos *expect.js* ya que es el que mejor se adapta al concepto de BDD. 

Para empezar podéis crear una carpeta vacía con el terminal y dentro inicializamos un paquete de node:

```
$ mkdir myProject
$ cd myProject
$ npm init
```
De esta forma NodeJS nos crea un archivo llamado `package.json`con las características iniciales de nuestro proyecto.
A continuación instalamos Mocha con el flag `--save-dev`:

```
$ npm install mocha --save-dev
```
Así le decimos a NodeJS que **no** nos incluya este paquete en producción.

Ahora si abrimos la carpeta `node_modules`nos aparecerá la sub-carpeta de mocha. Ya tenemos la *suite* de testing lista.

Además de *Mocha*, vamos a instalar un par de paquetes más:

- [Babel](https://babeljs.io/): Transpiler JS que nos permite utilizar sintaxis de ECMAScript 6.
- [Expect](https://www.npmjs.com/package/expect): Librería de aserciones que nos permite redactar test BDD del tipo: `expect(object).toBe(value, [message])`

Para instalarlos como dependencias de desarrollo haremos:

```
$npm install babel expect --save-dev
```

Una vez instalados estos paquetes configuraremos nuestro entorno con un script de NodeJS que nos permita lanzar todos nuestros test escribiendo:

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

Como convención a los archivos JS que contienen tests se les añade `Spec.js`o como en este caso: `_test.js`. En definitiva se trata de crear un *namespace* que nos permita diferenciar los test del código fuente de forma visual y en caso de ser necesario, podemos crear una expresión regular para ejecutar los test sólo a los archivos que correspondan con el *namespace* indicado.

### Escribiendo tests

Dada la estructura anterior, escribiremos los test en el archivo `numbers_test.js` Empezamos creando la descripción de la *Suite* de testing mediante **Describe**:

```
describe('Given two numbers', function(){
 (...)
  })
```
**describe** es una función que acepta dos parámetros:

- El Primero es una string que describe la principal acción del test. En este caso es: 'Dados dos números...' (Ahora veremos que hacemos con ellos...)
- El segundo es una función en la que tenemos que escribir qué es lo que ha de hacer el test:

```
describe('Given two numbers', function(){
  it('returns the biggest when is b', function(){
    var a = 10;
    var b = 20;
    expect(getBigger(a,b)).toBe(b);
  })
```

Para ello usaremos **it**. También se trata de una función que acepta otros dos parámetros, el primero es otra string con la descripción exacta de lo que haremos con esos dos números y la segunda es otra función que contiene el test definido en **expect**.

En este sencillo caso nuestra *espectativa* es que dados dos valores (var a = 10 y var b = 20) la función a testear llamada `getBigger()`nos diga que **b** es el valor mayor.

### Gestionando dependencias con ES6

Ya que tenemos *Babel* instalado vamos a sacarle partido importando y exportando las funciones que queremos testear y las librerías necesarias para ejecutar el entorno de testing al estilo **ES6**.

En la cabecera de nuestro archivo de test `numbers_test.js` escribiremos:

```
import expect from 'expect';
import {getBigger} from '../src/numbers_01.js';
```
En la primera línea indicamos que queremos cargar la librería *expect* de la carpeta *node_modules/expect*. Fijaros que no es necesario indicar la ruta exacta.

En la segunda línea, importamos la función getBigger del archivo fuente *numbers_01.js* situado en la carpeta *src*. Al importar un objeto podemos incluir múltiples funciones.

### Escribiendo el código a testear

Una vez que tenemos el test



### Reporters









<div class="referencias">
  <p><strong>Bibliografía:</strong></p>
  
  <p>BDD for JS: <br />
  <a href="https://jaxenter.com/behaviour-driven-development-for-javascript-part-one-107588.html">It's not about testing</a></p>
  
</div>