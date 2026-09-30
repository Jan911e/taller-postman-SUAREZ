# Hallazgos

## Fase 2 — Experimentación con JSONPlaceholder

La API utilizada durante el taller fue JSONPlaceholder:

`https://jsonplaceholder.typicode.com`

La siguiente tabla resume las peticiones realizadas.

| # | Petición        | Código esperado | Código obtenido | ¿Coincide? |
| - | --------------- | --------------: | --------------: | ---------- |
| 1 | GET /posts/1    |             200 |             200 | Sí         |
| 2 | GET /posts      |             200 |             200 | Sí         |
| 3 | GET /posts/9999 |             404 |             404 | Sí         |
| 4 | POST /posts     |             201 |             201 | Sí         |
| 5 | PUT /posts/1    |             200 |             200 | Sí         |
| 6 | PATCH /posts/1  |             200 |             200 | Sí         |
| 7 | DELETE /posts/1 |             200 |             200 | Sí         |

## Tarea 4 — GET /posts/1

La petición utilizada fue:

`GET https://jsonplaceholder.typicode.com/posts/1`

El servidor respondió con código **200 OK**.

La respuesta corresponde a un único recurso, por lo que se obtuvo un elemento.

Los campos encontrados fueron:

* `userId`
* `id`
* `title`
* `body`

La respuesta representa una publicación específica.

Cuando se solicita un recurso individual, los criterios de aceptación se concentran en comprobar que el recurso exista, que la respuesta tenga el código esperado y que los campos necesarios estén presentes.

## Tarea 4 — GET /posts

La petición utilizada fue:

`GET https://jsonplaceholder.typicode.com/posts`

El servidor respondió con código **200 OK**.

La respuesta contiene una colección de publicaciones.

La colección contiene **100 elementos**.

Cada publicación contiene los siguientes campos:

* `userId`
* `id`
* `title`
* `body`

La diferencia principal respecto a `GET /posts/1` es que una petición solicita un recurso individual mientras que la otra solicita una colección completa.

Por esta razón, al probar una colección también es importante verificar la cantidad de elementos, además de comprobar la estructura de los objetos.

## Tarea 5 — GET /posts/9999

La petición utilizada fue:

`GET https://jsonplaceholder.typicode.com/posts/9999`

El código esperado era:

**404 Not Found**

El código obtenido fue:

**404 Not Found**

Por lo tanto, el caso de prueba **pasó**.

Aunque 404 normalmente representa un error HTTP, en este caso era exactamente el resultado esperado porque se estaba solicitando un recurso inexistente.

Si la petición hubiera devuelto 200 con un cuerpo vacío, el resultado no coincidiría con el comportamiento esperado. Por lo tanto, se debería considerar un posible defecto y analizar la respuesta para determinar exactamente qué está ocurriendo.

## Tarea 6 — POST /posts

Para realizar la creación se utilizó:

`POST https://jsonplaceholder.typicode.com/posts`

Con el siguiente cuerpo:

```json
{
  "title": "Mi primera prueba",
  "body": "Taller de Ingeniería de Software II",
  "userId": 1
}
```

El código esperado fue **201 Created**.

Al ejecutar la petición varias veces, JSONPlaceholder devuelve respuestas simulando la creación del recurso.

Los resultados observados permiten comprobar que POST se utiliza para realizar operaciones de creación.

Una característica importante de JSONPlaceholder es que se trata de una API de prueba, por lo que las operaciones de escritura son simuladas y no representan necesariamente una persistencia real de los datos.

En una API real, para comprobar que un recurso se creó realmente se podría realizar posteriormente una petición GET al recurso creado y comprobar que existe y contiene la información enviada.

## Tarea 7 — PUT /posts/1

La petición utilizada fue:

`PUT https://jsonplaceholder.typicode.com/posts/1`

Cuerpo enviado:

```json
{
  "title": "Mi primera prueba"
}
```

El código esperado fue **200 OK**.

PUT representa una actualización del recurso y conceptualmente se utiliza para reemplazar o actualizar una representación completa del recurso.

## Tarea 7 — PATCH /posts/1

La petición utilizada fue:

`PATCH https://jsonplaceholder.typicode.com/posts/1`

Cuerpo enviado:

```json
{
  "title": "Mi primera prueba"
}
```

El código esperado fue **200 OK**.

PATCH está diseñado para realizar modificaciones parciales sobre un recurso.

La diferencia importante entre ambos métodos es que PATCH expresa explícitamente una modificación parcial, mientras que PUT se utiliza para reemplazar o establecer la representación del recurso.

Para corregir únicamente un error de escritura en el título, PATCH representa una actualización parcial porque solamente se necesita modificar un campo.

## Tarea 10 — Límite de publicaciones

Se realizaron peticiones incrementando el ID de las publicaciones.

El ID más alto que devuelve una respuesta exitosa es:

**100**

El primer ID que devuelve 404 es:

**101**

Esto permite establecer el límite de publicaciones disponibles en el recurso `/posts`.

El caso de prueba corresponde a una prueba de valores límite porque se está buscando la frontera entre un valor válido y uno inválido.

## Tarea 11 — Otros recursos

### `/users`

URL:

`https://jsonplaceholder.typicode.com/users`

Este recurso permite consultar usuarios.

Los objetos contienen información como:

* `id`
* `name`
* `username`
* `email`
* `address`
* `phone`
* `website`
* `company`

### `/comments`

URL:

`https://jsonplaceholder.typicode.com/comments`

Este recurso permite consultar comentarios.

Los objetos contienen:

* `postId`
* `id`
* `name`
* `email`
* `body`

### Ruta anidada

URL:

`https://jsonplaceholder.typicode.com/posts/1/comments`

Esta ruta permite obtener los comentarios relacionados con la publicación número 1.

La estructura de la URL se puede entender como:

`posts → publicación específica → comments`

Por lo tanto:

`/posts/1/comments`

significa los comentarios asociados a la publicación cuyo ID es 1.

## Tarea 13 — Pruebas automáticas

Se implementaron pruebas automáticas en Postman para comprobar diferentes características de la respuesta.

### Prueba 1 — Estado HTTP

```javascript
pm.test("El estado es 200", function () {
    pm.response.to.have.status(200);
});
```

**Verifica:** que el servidor responda con código HTTP 200.

### Prueba 2 — Campo `id`

```javascript
pm.test("La respuesta contiene el campo id", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("id");
});
```

**Verifica:** que el objeto JSON contenga el campo `id`.

### Prueba 3 — Tipo de `id`

```javascript
pm.test("El campo id es un número", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.id).to.be.a("number");
});
```

**Verifica:** que `id` sea un número.

### Prueba 4 — Campo `title`

```javascript
pm.test("La respuesta contiene el campo title", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("title");
});
```

**Verifica:** que la respuesta contenga el campo `title`.

## Resultado de las pruebas automáticas

Las pruebas permiten automatizar la verificación de la respuesta. En lugar de revisar manualmente cada característica, Postman ejecuta las comprobaciones y muestra cuáles pasan y cuáles fallan.

También se comprobó que una prueba puede fallar intencionalmente al cambiar el código esperado de 200 a 201. Esto demuestra que las pruebas automáticas están comparando realmente el resultado obtenido con el resultado esperado.
