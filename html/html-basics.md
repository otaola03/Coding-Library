---
description: Empezando desde cero
---

# HTML Basics

El Lenguaje de Marcado de Hipertexto (HTML) es el código que se utiliza para estructurar y desplegar una página web y sus contenidos. Por ejemplo, sus contenidos podrían ser párrafos, una lista con viñetas, o imágenes y tablas de datos. Como lo sugiere el título, este artículo te dará una comprensión básica de HTML y cúal es su función.

### Entonces, ¿qué es HTML en realidad? <a href="#entonces_-que_es_html_en_realidad" id="entonces_-que_es_html_en_realidad"></a>

HTML no es un lenguaje de programación; es un _lenguaje de marcado_ que define la estructura de tu contenido. HTML consiste en una serie de **elementos que usarás para encerrar diferentes partes del contenido** **para que se vean o comporten de una determinada manera**. Las etiquetas de encierre pueden hacer de una palabra o una imagen un hipervínculo a otro sitio, se pueden cambiar palabras a cursiva, agrandar o achicar la letra, etc. Por ejemplo, toma la siguiente línea de contenido:

```
Mi gato es muy gruñon
```

Si quieres especificar que se trata de un párrafo, podrías encerrar el texto con la etiqueta de párrafo ([`<p>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/p)):

```html
<p>Mi gato es muy gruñon</p>
```

### Anatomia de un elemento HTML

Las partes principales del elemento son:

* **La etiqueta de apertura**: consiste en el nombre del elemento (en este caso, p), encerrado por **paréntesis angulares** (< >) de apertura y cierre. Establece dónde comienza el contendio del el elemento
* **La etiqueta de cierre**: es igual que la etiqueta de apertura, excepto que incluye una barra de cierre (/) antes del nombre de la etiqueta. Establece dónde termina el elemento&#x20;
* **El contenido**: este es el contenido del elemento, que en este caso es sólo texto.
* **El elemento**: la etiqueta de apertura, más la etiqueta de cierre, más el contenido equivale al elemento.

### Elementos vacíos <a href="#elementos_vacios" id="elementos_vacios"></a>

Algunos elementos no poseen contenido, y son llamados **elementos vacíos**. Toma, por ejemplo, el elemento `<img>` de nuestro HTML:

```
<img src="images/firefox-icon.png" alt="Mi imagen de prueba">
```

Posee dos atributos (no hace falta que sepas lo que es todavia), pero no hay etiqueta de cierre `</img>` ni contenido encerrado. Esto es porque un elemento de imagen no encierra contenido al cual afectar. Su propósito es desplegar una imagen en la página HTML, en el lugar en que aparece.

### Estrucutra de un apagina web

Hasta ahora emos explicado un poco, los basico sobre los elemntos indicidaules, pero para que estos sea utilies hay que utilizarlso en conjunto, para asi formar una pagina web.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Mi pagina de prueba</title>
  </head>
  <body>
    <img src="images/firefox-icon.png" alt="Mi imagen de prueba">
  </body>
</html>
```

Tienes:

* `<!DOCTYPE html>` --> Establece el tipo de estandar del documento, en este caso (HTML5). En los princpios de HTML , era de utilidad, sin embargo hoy en dia no sirve para nada, aunque es necesaria su utilizacion.
* `<html></html>` --> Este elemento encierra todo el contenido de la página entera.
* `<head></head>` --> Coleccion de datos o metadatos del documento. Estos son  datos que le vamos a pasar al nevegador para que interprete nuestra pagian web. Esto no tiene un representacion visual, pero el navegador lo entiende.
* `<meta charset="utf-8">` --> Establece el juego de caracteres que tu documento usará en `utf-8`. Básicamente, puede manejar cualquier contenido de texto que puedas incluir. Es recomendable establecerlo para ahorrarte problemas.
* `<title></title>` --> Establece el título de tu página, que es el título que aparece en la pestaña
* `<body></body>` --> Encierra _todo_ el contenido que deseas mostrar a los usuarios web que visiten tu página.

#### Etiqueta meta

Los metadatos son datos que describen datos, y HTML tiene una forma «oficial» de introducir metadatos en un documento — el elemento `<meta>`. Hay muchos diferentes tipos de elementos `<meta>` que se pueden incluir en el \<head> de tu página y aqui te dejo unos cuantos:

```html
<meta name="viewport" content="width=device-width, initial-scale=1" />
```

Esta etiqueta en concreto se utliza para que nuestra pagina web responsive se visualice correctamente en dispositivos moviles.&#x20;

Otras bastante utilizadas son las que se utilizan para especificar el nombre del autor y. descripcion de la pagina:

```html
<meta name="description" content="Lorem ipsum ...">
<meta name="author" content="Pedro">
```

### Bibliografia

* d[eveloper.mozilla.org/es/docs/Learn/HTML/Introduction\_to\_HTML/The\_head\_metadata\_in\_HTML](https://developer.mozilla.org/es/docs/Learn/HTML/Introduction\_to\_HTML/The\_head\_metadata\_in\_HTML)
