# Formularios

Los **formularios web** son uno de los principales puntos de interacción entre un usuario y un sitio web o aplicación. Los formularios permiten a los usuarios la introducción de datos, que generalmente se envían a un servidor web para su procesamiento y almacenamiento, o se usan en el lado del cliente para provocar de alguna manera una actualización inmediata de la interfaz (por ejemplo, se añade otro elemento a una lista, o se muestra u oculta una función de interfaz de usuario).

El HTML de un **formulario web** está compuesto por uno o más **controles de formulario** (a veces llamados **widgets**), además de algunos elementos adicionales que ayudan a estructurar el formulario general; a menudo se los conoce como **formularios HTML**. Los controles pueden ser campos de texto de una o varias líneas, cajas desplegables, botones, casillas de verificación o botones de opción, y se crean principalmente con el elemento `<input>`, aunque hay algunos otros elementos que también hay que conocer.

Los controles de formulario también se pueden programar para forzar la introducción de formatos o valores específicos (**validación de formulario**), y se combinan con etiquetas de texto que describen su propósito para los usuarios con y sin discapacidad visual.

La estructura basica de un formulario es la siguiente:

```html
<form>
    <label>Nombre</label>
    <input>
    <button>Enviar formularios</button>
</form>
```

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-22 at 4.17.44 PM.png" alt=""><figcaption></figcaption></figure>

### \<form>

Todos los formularios comienzan con un elemento [`<form>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/form), como este:

```html
<form action="/my-handling-form-page" method="post">

</form>
```

Este elemento define formalmente un formulario. Es un elemento contenedor, como un elemento `<section>` o `<footer>`, pero específico para contener formularios; también admite algunos atributos específicos para la configuración de la forma en que se comporta el formulario. Todos sus atributos son opcionales, pero es una práctica estándar establecer siempre al menos los atributos `action` y `method`:

* El atributo `action` define la ubicación (URL) donde se envían los datos que el formulario ha recopilado cuando se validan.
* El atributo `method` define con qué método HTTP se envían los datos (generalmente `get` o `post`).

### Los elementos `<label>`, `<input>` y `<textarea>` <a href="#los_elementos_label_input_y_textarea" id="los_elementos_label_input_y_textarea"></a>

Nuestro formulario de contacto no es complejo: la parte para la entrada de datos contiene tres campos de texto, cada uno con su elemento `<label>` correspondiente:

* El campo de entrada para el nombre es un campo de texto de una sola línea.
* El campo de entrada para el correo electrónico es una entrada de datos de tipo correo electrónico: un campo de texto de una sola línea que acepta solo direcciones de correo electrónico.
* El campo de entrada para el mensaje es `<textarea>`; un campo de texto multilínea.

En términos de código HTML, para implementar estos controles de formulario necesitamos algo como lo siguiente:

```html
<form action="/my-handling-form-page" method="post">
 <ul>
  <li>
    <label for="name">Nombre:</label>
    <input type="text" id="name" name="user_name">
  </li>
  <li>
    <label for="mail">Correo electrónico:</label>
    <input type="email" id="mail" name="user_mail">
  </li>
  <li>
    <label for="msg">Mensaje:</label>
    <textarea id="msg" name="user_message"></textarea>
  </li>
 </ul>
</form>
```

{% hint style="info" %}
**Nota:** El atributo **`name` es obligatorio,** puesto que a la hora de enviar el formulario, es nombre de la "variable" que enviamos con la información que hemos escrito. Si no le ponemos `name` ese campo no existe!!!
{% endhint %}

En el elemento `<input>`, el atributo más importante es `type`. Este atributo es muy importante porque define la forma en que el elemento `<input>` aparece y se comporta. Para poder relacionar cada `<label>` con su correspondiente `<input>` se utiliza como se puede observar `for` y `id`.

> Id es atributo que se utilizar mucho para JavaScript

Por último, pero no por ello menos importante, ten en cuenta la sintaxis de `<input>` en contraposición con la de `<textarea></textarea>`. Esta es una de las rarezas del HTML. La etiqueta `<input>` es un elemento vacío, lo que significa que no necesita una etiqueta de cierre. El elemento `<textarea>` no es un elemento vacío, lo que significa que debe cerrarse con la etiqueta de cierre adecuada.

> Lo que introduzcas entre la etiquetas \<textarea> sera el contenido que hay por defecto en el contenedor de texto.

### El elemento `<button>` <a href="#el_elemento_button" id="el_elemento_button"></a>

El marcado de nuestro formulario está casi completo; solo necesitamos añadir un botón para permitir que el usuario envíe sus datos una vez que haya completado el formulario. Esto se hace con el elemento `<button>`; añade lo siguiente justo encima de la etiqueta de cierre `</form>`:

```html
<li class="button">
  <button type="submit">Envíe su mensaje</button>
</li>
```

El elemento `<button>` también acepta un atributo de `type`, que a su vez acepta uno de estos tres valores: `submit`, `reset` o `button`.

* Un clic en un botón `submit` (el valor predeterminado) envía los datos del formulario a la página web definida por el atributo `action` del elemento `<form>`.
* Un clic en un botón `reset` restablece de inmediato todos los controles de formulario a su valor predeterminado. Desde el punto de vista de UX, esto se considera una mala práctica, por lo que debes evitar usar este tipo de botones a menos que realmente tengas una buena razón para incluirlos.
* Un clic en un botón `button` no hace... ¡nada! Eso suena tonto, pero es muy útil para crear botones personalizados: puedes definir su función con JavaScript. No sirve para nvair formularios!

{% hint style="info" %}
**Nota:** \<input> tambien acepta este atribitu y de esta manera se comprotara como un boton:

`<input type="submit" value="Enviar input">`
{% endhint %}

### Ejemplo

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-22 at 4.41.09 PM.png" alt=""><figcaption></figcaption></figure>

### Mas elementos para formularios

Aqui tienes mass elementos que puedes implementar en to formulario para completarlo aun mas:

#### Fieldset

El elemento `fieldset` representa un conjunto de controles en un formulario ([`form`](https://www.htmlquick.com/es/reference/tags/form.html)), opcionalmente agrupados bajo un mismo nombre. Este elemento puede ser particularmente útil en formularios grandes, donde la legibilidad y la facilidad de acceso pueden ser mejoradas mediante la segmentación. Lo navegadores mostrarán normalmente un marco alrededor de los controles agrupados.

> Un `<fieldset>` puede adicionalmente tener un título o nombre, que puede ser provisto por el elemento `legend`. En tal caso, el elemento `legend` debe ser el primer hijo de `fieldset`.

```html
<form>
  <fieldset>
    <legend>Información personal</legend>
    <p>Nombre completo: <input type="text" name="nombrecompleto"></p>
    <p>Dirección: <input type="text" name="direccion"></p>
    <p>Teléfono: <input type="tel" name="telefono"></p>
  </fieldset>
```

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-23 at 10.25.08 AM.png" alt=""><figcaption></figcaption></figure>

#### Meter

El elemento `meter` representa una medida dentro de un rango conocido. Este elemento, nuevo en HTML5, puede ser útil para representar medidas en diferentes situaciones, como uso de disco, memoria o ancho de banda, los resultados de un encuesta, la cantidad recaudada en una colecta, el número de registros coincidentes en una consulta, etc.&#x20;

Esta etiqueta se estbalce con una serie de atributos:

* `min` y `max` representan los límites inferior y superior del rango.
* `low` y `high` ayudarán a los autores a definir segmentos (desde los márgenes) que contendrán valores considerados como bajos y altos respectivamente
* `optimal` indicará cuál es el valor óptimo en esta medida
* `value` representa el valor tomado por esta medida

> Si los atributos `min` y `max` no son declarados en este control, los límites de esta medida serán los predeterminados 0 (límite inferior) y 1 (límite superior)

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-23 at 10.31.43 AM.png" alt=""><figcaption></figcaption></figure>

#### progress

El elemento `progress` representa el estado de progreso de una operación, como ser la transferencia de un archivo, una codificación o la recuperación de valores desde una base de datos. Este control es normalmente representado por una barra de progreso, compuesta por un contenedor que es llenado de izquierda a derecha de acuerdo con el progreso de la operación.

Una barra `progress` puede representar un progreso en dos estados: como indeterminado, indicando que el proceso está siendo llevado a cabo pero no existe información acerca de su estado de completitud; o como un valor que indica la cantidad de trabajo que ha sido realizado en la tarea.

{% hint style="info" %}
Los autores no deben confundir este elemento con `meter`. A diferencia de `meter`, el elemento `progress` mide únicamente la completitud de _una tarea_.
{% endhint %}

```html
<p>Progreso: <progress max="100" value="20"></progress></p>
```

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-23 at 10.34.58 AM.png" alt=""><figcaption></figcaption></figure>

