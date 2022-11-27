# Selectores

Cuando comenzamos a trabajar con CSS, es habitual dar estilo con ejemplos muy sencillos, donde generalmente utilizamos un **selector genérico** que representa (_por ejemplo_) una **etiqueta HTML** como por ejemplo `<div>`. Sin embargo, lo que estamos haciendo en realidad es seleccionar todos los elementos del documento que sean dicha etiqueta.

Aunque el esquema general es mucho más amplio (_lo iremos viendo poco a poco_), para empezar, vamos a centrarnos en la sintaxis más básica de los selectores CSS: por etiqueta, por **ID** y por **clases**.

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### Selectores elementales

Los selectores elementales se utiliza cuando queremos hacer referencia a un grupo y ha dos tipos distinto, los de **tipo** o etiqueta, y el **universal**. Este ultimo se utiliza cuando queremso aplicar una propiedad a todo el documento:

```css
*{
    background-color: lightblue;
}
```

Es un selector que hay que utilizar con cuidado y solo se debe utilizar en ciertos momentos muy concretos. No es recomendable abusar de el ni utilizarlo para establecer `margin=0;`, aunque se ve muy a menudo.

#### Selector de etiqueta

Este selector se dirige a los tipos de elementos en la página, expecificamente a los elementos regulares, `<p>`, `<h1>`, `<h2>` ... y modifican todas las instancias de ese elemento en su página. Por ejemplo, con el siguiente fragmento de código se le aplicará un estilo a todas las etiquetas `<h2>` en su página, aplicandoles una fuente verde y un fondo negro.

```css
h2{
    color: green;
    background-color: black;
}
```

### Selectores de id

En ocasiones, es necesario **aplicar estilos CSS a un único elemento de la página**. Aunque puede utilizarse un selector de clase para aplicar estilos a un único elemento, existe otro selector más eficiente en este caso.

El selector de ID permite seleccionar un elemento de la página a través del valor de su atributo `id`. Este tipo de selectores sólo seleccionan un elemento de la página porque el valor del **atributo `id` no se puede repetir en dos elementos diferentes** de una misma página.

La sintaxis de los selectores de ID es muy parecida a la de los selectores de clase, salvo que se utiliza el símbolo de la almohadilla (`#`) en vez del punto (`.`) como prefijo del nombre de la regla CSS:

```css
#identified {
  background-color: skyblue;
}
```

Aunque pueda ser de utilidad, no es recomendable dar estilos mediante el `id`, pesto que solo puede haber uno y uno de los principio de CSS es que los estilos puedan ser reutilizables.

### Selectores de clase

Este tipo de selectores  son los más utilizados junto con los selectores de ID . La principal característica de este selector es que en una misma página HTML varios elementos diferentes pueden utilizar el mismo valor en el atributo `class`:

```html
<body>
  <p class="destacado">Lorem ipsum dolor sit amet...</p>
  <p>Nunc sed lacus et <a href="#" class="destacado">est adipiscing</a> accumsan...</p>
  <p>Class aptent taciti <em class="destacado">sociosqu ad</em> litora...</p>
</body>
```

Esto sería útil, por ejemplo, si quisiera diseñar varios párrafos de su página, pero no todos, de la misma manera. Esto le ahorraría la molestia de escribir muchos CSS repetitivos en línea. Para apuntar a un selector de clase, use un punto (`.`), en lugar de un hash, seguido del valor / nombre de la clase. Puede nombrar la clase como desee, siempre que no comience con un número y no se hay utilizado ese nombre anteriormente.

```css
.text1 {
  padding: 0.5em;
  border: 1px solid #98be10;
  background: #f6feda;
}
```

> A un elemento se le pueden poner el numero de clases que desees.

### Selectores de atributo

En esta sección vamos a ver los selectores de atributos que nos permitirán también realizar una selección más específica de los elementos a los que queremos aplicar un cierto estilo en función de los atributos o valores que tengan asignados.

Los **selectores de atributos** permiten elegir elementos HTML en función de sus atributos y/o **valores** de esos atributos.

Los tipos de selectores de atributos son los siguientes:

* \[**nombre\_atributo**], selecciona los elementos que tienen establecido el atributo llamado nombre\_atributo independientemente de su valor.&#x20;
* \[**nombre\_atributo=valor**], selecciona los elementos que tienen establecido un atributo llamado nombre\_atributo con un **** valor igual a valor**.**
* \[**nombre\_atributo\~=valor**], selecciona los elementos que tienen establecido un atributo llamado nombre\_atributo y al menos uno de los valores del atributo es valor**.**
* \[**nombre\_atributo|=valor**], selecciona los elementos que tienen establecido un atributo llamado nombre\_atributo, cuyo valor es una lista de valores, donde alguno comienza por valor**.**
* \[**nombre\_atributo$=valor**] Selecciona aquellas etiquetas cuyo atributo acabe en ese valor.
* \[**nombre\_atributo^=valor**] Selecciona aquellas etiquetas cuyo atributo comience por ese valor.

```css
[href="https://google.com"]{  //Es recomendable utilizar siempre lass comillas
    background-color: orange;
}
```

### Selectores agrupados

Uno de los principios de CCS en "don't repeat yourself", es decir no repitas varias veces el mismo código, por ello para ahorrarnos esas repeticiones, podemos crear un selector agrupado. Para ello tan solo hay agrupar los selectores q los que queramos dar la misma porpiedad y separarlos por comas:&#x20;

```
.text, .text-2, tex-3{
    background-color: steelblue;
}
```

Este tipo de codigo facilita muchísimo la lectura al navegador. Es verdad, que en este caso la diferencia de optimización no es apreciable y se podria poner por separado, pero en e momento aunque estas clases tenga muchísimas lineas mas, la diferencia de optimización es abismal.

### Selectores combinadores

Los selectores combinadores combinan otros selectores de manera que proporciona una relación útil entre ellos y la ubicación del contenido en el documento.

#### Selector descendiente (hijos)

Selecciona los elementos que se encuentran dentro de otros elementos. Un elemento es descendiente de otro cuando se encuentra entre las etiquetas de apertura y de cierre del otro elemento.

> Las buenas practicas especifican que nos es recomendable tener mas de un nivel, es decir, lo recomendable es el ejemplo siguiente

El selector del siguiente ejemplo selecciona todos los elementos `<span>` de la página que se encuentren dentro de un elemento `<p>`:

```css
p span { color: red; }
```

El selector `p span` selecciona tanto `texto1` como `texto2`. El motivo es que en el selector descendente, un elemento no tiene que ser descendiente directo del otro. La única condición es que un elemento debe estar dentro de otro elemento, sin importar el nivel de profundidad en el que se encuentre.

Al resto de elementos `<span>` de la página que no están dentro de un elemento `<p>`, no se les aplica la regla CSS anterior.

#### Selector de hermano siguiente

El selector de elementos hermanos adyacentes (`+`) se utiliza para seleccionar un elemento que se encuentra justo al lado de otro elemento en el mismo nivel de la jerarquía. Por ejemplo, para seleccionar todos los elementos `<img>` que aparecen justo después de elementos `<p>`:

```css
p + img {}
```

El caso de uso más común es modificar el párrafo que va justo después del título, como en el ejemplo siguiente. Vamos a buscar un párrafo que sea directamente adyacente a `<h1>` y le vamos a aplicar un estilo.

> Esto solo sirve para sleccionar ele elemento siguiente al que hemos especificado, no se puede acceder al anterior.

#### Selector de hermano siguiente

Si deseas seleccionar todos los hermanos de un elemento, incluso si no son directamente adyacentes, puedes utilizar el combinador de hermanos general (`~`). Por ejemplo, para seleccionar todos los elementos `<img>` que aparecen _después_ de los elementos `<p>`, hacemos esto:

```css
p ~ img {}
```

#### Selector de hijo directo

El selector de combinación de elementos hijo es un símbolo de «mayor que» (`>`), que selecciona solo cuando los selectores identifican elementos que son hijos directos. Los elementos descendientes que se encuentran más abajo en la jerarquía no se seleccionan. Por ejemplo, para seleccionar solo los elementos `<p>` que son hijos directos de elementos `<article>`:

<pre class="language-css"><code class="lang-css"><strong>article > p {}</strong></code></pre>

Esto nos libra de seleccionar los hijos de los hijos, a la hora de utilizar el siguiente código. Es decir no libra de leccioanr todos los `<p>` que haya dentro de `<article>.`

```css
article p {}
```





### Bibliografia

* [https://uniwebsidad.com/libros/css/capitulo-2/selectores-basicos](https://uniwebsidad.com/libros/css/capitulo-2/selectores-basicos)
* [https://www.eniun.com/selector-atributos-css/](https://www.eniun.com/selector-atributos-css/)
* [https://developer.mozilla.org/es/docs/Learn/CSS/Building\_blocks/Selectors/Combinators](https://developer.mozilla.org/es/docs/Learn/CSS/Building\_blocks/Selectors/Combinators)
