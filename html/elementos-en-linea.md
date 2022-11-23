# Elementos en línea

Un **elemento en línea HTML** solo ocupa **el ancho de su contenido**. Mira algunos ejemplos con los que has practicado hasta ahora:

* `<a>`&#x20;
* `<b>`
* `<i>`
* `<img>`

Para notar la diferencia, tomemos el grupo de párrafos de arriba y reemplacemos los elementos `<p>`  por  `<a>`. Lo que va a pasar es que, en vez de ocupar el ancho de la página, cada uno se limitará a ocupar el espacio suficiente para su contenido, en este caso, para cada frase. Aquí, coloreamos el fondo para que puedas ver la diferencia claramente:&#x20;

![Elementos en línea en HTML](https://media.gcflearnfree.org/content/6138c7ba90347d098804a48f\_09\_08\_2021/Elementos-en-li%CC%81nea-en-HTML.png)

¿Ves que no se extienden más allá del texto que contienen? A su vez, tienen tanto espacio que caben en una sola línea y no se moverán de ella hasta que el próximo elemento ya no quepa.

> Puedes utilizar elementos de bloque dentro de otros elementos de bloque, pero no elementos de linea dentro de elementos otros elementos de linea. Es posible hacerlo, pero no es recomendable.

### \<em>

El **elemento HTML `<em>`** es el apropiado para marcar con énfasis las partes importantes de un texto. El elemento `<em>` puede ser anidado, con cada nivel de anidamiento indicando un mayor grado de énfasis.

```html
<p>Get out of bed <em>now</em>!</p>

<p>We <em>had</em> to do something about it.</p>

<p>This is <em>not</em> a drill!</p>
```

### \<strong>

El elemento **strong** es el apropiado para marcar con especial énfasis las partes más importantes de un texto. Es como `<em>`, pero para dar mas enfasis.&#x20;

```html
 <p>
     <em>El dinero</em> es importante pero <strong>la salud</strong> lo es más.
 </p>
```

El navegador el ejecutar este fragmento de codigo, hara enfasis ha estas do palabras, pero hara mas enfasis en `la salud` que en `El dinero`.  Es decir si  `El dinero` valiera 1, `la salud` valdria 2.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-21 at 5.21.55 PM.png" alt=""><figcaption></figcaption></figure>

### \<small>

Mediante `<small>` se consigue que a ese texto se le haga menos enfasis que al texto normal. En HTML5, este elemento es reutilizado para representar comentarios laterales y letra pequeña, incluyendo derechos de autor y texto legal, independientemente de su estilo de presentación.

### \<br>

El elemento HTML _line break_ `<br>` produce un salto de línea en el texto (retorno de carro). Es útil para escribir un poema o una dirección, donde la división de las líneas es significante.

```html
Mozilla Foundation<br>
1981 Landings Drive<br>
Building K<br>
Mountain View, CA 94043-0801<br>
USA
```

{% hint style="info" %}
**Nota:** No utilices `<br> para aumentar el espacio entre paragrafos o lineas. Para eso` utiliza la propiedad `margin` de CSS o el elemento `<p>`&#x20;
{% endhint %}

## \<wbr>

El elemento HTML _word break opportunity_ `<wbr>` representa una posición dentro del texto donde el explorador puede opcionalmente saltar una línea , aunque sus reglas de salto de línea de otra manera no crearían un salto en esa posición.&#x20;

Es decir, mediante `<wbr>` en el caso de que se necesario realizar un salto de linea, por ejemplo al minimizar la pantalla, nosotros podremos decidir donde se realizara ese salto de linea.

> Los guiones ( - ) el navegador web los interpreta como "\<wbr>"

### \<time>

El **elemento HTML `<time>`** representa un periodo específico en el tiempo. Puede incluir el atributo `datetime` para convertir las fechas en un formato interno legible por un ordenador, permitiendo mejores resultados en los motores de búsqueda o características personalizadas como recordatorios.

> Aunque parezca un simple \<p>, el navegador entendera que es una fecha y por ello le dara la importancia semantica que requiere una fecha

Puede representar uno de los contenidos siguientes:

* Una hora en formato de 24 horas
* Una fecha precisa en el Calendario Gregoriano (con hora y zona horaria opcionales)
* Un periodo de tiempo válido

### \<i>, \<b> y \<u>

Estos elementos sirven para poner en italica, negrita (bold) y subrralla (underline) el texto respectivamente. Sin para realizar estas acciones, normalmente se utiliza CSS y no estas etiquetas.

> La etiqueta \<i> es de gran utilizad a la hora de trabajar con librerias de iconos.

```html
<p>
    <i>Italic</i>
    <b>Boldd</b>
    <u>Underline</u>
</p>
```

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-21 at 5.40.48 PM.png" alt=""><figcaption></figcaption></figure>

### \<sup> y \<sub>

Estas etiquetas se utilizan para poner Superindice y subindices, como en el siguiente ejemplo:

```html
<p>4 elevado al cuadrado se representa asi 4 <sup>2</sup></p>
<p>Agua oxigeneado tiene laa formula H<sub>2</sub>O<sub>2</sub></p>
```

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-21 at 5.44.53 PM.png" alt=""><figcaption></figcaption></figure>

### \<span>

En HTML, la etiqueta span es un elemento contenedor en línea genérico. Ses eule usar para encerrar palabras o pequeños textos y darles estilo a traves de CSS o localizarlos desde javascript. Semanticamnete no signifca nada

```html
<div style="border: 1px dotted blue;">
  <h4>Ejemplo de div y span </h4>
  <p>
    Esto es un párrafo dentro de un div,
    <span style="color: red;"> y esto un span dentro de un párrafo. </span>
  </p>
</div>
```

### \<q>

Es equivalente a blockquote, significa quote, por eso el del bloque se llama block - quote. Sirve para poner citas pero en linea

```html
<q cite="google.cm">Yo soy Iron man</q>
```

### \<code>

El elemento HTML code **inserta texto que representa código de computadora**. Puede ser útil para mostrar funciones, código de programación o variables. El contenido de este elemento es usualmente mostrado por los navegadores con un estilo de fuente de ancho fijo. Basicamente es para colocar los bloque de codigo que puedes ver aa lo largo de este documento.

> Suele ir unido de la etiqueta \<pre> para representarlo como bloque

```
<pre>
    <code>
        span {
            color: red;
        }
    </code>
</pre>
```

Para darle sus uso como elemento en linea tan solo hay que añadirlo a la linea que queramos y meter los elementos de codigo dentro. Sin embargo, hay simbolos que no interpreta y por ello habra que representarlos con su [codigo ascii](https://ascii.cl/es/codigos-html.htm) correspondiente:

<pre class="language-html"><code class="lang-html">&#x3C;p>La etiqueta &#x3C;code>&#x26;#62;h1&#x26;#62;&#x3C;/code> se utiliza para representar titulos
<strong>
</strong><strong>&#x3C;!-- esto se mostraria como &#x3C;h1> --></strong></code></pre>
