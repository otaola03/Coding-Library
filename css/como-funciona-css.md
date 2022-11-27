# Como funciona CSS

A la hora de aplicar estilos con CSS de vez en cuando te puede surgir el problema de que no se te aplique algun estilo y esto seguramente sera devido a algun inconveniente de  **cascada o especificidad**.

### Qué es la cascada en CSS

La cascada es el algoritmo por el cual el navegador decide qué estilos CSS aplicar a un elemento - a mucha gente le gusta pensar en esto como el estilo que "gana".

Especifica cómo el navegador debe manejar múltiples estilos que se aplican a la misma etiqueta HTML y qué hacer cuando las propiedades CSS entran en conflicto. La cascada es una parte fundamental del funcionamiento del lenguaje.

Los conflictos de estilo se producen en dos casos: por herencia y cuando uno o más estilos se aplican al mismo elemento.

Cabe mencionar que las iniciales de CSS significan **C**ascading **S**tyle **S**heets (Hojas de Estilo en Cascada), y es muy importante entender la palabra cascada ya que como podrás darte cuenta forma parte del propio nombre.

* En cascada se refiere a la forma en que CSS aplica un estilo encima de otro.
* Las hojas de estilo controlan la apariencia de los documentos web.

Podemos decir entonces que **la cascada es el algoritmo para resolver conflictos cuando se aplican varias reglas CSS a un mismo elemento HTML**. La forma en que se comporta la cascada es la clave para comprender el CSS.

Para que quede mas claro, aunque se le este aplicando dos colores distintos al siguiente ejemplo, el color que prevalecerá sera el azul, ya que es el que esta más abajo.

```css
h1 {
    color: red;
}

h1 {
    color: blue;
}
```

Si aun no te a quedado claro en esta pagina se [explica](https://dev.to/lupitacode/la-cascada-en-css-que-es-y-como-funciona-31cd) todo de una manera mas profunda.

### Qué es especificidad en CSS

La especificidad consiste en dar un valor a una regla CSS sobre **qué tan específico es el estilo**, esto para que los navegadores puedan saber qué estilos aplicar sobre otros, independientemente de dónde se encuentren en el código. **El estilo se aplicará donde la especificidad sea mayor.**

Existen 6 tipos de especificidad con su respectivo valor, donde `X` es la cantidad de estilos que lo contienen. Mira la siguiente imagen:

```
!important                         x0000
Estilos en linea                   x000
#id                                x00
clases, atributos y pseudclases    x0
Elementos y pseudoelementos        x
Selector universal                 0
```

Para ahorrarte los problemas de especificidad y  de que no se te apliquen clases. los mas recomendable e utilizar siempre clases y no utilizar nunca !important. En el caso de que quieras comprobar ti sienes un buen codigo de CSS puede utilizar la pagina [CSS Specificity Graph](https://jonassebastianohlsson.com/specificity-graph/) y en el caso de que tengas muchos picos y no sea nada lineal significa que tu codigo esta mal

### Herencia

La herencia es el proceso por el cual algunas propiedades CSS aplicadas a una etiqueta se pasan a las etiquetas anidadas.

Si un elemento no tiene un valor en cascada para una determinada propiedad, puede heredar uno de un elemento antecesor. Es común aplicar la propiedad `font-family` al elemento `<body>`. Todas las etiquetas descendientes de la etiqueta `<body>`, es decir, las que están dentro de la etiqueta `<body>` heredarán esta fuente y no es necesario aplicarla explícitamente a cada elemento de la página.

{% hint style="info" %}
**NOTA:** Cualquier etiqueta dentro de otra etiqueta es descendiente de esa etiqueta. por ejemplo, una etiqueta `<p>` dentro de la etiqueta `<body>` es descendiente de `<body>`, mientras que la etiqueta `<body>` es un ancestro de la etiqueta `<p>`.
{% endhint %}

La herencia también funciona a través de múltiples generaciones. Si una etiqueta como `<em>` o `<strong>` aparece dentro de una etiqueta `<p>`, entonces las etiquetas `<em>` y `<strong>` también heredan las propiedades de cualquier estilo aplicado a la etiqueta `<body>`.

La siguiente imagen muestra cómo la herencia fluye hacia abajo en el árbol del DOM. Las propiedades heredadas se transfieren por el árbol DOM desde los nodos padres a sus descendientes.

<figure><img src="https://dev-to-uploads.s3.amazonaws.com/uploads/articles/xptrm0otvatj9idia7o6.jpg" alt=""><figcaption></figcaption></figure>

#### Valores especiales

Podemos aplicar ciertos **valores especiales** que son **comunes** a todas las propiedades CSS existentes. Con estos valores modificamos el comportamiento de la herencia en dicha propiedad:

|         |                                                                                                  |
| ------- | ------------------------------------------------------------------------------------------------ |
| inherit | La propiedad hereda el valor que tiene la misma propiedad CSS en su elemento padre               |
| initial | Establece el valor al **valor inicial** definido por la especificación CSS.                      |
| unset   | Resetea el valor. En propiedades heredables, actua como `inherit`, en otro caso, como `initial`. |
| revert  | Similar a `unset`, salvo que haya definido un origen de agente o de usuario                      |

### Estilos y prefijos de los navegadores

Aunque hay establecidas ciertas normas de estilo, cada nevegador tines unos estilos propios predefinidos y cuanto mas viejo el navegador o dispositivo mas distintos seran estos estilos por defecto de los actuales.

Por ello existe un archivo CSS que normaliza estos estilos, es decir los resetea. De esta manera nuestra pagina web se vera igual en todos los navegadores. Mas o menos.

{% embed url="https://necolas.github.io/normalize.css/" %}

Para pode utilizar la hoja tan solo hay que **añadirla al principio** de nuestro head. Tiene que estar al principio para respetar la cascada.

```html
<head>
    <link rel="stylesheet" href="normalize.css" />
    <link rel="stylesheet" href="styles.css" />
</head>
```

Con respecto a los prefijos, como no siempre loss navegadores esta actualizados es necesario aplicar a ciertos estilos algunas prefijos, para que esos estilos funcionen en ciertos navegadores. Sin embargo, como los navegadores va actualizandose este prefijos iran cambiando y por ello utilizaremos el siguiente programa para que nos ponga los prefijos automaticamente

{% embed url="https://prepros.io/" %}

Para aprender a usar prepros:

{% embed url="https://youtu.be/d9cBmsODumI?list=PLROIqh_5RZeDbvISffzihyxzqJBt_z3-Z&t=392" %}

Este proceso es posible realizarlo sin programs externos, pero es necesario tener conocimiento sobre otros temas en programacion.

### Bibliografia

* [Especificidad](https://dev.to/lupitacode/especificidad-en-css-que-es-y-como-funciona-52k6)
* [Cascada](https://dev.to/lupitacode/la-cascada-en-css-que-es-y-como-funciona-31cd)
* [Especificidad y cascada](https://platzi.com/clases/2467-frontend-developer/40837-cascada-y-especificidad-en-css/)
* [https://codigofacilito.com/articulos/la-herencia-en-css](https://codigofacilito.com/articulos/la-herencia-en-css)
* [https://lenguajecss.com/css/cascada-css/herencia-css/](https://lenguajecss.com/css/cascada-css/herencia-css/)
