# taller-postman-SUAREZ
# Taller de APIs y Pruebas con Postman

**Estudiante:** Jan Esteban Suarez Escobar
**Código:** 1114148846
**Asignatura:** Ingeniería de Software II  
**Institución:** Corporación de Estudios Tecnológicos del Norte del Valle — Cotecnova  

---

## Marco conceptual

Una **API REST** (*Representational State Transfer*) es un estilo de arquitectura de software utilizado para la comunicación e intercambio de información entre sistemas a través del protocolo HTTP. Que sea "REST" significa que la arquitectura no mantiene estado (*stateless*), lo que implica que cada petición del cliente contiene toda la información necesaria para ser procesada sin depender de sesiones almacenadas en el servidor.

* **Recurso:** Es cualquier entidad de datos o información que la API expone y que puede ser consultada, creada o manipulada (por ejemplo: un usuario, un producto, una publicación o un comentario).
* **Endpoint:** Es la dirección URL específica exposed por el servidor a la cual el cliente envía sus peticiones para interactuar con un recurso determinado (por ejemplo: `https://jsonplaceholder.typicode.com/posts`).

### Ejemplo cotidiano
Cuando utilizo la aplicación de **Spotify** en mi teléfono móvil, la app no almacena todas las canciones ni la biblioteca completa internamente en el dispositivo. Cada vez que busco un artista o reproduzco un álbum, la app realiza peticiones HTTP REST a la API de Spotify para obtener los metadatos de las canciones, imágenes de portada y enlaces de transmisión en tiempo real.

*Fuente consultada:* [MDN Web Docs - REST / APIs Web](https://developer.mozilla.org/es/docs/Glossary/REST)

---

## Métodos HTTP

| Método | Operación CRUD | Qué hace |
| :--- | :--- | :--- |
| **GET** | **R**ead (Leer) | Consulta y recupera la información de uno o varios recursos del servidor sin modificar el estado del sistema. |
| **POST** | **C**reate (Crear) | Envía datos en el cuerpo de la petición para crear un nuevo recurso en el servidor. |
| **PUT** | **U**pdate (Actualizar) | Reemplaza **completamente** la representación del recurso existente en el servidor con los nuevos datos enviados. |
| **PATCH** | **U**pdate (Actualizar) | Aplica modificaciones **parciales** a un recurso existente, alterando únicamente los campos enviados sin afectar los demás. |
| **DELETE** | **D**elete (Eliminar) | Elimina un recurso específico identificado por su URL en el servidor. |

---

## Códigos de estado

Los códigos de estado HTTP indican el resultado de una petición realizada al servidor y se agrupan en cinco familias según su primer dígito:

1. **1xx (Informativos):** Indican que la petición fue recibida por el servidor y el proceso continúa.  
   *Ejemplo:* `100 Continue` (el cliente debe continuar con la solicitud).
2. **2xx (Éxito):** Indican que la acción solicitada fue recibida, entendida y procesada correctamente.  
   *Ejemplo:* `200 OK` (petición exitosa) o `201 Created` (recurso creado con éxito).
3. **3xx (Redirección):** Indican que el cliente debe realizar acciones adicionales o redirigirse a otra ubicación para completar la solicitud.  
   *Ejemplo:* `301 Moved Permanently` (el recurso cambió de dirección de forma permanente).
4. **4xx (Errores del Cliente):** Indican que la solicitud contiene sintaxis errónea, faltan parámetros, o no se puede procesar por responsabilidad del cliente.  
   *Ejemplo:* `404 Not Found` (el recurso solicitado no existe) o `401 Unauthorized` (falta autenticación).
5. **5xx (Errores del Servidor):** Indican que el servidor falló o sufrió una excepción interna al intentar procesar una petición aparentemente válida.  
   *Ejemplo:* `500 Internal Server Error` (fallo interno o error de código en el backend) o `503 Service Unavailable` (servidor sobrecargado o en mantenimiento).

### Separación entre errores 4xx y 5xx: ¿Quién tiene la culpa?
La distinción entre estas dos familias radica en la **asignación de la responsabilidad del fallo**:

* **Errores 4xx (Responsabilidad del Cliente):** El cliente envió una solicitud defectuosa (una URL mal escrita, parámetros incompletos, datos en un formato JSON inválido o sin las credenciales necesarias). La solución requiere que la persona o sistema que realiza la petición la corrija antes de volver a enviarla.
* **Errores 5xx (Responsabilidad del Servidor):** La petición enviada por el cliente estaba perfectamente formulada, pero el servidor sufrió un colapso interno, fallo de conexión con la base de datos, error de sintaxis en el código backend o falta de memoria. La solución requiere intervención técnica en la infraestructura o en el código del servidor por parte del equipo de desarrollo.

---

## Cómo reproducir este taller

Para ejecutar e inspeccionar las pruebas realizadas en este proyecto desde Postman, sigue estos pasos:

1. **Clonar el repositorio localmente:**
   ```bash
   git clone [https://github.com/](https://github.com/)Jane911/taller-postman-SUAREZ.git
   cd taller-postman-SUAREZ
