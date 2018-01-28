---
title:  "Scala, Introducción a Play"
date:   2016-06-29 10:00:00
categories:
    - Scala
---
# Play Framework

Cuando se aprende un lenguaje de programación la mejor forma de interiorizarlo es practicando, una de las cosas prácticas que podemos programar con Scala son aplicaciones web, para ello hay varios frameworks, y quizás el más representativo es Play Framework.

Play es uno de los tantos "clones" de Ruby on Rails solo que pensado para el mundo de la JVM. Tiene api para ser usado con Java también, e internamente utiliza Akka dándole una potencia bastante grande en cuanto a la administración de recursos de la máquina.


## Servidor auto contenido

A diferencia del mundo Java, con Play no se necesita un _servidor de aplicaciones_ para funcionar, ya que internamente trae su propio servidor (basado en akka-http). De ciera forma es muy similar a como funcionan las aplicaciones en Node.js en ese aspecto.


## Concurrente por defecto

En Play, todas las peticiones son recibidas de forma asíncrona, de forma que con el mismo hardware, es capaz de recibir muchísima más carga que otros frameworks más tradicionales en Java, sin complicar el desarrollo.


## Documentacion

Algo que tiene de bueno es que la documentación de Play es muy completa, siendo suficiente para aprender.

https://www.playframework.com/documentation/