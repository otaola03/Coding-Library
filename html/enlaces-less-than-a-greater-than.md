# Enlaces \<a>

El _Elemento HTML `Anchor`_ **`<a>`** crea un enlace a otras páginas de internet, archivos o ubicaciones dentro de la misma página, direcciones de correo, o cualquier otra URL.

### **Atributos**

#### **href**

El atributo `href` contiene una URL o un fragmento de URL al cual apunta el enlace. Un fragmento de URL es un nombre ("name") precedido por el símbolo de número (`#`), el cual especifíca una ubicación interna objetivo (un ID (en-US) de un elemento HTML) dentro del actual documento. Estos de los id se utiliza para navegar entre elementos de la misma pagina y se le llama [navegación con anclas](enlaces-less-than-a-greater-than.md#navegacion-con-anclas)

<pre class="language-html"><code class="lang-html">&#x3C;!-- enlace a un elemento en esta página con id="attr-href" -->
&#x3C;a href="#attr-href">
Descripción de enlaces de la misma página
<strong>&#x3C;/a></strong></code></pre>

Por otro lado tambien podemos nevegar entre distintas paginas internas mediante las direcciones de los archivos html, o utilizarla para mandar al usuario a otras pagina web, mediante su direcciones. Esto se logra medinate rutas absolutas y relativas

```html
<a href="./contactos.html" target="_blank"> Contactos </a>
<a href="https://developer.mozilla.org/en-US/" target="_blank"> Enlace </a>
```

#### target

Define donde se abrirá el recurso solicitado. Por normal general ssiempre que se utilicen rutas absolutas se pondra como valor `"_blank"`. Aunque hay mas opciones disponibles:

* `_self`: Carga la URL en el mismo contexto de navegación que el actual. Este es el comportamiento por defecto.
* `_blank`: Carga la URL en un nuevo contexto de navegación. Usualmente es una pestaña, sin embargo, los usuarios pueden configurar los navegadores para utilizar una ventana nueva en lugar de la pestaña.
* `_parent`: Carga la URL en el contexto de navegación padre (_parent_) del actual. Si no existe el padre, este se comporta del mismo modo que `_self`.
* `_top`: Carga la URL en le contexto más alto de navegación (el cual es un ancestro del actual, y no tiene padre (_parent_)). Si no hay padre (_parent_), este se comporta del mismo modo que `_self`.

```html
<a href="archivos/curso.pdf" target="_blank"> Descargar </a>
```

#### download

Este atributo, indica descargar a los navegadores una URL en lugar de navegar hacia ella, por lo que el usuario será dirigido para descargarla como un archivo local. Si el atributo tiene un valor, éste se utilizará como nombre de archivo por defecto en el mensaje Guardar que se abre cuando el usuario hace clic en el enlace (sin embargo, el usuario puede cambiar el nombre antes de guardar el archivo).

> Solo funciona con archivos locales, no se pueden poner enlaces a otras paginas web externas a la nuestra. Hay que especificar claremente la direccion local del archvio.

Se debe tener en cuenta que la mayoría de los sistemas de archivos tienen limitaciones con respecto a los símbolos de puntuación admitidos en los nombres de archivo, por lo que los navegadores ajustarán los nombres de los archivos en consecuencia.

```html
<a href="archivos/curso.pdf" download> Descargar </a>
```

### Rutas absolutas

Este tipo de rutas especifican la dirección directa al archivo alojado en un servidor (hosting), se debe de escribir la URL completa del archivo, por ejemplo si tenemos el archivo **curso.pdf** alojado en el servidor, escribimos su URL absoluta o completa.

Tienen un protocolo, http, https y son únicas en lar red y se suelen utilizar para rutas externas.

```html
<!-- Ruta absoluta al archivo curso.pdf --> 
<a href="https://www.mipaginaweb.com/archivos/curso.pdf" alt="Curso"> Descargar PDF </a>
```

Una de las ventajas de este tipo de rutas es que al copiar y pegar la URL no hay errores, porque estamos usando una ruta que ya existe en el servidor y no hay que averiguar algo mas, salvo casos específicos.

### Rutas relativas

Este tipo de rutas especifican la ruta de un archivo en su ubicación actual en el servidor o directorio del proyecto, por ejemplo un archivo PDF puede estar apuntando al directorio **archivos** pero en 3 niveles arriba de la ubicación actual del archivo **index.html**

```html
<!-- Ruta relativa al archivo curso.pdf --> 
<a href="../../../archivos/curso.pdf" alt="Curso"> Descargar PDF </a>
```

También podemos tener el archivo en el directorio **archivos** que este en el mismo directorio en donde se encuentre el archivo **index.html**

```html
<!-- Ruta relativa al archivo curso.pdf --> 
<a href="archivos/curso.pdf" alt="Curso"> Descargar PDF </a>
```

Como puedes ver, las rutas relativas, especifican los directorios y sus nombres para cargar un archivo

{% hint style="info" %}
**Nota:** Es necesario que en el directorio raiz `href="/"` es necesario que este el elemento `index.html`. Des esta manera mediante este enlace podras acceder al index.
{% endhint %}

Pero tiene una inconveniente, si por error se borran los directorios o cambian el nombre de estos, el archivo dejará de mostrarse, porque la ruta cambiaría.

### Navegación con anclas

La nevegacion mediante anclas se utiliza para moverse por la pagina mediante distinto marcadores que se establezcan. Los marcadores se establecen con el atributo `id`y para acceder a ellos con un enlace `<a>` habra que que poner en su `href` el nombre del `id` con `#` por delante.

```html
<nav>
    <a href="#post-1">Post 1</a>
    <a href="#post-2">Post 2</a>
    <a href="#post-3">Post 3</a>
</nav>
<article id="post-1">
    <h2>Post 1</h2>
    <p>Este es el posto numero 1</p>
</article>
<article id="post-2">
    <h2>Post 1</h2>
    <p>Este es el posto numero 1</p>
</article>
<article id="post-3">
    <h2>Post 1</h2>
    <p>Este es el posto numero 1</p>
</article>
```

Con estos ides podremos acceder a cada uno de los artículos mediante su enlace correspondiente. y no hara scroll hasta llegar a su posicion el la pagina actual.

{% hint style="info" %}
**Nota:**&#x20;

También es posible ir a anclas de otros documentos html, especificando la direccion del fichero y el id del ancla.

`<a href="/paginas/blog#post-3">Post 3</a>`
{% endhint %}

### Bibliografia

* [https://developer.mozilla.org/es/docs/Web/HTML/Element/a#attr-target](https://developer.mozilla.org/es/docs/Web/HTML/Element/a#attr-target)
* [https://blog.nubecolectiva.com/los-tipos-de-rutas-de-archivos-que-existen-en-html-5/](https://blog.nubecolectiva.com/los-tipos-de-rutas-de-archivos-que-existen-en-html-5/)
