# Input

El elemento HTML `<input>` se usa para crear controles interactivos para formularios basados en la web con el fin de recibir datos del usuario.Hay disponible una amplia variedad de tipos de datos de entrada y widgets de control, que dependen del dispositivo y el agente de usuario ([user agent (en-US)](https://developer.mozilla.org/en-US/docs/Glossary/User\_agent)).El elemento `<input>` es uno de los más potentes y complejos en todo HTML debido a la gran cantidad de combinaciones de tipos y atributos de entrada.

### Atributo `type`

El tipo de control a mostrar. Su valor predeterminado es `text`, si no se especifica este atributo. Los posibles valores son:

* `button`: Botón sin un comportamiento específico.
* `date`: Control para introducir una fecha (año, mes y día, sin tiempo).
* `time`: Control para introducir un valor de tiempo sin zona horaria específica.
* `month`: Control para introducir un mes y año, sin zona horaria específica.
* `search`: Cuadro de texto de línea simple para introducir textos de búsqueda. Los saltos de línea son eliminados automáticamente del valor introducido.
* `tel`: Control para introducir un número telefónico. Los saltos de línea son eliminados automáticamente del valor introducido, pero no hay otra sintaxis forzada
* `email`: Correo electrónico.
* `password`: Control de línea simple cuyo valor permanece oculto. Se puede usar el atributo maxlength para especificar la longitud máxima del valor que se puede introducir. **No es seguro**, si se le cambia el atributo, el texto que hay en el input sera visible.
* `url`: Campo para editar una URL. El valor introducido se valida para que contenga una cadena vacía o una ruta URL absoluta antes de enviarse. Los saltos de línea y espacios en blanco al principio o al final del valor son eliminados automáticamente.&#x20;
* `color`: Control para espicificar un color. Una interfaz de selección de color no requiere más funcionalidad que la de aceptar colores simples como texto ([más información](https://www.w3.org/TR/html5/forms.html#color-state-\(type=color\))).
* `number`: Control para introducir un número de punto flotante.
* `range`: Control para introducir un número cuyo valor exacto no es importante. Este control usa los siguientes valores predeterminados si no se especifica cada atributo:
  * `min`: 0
  * `max`: 100
  * `value`: `min` + (`max -` `min`) / 2, o `min` si `max` es menor que `min`
  * `step`: 1
* `reset`: Botón que restaura los contenidos de un formulario a sus valores predeterminados.
* `text`: Campo de texto de línea simple. Los saltos de línea son eliminados automáticamente del valor introducido.
* `file`: Control que permite al usuario seleccionar un archivo. Se puede usar el atributo **accept** para definir los tipos de archivo que el control podrá seleccionar.

#### radio y checkbox

Permite **seleccionar una unica opcion** de una lista de opciones relacionadas. Se debe usar el atributo `value` para definir el valor que se enviará por este elemento, es obligatorio!!!. Se usa el atributo `checked` para indicar si el elemento está seleccionado de forma predeterminada.

> Los botones radio que tengan el mismo valor para su atributo **name** están dentro del mismo "grupo de botones radio"

```html
<label>Masculino
    <input type="radio" name="gender" value="masculino">
<label>
<label>Femenino
    <input type="radio" name="gender" value="femenino"
<label>
<label>Deconocido
    <input type="radio" name="gender" value="Desconocido">
<label>
```

`Checkbox` es una opcion parecida, solo que nos ofrece la posibilidad de seleccionar varios elementos a la vez

### Otros argumentos

Hay infinidad de argumentos para especificar que nuestros inputs hagan una cosa u otra, pero estos son los mas utilizados:

* `placeholder`: Una pista para el usuario sobre lo que puede introducir en el control. El texto no debe contener saltos de línea.
* `required`: Hace que un campo sea obligatorio
* `readonly`: Hace que un campo sea solo de lectura
* `disabled`: Desactiva el campo, no se podrá escribir en el i se enviara
* `min`, `max`: Para contrlar el minimo y el maximo de un caampo numerico como `type="number"`. No son necesarios los dos elementos
* `minlenght`, `maxlenght`: Establece el minimo y el maximo de un campo de texto
* `selected`: Para establecer una opcion por defecto, como `checked`
* `focus`: Para oner el foco por defecto al cargar el formulario.





### Bibliografia

* [https://developer.mozilla.org/es/docs/Web/HTML/Element/input](https://developer.mozilla.org/es/docs/Web/HTML/Element/input)
* [https://www.htmlquick.com/es/reference/tags/meter.html](https://www.htmlquick.com/es/reference/tags/meter.html)
