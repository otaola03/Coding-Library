# Desbordamiento y Colapso de margenes

### &#x20;Overflow

La propiedad CSS `overflow` especifica: si recortar contenido, dibujar barras de desplazamiento o mostrar el contenido excedente en un elemento a nivel de bloque. Es un shorthand que engloba `overflow-x` y `overflow-y`.

> Es la propiedad que controla que debe hacer la caja cuando su contenido se desborda del contenedor

Usando la propiedad `overflow` con un valor distinto a `visible`, valor por defecto, creará un nuevo contexto de formatos de bloques. Esto es técnicamente necesario debido a que si un elemento flotante interceptara con otros forzaría a reajustar el contenido alrededor de los elementos que se interceden. El reajuste sucedería luego de cada desplazamiento, y llevaría a un desplazamiento demasiado lento.

Por defecto, el navegador desborda el contenido del elemento, sin embargo, nosotros podemos decidir que hacer:

* `visible`: No se controla el desbordamiento, el contenido simplemente se desborda. Valor por defecto.
* `hidden`: Oculta el contenido desbordado y las barras de desplazamiento del elemento.
* `clip`: Igual que `hidden`, pero no permite desplazamiento mediante programación.
* `scroll`: Oculta el contenido desbordado y muestra barras de desplazamiento.
* `auto`: El navegador decide. Generalmente, aplica `scroll.`

<figure><img src="https://lenguajecss.com/css/interacciones/scroll-y-overflow/overflow-css.png" alt=""><figcaption></figcaption></figure>

Ten en cuenta que `overflow-x` aplica estos valores a la barra de desplazamiento **horizontal**, `overflow-y` a la barra de desplazamiento **vertical**, mientras que `overflow` puedes utilizarlo con un parámetro para indicar el mismo valor a ambos ejes, o con dos parámetros para indicar uno para `overflow-x` y otro para `overflow-y` respectivamente

### Colapso de margenes

Ahora bien, cuando dos elementos de bloque HTML tienen márgenes verticales que se tocan entre sí, estos dos márgenes colapsan en uno o se fusionan entre sí, y aquí dominará el más grande.

La documentación de la W3C define el colapso de márgenes de la siguiente manera:

> "En CSS, los márgenes adyacentes de dos o más bloques (que podrían o no ser hermanos) pueden combinarse para formar un único margen. Cuando los márgenes se combinan de esta manera decimos que colapsan, y el margen combinado resultante se denomina margen colapsado."

#### ¿Cuando colapsan los margenes?

Los márgenes horizontales no colapsan nunca, solo los verticales, es decir, los márgenes **top y bottom**, y colapsan siempre que dos márgenes verticales cualesquiera son contiguos y se «tocan», cuando no hay nada más entre ellos. Las situaciones de colapso se pueden clasificar en cuatro casos:

1. Hermanos adyacentes
2. Un contenedor y su primer elemento
3. Un contenedor y su último elemento
4. Bloques vacíos

El colapso de márgenes **solo afecta al modelo de bloques**, no afecta a otros modelos de display, por ejemplo al flex model (`display: flex`).

#### Hermanos adyacentes

Este ejemplo visual es la mejor manera de entenderlo:

```css
.box-1 {
    margin-bottom: 40px;
    padding: 20px;
    border: solid 5px red;
}
.box-2 {
    margin-top: 40px;
    padding: 20px;
    border: solid 5px blue;
}

span {
    font-weight: bold;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--JSeX1hqy--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/o426ek9d5ch5arnvl6bc.png" alt=""><figcaption></figcaption></figure>

Cuando los desarrolladores hace algo así, espera que el margen de la primera caja y la segunda sea de 80px (40px + 40px), pero en realidad es de 40px. Los dos márgenes se tocan entre sí, por lo que se combinan o se colapsan el uno con el otro.

El margen inferior del elemento se colapsa con el margen superior del siguiente elemento. Ahora para empujar aún más, vamos a dar a nuestra primera caja un margen inferior (margin-bottom) de 100px

```css
.box-1 {
    margin-bottom: 100px;
}
.box-2 {
    margin-top: 40px;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--fQfOR48O--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/whn9aum2xgm3vihtvize.png" alt=""><figcaption></figcaption></figure>

Como podemos observan en la imagen el margen más grande siempre gana, es decir, como la primera caja tiene un margen de 100px y la otra caja 40px el que termina ganando es el que tenga un valor superior, podemos decir que hay 100px de margen entre la primera y la segunda caja.

{% hint style="info" %}
El mejor método o truco para solucionar esto, es utilizar siempre `margin-bottom` para separar elementos  olvidarte de `margin-top`
{% endhint %}

#### Un contenedor padre y su primer elemento

En este ejemplo vamos a tener un `header` y dentro de el un encabezado `<h1>`.

```html
<header class="header">
   <h1 class="title">Lupita code</h1>
</header>
```

```css
body {
    margin: 0;
    font-family: arial;
    background-color: #ccc;
}

.header {
    height: 50px;
    background-color: steelblue;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--J_wiAEg4--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/62lx772642wqs7aujqhh.png" alt=""><figcaption></figcaption></figure>

Como podemos observar en la imagen hay un espacio entre la parte superior del viewport y el `header`, ese espacio extra no corresponde al `body` ya que si te fijas en el código CSS, el `body` tiene un margen con valor de 0. ¿Adivinas de dónde viene?

Ese margen tampoco es del `header` lo que nos lleva a concluir que ese margen le corresponde al encabezado `<h1>`, y si revisas la herramienta de desarrollo te puedes dar cuenta que el encabezado ya viene con un margen vertical de la hoja de estilo del navegador.

¿Recuerdas cuando mencioné sobre las hojas de estilo del navegador?

[![Alt Text](https://res.cloudinary.com/practicaldev/image/fetch/s--tJk2sTEc--/c\_limit%2Cf\_auto%2Cfl\_progressive%2Cq\_auto%2Cw\_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8ph767z937bzzuloshb6.png)](https://res.cloudinary.com/practicaldev/image/fetch/s--tJk2sTEc--/c\_limit%2Cf\_auto%2Cfl\_progressive%2Cq\_auto%2Cw\_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/8ph767z937bzzuloshb6.png)

La solución es colocar un `margin: 0` al `<h1>` y así ya no se tiene esa separación. El resultado es el siguiente:\


```
.title {
    margin: 0;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--6qVyR9qE--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/0vvlopfd2gvbayj84i35.png" alt=""><figcaption></figcaption></figure>

Ahora quiero agregar nuevamente un `margin-top` de 10px al `<h1>`\


```
.title {
    margin: 0;
    margin-top: 20px;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--sQWXYbDc--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/k0if3i1a62csqcq41mm1.png" alt=""><figcaption></figcaption></figure>

Como puedes observar el `header` se movió, y se supone que solo le indicamos que se moviera el `<h1>`. Para que esto no ocurra, tenemos varias **soluciones**:

1. Añadir la declaración `overflow: hidden` al `header`.
2. Añadir un `padding-top` al `header`.
3. Añadir un `border-top` al header.

Si añadimos padding, border o espacio a los elementos de los ejemplos anteriores, no se aplicará el colapso. En otras palabras, una forma de deshacerse del comportamiento del colapso de márgenes consiste en añadir algún tipo de separación (borde, padding o espacio libre) entre los márgenes.

#### Un contenedor padre y su último elemento.

De forma análoga a lo que ocurre en el caso anterior con los márgenes superiores, los márgenes inferiores del contenedor y de su último elemento también colapsan en uno solo. Y también como en el caso anterior, el colapso de márgenes no se produce si el borde o el padding del contenedor es mayor a cero.\


```html
<div class="parent">
   <div class="child">Here is a paragraph</div>
</div>
<div class="div">Outside the parent</div>
```

```css
body {
    margin: 0;
    font-family: arial;
}

.parent {
    margin-bottom: 30px;
    background: #49b293;
    height: auto;
}
.child {
    margin-bottom: 50px;
    background: blue;
    height: 100px;
    width: 200px;
}

.div {
    background-color: red;
}
```

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-25 at 11.43.43 AM.png" alt=""><figcaption></figcaption></figure>

Como puedes observar al igual que pasa con el primeri hijo, aunque hayamos establecido un `margin-bottom: 30px;` al padre y un `margin-bottom: 50px;` al hijo estos, máargenes se colapsen y al final solo queda el del hijo, puesto que es el mas grande.

#### Bloques vacíos <a href="#caso-4-bloques-vac-c3-ados" id="caso-4-bloques-vac-c3-ados"></a>

Los márgenes verticales de un bloque vacío (sin height ni padding ni contenido) también colapsan entre sí. Por ejemplo, si tenemos un bloque vacío con un margen top de 40px y un margen bottom de 20px, el elemento ocupará una zona de 40px de altura al colapsar sus propios márgenes verticales:\


```
<div class="box">Lorem, ipsum.</div>
<div class="empty"></div>
<div class="box">Lorem, ipsum.</div>
```

```
body {
    margin: 0;
    font-family: arial;
}

.box {
    margin: 0;
    height: 40px;
    padding: 10px;
    border: 2px solid;
    background: khaki;
}
.empty {
    margin-top: 40px;
    margin-bottom: 20px;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--xTNnoQk_--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/9q0pjqki9yk40ouimycc.png" alt=""><figcaption></figcaption></figure>

### Bibliografia <a href="#excepciones" id="excepciones"></a>

* [https://webdesign.tutsplus.com/es/tutorials/css-basics-understanding-collapsing-margins--cms-34272](https://webdesign.tutsplus.com/es/tutorials/css-basics-understanding-collapsing-margins--cms-34272)
* [https://cybmeta.com/colapso-de-margenes-en-css](https://cybmeta.com/colapso-de-margenes-en-css)
* [https://dev.to/lupitacode/entendiendo-el-colapso-de-margenes-margin-collapsing-4oj6](https://dev.to/lupitacode/entendiendo-el-colapso-de-margenes-margin-collapsing-4oj6)
* [https://lenguajecss.com/css/interacciones/snap-scroll/](https://lenguajecss.com/css/interacciones/snap-scroll/)
