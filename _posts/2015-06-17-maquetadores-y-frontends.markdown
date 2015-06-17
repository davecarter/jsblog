---
layout: post
title:  "Maquetadores y frontends"
date:   2015-06-17 23:00:00
categories: mediator feature
tags: opinion
image: /assets/article_images/2015-06-17-maquetadores-y-frontends/night-track.JPG
---

### Un poco de Historia:

En el diseño web han habido algunos momentos claves que han marcado un antes y un después. Para mi, la llegada de Google Chrome en [Septiembre del 2008](https://es.wikipedia.org/wiki/Google_Chrome#Historial_de_versiones) fue uno de esos momentos ya que no sólo presentó una interfaz minimalista que después han ido copiando el resto sino que además incorporaba un motor de javascript mucho más potente que Firefox, el Rey del Mambo de entonces y además no tragaba memoria de sistema como si no hubiera un mañana.

Casualmente, librerías como jQuery y frameworks como MooTools también empezaron por esa época. Estas dos piezas encajaban perfectamente con el pedazo de motor de javascript de Chrome llamado [V8](https://developers.google.com/v8/intro).


### iPhone killed the Flash star

A pesar del título un tanto chorra que me ha quedado, el lanzamiento del iPhone sin soporte a Flash provocó una estampida de developers que habíamos estado muchos años metidos a fulltime con `actionscript` hacia eso de los estándares web y ese nuevo HTML5 que lanzaron unos **reveldes** con nombre cool [WHATWG](https://en.wikipedia.org/wiki/WHATWG) y que además provocaron mucho *hype*...

### HTML5, Chrome con V8, jQuery... y además RWD!

A todo esto sólo faltaba darle una vuelta de tuerca al diseño fluido y hacerlo **responsive**. La primera vez que vi un diseño así pensé... [OMG! a double rainbow!!](https://www.youtube.com/watch?v=OQSNhk5ICTI) Ya sé lo que quiero ser de mayor!

### Maquetación CSS

El caso es que hasta la fecha, los frontends nos dedicábamos a ver quien era el que se sabía el bug más raro de IE6. Por necesidades corporativas, en el proyecto se especificaba: **Compatibilidad con IE6 y 1024px** y eso nos convirtió en auténticas béstias pardas del hackeo CSS... menudo waist!

### Javascript or die

Como ya no había Flash, las cosas guapas tipo *parallax* se hacían en JS. Personalmente, lo tenía 'un poco' abandonado... Reconozco que le pillé manía desde finales de la [Browsers War](https://en.wikipedia.org/wiki/Browser_wars) en la que si hacías algo en Javascript era sólo para Netscape. Si querías hacer lo mismo en IE4, o IE5, tenías que usar [JScript](https://es.wikipedia.org/wiki/JScript) de Microsoft. A pain in the ass..

### jQuery to the rescue? not really.

Menos mal que teníamos jQuery! Me ayudó a ser productivo y entregar trabajos con cierto profesionalismo como para poder emitir facturas a mis clientes y no sentirme mal por ello.

El problema es que el *gap* entre maquetación pura CSS y modificación del DOM en JS cada vez se iba haciendo mayor ya que no paraban de salir cosas incleíbles como SASS, los grids semánticos y el OOCSS, que irrumpieron con fuerza y consumían ingentes cantidades de tiempo libre y llenaban mi *reeder* de artículos *read later*

## Maquetadores CSS y Frontends JS

Actualmente, con la irrupción de los frameworks JS tipo Angular, Ember y sobretodo React; la librería JS que utiliza NodeJS para crear interfaces super-performantes, no concibo una separación de roles entre CSS y JS. 

Así que si en algún momento te has sentido identificado, tienes curiosidad o simplemente quieres aportar algo a mis avances en JS, [suscríbete a mi feed](http://davecarter.me/feed.xml) ya que de momento no tengo implementado un sistema de comentarios. Si quieres hacerlo tú mismo no dudes en solicitar una [pull request](https://github.com/davecarter/jsblog) :)