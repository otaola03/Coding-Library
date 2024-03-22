# Eventos

El manejo de eventos es esencial en el desarrollo de aplicaciones web interactivas, y Svelte facilita esta tarea mediante su sintaxis intuitiva y eficiente. Esto podremos lograrlo mediante la directiva `on:`.En este artículo, exploraremos las diversas formas de manejar eventos en Svelte.

### Uso básico

En Svelte, el manejo de eventos se realiza directamente en la plantilla. Aquí tienes un ejemplo simple de cómo manejar un evento de clic:

```markup
<script>
  // Estado del componente
  let contador = 0;

  // Función para manejar el clic
  function handleClick() {
    contador += 1;
  }
</script>

<!-- Plantilla con manejo de evento de clic -->
<button on:click={handleClick}>Incrementar Contador</button>

<!-- Mostrar el resultado -->
<p>Contador: {contador}</p>
```

En este ejemplo, la función `handleClick` se ejecutará cada vez que se haga clic en el botón, incrementando el contador y actualizando automáticamente la interfaz de usuario. Al igual que estabus manejando el evento `click`, podemos manejar cualquier otro evento utilizado en JavaScript.

En el caso de que no quieras relazionar el evento con una funcion, tambien es posible hacerlo in-line con funciones de flecha:

```markup
<script>
  let contador = 0;
</script>

<!-- Plantilla con manejo de evento de clic utilizando arrow function -->
<button on:click={() => contador += 1}>Incrementar Contador</button>

<!-- Mostrar el resultado -->
<p>Contador: {contador}</p>
```

### Event modifiers

En Svelte, los "event modifiers" o modificadores de eventos son funciones que puedes utilizar para personalizar el comportamiento de los eventos enriqueciendo la experiencia de manejo de eventos en tus componentes. Estos modificadores se aplican directamente en las plantillas y proporcionan una forma concisa de realizar acciones específicas en respuesta a eventos.

Aquí hay algunos ejemplos de modificadores de eventos en Svelte:

#### `prevent`

El modificador `.prevent` se utiliza para prevenir el comportamiento predeterminado del evento. Por ejemplo, para prevenir el envío de un formulario al hacer clic en un botón, puedes usar:

```markup
<script>
  function handleSubmit() {
    // Lógica de manejo del envío del formulario
  }
</script>

<form on:submit|prevent={handleSubmit}>
  <!-- Otros elementos del formulario -->
  <button type="submit">Enviar</button>
</form>
```

#### `stop`

El modificador `.stop` detiene la propagación del evento, evitando que se propague a los elementos secundarios. Puedes usarlo para evitar que eventos de padres afecten a elementos hijos.

```markup
<div on:click|stop={handleParentClick}>
  <button on:click={handleChildClick}>Haz clic en mí</button>
</div>
```

#### `self`

El modificador `.self` asegura que el evento solo se maneje si se originó en el elemento al que se le aplicó el modificador. Evita que eventos de elementos secundarios se propaguen al elemento padre.

```markup
<div on:click|self={handleClick}>
  <!-- Solo se manejará si se hace clic directamente en este div -->
</div>
```

#### `once`

El modificador `.once` garantiza que el manejador de eventos se ejecute solo una vez. Es útil cuando solo necesitas que una acción ocurra la primera vez que se produce un evento.

```markup
<button on:click|once={handleClick}>Haz clic una vez</button>
```

#### `capture`

El modificador `.capture` se utiliza para establecer el evento en modo de captura en lugar de burbujeo. Esto significa que el evento se manejará en la fase de captura antes de llegar al objetivo real.

```markup
<div on:click|capture={handleCaptureClick}>
  <!-- Se manejará en la fase de captura antes de elementos secundarios -->
</div>
```

### `createEventDispacther`

`createEventDispatcher` es una función proporcionada por Svelte para facilitar la comunicación entre componentes. Esta función permite a un componente enviar eventos personalizados y a otros componentes escuchar y reaccionar a esos eventos. Es una forma eficaz de lograr la comunicación entre componentes sin acoplarlos directamente.

A continuación, explicaré cómo usar `createEventDispatcher` y cómo se integra en la estructura de un componente Svelte.

#### Uso de básico

En tu componente Svelte, puedes utilizar `createEventDispatcher` de la siguiente manera:

```markup
<!-- Boton.svelte -->
<script>
  import { createEventDispatcher } from 'svelte';

  // Crear un dispatcher de eventos
  const dispatch = createEventDispatcher();

  // Función que envía un evento personalizado
  function pulsar() {
    dispatch('pulsado')
  }
</script>

<!-- Botón que dispara la función enviarMensaje -->
<button on:click={pulsar}>Enviar Mensaje</button>
```

Como puedes observar , en este ejemplo se importa `createEventDispatcher` y se crea un objeto `dispatch`, que envia un evento `pulsado` cuando el boton es pulsado. Esto se hace desde elemento hijo y para poder capturarlo desdde elpadre hay que hacer lo siguiente:

<pre class="language-markup"><code class="lang-markup"><strong>&#x3C;!-- +page.svelte -->
</strong>&#x3C;script>
  import Boton from './Boton.svelte';
  
  let veces = 0;  
  // Propiedad que maneja el evento personalizado del otro componente
  function sePulso() {
    veces++;
  }
&#x3C;/script>

&#x3C;p>Me han pulsado {veces} veces&#x3C;/p>
&#x3C;!-- Escuchar el evento personalizado del otro componente -->
&#x3C;Boton on:pulsado={sePulso} />
</code></pre>

#### Como propagar eventos

La propagación de eventos a través de más de dos componentes sigue la misma lógica, pero ahora necesitamos considerar la estructura de nuestra aplicación. Ahora añadiremos un 3 elevento llamado `BotonBox` q englobara el componente `Box` y que propagara el evento hacia `+page.svelte`:

```markup
<!-- BotonBox.svelte -->
<script>
  import Boton from './Boton.svelte';
</script>

<!-- Escuchar el evento personalizado del otro componente -->
<Boton on:pulsado />
```

Como puedes observar, en esta caso el componente `Boton` tiene la directiva `on:pulsado`, pero si indicar la funcion que realizara. Esto se deve a que si no le especificamos nada, svelte propagara el evento al evento padre para asi no tener que repetir codigo.

Por supuesto, luego tendremos que capturar el evento en el componente padre:

```markup
<!-- +page.svelte -->
<script>
  import BotonBox from './BotonBox.svelte';
  
  let veces = 0;  
  // Propiedad que maneja el evento personalizado del otro componente
  function sePulso() {
    veces++;
  }
</script>

<p>Me han pulsado {veces} veces</p>
<!-- Escuchar el evento personalizado del otro componente -->
<BotonBox on:pulsado={sePulso} />
```

#### Agregar metadatos&#x20;

En Svelte, puedes agregar metadatos a un evento personalizado enviando un objeto con la propiedad `detail` al método `dispatch` de `createEventDispatcher`. Este objeto `detail` puede contener cualquier información adicional que desees enviar junto con el evento.

Aquí hay un ejemplo de cómo agregar metadatos a un evento personalizado:

```markup
<!-- Boton.svelte -->
<script>
  import { createEventDispatcher } from 'svelte';

  // Crear un dispatcher de eventos
  const dispatch = createEventDispatcher();

  // Función que envía un evento personalizado
  function pulsar() {
    let timestamp = new Date();
    let ahora = timestamp.toLocaleString();
    dispatch('pulsado', {
      fecha: ahora,
    })
  }
</script>

<!-- Botón que dispara la función enviarMensaje -->
<button on:click={pulsar}>Enviar Mensaje</button>
```

En este ejemplo, la función `pulsar` envía un evento personalizado llamado 'boton pulsado' junto con un objeto `fecha` que contiene la fechaa actual. Estas propiedades representan los metadatos que se adjuntarán al evento.

Luego, en otro componente que escucha este evento, puedes acceder a esos metadatos en la función manejadora accediendo a la propiedad `details` de el argumento `event` que recibe la funcion manejadora:

```markup
<!-- +page.svelte -->
<script>
  import Boton from './Boton.svelte';
  
  let fechas = []
  // Propiedad que maneja el evento personalizado del otro componente
  function sePulso(event) {
    const fecha = event.detail.fecha;
    fechas = fechas[..., fecha];
  }
</script>

{#each fechas as fecha}
  <p>{fecha}</p>
{/each}
<!-- Escuchar el evento personalizado del otro componente -->
<OtroComponente on:pulsado={sePulso} />
```
