---
description: Métodos de petición
---

# GET y POST

Para enviar ciertos tipos de información al servidor, el protocolo HTTP provee diferentes **métodos de petición**. Los dos más importantes son GET y POST, los cuales, aunque entregan los mismos resultados, revelan algunas diferencias entre ellos. Lee a continuación cuáles son estas diferencias y cuándo conviene utilizar uno u otro.

### GET

Con el método GET, los datos que se envían al servidor **se escriben en la misma dirección URL**. En la ventana del navegador, lo encontrarás así:

```url
www.ejemplo.com/index.htm?key1=value1&key2=value2&key3=value3...
```

* El método GET envía la información en la propia URL, estando limitada a 2000 caracteres.
* La información es visible por lo que con este método nunca se envía **información sensible**.
* No se pueden enviar **datos binarios** (archivos, imágenes...).

#### Ventajas de GET

Los parámetros URL se pueden **guardar junto a la dirección URL como marcador**. De esta manera, puedes introducir una búsqueda y más tarde consultarla de nuevo fácilmente. También se puede volver a acceder a la página a través del historial del navegador.

Esto resulta práctico, por ejemplo, si visitas con asiduidad un mismo lugar en Google Maps o si guardas páginas web con configuraciones de filtro determinadas.

#### Desventajas de GET

La mayor desventaja del método GET es su **débilprotección de los datos**. Los parámetros URL que se envían quedan visibles en la barra de direcciones del navegador y son accesibles sin clave en el historial de navegación, en el caché y en el _log_ de los servidores.

Otra desventaja es que su **capacidad es limitada**: dependiendo del servidor y del navegador, no es posible introducir más de 2000 caracteres. Además, los parámetros URL solo pueden contener caracteres ASCII (letras, números, signos, etc.) y no datos binarios como archivos de audio o imágenes.

### POST

Con el método **HTTP POST** también se codifica la información, pero ésta se envía a través del **body** del **HTTP Request**, por lo que no aparece en la URL.

* El método POST no tiene **límite de cantidad de información** a enviar.
* La información proporcionada no es visible, por lo que se puede enviar **información sensible**.
* Se puede usar para enviar **texto normal** así como **datos binarios** (archivos, imágenes...).

#### Ventajas de POST

En lo relativo a los datos, como, por ejemplo, al rellenar formularios con nombres de usuario y contraseñas, el método POST ofrece mucha **discreción**. Los datos no se muestran en el caché ni tampoco en el historial de navegación. La **flexibilidad** del método POST también resulta muy útil: no solo se pueden enviar textos cortos, sino también otros tipos de información, como fotos o vídeos.

#### Desventajas de POST

Cuando una página web que contiene un formulario se actualiza (por ejemplo, cuando se retrocede a la página anterior) **los datos del formulario debentransferirse de nuevo** (puede que alguna vez hayas recibido una de estas advertencias). Por este motivo, existe el riesgo de que los datos se envíen varias veces por error, lo que, en el caso de una tienda online, puede dar lugar a pedidos duplicados. No obstante, las webs modernas de las tiendas suelen estar preparadas para evitar este tipo de problemas.

Además, los datos transferidos con el método POST no pueden **guardarsejunto al URL como marcador**.

### ¿Cuándo usar uno u otro?

El método **POST** es aconsejable cuando el usuario debe enviar datos o archivos al servidor, como, por ejemplo, cuando se rellenan formularios o se suben fotos.

El método **GET** es adecuado para la personalización de páginas web: el usuario puede guardar búsquedas, configuraciones de filtros y ordenaciones de listas junto al URL como marcadores, de manera que en su próxima visita la página web se mostrará según sus preferencias.

A modo de resumen:

* **GET** para la configuración de páginas web (filtros, ordenación, búsquedas, etc.)
* **POST** para la transferencia de información y datos
