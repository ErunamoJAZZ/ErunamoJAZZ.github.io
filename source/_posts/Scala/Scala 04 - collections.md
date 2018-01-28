---
title:  "Scala, Collections"
date:   2016-06-28 10:00:00
categories:
    - Scala
---
# Collections

Una colección es básicamente un conjunto de "cosas", dependiendo del tipo de colección, puede que el orden de las cosas que contenga sea importante, o que no se permitan repetidos, o que tengan una etiqueta que los identifique, etc.

Esta forma de expresar datos es de las más elementales cuando hablamos de programación funcional, casi todo se puede expresar como una _monada_, pero conceptos como este, son también algo de lo que no hay que preocuparse mucho al inicio ya que se van aprendiendo en el camino.

Quiero empezar con las listas. 


## Listas

Desde el punto de vista funcional, una lista es algo que tiene una cabeza (*head*) y una cola (*tail*), y que puede contener cualquier cosa, incluyendo otra lista, que a su vez puede tener otra lista que a su vez... y que puede también tener una lista vacía!

Aunque claro, una lista de este estilo se vería como algo así:

```scheme
miLista = (a, (b, (c, (d, (e, Nil)))))
```

En lenguajes como _Scheme_ esa cantidad de paréntesis son el pan de cada día. En otros lenguajes, para recorrer una lista hace falta usar una estructura externa (casi siempre un `for`). Pero en lenguajes funcionales la forma natural de hacerlo es mediante un método interno que aplicar una función a todos los elementos. 

En Scala se usa para ello el método `.map`, que recibe una función como parámetro (recordar que las funciones son expresiones en Scala)... solo leyendo puede sonar extraño, poniéndolo en código se vería así:

```scala
val miLista = List(1, 2, 3, 4, 5)        // Se declara una lista
val nuevaLista = miLista.map{ item =>    // Se de clara una función anónima
  item * item                            //  que multiplica el item.
}
```

El método `.map` recibe una función como argumento, una función anónima en este caso, la cual aplica a toda la lista, y retorna una **nueva lista** como resultado.


## Inmutabilidad

Otra cosa interesante para notar es que todo se está declarando como un **valor** (es decir, inmutable). En principio puede parecer mala idea tener que declarar una expresión que no se puede sobre escribir por cada sentencia que escribamos en nuestro algoritmo, pero hacerlo de esta forma tiene **grandes ventajas**.

La primer ventaja es que de esta forma aseguramos la **integridad** de los datos, ya que no habrá posibilidad de que se modifique el contenido en ninguna parte, con lo que se induce a evitar una gran cantidad de errores.

Esto además **simplifica** enormemente la programación en **diferentes hilos**. Así no hay que preocuparse de condiciones de carrera por acceso a variables que están siendo usadas por diferentes hilos a la vez!

La otra ventaja que trae, es que al evitar el uso de variables nos obligará a pensar de forma diferente el cómo abordar un problema. Un ejemplo (trivial) sería este:

```scala
var x: Boolean
if(h % 2 == 0)
  x = true
else 
  x = false
```

¿cómo evitar el uso de la variable?, como los `if` devuelven **expresiones**, podemos hacer esto:

```scala
val x: Boolean = if(h % 2 == 0) true else false
```

Es un ejemplo muy sencillo, pero que ilustra una forma más elegante de abordar el mismo problema.


## Rendimiento

¿Y qué pasa con el rendimiento?, ¿esto no hace menos óptimos los algoritmos?. Un amigo una vez hizo la comparación entre el mismo algoritmo escrito en C++ vs Scala, y este último fue más rápido, incluso sin usar paralelismo. No quedé con el código que él hizo, así que desconozco cualquier detalle de la implementación, sin embargo eso muestra que el uso de inmutabilidad tiene más beneficios que problemática.


### Resumen
De facto, las colecciones tienen una gran cantidad de métodos por defecto, además de `map()`, se puede filtrar y ordenar, etc.

Para más información, recomiendo esta página de twitter donde se explica detalladamente todo acerca de las colecciones:
https://twitter.github.io/scala_school/collections.html

