# Tablas

Al crear un sitio web seguramente habrá ocasiones en las que necesites incluir datos de forma visual para que resulten más fáciles de leerse o comprenderse. Para esto, uno de los métodos que puedes utilizar en el diseño web son las tablas HTML.

Las tablas HTML son ideales para mostrar grandes cantidades de datos de manera estructurada y, por ello, en este artículo vamos a explorar su definición y el modo en que puedes crear una fácilmente.

### Estructura de una tabla (\<table>)

Una tabla HTML `<table>` es un conjunto de celdas (`<td></td>`) organizadas en filas (`<tr>`) que a su vez de organizan en grupos de filas (`<thead>`, `<tbody>`o `<tfoot>`). Ademas, laa tabla puede tener una leyenda (`<caption>`) y hacer referencia a las columnas (`<col>` y `<colspan>`).

{% hint style="info" %}
**Truco:** el numero de celdas dentro de un `<tr> establecera el numero de columnas de la tabla`
{% endhint %}

La leyenda y los grupos de filas se muestran en este orden:

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 11.32.41 AM.png" alt=""><figcaption></figcaption></figure>

A su vez, tanto los cuerpos de tabla como la cabecera y el pie de tabla están formados por varias filas (`<tr>`) formadas por varias celdas (`<td>` o `<th>`). Todas las filas tienen el mismo número de celdas (aunque también se pueden unir celdas horizontal y verticalmente).

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 11.33.50 AM.png" alt=""><figcaption></figcaption></figure>

Las celdas de la tabla suelen ser elementos \<td>, aunque también pueden ser elemento \<th> para indicar que la celda es una cabecera de la fila o columna correspondiente.

El codigo de una tabla sencilla es el siguiente:

<div align="right">

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 11.45.49 AM.png" alt=""><figcaption></figcaption></figure>

</div>

### Leyenda

La leyenda (`<caption>`) es un texto explicativo opcional que se muestra fuera de la tabla (normalmente, arriba). La leyenda no puede incluir párrafos ni otros elementos de bloque, aunque sí etiquetas en línea (`<strong>`, imágenes, etc).

Los navegadores dan a la leyenda el mismo ancho que a la tabla, por lo que si una leyenda es larga y la tabla estrecha, la leyenda ocupará varias líneas, como muestra el ejemplo siguiente:

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 11.47.45 AM.png" alt=""><figcaption></figcaption></figure>

### Cuerpos de tabla (\<tbody>), encabezados (\<thead>) y pies (\<tfoot>)

Los elementos `<tbody>`, `<thead>` y `<tfoot>` abarcan una o varias filas seguidas para indicar que varias filas forman un grupo de filas. Un grupo de filas puede ser una cabecera de la tabla (`<thead>`), un pie de tabla (`<tfoot>`) o formar parte del contenido de la tabla (`<tbody>`)

Si una tabla contiene un elemento \<thead>, este debe aparecer al principio. Si una tabla contiene un elemento \<tfoot>, este debe aparecer al final.

Una tabla puede contener varios \<tbody> consecutivos.

> Si una tabla contiene filas (\<tr>) no incluidas en algún grupo (\<tbody>, \<thead> o \<tfoot>), los navegadores crean automáticamente elementos \<tbody> que agrupen las filas consecutivas no incluidas en ningún grupo.

Al imprimir una tabla que ocupa varias páginas, los navegadores repiten al principio y al final de cada página las cabeceras `<thead>` y pies de tabla `<tfoot>`. Se puede comprobar, por ejemplo, con la lista de entidades de carácter de HTML 4, que no cabe en una sola página.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 11.50.32 AM.png" alt=""><figcaption></figcaption></figure>

### Celdas de datos (\<td>) y celdas de cabecera (\<th>)

Cada celda de la tabla está marcada con la etiqueta `<td>` (celda de datos), aunque también se pueden marcar con la etiqueta `<th>` (celda de cabecera). Las celdas `<th>` están pensadas para utilizarse en las celdas que sirven de cabecera para la fila o columna, por lo que los navegadores las muestran resaltadas (normalmente, en negrita y centradas en horizontal), aunque se pueden utilizar en cualquier celda.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 11.53.43 AM.png" alt=""><figcaption></figcaption></figure>

### Columnas (\<col>) y grupos de columnas (\<colgroup>)

Cuando necesitamos sleccionar auna columna, tenemos la etiqueta `<colgroup>`, que nos permite seleccionar una columna en concreto. Dentro podremos tantas etiquetas `<col>` como columnas tengamos, cada etiqueta `<col>` equivaldra a una columna siguiendo el mismo orden que necesite la tabla.

Las etiquetas `<col>` y `<colgroup>` se encuentran situadas al principio de la tabla, después de la etiqueta `<caption>`.

El ejemplo siguiente muestra la situación de las etiquetas \<col> y \<colgroup> en una tabla:

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 12.15.34 PM.png" alt=""><figcaption></figcaption></figure>

Cada etiqueta `<col>` corresponde a una columna, en el mismo orden (la primera etiqueta `<col>` corresponde a la primera columna, y así sucesivamente). En el ejemplo anterior, hay definidos dos grupos de columnas, el primero de los cuales abarca dos columnas y el segundo una columna.

El número de columnas que se defina mediante etiquetas `<col>` y `<colgroup>` debe coincidir con el número de columnas de la tabla.

Todas las etiquetas `<col>` deben estar incluidas en algún `<colgroup>`. Si alguna o algunas etiquetas `<col>` no están incluidas en ninguna etiqueta `<colgroup>`, los navegadores crean automáticamente etiquetas `<colgroup>` que agrupan las etiquetas `<col>` "huérfanas" consecutivas.

### Atributos

Las tablas tiene varios atributos, pero los mass utilizados son `rowspan` y `colspan`.

* `rowspan`: sirve para que una celda ocupe mas de una fila, el valor por defecto es 1
* `colspan`: sirve para que una celda ocupe mas de una columna, el valor por defecto es 1

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 12.01.34 PM.png" alt=""><figcaption></figcaption></figure>
