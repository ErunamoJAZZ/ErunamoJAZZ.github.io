---
title:  "Scala, Orientado a objetos"
date:   2016-06-24 12:00:00
categories:
    - Scala
---
# Orientado a objetos

La gran mayoría de programadores de habla hispana conoce o trabaja en su día a día con **Java**, ya que es uno de los lenguajes de programación que todas las universidades como mínimo enseñan.

Además, con plataformas como _Android_, el incentivo para aprenderlo no ha menguado con los años.

Por funcionar sobre la **Java Virtual Machine** (JVM), Scala mantiene compatibilidad con muchos de los principios de _Programación Orientada a Objetos_ de Java, **pero a su modo**.


## Types

Para empezar, el tipo de dato "padre" de todos los objetos en scala es el tipo  `Any`, y de este también se separa `AnyValue`. También está el tipo de dato  `Nothing`.

Estos tipos de dato van mostrando hasta cierto punto una diferenciación sustancial respecto al estilo objetual de Java, encaminadolo a un estilo de programación funcional.

En Scala los tipos de dato básicos son objetos también, y empiezan con su primer letra en mayúscula:  `Int`,  `Short`,  `Float`, `Double`,  
`Boolean`,  `Byte`, etc. Internamente el compilador es capaz de analizar estos tipos de dato y usar el bytecode más eficiente para cada caso.

En Scala las _clases_ y _clases abstractas_ funcionan casi igual que en Java (quizás se vean más similares a las clases de python), pero además incluye más formas.


## Objects

Cuando una clase va a ser o debe ser instanciada una sola vez, en vez de declararla como clase, se puede declarar directamente como objeto:

```scala
// Un ejemplo de ello, sería el main
object aplicacion {
  def main = {
    println("Hola, mundo")
  }
}
```

Esta es una implementación a nivel del lenguaje del patrón de diseño _Singleton_.


## Traits

Todos los lenguajes de programación orientados a objetos tienen un mecanismo para programar _comportamientos_ que pueden ser usados por otras clases, generalmente esto se conocen como *mixins*. En Java las interfaces cumplen esta función; en otros lenguajes como Swift, se tienen los _protocolos_. En Scala existen los `trait` para ello.

Los *trait* pueden contener funciones implementadas o sin implementar, y pueden heredarse muchas, y en caso de existir ambigüedades hay reglas que le dan prioridad a un trait sobre otro.


### Resumen

Esta es solo una vista general de las diferencias notorias respecto a Java en su visión objetual. Hay muchos más detalles, pero son cosas que poco a poco se pueden ir notando.