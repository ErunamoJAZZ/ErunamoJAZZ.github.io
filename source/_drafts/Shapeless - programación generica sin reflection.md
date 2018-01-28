---
title:  "Shapeless, programación genérica sin reflection"
date:   2016-08-04 10:00:00
categories:
    - Scala
---
Shapeles es una librería que implementa una gran cantidad de funcionalidades al rededor de una estructura llamada listas heterogéneas (HList)

Una lista heterogénea es una lista donde cada elemento contiene su propio tipo de dato.

Comparándolo con las listas normales, ellas solo pueden contener un tipo de dato, es decir, si dices que la lista es de números enteros `List[Int]` así se guarde un tipo distinto, al tratar de usarlo por defecto se casteará como un `Int`.

En cambio en una HList, al ser consciente del tipo de dato de cada elemento, permite guardar cualquier tipo de dato de forma explícita.

```
val myList = 1 :: "texto" :: HNil
```
Esta estructura en esencia simple, permite una gran flexibilidad cuando solucionamos problemas con ella, pudiendo usarse como alternativa a scala-reflect.

La primer parte complicada del asunto, es que al ser una lista, la forma de solucionar problemas con ella es con mucha programación funcional.
La otra parte complicada, es que además de ser una lista, es una lista tipada, por lo que manejar los tipos de la lista(que además, su tipo puede cambiar en el tiempo).

Aunque es un poco enredado en principio, es una de las librerías más interesantes en la comunidad de Scala.