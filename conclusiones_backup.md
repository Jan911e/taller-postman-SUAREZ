# Conclusiones

## Tarea 8 — Idempotencia

La idempotencia significa que ejecutar varias veces una misma operación produce el mismo efecto final que ejecutarla una sola vez.

En los métodos utilizados durante el taller, GET, PUT y DELETE son métodos idempotentes. POST no es idempotente porque cada ejecución puede representar una nueva creación de un recurso. PATCH puede ser idempotente dependiendo de la operación específica que realice.

Al realizar varias veces una petición PUT sobre el mismo recurso, el recurso termina con los mismos valores establecidos por la petición. En cambio, al ejecutar varias veces POST, cada petición de creación puede producir un nuevo resultado.

La diferencia permite observar que la idempotencia está relacionada con el efecto que tienen las peticiones cuando se repiten.

## Tarea 9 — Cabeceras de la respuesta

Las cabeceras HTTP proporcionan información adicional sobre la respuesta que entrega el servidor.

### Content-Type

La cabecera `Content-Type` indica el tipo de contenido que contiene el cuerpo de la respuesta. En las respuestas de JSONPlaceholder se utiliza para indicar que la información se entrega en formato JSON.

Esta cabecera es importante al probar una API porque permite saber cómo debe interpretarse el contenido recibido.

### Content-Length

La cabecera `Content-Length` indica el tamaño del contenido enviado en la respuesta.

Esta información puede ser útil para conocer cuánto contenido está siendo transferido entre el servidor y el cliente.

### Date

La cabecera `Date` indica la fecha y hora en la que el servidor generó la respuesta.

Permite conocer cuándo fue producida la respuesta y puede ser útil para analizar comunicaciones entre el cliente y el servidor.

## Tarea 10 — Límite de publicaciones

Para encontrar el límite de publicaciones se pueden realizar peticiones cambiando progresivamente el ID.

El último ID que devuelve una respuesta exitosa es:

**100**

El primer ID que devuelve 404 es:

**101**

Esto permite identificar el límite entre un recurso existente y uno que no existe.

Este tipo de prueba se conoce como **prueba de valores límite**. Consiste en comprobar los valores que se encuentran en los extremos de un rango válido.

Los defectos pueden concentrarse en los límites porque un sistema puede comportarse correctamente con valores normales y presentar problemas cuando se utilizan valores que están justo en el límite permitido o inmediatamente fuera de él.

## Tarea 11 — Exploración de otros recursos

Además del recurso `/posts`, JSONPlaceholder dispone de otros recursos.

### Recurso `/users`

La ruta:

`https://jsonplaceholder.typicode.com/users`

permite consultar usuarios.

Los elementos contienen información relacionada con los usuarios, como su identificación, nombre, nombre de usuario, correo electrónico y otros datos.

### Recurso `/comments`

La ruta:

`https://jsonplaceholder.typicode.com/comments`

permite consultar comentarios.

Los comentarios tienen campos como `postId`, `id`, `name`, `email` y `body`.

### Ruta anidada

También se puede utilizar una ruta como:

`https://jsonplaceholder.typicode.com/posts/1/comments`

Esta ruta permite consultar los comentarios relacionados con la publicación cuyo ID es 1.

La estructura se puede deducir observando que `/posts` representa el recurso principal y que `/posts/1/comments` relaciona los comentarios con una publicación específica.

## Tarea 12 — Primera prueba automática

La primera prueba automática utilizada fue:

```javascript
pm.test("El estado es 200", function () {
    pm.response.to.have.status(200);
});
```

Esta prueba verifica que la respuesta de la petición tenga código de estado HTTP 200.

Al cambiar el valor esperado de 200 a 201, la prueba falla porque la respuesta real continúa siendo 200. Esto demuestra que una prueba automática puede detectar cuando el resultado obtenido no coincide con el resultado esperado.

Es importante observar una prueba fallar antes de confiar en ella porque una prueba que nunca ha demostrado detectar un resultado incorrecto podría estar mal configurada.

## Tarea 13 — Pruebas automáticas adicionales

### Prueba 1 — Existencia del campo `id`

```javascript
pm.test("La respuesta contiene el campo id", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("id");
});
```

Esta prueba verifica que la respuesta contenga el campo `id`.

### Prueba 2 — Tipo de dato de `id`

```javascript
pm.test("El campo id es un número", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData.id).to.be.a("number");
});
```

Esta prueba verifica que el campo `id` tenga un valor de tipo numérico.

### Prueba 3 — Existencia del campo `title`

```javascript
pm.test("La respuesta contiene el campo title", function () {
    const jsonData = pm.response.json();
    pm.expect(jsonData).to.have.property("title");
});
```

Esta prueba verifica que el recurso obtenido contenga el campo `title`.

## Pregunta final 1 — Plan de pruebas formal

La tabla utilizada durante el taller contiene la petición, el código esperado, el código obtenido y si ambos coinciden.

Para convertirse en un plan de pruebas formal tendría que incluir información adicional como el identificador del caso de prueba, objetivo, precondiciones, datos de entrada, pasos para ejecutar la prueba, resultado esperado, resultado obtenido, estado de la prueba y evidencia.

De esta manera, otra persona podría reproducir las pruebas siguiendo un procedimiento definido.

## Pregunta final 2 — ¿Por qué un 404 puede ser una buena noticia y un 200 puede ser un defecto?

Un código de estado HTTP no determina por sí mismo si una prueba pasó o falló.

La prueba debe compararse con el resultado esperado.

Por ejemplo, cuando se solicita:

`GET /posts/9999`

se está solicitando un recurso que no existe. Por eso se espera un código 404. Si la API devuelve 404, el caso de prueba pasa porque el resultado obtenido coincide con el resultado esperado.

En cambio, si esa misma petición devuelve 200, podría existir un defecto porque la API estaría indicando que la solicitud fue procesada correctamente cuando el recurso solicitado no existe.

Por lo tanto, un 404 puede representar un resultado correcto y esperado, mientras que un 200 puede representar un defecto dependiendo del comportamiento que se esperaba de la API.

## Conclusión general

El desarrollo del taller permitió comprobar que probar una API no consiste solamente en enviar peticiones y observar si aparece un código 200. Es necesario definir previamente qué resultado se espera, ejecutar la petición, comparar el resultado obtenido con el esperado y documentar las diferencias.

También se pudo observar la importancia de diferenciar los métodos HTTP, comprender los códigos de estado, reconocer la diferencia entre PUT y PATCH, analizar la idempotencia y utilizar pruebas automáticas para verificar las respuestas.
