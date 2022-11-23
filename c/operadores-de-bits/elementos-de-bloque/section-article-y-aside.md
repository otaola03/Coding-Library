# Section, article y aside

### Section

Section es un contenedor generico que **agrupa contenido que esta relacionado**. Cuando creams bloques cuyo contenido es parte de un bloque usaremos section.

Su funcionalidad principal es estructurar semánticamente un documento a la hora de ser representado por parte de un agente usuario. Por ejemplo, un agente de usuario que represente el documento en voz, podría exponer al usuario el índice de contenido por niveles para navegar rápidamente por las distintas partes.

{% hint style="info" %}
Nota:

* No se debe usar el elemento `<section>` como un mero contenedor genérico; para esto ya existe `<div>`, especialmente si el objetivo solamente es aplicar un estilo (CSS) a la sección. Como regla general, el título de una sección debería aparecer en el esquema del documento.
{% endhint %}

```html
<section>
  <h1>Encabezado</h1>
  <p>Un montón de contenido impresionante.</p>
</section>
```

### Article

Es un contenedor que representa contenido independiente, es decir, podemos leer ese fragmente en cualquier otro sitio y tendria sentido por si mismo.

Algunos ejemplos podrían ser un mensaje en un foro, un artículo de una revista o un periódico, una entrada de blog, el comentario de un usuario, un widget o gadget interactivo, o cualquier otro elemento de contenido independiente.

Un mismo documento puede tener varios artículos; por ejemplo, en un blog en el que se que muestran distintos mensajes a medida que el usuario va navegando, cada mensaje estaría en un elemento `<article>`, posiblemente con uno o más elemenentos `<section>` dentro.

> Un \<article> puede tener su propio \<header> y \<footer>, ya que son contenido independinte.

#### Notas de uso <a href="#notas_de_uso" id="notas_de_uso"></a>

* Cada `<article>` debe ser identificado, normalmente con un elemento de encabezado (elementos [`<h1>` - `<h6>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/Heading\_Elements)) como hijo.
* Cuando un `<article>` está incorporado dentro de otro, representa un artículo cuyo contenido está relacionado con el artículo que lo anida. Por ejemplo, un comentario en una entrada de blog puede ser un `<article>` dentro de otro `<article>` que representa la propia entrada del blog.

### ¿Article o section? ¿Pueden estar juntos?

Si el fragmento de código posee significado por si mismo, si en caso de escribirlo en un papel separado del resto de la web el fragmento continua teniendo su sentido, podemos usar un `<article>`.

Si no tiene tanto sentido, pero tiene relación con lo comentado en el resto de esa página, podemos usar un `<section>`.

> Si no cumple con ninguna de las condiciones anteriores, pero necesitamos encerrarlo entre dos etiquetas para poder aplicarle estilos o scripts, entonces lo que debemos usar es un Div.

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

Aquí tenéis unos ejemplos que os pueden ser de utilidad a la hora de diferenciar las etiquetas article y section:

#### Un artículo sobre manzanas simple:

```html
  <article>
    <h1>Apple</h1>
    <p>La <b>manzana</b> es la fruta de la semilla de la manzana del árbol.</p>
    ...
  </article>
```

#### Un artículo sobre manzanas con un encabezado y un pie en el estilo de un blog:

```html
 <article>
    <header>
      <h1>Apple</h1>
      <p>En línea: <time pubdate="pubdate">09/10/2009</time></p>
    </header>
    <p>La <b>manzana</b> es la fruta de la semilla de la manzana del árbol.</p>
    ...
    <footer>
      <p><small>Licencia Creative Commons Reconocimiento-Compartir bajo la misma</small></p>
    </footer>
  </article>
```

#### Un artículo con secciones

```html
 <article>
    <h1>Las variedades de manzanas</h1>
    <p>La manzana es la fruta de la semilla de la manzana del árbol.</p>
    <section>
      <h2>Red Delicious</h2>
      <p>Estas manzanas rojas brillantes son los más comunes se encuentran en muchos supermercados.</p>
    </section>
    <section>
      <h2>Granny Smith</h2>
      <p>Estas manzanas verdes jugosas hacen un gran relleno para tartas de manzana.</p>
    </section>
  </article>
```

#### También podemos encontrar casos en que la sección sea el elemento contenedor de distintos artículos relacionados:

```html
 <section>
    <h1>Artículos sobre: Frutas</h1>
    <article>
      <h2>Manzana</h2>
      <p>La manzana es la fruta de la semilla de la manzana del árbol.</p>
    </article>
    <article>
      <h2>Naranja</h2>
      <p>La naranja es un híbrido de origen cultivado antiguo, posiblemente entre el pomelo y la mandarina.</p>
    </article>
    <article>
      <h2>Plátano</h2>
      <p>Los plátanos vienen en una variedad de tamaños y colores cuando madura, incluyendo amarillo, púrpura y rojo.</p>
    </article>
  </section>
```

### Aside

Se utiliza para respresentar contenido indirectamente relacionado pero que no forma parte del contenido principal

Estas secciones son a menudo representadas como barras laterales o como inserciones y contienen una explicación al margen como una definición de glosario, elementos relacionados indirectamente, como publicidad, la biografía del autor, o en aplicaciones web, la información de perfil o enlaces a blogs relacionados.

### Bibliografia

* [https://comocreartuweb.com/curso-de-html/estructura-semantica-html5/etiquetas-semanticas/section-o-article.html](https://comocreartuweb.com/curso-de-html/estructura-semantica-html5/etiquetas-semanticas/section-o-article.html)
* [https://www.espai.es/blog/2015/01/cuando-debemos-poner-section-y-cuando-article/](https://www.espai.es/blog/2015/01/cuando-debemos-poner-section-y-cuando-article/)
* [https://developer.mozilla.org/es/docs/Web/HTML/Element/section](https://developer.mozilla.org/es/docs/Web/HTML/Element/section)
* [https://developer.mozilla.org/es/docs/Web/HTML/Element/article](https://developer.mozilla.org/es/docs/Web/HTML/Element/article)
