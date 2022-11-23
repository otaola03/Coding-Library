# Select y datalist

### Select

El elemento select (`<select>`) de HTML representa un control que muestra un menú de opciones. Las opciones contenidas en el menú son representadas por elementos `<option>`, los cuales pueden ser agrupados por elementos `<optgroup>` (en-US). La opcion puede estar preseleccionada por el usuario.

```html
<select name="select">
  <option value="value1">Value 1</option>
  <option value="value2" selected>Value 2</option>
  <option value="value3">Value 3</option>
</select>
```

> La propiedad selected establece que la opcion por defecto sera la segunda

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-22 at 5.22.46 PM.png" alt=""><figcaption></figcaption></figure>

#### \<optgroup>

Si tenemos muchas opciones podemos ordenarlas por categorias a traves de la etiqueta `<optgroup>` con el atributo label para nombrar la categoria.

```html
<select name="select">
    <optgroup label="grupo1">
        <option value="value1">Value 1</option>
        <option value="value2" selected>Value 2</option>
    </optgroup>
    <optgroup label="grupo2">
        <option value="value3">Value 3</option>
        <option value="value4" selected>Value 4</option>
    </optgroup>
</select>
```

### Datalist

El **elemento HTML `<datalist>`** contiene un conjunto de elementos `<option>` que representan los valores disponibles para otros controles. Este elemento fucniona parecido a `<select>` aunque es mas comodo, ya que nor permite dar una descripcion sobre los elementos y filtrarlos.&#x20;

> Para su utilizacion es necesaria la combinacion de `input` con el atributo `list`

```html
<label>Choose a browser from this list:
<input list="browsers" name="myBrowser" /></label>
<datalist id="browsers">
  <option value="Chrome">
  <option value="Firefox">
  <option value="Internet Explorer">
  <option value="Opera">
  <option value="Safari">
  <option value="Microsoft Edge">
</datalist>
```

