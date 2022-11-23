# Imagenes

Antes de colocar una imagen en una página web debemos tener claro en que clasificación se encuentra. Las imágenes utilizadas en una página web pueden ser de dos tipos: de **contenido** o de **decoración**. En el primer caso, si la imagen pertenece al contenido y tema tratado en esa página, debería incluirse mediante una etiqueta HTML `<img>`, pero si por el contrario pertenece a la decoración de la página, deberíamos incluirla como un [fondo](http://lenguajecss.com/css/propiedades/fondos-css) mediante la propiedad CSS `background-image`.

### \<img>

Para incluir imágenes en el contenido de una página utilizaremos la etiqueta `<img>`, que es una etiqueta muy sencilla, que dispone de varios atributos para modificar como se verá la imagen (_los atributos src y alt son siempre obligatorios_):

* `src`: Indica el nombre o la URL de la imagen a mostrar. **Atributo obligatorio**.
* `alt`: Establece un texto alternativo que describa la imagen a mostrar. **Atributo obligatorio**.
* `width`: Indica el ancho de la imagen en píxels (sin la unidad). Se puede hacer desde CSS.
* `height`: Indica el alto de la imagen en píxels (sin la unidad). Se puede hacer desde CSS.

```html
<img src="https://lenguajehtml.com/img/logo.png" alt="Logotipo de HTML5" width="400" height="453" />
```

### Formatos de imagenes

En el ámbito informático existen múltiples formatos de imágenes (_¡muchísimos!_) pero no todos son aptos para utilizar en web. Vamos a dar un repaso a los formatos más utilizados y cuales son más apropiados:

| Formato  | Características                                                         | ¿Recomendado?        |
| -------- | ----------------------------------------------------------------------- | -------------------- |
| PNG      | Soporta transparencia. Compresión sin pérdidas. Imágenes «lisas».       | Sí                   |
| JPG      | Compresión con pérdidas. Ideal para imágenes con texturas.              | Sí                   |
| SVG      | Formato vectorial. Ideal para imágenes escalables.                      | Sí                   |
| GIF      | Formato para imágenes pequeñas y animadas.                              | Intentar evitar.     |
| WEBP     | Alternativa libre de Google al JPEG. Soporta transparencias. Muy ligera | Sí, con precaución   |
| JPEG2000 | Evolución del JPEG.                                                     | No, solo Safari      |
| JPEG-XR  | Alternativa libre de Microsoft al JPEG.                                 | No, solo IE          |
| APNG     | Alternativa libre a GIF. Compatible con PNG. Soporta animaciones.       | Sí, con precaución   |
| AVIF     | Formato de imagen basado en AV1. No confundir con videos AVI.           | Aún no, poco soporte |
| JPEG-XL  | Alternativa competidora a AVIF.                                         | Aún no, poco soporte |

Por otro lado, un factor muy importante a la hora de seleccionara las imagenes para tu pagina web e recomendable que sean imagenes de vectoriales, en vez de imagenes de bits. Es decir que se les pueda hacer todo el zoom que quieras sin perder calidad. Esto deverias tenerlo en cuenta al crear tu las imagenes de tu web. En caso de que las cogas de internet, suele ser mas dificil.

### Device Pixel Ratio (DPR)

Es el ratio entre los pixels lógicos y los pixels físicos de un dispositivo. Para ver el DPR de tu pantalla puedes utilizar la siguiente [web](https://whatismyviewport.com/).

Llamamos pixel físico a uno de los miles de puntos (hardware) que forman la pantalla de un dispositivo. Un pixel lógico, sin embargo, no tiene dimensiones específicas, sino que están establecidas por software por el fabricante. De esta manera en un dispositivo con device pixel ratio 1, un pixel lógico ocupará un pixel físico, en cambio en un dispositivo con device pixel ratio 2 un pixel lógico ocupará un área de la pantalla de 2×2 pixels físicos.

<figure><img src="https://binaria.com/static/13685990da344ed98a5ff7dcd6e3c646/549b4/dpr01.jpg" alt=""><figcaption></figcaption></figure>

> Podríamos comparar el valor del DPR con un lápiz, cuanto más alto sea el valor más fina será su punta. Pero eso no significa necesariamente que vayamos a hacer la letra más pequeña.

En el mundo del desarrollo web, DPR (también llamado CSS Pixel Ratio) **es lo que determina cómo la resolución de la pantalla de un dispositivo** es interpretada por CSS. De esta forma, todas las propiedades CSS relacionadas con las dimensiones de los elementos responderá a la resolución lógica y no a la resolución física.

La razón por la que se creó el DPR o CSS pixel ratio  fue el aumento de la resolución en los dispositivos móviles. Con el aumento de la densidad de pixels físicos, si todos los dispositivos tuvieran un DPR de 1 las páginas se renderizarían demasiado pequeñas.

#### Atributo srcset

A al hora de hacer una web responsive tenemos opciones que nos permiten cargar imágenes de unas dimensiones u otras en función del dispositivo que esté accediendo a nuestra web, y una de estas opciones es el atributo `srcset` de las imágenes.

Por lo general, cuando incluimos una imagen en nuestra web, incluimos un código HTML como el siguiente:

`<img src="imagen_grande.jpg" alt="la imagen de mi producto">`

Este código le dice al navegador que tiene que mostrar en esa parte de la página la imagen contenida en el fichero imagen\_grande.jpg. **Si utilizamos el atributo srcset, podemos darle distintas opciones de imágen en función del la resolución del dispositivo, por lo que podremos hacer que nuestras imágenes sean responsive**:

```html
<img src="
    imagen_grande.jpg,
    imagen_pequeña.jpg 2x" alt="la imagen de mi producto">
```

Con este fragmento de codigo conseguiremos que en el caso de que el device pixel ratio es de 2, el navegador cargara la `imagen_pequeña.jppg` y de ste manera se utilizaran menos recursos y obtimizaremos el contenido de nuestra web.

{% hint style="warning" %}
Hay algunos navegadores que no soportan srcset, por lo que es recomendable añadir siempre el `src` para que carge al menos una imagen
{% endhint %}

Esto tambien se puede utilizar para implementar varios tipos de imagenes y que de esta manera eel ordenador utilice el formato de imagen que soporte:

```html
<img src="
    imagen_grande.webp,
    imagen_grande.jpg" alt="la imagen de mi producto">
```

Otro ejemplo seria el siguiente:

```html
<img src="imagen_grande.jpg" srcset="imagen_pequena.jpg 300w, 
imagen_mediana.jpg 1000w, imagen_grande.jpg 2000w"alt="la imagen de mi producto">
```

De esta forma lo que le estamos diciendo al navegador es lo siguiente:

* Tienes una imagen por defecto, que es imagen\_grande.jpg, pero también tenemos otras opciones.
* Una imagen que se llama imagen\_pequena.jpg que tiene un ancho de 300 píxeles (se especifica con 300w y no con 300px como podría parecer)
* Una imagen que se llama imagen\_mediana que tiene un ancho de 1000 píxeles

Con esto el navegador ya tiene información para poder determinar qué imagen debe cargar. Para hacerlo, primero tiene en cuenta un par de datos del dispositivo. Imaginemos que estamos accediendo desde un dispositivo no retina (1x, ya que no tiene una resolución mayor de la habitual) y unas dimensiones de 320 píxeles de ancho de la pantalla:

* imagen\_pequena.jpg: 300 píxeles de ancho / 320 píxeles de la pantalla = 0,9375
* imagen\_mediana.jpg: 1000 píxeles de ancho / 320 píxeles de la pantalla = 3,125
* imagen\_grande.jpg: 2000 píxeles de ancho / 320 píxeles de la pantalla = 6,25

En este caso el navegador cogería la imagen\_mediana.jpg ya que imagen\_pequeña tiene un ratio de 0,9375 (menor del 1x de los dispositivos no retina) para asegurarse estar cogiendo la imagen más pequeña que le proporciona una buena calidad.

Si estuviéramos accediendo con un dispositivo retina (2x) entonces se buscaría que el ratio fuera mayor de 2 y no de 1.

### Atributo picture

El elemento HTML `<picture>` es un contenedor usado para especificar múltiples elementos `<source>` y un elemento `<img>` contenido en él para proveer versiones de una imagen para diferentes escenarios de dispositivos.&#x20;

Si no hay coincidencias con los elementos `<source>`, el archivo especificado en los atributos `src` del elemento `<img>` es utilizado. La imagen seleccionada es entonces presentada en el espacio ocupado por el elemento `<img>`.

<pre class="language-html"><code class="lang-html">&#x3C;picture>
    &#x3C;source srcset="
        ../assets/images/index/banner-lorem-ipsum-herreria-desktop.webp,
        ../assets/images/index/banner-lorem-ipsum-herreria-desktop.jpg"
<strong>        media="(min-width:1200px)">
</strong>    &#x3C;source srcset="
        ../assets/images/index/banner-lorem-ipsum-herreria-mobile.webp,
        ../assets/images/index/banner-lorem-ipsum-herreria-mobile.jpg"
        media="(max-width:1200px)">
    &#x3C;img src="/assets/images/index/banner-lorem-ipsum-herreria-desktop.jpg" 
    alt="Banner Lorem Ipsum">
&#x3C;/picture></code></pre>

Como puedes observar se pueden anidar varias etiquetas source dentro de picture haciendo que asi podamos tener una imagen para mobile y otra para desktop, la ultima etiqueta img es un "fallback" el cual va a cargar en caso de que el navegador no agarre la etiqueta srcset.

> Como norma general se suele utilizar `picture`, en vez de `img` y `srcset`.

### Bibligrafia

* [https://www.fotografiaecommerce.com/blog/imagenes-responsive-srcset/](https://www.fotografiaecommerce.com/blog/imagenes-responsive-srcset/)
* [https://lenguajehtml.com/html/multimedia/etiquetas-html-de-contenido-externo/](https://lenguajehtml.com/html/multimedia/etiquetas-html-de-contenido-externo/)
* [https://developer.mozilla.org/es/docs/Web/HTML/Element/picture](https://developer.mozilla.org/es/docs/Web/HTML/Element/picture)
