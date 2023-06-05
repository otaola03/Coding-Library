# Listas

Una de las formas más comunes de presentar contenido en una página web son las listas.

**Las listas son elementos que posibilitan una mejor navegación en las páginas web, ya que permiten agrupar cierto contenido** según se requiera. Para los archivos HTML, las **listas se clasifican en ordenadas, desordenadas y descriptivas**. Cada una de estas posee su propia etiqueta y dispone de los atributos que le sean convenientes.

Todos los tipo de listas tiene como elementos `<li></li>`, pero ara diferencia si sson u tipo de lista u otro se engloban con un tag u otro.

> Esto es muy util para posteriormente con CSS aplicarles cambios a todo eel grupo

### Listas desordenadas

Las listas desordenadas son aquellas en las que la información enlistada no necesita una secuencia o jerarquía. Por ejemplo, cuando mencionamos las ciudades de España, pero no estamos haciendo un ranking ni debemos mencionarlas en orden alfabético ni ninguna exigencia secuencial.

Para crear esta lista se utiliza la etiqueta `<li></li>`:

```html
<ul>
  <li>Joaquín</li>
  <li>Carmen</li>
  <li>Teresa</li>
  <li>Fermín</li>
</ul>
```

#### Atributos

Por defecto lass listas desordenadas imprimen antes de cada elemento un punto, pero esto podeos cambiarlo mediante el atributo `type` y su correspondiente paràmetro (`disc, square, circle`).

### Listas ordenadas

En cuanto a las listas ordenadas, las usamos cuando cada punto tiene un lugar fijo y su ubicación obedece a unas razones, como cuando realizamos una lista con el top 5 de restaurantes o los resultados de una votación. En este caso, la etiqueta HTML que corresponde a las listas ordenadas es `<ol> </ol>`.

```html
<ol>
  <li>Enero</li>
  <li>Febrero</li>
  <li>Marzo</li>
  <li>Abril</li>
</ol>
```

#### Atributos

Las listas ordenadas tienen los siguientes atributos

* `type`: Estilo de numeracion (1, A, a, I, i)
* `start`: Inicio de la secuencia (un numero)

### Listas descriptivas

Las listas descriptivas corresponden a las listas en las que **se establecen definiciones**, como, por ejemplo, los glosarios. Si bien este contenido podría ubicarse como lista ordenada o desordenada, las listas descriptivas tienen su propio código y sus etiquetas establecidas son `<dl>, <dt>, <dd>`.

* `<dl> </dl>:` es la etiqueta de apertura y cierre que indica que dentro viene una lista descriptiva.
* `<dt> </dt>`: señala el término a definir.
* `<dd> </dd>`: establece el inicio y fin de la definición.

> Este tipo de listas no hace falta englobarlas con \<ul>, ya que tinen su propia etiqueta para ello \<dl>

```html
<dl>
  <dt>Listas ordenadas</dt>
  <dd>Aquí va la definición</dd>
  <dt>Listas desordenadas</dt>
  <dd>Aquí va la definición</dd>
  <dt>Listas descriptivas</dt>
  <dd>Aquí va la definición</dd>
</dl>
```

<figure><img src="../.gitbook/assets/Screen Shot 2022-11-22 at 11.04.24 AM.png" alt=""><figcaption></figcaption></figure>

### Listas anidadas

En el caso e que queramos meter una lista dentro de otra, taan solo hay que meter un elemento \<ul> nuevo dentro de cualqueira de los elementos de la lista. Esto es muy util para crear los menus para las paginas web.

```html
<ul>
  <li>
    Fruta
    <ul>
      <li>Manzana</li>
      <li>Pera</li>
      <li>Sandia</li>
    </ul>
  </li>
  <li>
    Pescado
    <ul>
      <li>Lubina</li>
      <li>Merluza</li>
      <li>Salmmon</li>
    </ul>
  </li>
</ul>
```

### Bibliografia

* [https://developer.mozilla.org/es/docs/Web/HTML/Element/li](https://developer.mozilla.org/es/docs/Web/HTML/Element/li)
* [https://keepcoding.io/blog/como-crear-listas-en-html/](https://keepcoding.io/blog/como-crear-listas-en-html/)
