---
title:  "Scala, Introducción a Akka"
date:   2016-06-30 10:00:00
categories:
    - Scala
---
# Akka.io

Akka es un Framework para programación concurrente y distribuida escrito en Scala y compatible con Java.

Se conforma de dos módulos, el primero implementa la arquitectura de comunicación entre actores, el segundo hace lo suyo con el patrón Publicador-Suscriptor, mejor conocido como _Reactive Streams_.

Conceptualmente, un actor es un procesador de información independiente, que puede comunicarse con otros actores mediante mensajes. Como los actores consumen recursos limitados, si mientras ocupado procesando algo le llegan más mensajes, los guarda en un buzón de entrada hasta que esté disponible para procesarlos.

Además, los actores no necesitan estar en la misma máquina, pueden distribuirse en diferentes servidores, lo cual puede llegar a ser bastante potente dependiendo del problema que se esté solucionado.

Por otro lado, akka-streams, la implementación del patrón Publicador-Suscriptor, es compatible con el api de Reactive Streams, así que es interoperable con cualquier otro framework que lo implemente (como por ejemplo, RxJava).

Este patrón permite abstraer la forma de procesar datos de forma continua a medida que van llegando.

Akka puede usarse para crear aplicaciones distribuidas en diferentes infraestructuras, siendo ya usado para aplicaciones empresariales por compañías muy grandes (como empresas de seguros, hipermercados, etc), así como aplicaciones que requieren funcionar en tiempo real (algo básico en una aplicación moderna).


### Resumen

Esta es una breve introducción sobre Akka y sus posibilidades. En futuros post seguramente pondré más ejemplos y casos en los que lo he usado.
