---
title: Introducción a Postgraphile
date: 2018-09-20 19:13:41
tags:
  - PostgreSQL
  - Nodejs
  - RLS
  - GraphQL
  - Postgraphile
---
# Introducción a Postgraphile

[Postgraphile](https://www.graphile.org/postgraphile/) es una libreria para Node.js que permite generar un servidor de [GraphQL](https://graphql.org/) usando como base los elementos de un schema (tablas, vistas, procedimientos, funciones, etc) de una base de datos [PostgeSQL 9.6+](https://www.postgresql.org/download/).

En realidad, la forma más básica de probarlo es tan simple como instalar el `postgraphile` y ejecutar un:
```bash
$ postgraphile -c postgres://user:pass@host/dbname --schema schema_name
```
Pero vamos en orden.

## ¿Qué es GraphQL?
GraphQL viene siendo como una evolución de RESTful, en el sentido que su propósito es exponer como un API una variedad de recursos desde un servidor. Lo que lo hace diferente es la forma en que lo hace.

Estrictamente hablando, **GraphQL es un lenguaje de consulta**. Fue inventado por Facebook y su utilidad frente a REST radica en que le delega al lado del cliente, el escoger/consultar qué cosas requiere del API y en qué forma.

Así, en vez de solicitar un usuario desde una url como `GET /api/user/1`, con GraphQL solo tenemos un endpoint desde el que se hacen todas las consultas (generalmente `POST /graphql`, aunque el estándar permite un GET también). A este endpoint se le manda la consulta en el formato de GraphQL, que en el caso del usuario podría ser algo similar a:

```graphql
query {
  userById(id: 1) {
    id
    name
  }
}
```
Entonces, sin importar cuántos atributos tenga un usuario, o si se agregan o se cambian en el futuro, es el cliente quien escoge cuáles de esos campos necesita, y el servidor le responderá con el usuario y los atributos que se pidieron en la consulta, bastante cool cierto?

Pero GraphQL no solo sirve para hacer consultas (con el selector `query`), si no que permite también hacer mutaciones sobre los elementos que lo permitan, usando la palabra `mutation`.


## Clientes y Servidores de GraphQL
Dado que GraphQL es solo un lenguaje de consulta, en realidad hay muchas librerías que implementan el estándar. Particularmente las más famosas son Apollo y Relay, y se encuentran por un lado para la parte del cliente, donde hay para el navegador y más interesante aún para Android e iOS. Y desde el lado del servidor, hay muchas implementaciones para muchos lenguajes. Todos se pueden ver en la página de GraphQL: https://graphql.org/code/

La dificultad de implementar un servidor de GraphQL radica en que hay que escribir una buena cantidad de código para que al momento de ejecutar una consulta, el servidor sepa cómo consultar el recurso que se pide. Porque, hablando honestamente, implementar un servidor REST es bastante trivial hoy en día, pero hacer lo mismo con API de GraphQL, no es para nada trivial, ya que incluye el escribir también el llamado "Schema de GraphQL", que es una colección de los tipos de datos y su relación de los unos con los otros, también escribir los "resolvers", quienes se encargan de ir a buscar los datos como tal, etc.

Es aquí cuando Postgraphile entra en escena como una alternativa bastante práctica.


## Cómo funciona Postgraphile
Postgraphile hace una inspección del schema que le digamos, generando lo que comúnmente se conoce como "el CRUD de la aplicación". Es decir, que genera un Selector de todos los elementos, el selector para uno solo, y mutaciones para crearlos, actualizarlos, y eliminarlos. Además, si se desea crear funcionalidades especiales que no sean directamente de CRUD, Postgraphile genera entradas para procedimientos almacenados y funciones que uno escriba directamente.

¡Todo esto de forma automática!

Aún más impresionante, viene con un modo "watch", que detecta cuándo cambiamos algo en la base de datos para automáticamente refrescar el servidor con las modificaciones!

De esta manera, la promesa de valor que ofrece Postgraphile es:
- Solo hay que concentrarse en realizar un buen modelo de datos, para inmediatamente poder probarlo desde un cliente.
  Esto permite tiempos de desarrollo mucho más rápidos sobretodo cuando se hace un prototipo.
- La mayoría de la lógica recae en la base de datos, evitando el tener que repetir lógica de control en el backend y en la DB.
  Pero esto es igual discutible ya que eso no necesariamente significa que sea mejor o peor.

De igual forma, Postgraphile no solamente es bueno para hacer prototipos, también es lo suficientemente robusto como para considerarlo en ambientes de producción. Esto porque su esquema de seguridad está cimentado en el de la base de datos directamente haciendo uso del [Row Level Security](https://www.postgresql.org/docs/current/static/ddl-rowsecurity.html) de PostgreSQL, y porque ha sido [optimizado para soportar cargas considerablemente altas](https://medium.com/@Benjie/how-i-made-postgraphile-faster-than-prisma-graphql-server-in-8-hours-e66b4c511160).

Ah, y hay personas que llevan usándolo en producción un buen tiempo ya!

Si con todo esto no te has convencido o si por el contrario te emocioné con el asunto, de igual forma **[dale a PostGraphile una oportunidad de convencerte](https://www.graphile.org/postgraphile/)**, es realmente súper fácil darle una probada ahora mismo.

:)


### Siguientes artículos
Si leíste hasta acá, espero que hayas encontrado este artículo interesante. No suelo escribir mucho en mi blog, pero como todavía no hay mucha información sobre Postgraphile en español, me animé a hacer este artículo introductorio.

Mi intención en el futuro cercano es hacer más artículos sobre esta librería y sobre estos temas.

Si te gustó, me gustaría saber que lo leíste así que cualquier mention en twitter me va a llenar de ánimos para continuar escribiendo, ejejeje.


Peace!
