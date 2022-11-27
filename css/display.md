# Display

Antes de comenzar, debemos saber que cada **etiqueta HTML** tiene un «tipo de representación visual» en el navegador, lo que habitualmente se suele denominar el **tipo de caja**. Si no sabes nada sobre esto, te aconsejo echarle un vistazo antes al apartado [Modelo de cajas](box-model.md).

Recordemos que, por defecto, cada elemento HTML tiene un tipo de representación concreto. Como norma general (_con excepciones_) los elementos que se utilizan dentro de un párrafo, son de tipo `inline`, mientras que los que se utilizan para agrupar, son de tipo `block`. La propiedad `display` de CSS permite modificar el comportamiento de un elemento HTML, cambiándolo al que le indiquemos, como por ejemplo `inline` o `block` (_u otro de los que veremos más adelante_).

Esta propiedad puede tomar muchos valores diferentes, pero **los más comunes son estos tres**:

* **`block`**: hace que el comportamiento del elemento sea como un bloque.
* **`inline`**: el elemento se renderizará en línea con otros elementos.
* **`inline-block`**: el elemento tendrá un comportamiento mezcla entre los dos anteriores, que ahora voy a describir.

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-25 at 12.23.24 PM.png" alt=""><figcaption></figcaption></figure>

Estos se utiliza para alterar el flujo noramle de una pagina web. En el queso de que no seppas lo que es el flujo normal, la documentación de la MDN define el flujo normal de la siguiente manera:

> El flujo normal, o flow Layout, es la forma en que los elementos de bloque y en línea se muestran en una página antes de que se realicen cambios en su diseño.

### display: inline

Los elementos en línea **no admiten dimensiones** (width, height) pero si admiten margin, padding y border, solo ocupan lo que tengan en su contenido, es decir, aunque quieras declarar un ancho y alto a un elemento de línea no podrá tener efecto ya que estos elementos no aceptan dimensiones, así también lo explica la documentación de la MDN:

{% hint style="info" %}
Aunque puedas aplicarle margin, padding y border a un elementos en linea tiene algunas pegas:

* Si el `padding` o el `border` es muy grande, ese este no respetara los elementos de bloque, se los comera. Sin embargo si respeta los elementos en linea
* Si se solapa con margenes de los elementos en bloque, los de bloque ganara, es decir se superponeran.
{% endhint %}

Si hay varios elementos en línea estarán colocados de izquierda a derecha (uno al lado de otro).

Por ejemplo, el elemento HTML `<span>` es un elemento de línea por defecto y no importa cuántas etiquetas `<span>` haya, siempre aparecerán en línea o, en otras palabras, una inmediatamente después de la otra, produciendo una cadena continua de texto.\


```html
 <span class="inline">Soy un elemento de linea</span>
 <span class="inline">Soy otro elemento de linea</span>
 <span class="inline">Soy otro elemento más de linea</span>
```

```css
.inline {
    background-color: khaki;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--EFPV2GP6--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/g1xr8rpxh6rxk8eb8898.png" alt=""><figcaption></figcaption></figure>

### display: block

Un elemento de bloque es un elemento que ocupa el ancho máximo disponible. Tal y como dice la documentación de la MDN:

> De manera predeterminada, el contenido de un elemento de nivel de bloque es el 100% del ancho de su elemento padre y su altura viene determinada por su contenido.

Esto nos quiere decir que los elementos de tipo bloque abarcan el 100% del espacio que tengan disponible, es decir, se estiran por todo el ancho de la página.

Cabe mencionar que estos elementos si admiten dimensiones pero no pueden tener otro elemento a su lado ya que abarcan todo el espacio que tengan disponible por lo tanto estarán colocados de arriba hacia abajo.\


```html
 <p class="block">Soy un elemento de bloque</p>
 <p class="block">Soy otro elemento de bloque</p>
 <p class="block">Soy otro elemento más de bloque</p>
```

```css
.block {
    background-color: khaki;
}
```

<figure><img src="https://res.cloudinary.com/practicaldev/image/fetch/s--444M8d5G--/c_limit%2Cf_auto%2Cfl_progressive%2Cq_auto%2Cw_880/https://dev-to-uploads.s3.amazonaws.com/uploads/articles/qhhg516qhqvtnkitr90c.png" alt=""><figcaption></figcaption></figure>

### display: inline-block

Es una combinación entre los dos tipos de elementos mencionados anteriormente (block e inline), los elementos con el valor `inline-block` admiten dimensiones pero todavía son elementos de línea, es decir estarán colocados uno al lado de otro.

> Ele elemento `<img>` es un elemento con la propiedad `display: inline-block;`

```html
<div class="block"> Bloque 1 </div>
<div class="block"> Bloque 2 </div>
```

```css
.block{
  background-color: lightblue;
  width: 100px;
  height: 100px;
  margin: 5px;
  padding: 5px;
  display: inline-block;
}
```

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-25 at 12.22.09 PM.png" alt=""><figcaption></figcaption></figure>

### Bibliografia

* [https://www.campusmvp.es/recursos/post/Que-diferencias-hay-entre-display-block-inline-e-inline-block-en-CSS.aspx](https://www.campusmvp.es/recursos/post/Que-diferencias-hay-entre-display-block-inline-e-inline-block-en-CSS.aspx)
* [Mejor pagina](https://dev.to/lupitacode/la-propiedad-display-en-css-1b6a)
* [https://lenguajecss.com/css/maquetacion-y-colocacion/propiedad-display/](https://lenguajecss.com/css/maquetacion-y-colocacion/propiedad-display/)
* [https://keepcoding.io/blog/propiedad-display-en-css/](https://keepcoding.io/blog/propiedad-display-en-css/)
