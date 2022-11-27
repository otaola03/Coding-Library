# Box Model

Todo en CSS tiene una caja alrededor, y comprender estas cajas es clave para poder crear diseños con CSS o para alinear elementos con otros elementos. En este artículo, echaremos un vistazo más de cerca al _modelo de cajas_ en CSS con el que vas a poder crear diseños de compaginación más complejos con una comprensión de cómo funciona y la terminología relacionada.

&#x20;Este modelo consta de 4 elementos, el `content`, el `padding`, el `border` y el `margin`. y en le caso de que quieras visualizar cualquiera de estos elemntos de cualqueir pagina web, puedes hacerlo haciendo click derecho y luego selccionando `inpeccionar elemento`.

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--g56e5S1F--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/5h8byogi4mzsiuxxe7jw.png" alt=""><figcaption></figcaption></figure>

### Content

El área del content (como su nombre lo dice) contiene el “contenido” central a mostrar, es decir, un texto, una imagen, un video, etc. El contenido siempre es lo que queremos mostrarle al usuario. Esta área en muchas ocasiones tiene un color o imagen de fondo para hacerla más atractiva.

Como podemos observar en la imagen, el contenido es el área central de todo el elemento, de tal forma, que el siguiente elemento que lo rodea es el padding. El tamaño de esta área se puede modificar con las propiedades `height` , `width` , `max-height` , `max-width` , `min-height` , `min-width`.

> Estos estilos, solo se pueden aplicar a los elementos de bloque. Los elementos en linea no tienen medidas, su tamaño lo determina el contenido

### Margin

Es la separación entre una caja y las cajas adyacentes.

El margen es la última área del Box Model y se puede ver como una separación invisible o transparente que ayuda a separar un elemento de otro. Cuando definimos un color o imagen de fondo, este no se propaga a esta sección.

Los márgenes siempre quedan fuera del modelo de caja, por lo que pueden utilizarse para crear espacio entre los elementos.

> Los valores pueden ser positivos o negativos.

```
margin-top:    Margen superior
margin-right:  Margen derecho
margin-bottom: Margen inferior
margin-left:   Margen izquierdo

Admite hasta 4 valores que van en el orden de las agujas del reloj
4 valores    -> margin: top right bottom left;
3 valores    -> margin: top left/right bottom;
2 valores    -> margin: top/bottom left/right;
1 valore     -> margin: top/right/bottom/left;

Mediante margin-___: auto; se puede colocar el bloque que deses
en una de las esquinas.
```

Un habito bastante comun es colocar al estilo global `margin: 0;` y `padding: 0;`, sin embargo es una mala practica, ya que queda todo bastante ilegible, puesto que te quedaria sin espacio entre los paragrafos y elementos de la pagina.

Otra mala practica que no es tan comun es utilizar `margin: 0 auto;` para centra un elemento en la pagina, ya que por la cascada sobrescribira los margenes ya establecidos anteriormente, o cambia margenes que no es necesario cambiar. Por ello para centra un elemento lo recomendable es lo siguiente:

```css
margin-left: auto;
margin-right: auto;
```

lo que si es recomendable es establecerle un `margin: 0;` al body, puesto que por defecto los navegadores establecen un margen de 8 pixeles al body.

```css
body{
    margin: 0;
}
```

### Padding

Es el área alrededor del contenido. El `padding` es transparente.

El padding es una separación o espacio interior que existe entre el contenido y el borde de la caja, el cual se utiliza para dar una apariencia estética más atractiva y que el contenido no este pegado al borde.

> Cabe mencionar que el padding sigue siendo parte de la caja visible, por lo que, si tenemos una imagen o color de fondo, este se extenderá a través del padding.

Basicamente sirve para establecer una distancia entre el borde del bloque y el contenido de su interior. Es decir si establecemos un `padding-top: 50px;`a una caja azul con texto en su interior el texto se situara 50px por debajo del margen superior de la caja, pero esos 50px seguiran siendo azule, al contrario que con margin.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-24 at 5.11.05 PM.png" alt=""><figcaption></figcaption></figure>

```
padding-top:    Margen superior
padding-right:  Margen derecho
padding-bottom: Margen inferior
padding-left:   Margen izquierdo

Admite hasta 4 valores que van en el orden de las agujas del reloj
4 valores    -> padding: top right bottom left;
3 valores    -> padding: top left/right bottom;
2 valores    -> padding: top/bottom left/right;
1 valore     -> padding: top/right/bottom/left;
```

### Border

El borde es la línea que rodea la caja, es como la frontera que rodea al elemento, esta se utiliza para darle una apariencia estética a la caja, pues nos permite dibujar una línea de algún color, la línea puede tener los siguientes estilos:

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--nP5C64Q1--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/632ozf15t66crmlkqi11.png" alt=""><figcaption></figcaption></figure>

Las tres propiedades básicas para crear bordes son:

* `border-style`: sus valores son: \[ none | hidden | solid | dotted | dashed | double | groove | ridge | inset | outset ]
* `border-width`: indica al navegador el tamaño del borde, normalmente, se utiliza el valor en píxeles para esta propiedad, por ejemplo, `border-width: 5px`.
* `border-color`: por defecto, el valor utiliza el currentColor del texto. Sin embargo, preferimos definirlo aunque no sea necesario. Por ejemplo, `border-color: red`.

La mayoría de los desarrolladores web no utilizan estas tres propiedades por separado. En su lugar, existe el shorthand: `border`. Con este shorthand podemos escribir sólo `border: solid 5px red`.

También podemos controlar y dar un estilo diferente a cada parte de los bordes, por ejemplo:

```
border-width: 5px 10px 15px 20px; 
border-style: solid dashed dotted double; 
border-color: red green blue brown;

Tambien podemso especificar las propiedades con cada lado del borde, por ejemplo:
    border-top-style: doted;
    
border: 5px solid lightcoral;
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--YUObVpBD--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/y2mvxf809ztexwwnmrm2.png" alt=""><figcaption></figcaption></figure>



#### Border-radius

La propiedad CSS `border-radius` redondea las esquinas del borde exterior de un elemento. Puedes establecer un solo radio para hacer esquinas circulares, o dos radios para hacer esquinas elípticas.

<pre><code><strong>Border-radius: Es la propiedad que nos permite redondear vértices de
</strong><strong>forma independiente.
</strong>Es un shorthand que engloba 4 propiedades:
    border-top-left-radius -> Radio del borde superior izquierdo
    border-top-right-radius -> Radio del borde superior derecho
    border-bottom-right-radius -> Radio del borde inferior derecho
    border-bottom-left-radius -> Radio del borde inferior izquierdo</code></pre>

> Si recibe un solo valor impirmira una esfer y si recibe dos, imprimira una elipse

### Outline

La propiedad CSS **`outline`** es una forma reducida para establecer una o más de las propiedades individuales de contorno `outline-style`, `outline-width` y `outline-color` en una sola declaración. En la mayoría de los casos el uso de este atajo es preferible y más conveniente.

Basicamente `outline` crea un borde por el exterior del contenedor, es decir que el borde que establece esta fuera de `Box model`.

```
Es un shorthand que engloba
    outline-width: Controla el ancho del outline
    outline-syle: Controla el estilo del outline
    outline-color: Controla el color del outline
    
outline: 20px solid lightcoral;
```

{% hint style="info" %}
**Nota:** al no ser parte del box model, si creas un borde muy grande, este se superpondra a los elementos que tenga a su alrededor.
{% endhint %}

Otra propiedad que ofrece `outline` es `outline-offset`. Esta propiedad establece a que distancia se situara el borde de la caja. En el caso de que sea negativo se meterá dentro de la caja.

### Marging vs Padding

Aunque estas dos propiedades son similares, a veces se utilizan erróneamente de forma intercambiable, aunque son muy diferentes. Entender sus diferencias puede ser beneficioso para los desarrolladores web.

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--Hjfh7Oqq--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/cm8npdmxa0r15d74klzl.jpeg" alt=""><figcaption></figcaption></figure>

El padding y el margin son dos elementos importantes en el diseño web que añaden espacio extra en diferentes lugares. Pero, ¿Dónde y cuándo se debe utilizar uno en vez del otro?

Para el padding, puedes utilizarlo en las siguientes situaciones:

* Cuando no quieras que el contenido toque los bordes del contenedor.
* Cuando quiera aumentar el tamaño de un bloque de contenido sin que el propio contenido sea más grande.
* Cuando se necesita espacio entre un elemento interior y la caja padre.
* Cuando quieras que el background del elemento se muestre en el espacio generado. por ejemplo, si tienes dos divs, quieres que ambos divs (con diferente color de fondo) esten juntos, pero no quieres que sus textos se toquen.
* Cuando quieras aumentar el tamaño del elemento. Ejemplo: si quieres aumentar el tamaño de un botón.

Para el margin, puedes utilizarlo en las siguientes situaciones:

* Cuando necesite espacio alrededor de los elementos, como separar una imagen y la descripcion de la misma.
* Utilizarías el margen para establecer la distancia entre elementos cercanos.
* Cuando quiera centrar un elemento horizontalmente.
* Cuando quieras mover un elemento hacia arriba, hacia abajo o de lado a lado.
* Cuando quieras sobreponer elementos.

En resumen, si tu objetivos es separar tu caja de los elementos que le rodean tienes utilizar margin y si tu objetivos es aumentar el tamaño de la caja y separar los bordes del contenido tienes que utilizar padding

{% hint style="info" %}
**Nota:** El margen sirve para aumentar la distancia entre hermanos. No esta pensado para aumentar la distancia entre un elemento hijo y su contenedor padre, para eso esta el`padding`.
{% endhint %}

### Box sizing&#x20;

La propiedad de CSS `box-sizing` indica cómo se deben calcular las medidas de un elemento. Esto, que parece trivial, no lo es tanto ya que por defecto **CSS considera que el ancho y alto de la caja es de las propiedades `width` y `height`**. ¿Qué significa esto? Pues que si le añades un `padding` o un `border` el tamaño de renderizado de la caja será: **width + padding + border**.

En el siguiente ejemplo tendríamos una caja de 290px de ancho ya que: _250px de width + (10px \* 2) de padding + (10px \* 2) de border_

```css
div {
  width: 250px;
  border: 10px;
  padding: 10px;
}
```

Aunque no la veamos ahí, la propiedad `box-sizing` es la que se encarga de decir cómo debe ser ese cálculo. En este caso está utilizando el valor `content-box`, ya que es **su valor por defecto.**

#### **border-box**

El valor `border-box` en el `box-sizing` hace que el `padding` y el `border` pasen a formar parte del cálculo del ancho de la caja y no lo suman posteriormente.

En el siguiente ejemplo tendríamos una caja de 250px de ancho ya el `padding` y el `border` ya forman parte del cálculo del `width` del elemento:

```css
div {
  box-sizing: border-box;
  width: 250px;
  border: 10px;
  padding: 10px;
}
```

En este caso lo que hara box-sizing sera cambiar el with del contenedor para que asi el width del contenedor siga siendo 250px

### Bibliografia

* [https://developer.mozilla.org/es/docs/Learn/CSS/Building\_blocks/The\_box\_model](https://developer.mozilla.org/es/docs/Learn/CSS/Building\_blocks/The\_box\_model)
* [https://codigofacilito.com/articulos/que-es-el-box-model](https://codigofacilito.com/articulos/que-es-el-box-model)
* [https://dev.to/lupitacode/que-es-el-box-model-4mnj](https://dev.to/lupitacode/que-es-el-box-model-4mnj)
* [https://midu.dev/que-es-y-para-que-sirve-box-sizing-border-box/](https://midu.dev/que-es-y-para-que-sirve-box-sizing-border-box/)
* [https://developer.mozilla.org/es/docs/Web/CSS/box-sizing](https://developer.mozilla.org/es/docs/Web/CSS/box-sizing)
