---
title:  "Scala, Expresiones"
date:   2016-06-24 10:00:00
categories:
    - Scala
---
# Expresiones

Al momento de aprender un lenguaje de programación, asignar variables es de lo más básico que se debe conocer.

Sin embargo, esto en Scala tiene una particularidad: existen 3 formas para declarar **expresiones** 

1. Declarar la expresión como una **variable**, implicando que lo que se asigne allí puede cambiar (es mutable).
Esto se hace con `var`.
2. Declarar la expresión como un **valor**, implicando que no puede cambiar (es inmutable).
Se hace con `val`.
3. Declarar la expresión como una **función**, implicando que se ejecutará la asignación de ese recurso cuando se llame.
Se hace con `def`.

En resumen:

```scala
var a = 5
a = 4     // variable

val b = 5
val c = b // valor

def d = 5 // función
```

El último ejemplo es bastante trivial y no se logra apreciar el verdadero sentido de la declaración de funciones.

Una función, matemáticamente hablando, es una definición que recibe algo como entrada, lo transforma, y devuelve un resultado. 

```scala
def pow2(x: Int): Int = {
  x * x
}
```

Este ejemplo es de la definición de una función que aplica exponente a la 2 a un número. Las funciones pueden recibir otras funciones como argumento de entrada también (Esto se conoce como funciones de orden superior):

```scala
def runner(f: Int => Int, in: Int): Unit = {
  val out = f(in)
  println(s"Entró $in, y salió $out.")
}

runner( pow2, 5 )
```

(La  `s` al inicio del String en el  `println` es para permitir la interpolación, se usa para permitir escribir internamente con declaraciones hechas antes).

Muchas veces, aquellas funciones que son tan pequeñas y que son utilizadas como entrada de otras funciones pueden escribirse como funciones anónimas, en otros lenguajes se les conoce como lambdas:

```scala
runner( x => x * x, 5)
```

Dentro de un `class`, una función hace las veces de operador (usando la terminología de programación orientada a objetos).

A diferencia de otros lenguajes como JavaScript, C, o Java, en Scala la palabra `return` no es necesaria. El compilador asumirá que el valor final de la expresión es lo que debe retornar. Esto también implica que se debe ser explícito en los valores de retorno. Por ejemplo:

```scala
def miFuncion(x: Int) = {
  if(x < 0)
    true
}
```

¿Cual sería el tipo de dato que retorna esta función?, a simple vista, debería ser un tipo  `Boolean` , pero al no retornarse nada del lado del `else` no se puede asumir ningún tipo de dato. Esto nos obliga a tener que responder ante todas las posibilidades, este es un principio que también se usa en otro tipo de cosas como los `match`.

Es decir que la función debe quedar así:

```scala
def miFuncion(x: Int): Boolean = {
  if(x < 0)
    true
  else
    false
}
```

Aunque es un ejemplo algo forzado, la idea de tener que responder a todos los posibles caminos, hace que la definición de la función esté completa, o en términos más matemáticos, que sea una función "pura".

### Resumen
- Las expresiones pueden ser variables, valores, o funciones.
- Las funciones pueden pasarse como argumentos (funciones de orden superior).
- Scala permite escribir funciones anónimas.
- Las funciones deberían contemplar todos los posibles casos.

