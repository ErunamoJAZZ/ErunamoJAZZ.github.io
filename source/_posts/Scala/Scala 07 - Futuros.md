---
title:  "Scala, Futuros"
date:   2016-07-02 10:00:00
categories:
    - Scala
---
# Futuros

La mayoría de los programas que se escriben cuando uno aprende a programar, son muy sencillos y tienen flujos de procesamiento bien definidos y cortos que no importa si demoran mucho o poco, pero en aplicaciones del mundo real no siempre es así, ya que el tiempo de respuesta y los recursos de la máquina son valiosos y deberían aprovecharse lo máximo posible.

Aquí es cuando entra el concepto de programación asíncrona, es decir, programar porciones de código que no bloquean el curso del programa y que se ejecutan solo cuando sus prerrequisitos están listos.

La forma de hacer esto, es haciendo que éste código se ejecute en un hilo de procesamiento independiente del que lo llamó. Todos los lenguajes tienen métodos para crear nuevos hilos, pero manejar estos hilos puede llegar a ser muy engorroso, ya que hay que cuidar una cantidad de posibles problemas (condiciones de carrera, acceso a recursos compartidos, _loop death_, etc).


## scala.concurrent

Afortunadamente, Scala tiene un api que simplifica completamente esto. `scala.concurrent.Future` es la implementación de lo que en otros lenguajes se conoce como promesas: un envoltorio que encapsula un resultado futuro.

Un ejemplo trivial sería este:
```scala
val myNumber = Future(5)
```
Los futuros pueden estar en uno de tres estados:

1. Puede no haberse completado.
2. Puede ya estar completo.
3. Puede haber fallado.

Un futuro no bloquea el curso del programa, cualquier instrucción que le siga se ejecutará. Así que para hacer algo útil con el resultado de un futuro, debemos indicar qué debe de ejecutarse una vez se complete. Eso se hace con la función `.map`.
```scala
val newFuture = myNumber.map{ x =>
  x * 2
}
```
Los futuros tienen comportamiento monádico (hasta cierto punto), por lo que puede hacerse todo lo que una monada permite, se pueden componer, filtrar, mapear, etc.

## Rendimiento

Entrando a las tripas de cómo funcionan los futuros internamente, usualmente surgen dudas respecto al rendimiento, ya que es sabido que crear nuevos hilos es un proceso costoso.
Al momento de crear un futuro, se requiere un **contexto de ejecución**. 
Un contexto de ejecución es básicamente un administrador de los hilos que pueden ejecutar futuros, de esta forma, el futuro no tiene que crear su propio hilo si no que usa alguno de los "espacios disponibles" que le provee el contexto.
Así que es el contexto el responsable de comunicar el resultado de un futuro con el siguiente proceso, etc.

Por defecto podemos usar un contexto de ejecución _global_, que para el tiempo de desarrollo suele estar bien. Aunque es mala práctica usarlo en aplicaciones de producción, es mejor explícitamente declarar nuestros propios contextos de ejecución, lo cual tampoco es difícil.

### Resumen

Esta es una pequeña introducción para saber de qué van los Futuros y la programación asíncrona en Scala. En realidad hay mucha tela para cortar con este tema, pero eso lo haré en otros posts.


