# Titulos y parrafos

Los elementos de **encabezado** implementan seis niveles de encabezado del documento, `<h1>` es el más importante, y `<h6>`, el menos importante. Un elemento de encabezado describe brevemente el tema de la sección que presenta. La información de encabezado puede ser usada por los agentes usuarios, por ejemplo, para construir una tabla de contenidos para un documento automáticamente.

El elemento p (párrafo) es el apropiado para distribuir el texto en párrafo y este se define mediante la siguiente etiquetas `<p></p>` y el cntenido en su interior.

```html
<p>Esto es un párrafo </p>
```

{% hint style="info" %}
Nota:

* No se deben usar niveles inferiores para reducir el tamaño de la fuente: use la propiedad CSS `font-size` para eso.
* Evite omitir niveles de encabezado: siempre comience con `<h1>`, después use `<h2>` y así sucesivamente.
* Utiliza un uncio \<h1> por pagina
{% endhint %}

El siguiente código muestra todos los niveles de encabezado:

```html
<h1>Heading level 1</h1>
<h2>Heading level 2</h2>
<h3>Heading level 3</h3>
<h4>Heading level 4</h4>
<h5>Heading level 5</h5>
<h6>Heading level 6</h6>
```

### Ejemplo

El código siguiente muestra unos pocos encabezados con algo de contenido debajo de ellos.

```html
<h1>Heading elements</h1>
<h2>Summary</h2>
<p>Some text here...</p>

<h2>Examples</h2>
<h3>Example 1</h3>
<p>Some text here...</p>

<h3>Example 2</h3>
<p>Some text here...</p>

<h2>See also</h2>
<p>Some text here...</p>
```
