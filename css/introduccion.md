# Introduccion

### ¿Qué es CSS?&#x20;

CSS son las siglas en inglés para «hojas de estilo en cascada» (Cascading Style Sheets). Básicamente, es un lenguaje que maneja el diseño y presentación de las páginas web, es decir, cómo lucen cuando un usuario las visita. Funciona junto con el lenguaje HTML que se encarga del contenido básico de las páginas.

Se les denomina hojas de estilo «en cascada» porque puedes tener varias hojas y una de ellas con las propiedades heredadas (o «en cascada») de otras.

Para muchas personas una simple plantilla de blog es suficiente. Aun así, cuando quieras personalizar la apariencia de un sitio necesitarás implementar CSS que, en conjunto con un buen CMS, te ayudará a potenciar el alcance de tu contenido.

### ¿Para qué sirve CSS?

Con CSS puedes crear reglas para decirle a tu sitio web cómo quieres mostrar la información y guardar los comandos para elementos de estilo (como fuentes, colores, tamaños, etc.) separados de los que configuran el contenido.

Además, puedes crear formatos específicos útiles para comunicar tus ideas y producir experiencias más agradables visualmente para los usuarios del sitio web.

### Mejor guia sobre CSS

Esta es la mejor y mas completa guia sobre CSS:

{% embed url="https://lenguajecss.com/css/introduccion/que-es-css/" %}

### Formas de enlazar CSS <a href="#formas-de-enlazar-css" id="formas-de-enlazar-css"></a>

Por supuesto, CSS no sirve de mucho si no está vinculado a un archivo HTML. Existen tres estilos para llevar a cabo esta importante tarea: mediante un CSS externo (external), CSS interno (internal) o CSS en línea (inline). A continuación, veremos las características de estos tres estilos de CSS.

#### CSS externo

En la cabecera de nuestro documento HTML, más concretamente en el bloque `<head></head>`, podemos incluir una etiqueta `<link>` con la que establecemos una relación entre el **documento HTML actual** y el archivo `.css` que indicamos en el atributo `href`.&#x20;

Veamos el código de nuestro `index.html`:

```html
<head>
    <link rel="stylesheet" href="index.css" />
</head>
```

Esta es la manera mas recomendada, ademas de que nos ofrece la posibilidad de utilizar el mismo ficher .css en vario archivos .html.

#### Bloque de estilos

Otra de las formas que existen para incluir estilos CSS en nuestra página es la de añadirlos directamente en el documento HTML, a través de una etiqueta `<style>` que contendrá el código CSS:

```html
<!DOCTYPE html>
<html>
  <head>
    <title>Título de la página</title>
    <style>
      div {
        background: hotpink;
        color: white;
      }
    </style>
  </head>
  ...
</html>
```

#### Estilos en linea

Por último, la tercera forma de aplicar estilos en un documento HTML es el conocido como **estilos en línea**. Se trata de hacerlo directamente, a través del atributo `style` de la propia etiqueta donde queramos aplicar el estilo, colocando ahí las propiedades CSS (_que pueden separarse por `;`_):

```html
<p>¡Hola <span style="color: red; padding: 8px">amigo lector</span>!</p>
```

De la misma forma que en el método anterior, con la etiqueta `<style>`, se recomienda no utilizar este método salvo en casos muy específicos y justificados, ya que los estilos se asocian a la etiqueta HTML en cuestión y no pueden reutilizarse. Es por eso, que se suele considerar una mala práctica por muchos diseñadores cuando la sobreutilizas (_sin una razón de peso_).

Sin embargo, es una excelente forma de inyectar o incluir variables CSS en una etiqueta y sus etiquetas hijas.

### Sintaxis

Las personas que ya están familiarizadas con HTML notarán que la sintaxis de CSS es un poco distinta. En lugar de hacer un listado del contenido de la página, CSS utiliza las reglas asignadas a elementos HTML, un documento HTML completo o varios de ellos. Estas reglas son procesadas por el navegador web cuando carga el archivo HTML.

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

Estos son los componente principales de la sintaxis css:

* **Selector**: Este indica la parte del documento donde se aplica la regla
* **Declaracion:** le dice al navegador qué estilo brindar al elemento seleccionado gracias a sus dos aspectos
  * **Propiedad:** le indica al navegador cuál característica de estilo del elemento debe cambiarse
  * **Valores**: Cada propiedad tiene un paquete de valores, los cuales especifican el estilo de la propiedad

### Ordenar propiedades

Ordenar las propiedades es muy importante para la hora de leer codigo y aunque no exista ninguna norma ni especificacion sobre como hacerlo, la mayoria de experto coinciden en los mismos puntos:

1. Propiedades de posicionamiento
2. Propiedades del box model
3. Propiedades del texto
4. Propiedades visuales (colores, bordes, background...)
5. El resto

```css
body{
    position: relative;
    top: 0;
    
    display: block;
    width: 100px;
    height: 100px;
    
    font-size: 16px;
    text-aling: center;
    
    color: blue;
    border: 2px solid red;
    
    opacity: 1;
}
```

A la hora de que le navegador lea la pagina web, no lo tendra en cuenta, pero para las demas personas que quieran leer to codigo, sera de ayuda que este este ordenado.
