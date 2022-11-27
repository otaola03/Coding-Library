# Elementos de bloque

Cuando cargas una página web en tu navegador, todos los elementos HTML se organizan de forma predeterminada. Así, los elementos `<p>` o párrafos se agrupan en bloques que **van de lado a lado en la página web**, mientras que, los elementos `<a>`, usados en los _links_, se organizan en **una sola línea**.

Casi todos los elementos HTML siguen alguno de estos patrones:  pertenecen a los **elementos de bloque** o a los **elementos en línea**.&#x20;

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

### **Elementos de bloque**&#x20;

Un **elemento de bloque HTML** es aquel que ocupa **todo el ancho de la página** o del elemento que lo contiene. Ya has visto algunos de ellos, como por ejemplo:

* `<p>`&#x20;
* `<h1>`hasta `<h6>`&#x20;
* `<ul>`

Aunque sólo pongas una palabra dentro del elemento `<p>`, ésta ocupará todo el ancho que tiene disponible. En el siguiente ejemplo, puedes ver que el elemento `<p>` ha sido coloreado; aunque sólo una parte tiene realmente texto, el tono azul **va de un extremo de la imagen al otro**.

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

Como los elementos de bloque ocupan todo el ancho de la página, suelen agruparse uno sobre otro:

![Elementos en bloque HTML](https://media.gcflearnfree.org/content/6138c7ba90347d098804a48f\_09\_08\_2021/Co%CC%81mo-son-los-elementos-en-bloque-HTML.png)

Los elementos sobre los que se habalara en lo siguinetes tres articulos () son elementos de bloque

### \<adress>

El **elemento HTML `<address>`** aporta información de contacto para su `<article>` más cercano o ancestro `<body>`; en el último caso lo aplica a todo el documento.

```html
 <address>
    You can contact author at <a href="http://www.somedomain.com/contact">www.somedomain.com</a>.<br>
    If you see any bugs, please <a href="mailto:webmaster@somedomain.com">contact webmaster</a>.<br>
    You may also want to visit us:<br>
    Mozilla Foundation<br>
    1981 Landings Drive<br>
    Building K<br>
    Mountain View, CA 94043-0801<br>
    USA
  </address>
```

### \<blockquote>

**blockquote** -_cita en bloque_ . Crea citas en bloque, marca las citas a otros autores o documentos. Es una etiqueta de bloque, pero tiene su equivalente en elemento en linea.

```html
<blockquote cite='http://html.conclase.net/w3c/html401...def-BLOCKQUOTE'>
  <p>
    <strong>Nota.</strong> Recomendamos que las implementaciones de hojas
    de estilo porporcionen un mecanismo para insertar signos de puntuación de citas
    antes y después de una cita delimitada por un BLOCKQUOTE de un modo apropiado según
    el contexto del idioma actual y el grado de anidamiento de las citas.
  </p>
</blockquote>
```

Aunque se ponga la direccio de donde hemos sacado la informacion, esta informacion no sera mostrada en pantalla, tan solo es visible para el navegador.

### \<pre>

El **Elemento** **HTML \<pre>** (o _Texto HTML Preformateado_) representa texto preformateado. El texto en este elemento típicamente se muestra en una fuente fija, no proporcional, exactamente como es mostrado en el archivo. Los espacios dentro de este elemento también son mostrados como están escritos.

Es decir mostrara el texto coo tu lo hayas escrito en tun editor de texto:

```html
<pre>
                Hola
      ¿que tal?
</pre>
```

### \<div>

En HTML, la etiqueta \<div> es un contenedor genérico de bloque para otros elementos que se utiliza para dividir contenido. Es «genérico» porque no describe el contenido que contiene. Normalmente se utiliza para organizar la pagina web y asi a la hora de aplicarle estilos o scripts que este proceso se mas facil.

```html
<div style="color: blue;">
 <h2> Ejemplo de div y span </h2>
  <p>
    Esto es un párrafo dentro de un div,
  </p>
</div>
```

### \<hr>

El **elemento HTML \<hr>** representa un cambio de tema entre párrafos (por ejemplo, un cambio de escena en una historia, un cambio de tema en una sección). En versiones previas de HTML representaba una línea horizontal. Aún puede ser representada como una línea horizontal en los navegadores visuales, pero ahora es definida en términos semánticos y no tanto en términos representativos, por tanto para dibujar una línea horizontal se debería usar el CSS apropiado.

### Bibliografia

* [https://developer.mozilla.org/es/docs/Web/HTML/Block-level\_elements](https://developer.mozilla.org/es/docs/Web/HTML/Block-level\_elements)
* [https://edu.gcfglobal.org/es/curso-basico-de-html/elementos-de-bloque-en-linea-y-de-organizacion-html/1/](https://edu.gcfglobal.org/es/curso-basico-de-html/elementos-de-bloque-en-linea-y-de-organizacion-html/1/)
