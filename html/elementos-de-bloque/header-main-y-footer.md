---
description: Estructurando el <body>
---

# Header, Main y Footer

Para organizar las paginas web de una manera mas sencilla se utilizan las siguiente secciones:

### Header

El _elemento de HTML Header_ `<header>` representa un grupo de ayudas introductorias o de navegación. Puede contener algunos elementos de encabezado, así como también un logo, un formulario de búsqueda, un nombre de autor y otros componentes. Este apartado normelmente se utiliza para colocar los menus de nevegacion

### Main

El **elemento HTML `<main>`** representa el contenido principal del [`<body>`](https://developer.mozilla.org/es/docs/Web/HTML/Element/body) de un documento o aplicación. El área principal del contenido consiste en el contenido que está directamente relacionado, o se expande sobre el tema central de un documento o la funcionalidad central de una aplicación.&#x20;

El contenido del main debe ser único al documento, excluyendo cualquier contenido que se repita a través de un conjunto de documentos como barras laterales, enlaces de navegación, información de derechos de autor, logos del sitio y formularios de búsqueda (a menos, claro, que la función principal del documento sea un formulario de búsqueda).

{% hint style="info" %}
**Nota:** **no debe haber** más de un elemento `<main>` en un documento, y este **no debe ser** descendiente de un elemento `<article>`, `<aside>`, `<footer>`, `<header>`, o `<nav>`.
{% endhint %}

### Footer

El _Elemento_ _HTML Footer_ `<footer>` representa un pie de página para el contenido de sección más cercano o el elemento raíz de sección. Un pie de página típicamente contiene información acerca de el autor de la sección, datos de derechos de autor o enlaces a documentos relacionados.

### Ejemplo

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Mi pagina de prueba</title>
  </head>
  <body>
    <header> Inicio Novelas Peliculas Contactos </header>
    <main>
      <h1> Harry Potter </h1>
      <h2> Sinopsis </h2>
        <p> El elemento de HTML Header header 
        representa un grupo de ayudas introductorias o de navegación. </p>
      <h2> Personajes </h2>
        <p> Perosonaje1 Personaje2 Personaje3 </p>
    </main>
    <footer>
      Piscine Discovery 2022-2023
    </footer>
  </body>
</html>
```
