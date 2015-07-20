---
layout: post
title:  "TDD en Javascript con NodeJS y Mocha"
date:   2015-07-19 23:00:00
categories: node TDD ES6 Mocha
tags: opinion
image: /assets/article_images/cover-tdd.jpg
comments: true
---

### Test Driven Development

La primera vez que oí hablar sobre cómo testear código de forma automatizada; es decir, escribiendo más código con una sintaxis específica etc.. , me pareció que se añadía una capa de complejidad que difícilmente se vería compensada. Una vez que lo pruebas te das cuenta de la importancia que tiene *apuntalar* nuestro código con una batería de test automáticos que nos garanticen que cada función va hacer lo que teníamos pensado que hiciera. 

Las ventajas de usar TDD no sólo afectan a la estabilidad del código en sí. Además nos va a permitir **conceptualizar y diseñar** de forma más eficiente cada una de las funcionalidades de nuestra aplicación.

El flujo para desarrollar software basado en **TDD** es el siguiente:

- Escribimos la especificación del test.
- Escribimos el código para que pase el test.
- Si falla, refactorizamos el código hasta que pase el test.

Podemos ver este proceso en la siguiente gráfica:

![TDD](/assets/images/tdd-cycle-around.png)

Más abajo os pongo un ejemplo práctico de cómo llevar a cabo este proceso.

### Mocha
Si queremos poner en práctica todo esto, lo primero que haremos es *setear* un entorno de testing. En este post os hablaré de [Mocha](http://mochajs.org) corriendo sobre NodeJS, de modo que entiendo que tenéis NodeJS instalado.

Mocha es una *Testing Suite* altamente configurable. Podemos especificar diferentes librerías de aserciones como por ejemplo [chai](http://chaijs.com/) o [expect.js](https://github.com/LearnBoost/expect.js). Estas librerías definen cómo vamos a escribir nuestros test. Para este ejemplo usaré *expect.js*. Personalmente me gusta porque su sintaxis hace especialmente fácil declarar el qué ha de hacer el test y el cómo ha de pasarlo.

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
- [Expect](https://www.npmjs.com/package/expect): Librería de aserciones que nos permite redactar test TDD del tipo: `expect(object).toBe(value, [message])`

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

Ahora crearemos un test de ejemplo:

![DarthTesting](/assets/images/DarthTesting.png)

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

Si queréis ver un listado completo de todo lo que podemos hacer con *expect* os recomiendo visitar la documentación del API en su [repo](https://github.com/Automattic/expect.js).

### Gestionando dependencias con ES6

Ya que tenemos *Babel* instalado vamos a sacarle partido importando y exportando las funciones que queremos testear y las librerías necesarias para ejecutar el entorno de testing al estilo **ES6**.

En la cabecera de nuestro archivo de test `numbers_test.js` escribiremos:

```
import expect from 'expect';
import {getBigger} from '../src/numbers_01.js';
```
En la primera línea indicamos que queremos cargar la librería *expect* de la carpeta *node_modules/expect*. Fijaros que no es necesario indicar la ruta exacta.

En la segunda línea, importamos la función *getBigger* del archivo fuente *numbers_01.js* situado en la carpeta *src*. Al importar un objeto podemos incluir múltiples funciones separadas por comas. Ejem: {getBigger, getSmaller}.

### Escribiendo el código a testear

**Una vez que tenemos definido el test con lo que ha de hacer nuestra aplicación empezamos a crear el código que permita pasar ese test.**

Esta es la base del TDD. Es importante destacar que primero escribimos el test y luego el código que lo pasa. Sólo sería correcto hacerlo al revés en el caso de estar refactorizando código *legacy*.

En el archivo situado en `../src/numbers_01.js`escribimos la función que ha de obtener lo especificado en nuestro test:
- Given two numbers, returns the biggest.

```
const getBigger = (a, b) =>  a > b ? a : b;
```
La siguiente *function expression* retorna **a** si se da la condición **a > b** o **b** en caso contrario.

Al utilizar una [ternaria](https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Conditional_Operator) con la sintaxis de ES6 queda super-simplificado. Quizás no es tan *verbose* como la versión correspondiente de JS en ES5 pero es fácil acostumbrarse. Veamos como quedaría en ES5:

```
var getBigger = function(a, b){
   return a > b
   ? a
   : b;
}
```
Una característica a destacar es la asignación de la función a una constante. De esta forma la dotamos de inmutabilidad. Puedes consultar el [post anterior](http://davecarter.me/scope-de-variables/) en el que hablo sobre las nuevas variables en ES6.

Finalmente, exportamos la función mediante export para que sea accesible:

```
export default {getBigger}
```

### Reporters

Como comentaba anteriormente, el hecho de que Mocha sea una *Suite* de testing nos permite además indicar como queremos que nos muestre los resultados: En consola, en un navegador web, en la consola JS de un navegador web, generando un archivo JSON, etc.. De esto precisamente se encargan los *reporters*

Mocha usa por defecto la salida por terminal con el formato `spec`.  Este es un ejemplo de iTerm:

![reporter](/assets/images/reporters.png)

Dependiendo del número de test que tengamos puede interesarnos un formato más reducido u otro. Incluso podemos decirle a Nyan Cat que nos diga cómo ha ido la cosa :) Si quieres probarlo añade esta línea al archivo `package.json`del ejemplo:

```
"test": "mocha --compilers js:babel/register --reporter nyan"
```

### Conclusiones

El TDD es una herramienta importante a la hora de crear código estable y de calidad. Te puede gustar más un sistema u otro pero es indudable que como humanos que cometemos fallos con facilidad podamos acotarlos de alguna manera e incluso llegar a eliminarlos por completo.

Si te ha gustado esta entrada y la has encontrado útil, puedes dejar un comentario o ayudarme a difundirlo.


<div class="referencias">
  <p><strong>Bibliografía:</strong></p>

  <p>Mocha Wiki: <br />
  <a href="https://github.com/mochajs/mocha/wiki">All `bout Mocha</a></p>
  
  <p>TDD for JS: <br />
  <a href="https://jaxenter.com/behaviour-driven-development-for-javascript-part-one-107588.html">It's not about testing</a></p>

<p>MDN<br />
<a href="https://developer.mozilla.org/es/docs/Web/JavaScript/Reference/Operators/Conditional_Operator">Conditional Ternary operator</a></p>
  
</div>