# Position

La propiedad CSS position establece cómo se posiciona un elemento en un documento. Las propiedades `top`, `right`, `bottom` y `left` determinan la ubicación final de los elementos posicionados.

Por defecto, la propiedad `position` de todos los elementos HTML en CSS se establece como `static`. Esto significa que si no se especifica ningún otro valor de `position` o si la propiedad position no se declara explícitamente, será `static`.

Visualmente, todos los elementos siguen el orden del código HTML, y de esa manera se crea el típico flujo del documento.

<img src="https://www.freecodecamp.org/news/content/images/2021/08/Screenshot-2021-08-30-at-2.00.39-PM.png" alt="Screenshot-2021-08-30-at-2.00.39-PM" data-size="original">

### top, right, bottom, left

Recordemos que cada elemento HTML contiene su propio sistema de coordenadas local (`top`, `right`, `bottom` y `left`). Estas propiedades empujara el elmentos hacia la direccion especificada.

Por ejemplo, si desea colocar un elemento hijo dentro de un elemento padre ya situado en algún lugar de su documento HTML, el hijo heredará el sistema de coordenadas del padre, que tiene su origen en la esquina superior izquierda del elemento padre (0x0).

> Al mover un elementos este se mueve con respecto a su posicion inicial

### position relative <a href="#whatispositionrelativeincss" id="whatispositionrelativeincss"></a>

`position: relative` funciona igual que `position: static;`, pero **permite cambiar la posición de un elemento**.

Sin embargo, escribir sólo esta regla CSS no cambiará nada.

Para modificar la posición, tendrás que aplicar las propiedades `top`, `bottom`, `right` y `left` mencionadas anteriormente y de esa manera especificar dónde y cuánto quieres mover el elemento.

Ahora, puedes mover el primer cuadrado a la izquierda actualizando el CSS así:

![Screenshot-2021-08-30-at-2.14.15-PM](https://www.freecodecamp.org/news/content/images/2021/08/Screenshot-2021-08-30-at-2.14.15-PM.png)&#x20;

`position: relative;` cambia la posición del elemento con respecto al elemento padre y con respecto a sí mismo y a donde estaría normalmente en el flujo regular del documento de la página. Esto significa que es relativo a su posición original dentro del elemento padre.

### position absolute <a href="#whatispositionabsoluteincss" id="whatispositionabsoluteincss"></a>

El elemento es eliminado del flujo del documento y los demás elementos se comportarán como si no estuviera allí, mientras que todas las demás propiedades posicionales funcionarán en él.  Si lo mueves usará el elemento posicionado contenedor como referencia. Si no tiene ninguno, usara el elemento html como referencia.

{% hint style="warning" %}
Con `position: absolute;` el elemento pierde sus medidas, en vez de ocupar el 100% como un elemento de bloque, ocupa lo que ocupe su contenido ya que **pierde su espacio reservado**. Sin embargo, si le aplicas tu medidas con `width` y `height` este ocupara lo que le especifiques.
{% endhint %}

Para que quede mas claro observa lo que genera el siguiente codigo:

```css
.one {
  background-color: powderblue;
  position: absolute;
}
```

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Como puedes observar la caja 2 ha "desaparecido". Esto de debe a que como ya no esta en el flujo normal, los demas objetos se comportan como si no existiera y por ello suben todos una posicion hacia arriba. &#x20;

### Relacion entre posicion relativa y absoluta <a href="#posici-n-relativa-vs-absoluta-en-css" id="posici-n-relativa-vs-absoluta-en-css"></a>

Ambas posiciones, la relativa y la absoluta, funcionan de la misma manera excepto en un campo. Usamos _**relative**_ para identificar las clases padre. Y usamos _**absolute**_ para identificar las clases hijo.

<figure><img src="https://www.freecodecamp.org/espanol/news/content/images/2021/08/relab.png" alt="relab"><figcaption></figcaption></figure>

Para que quede mas claro aqui tienes el siguiente ejemplo;

```html
<body>
   <div class="caja-1">
    
       <div class="caja-2"> </div>	
        
   </div>
</body>
```

```css
.caja-1{
	width: 300px;
	height: 300px;
	background-color: skyblue;
	border: 2px solid black;
    margin: auto;
}

.caja-2{
	width: 100px;
	height:100px;
	background-color: pink;
	border: 2px solid black;
}
```

Debería verse así:

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-25 at 4.39.33 PM.png" alt=""><figcaption></figcaption></figure>

Ahora, seleccionamos nuestras clases así:&#x20;

```css
body{ }

.caja-1{ }

.caja-2{ }
```

Ahora, escribe esto en tu código CSS:&#x20;

```css
body{
	
}

.caja-1{
/* Este es el padre */
	position: relative;
}
.caja-2{
/* Este es el hijo */
	position: absolute;
	left: 100px;
}
```

Aquí está el resultado:&#x20;

<figure><img src="https://www.freecodecamp.org/news/content/images/2021/06/Frame-14.png" alt="Frame-14"><figcaption><p><strong>The result is that the pink box has moved right 100px</strong></p></figcaption></figure>

Observa que la _.caja-2_ se movió **100px** a partir _.caja-1_.

Esto es porque _.caja-1_ es el **padre** y _.caja-2_ es el **hijo**.

Cambiémoslo otra vez. Escribe esto en tu código CSS:

```css
body{
/* Este es el padre */
   position: relative;	
}

.caja-1{

}
.caja-2{
/* Este es el hijo */
   position: absolute;
    left: 100px;
}
```

Aquí tenemos el resultado:&#x20;

<figure><img src="https://www.freecodecamp.org/news/content/images/2021/06/Frame-15.png" alt="El resultado es que la caja rosa se movió 100px desde el body."><figcaption><p><strong>The result is that the pink box has moved 100px from the body</strong></p></figcaption></figure>

Observa que _.caja-2_ se movió 100px a partir el elemento **body**.

Esto es porque el **body** es el **padre** y _.caja-2_ es el **hijo**.

### Position fixed

funciona parecido a `position: absolute;`, el elemento perdera su posicion y medidas y en el caso de que lo movamos usara el elemento html de referecia. Sin embargo la propiedad unica que tiene, es que aunque hagamos scroll, se quedara fijo en esa posicion de la pantalla

> Con la aparición de sticky ya casi no se usa, sobretodo esta para dar soporte a naavegadores antiguos

con un ejemplo visual quedara mas claro:

```html
<div class="contenedor">
	<p>lorem200</p>   
	<div class="caja-1"> fixed </div>
	<p>lorem200</p>		
</div>
```

```css
.contenedor{
	height: 3000px;
}

.caja-1{
	height: 120px;
	width: 120px;
	background-color: skyblue;
	border: 2px solid black;
	
	display: grid;
	place-content: center;
	
	position: fixed;
	top: 100px;
	left: 200px;
}
```

Aquí está el resultado:

<figure><img src="https://media.giphy.com/media/J6hbBulobEQz6HftRv/giphy.gif" alt=""><figcaption></figcaption></figure>

### Position sticky

Después de desplazarnos a cierto punto de nuestra pantalla este valor, podrá **fijar la posición** de nuestro elemento en la pantalla entonces no se moverá.

{% hint style="info" %}
`position: sticky;` coge como referencia el `height` del elemento padre, por ello si el padre no tiene un `height` establecido esta propiedad no funcionara.
{% endhint %}

```css
.caja-1{
   position: sticky;
   top: 30px;
   left: 200px;
}
```

<figure><img src="https://media.giphy.com/media/175hkevbKC3yUfiLQc/giphy.gif" alt=""><figcaption></figcaption></figure>

El elemento solo se queda pegado "sticky" mientras recorra el height del padre. Es decir si el padre tiene `200px`, y le aplicamos a nuestra caja un `top: 50px` el elemento estara pegado a partir del pixel 50 durante `150px`. Luego, si seguimos haciendo scroll si ira para arriba.

{% hint style="warning" %}
Con la propiedad `overflow` declarada no funciona
{% endhint %}

### z-index

La propiedad `z-index` en CSS se utiliza para **ordenar los elementos que se superpongan entre sí**. Con la propiedad `z-index` podemos controlar qué elemento iría encima y cual debajo, como si el documento tuviera **profundidad**, tres dimensiones en lugar de dos.

El valor predeterminado de `z-index` es `auto`. El navegador irá ordenando los elementos en el **orden en el que aparezcan**, el primero quedará abajo y los siguientes elementos se irán apilando encima. Esta regla la aplica en este orden:

1. Primero posiciona el **elemento raíz** `<html>`
2. Luego los **elementos no posicionados** (cualquiera con el valor predeterminado `position: static`)
3. Luego los **elementos posicionados** (cualquiera con `position: relative`, `position: absolute`, `position: fixed`, `position: sticky`, o cualquier otro valor diferente a `position: static`).

> Al tener dos elementos posicionados prevalece el orden del HTML

Vamos a ver como los elementos no posicionados son colocados primero **aunque aparezcan los últimos en el HTML**:

```html
<style>
    .azul, .rojo, .verde {
        position: absolute;
    }
</style>
<div class="rojo">
    <div class="verde"></div>
</div>
<div class="gris"></div>
<div class="azul"></div>
```

El orden de apilamiento automático daría lugar al siguiente resultado:

<figure><img src="https://cybmeta.com/wp-content/uploads/2018/06/stacking-predeterminado-1-1024x660.png" alt=""><figcaption></figcaption></figure>

{% hint style="info" %}
No es recomendable utilizar los valores de uno en uno, mejor hacerlo de diez en dize o de cien en cien, por si algun dia quieres meter un valor entre medias
{% endhint %}

Ahora utilizando `z-index`, queda el siguiente resultado

```css
.gris, .rojo, .verde {
    position: absolute;
}
.gris {
    z-index: 2;
}
.verde {
    z-index: 3;
}
.azul {
    z-index: 100; // Sin efecto, es un elemento no-posicionado.
}
```

<figure><img src="https://cybmeta.com/wp-content/uploads/2018/06/z-index-ejemplo-1a-1024x660.png" alt=""><figcaption></figcaption></figure>

Un problema muy común a la hora de utilizar `z-index` es intentar colocar un elemento padre por delante de un elemento hijo. Esto es totalmente imposible. Lo que si es posible y aunque parezca lo mismo, es colocar un elemento hijo por detrás del padre. Para esto tan solo hay que aplicarle la propiedad `z-index` negativa al hijo.

```css
.verde {
    z-index: -1;
}
```

Sin embargo, en el momento en el que le demos un valor `z-index` al padre esto se rompera. Es decir que para que un hijo este por detrás de un padre, es necesario que el padre no tenga la propiedad `z-index` o que tenga declarado `z-index: auto;`.

### Bibliografia

* [https://developer.mozilla.org/en-US/docs/Web/CSS/position](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
* [https://dev.to/lupitacode/guia-completa-y-practica-sobre-posicionamiento-css-position-absolute-3ghn](https://dev.to/lupitacode/guia-completa-y-practica-sobre-posicionamiento-css-position-absolute-3ghn)
* [https://www.freecodecamp.org/news/css-positioning-position-absolute-and-relative/](https://www.freecodecamp.org/news/css-positioning-position-absolute-and-relative/)
* [https://www.freecodecamp.org/espanol/news/como-funciona-la-propiedad-posicion-en-css-explicada-con-codigos-de-ejemplo/](https://www.freecodecamp.org/espanol/news/como-funciona-la-propiedad-posicion-en-css-explicada-con-codigos-de-ejemplo/)
* [https://css-tricks.com/almanac/properties/p/position/](https://css-tricks.com/almanac/properties/p/position/)
* [https://cybmeta.com/como-se-utiliza-z-index](https://cybmeta.com/como-se-utiliza-z-index)
