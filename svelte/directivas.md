# Directivas

Las directivas en Svelte son atributos especiales que llevan a cabo tareas específicas en el DOM o interactúan con componentes. Este post proporcionará una visión general completa de las directivas en Svelte y cómo puedes utilizarlas para mejorar y personalizar la funcionalidad de tus componentes.

### `if:`: Condicionales

La directiva `if:` permite mostrar o ocultar elementos en función de una condición.

```markup
<script>
  let mostrarMensaje = true;
</script>

{#if mostrarMensaje}
  <p>Este mensaje se muestra si mostrarMensaje es verdadero.</p>
{/if}
```

Tambien es posible escribir condicionales dentro de los scopes sin necesidad de realizar una directiva if:

```html
<button disabled={nombre.length === 0} > Boton </button>
```

En el caso de que quieras establecer una alternaativa `else` tienes que hacerlo de la siguiente manera:

```markup
<script>
  let mostrarMensaje = true;
</script>

{#if mostrarMensaje}
  <p>Este mensaje se muestra si mostrarMensaje es verdadero.</p>
{:else}
  <p>Este mensaje se muestra si no es verdadera</p>
{/if}
```

En el caso de que quieras establecer varias condiciones podras utilizar la directiva `:else if` para lograrlo:

```markup
{#if count > 10}
	<p>{count} count es mayor que 10</p>
{:else if count < 5}
	<p>{count} es menor que 5</p>
{:else}
	<p>{count} esta entre 5 y 10</p>
{/if}
```

### `each:`: Iteración

La directiva `each:` se utiliza para iterar sobre una lista y renderizar elementos para cada elemento de la lista.

```markup
<script>
  let colores = ['rojo', 'verde', 'azul'];
</script>

<ul>
  {#each colores as color}
    <li>{color}</li>
  {/each}
</ul>
```

En el caso de que queiras caputar el numero de la iteracion de bucle puedes utilizar una segunda variable:

```markup
<script>
  let colores = ['rojo', 'verde', 'azul'];
</script>

<ul>
  {#each colores as color, num}
    <li>El color {num} es: {color}</li>
  {/each}
</ul>
```

#### Keyed each block

En Svelte, un "Keyed each block" se refiere a la práctica de asociar una clave única a cada elemento en un bucle `each`. Esta clave permite a Svelte realizar actualizaciones más eficientes en el DOM cuando la lista de elementos cambia dinámicamente. **Proporciona una manera de identificar de manera única cada elemento** y garantiza una manipulación del DOM más precisa y eficiente durante las operaciones de añadir, eliminar o reordenar elementos.

Supongamos que tenemos una lista de tareas que pueden cambiar dinámicamente. Utilizaremos una clave única para cada tarea en el bucle `each`.

```markup
<script>
  let tareas = [
    { id: 1, texto: 'Hacer compras' },
    { id: 2, texto: 'Realizar ejercicio' },
    { id: 3, texto: 'Estudiar para el examen' }
  ];

  function eliminarTarea(id) {
    tareas = tareas.filter(tarea => tarea.id !== id);
  }

  function agregarTarea() {
    const nuevaTarea = { id: Date.now(), texto: 'Nueva tarea' };
    tareas = [...tareas, nuevaTarea];
  }
</script>

<ul>
  {#each tareas as tarea (tarea.id)}
    <li key={tarea.id}>
      {tarea.texto}
      <button on:click={() => eliminarTarea(tarea.id)}>Eliminar</button>
    </li>
  {/each}
</ul>

<button on:click={agregarTarea}>Agregar Tarea</button>
```

En este ejemplo, cada tarea tiene una propiedad `id` única. La clave (`key={tarea.id}`) está asociada al `id` de cada tarea en el bucle `each`. Esto permite a Svelte identificar de manera única cada elemento y optimizar las actualizaciones del DOM durante las operaciones de agregar o eliminar tareas.

{% hint style="info" %}
Este concepto suele costar entenderlo, pero en este [ejemplo practico](https://learn.svelte.dev/tutorial/keyed-each-blocks) esta bastante bien explicado.
{% endhint %}

En resumen, el uso de un "Keyed each block" es importante cuando trabajas con listas dinámicas para garantizar un rendimiento eficiente y preciso durante las actualizaciones del DOM.

#### `else`

En Svelte, la directiva `else` en combinación con un bucle `each` se utiliza para renderizar contenido cuando la lista proporcionada al bucle está vacía. Esto permite mostrar un mensaje o un elemento alternativo cuando no hay elementos para iterar. A continuación, te mostraré un ejemplo para ilustrar el uso de `else` con un bucle `each`.

```markup
<script>
  let tareas = [];

  function agregarTarea() {
    const nuevaTarea = { id: Date.now(), texto: 'Nueva tarea' };
    tareas = [...tareas, nuevaTarea];
  }
</script>

<ul>
  {#each tareas as tarea (tarea.id)}
    <li key={tarea.id}>
      {tarea.texto}
    </li>
  {:else}
    <li>No hay tareas pendientes</li>
  {/each}
</ul>

<button on:click={agregarTarea}>Agregar Tarea</button>
```

### `await:`

En el vasto paisaje del desarrollo web, la asincronía es un componente esencial. En el mundo de Svelte, la directiva `await` se erige como una herramienta poderosa para manejar operaciones asíncronas de manera elegante. En este post, sumérgete en el universo de la directiva `await` en Svelte y descubre cómo simplifica la gestión de promesas y mejora la experiencia de desarrollo.

#### **Introducción a la Directiva `await`**

La directiva `await` en Svelte se utiliza en combinación con operaciones asíncronas para manejar el flujo de ejecución de un componente mientras espera que una promesa se resuelva o se rechace. Proporciona una manera declarativa y concisa de gestionar la asincronía, facilitando la creación de componentes más robustos.

#### **Uso Básico de `await`**

Veamos un ejemplo sencillo de cómo utilizar `await` para manejar una operación asíncrona, como una solicitud a una API:

```markup
<script>
  let datos;

  async function obtenerDatos() {
    const respuesta = await fetch('https://api.ejemplo.com/datos');
    datos = await respuesta.json();
  }

  await obtenerDatos(); // Esperamos a que la operación asíncrona se complete antes de continuar

  // Resto del componente que usa los datos
</script>

{#if datos}
  <ul>
    {#each datos as dato}
      <li>{dato}</li>
    {/each}
  </ul>
{:else}
  <p>Cargando datos...</p>
{/if}
```

En este ejemplo, `await obtenerDatos()` pausa la ejecución del componente hasta que la operación asíncrona se resuelva. La interfaz del usuario se actualiza automáticamente una vez que los datos están disponibles.

#### **Manejo de Errores con `await` y `{#await}`**

La directiva `await` también facilita el manejo de errores en operaciones asíncronas. Puedes utilizar la estructura `{#await}` junto con `{:catch}` para manejar cualquier error que pueda ocurrir durante la ejecución de la promesa:

```markup
<script>
  let datos;

  async function obtenerDatos() {
    try {
      const respuesta = await fetch('https://api.ejemplo.com/datos');
      datos = await respuesta.json();
    } catch (error) {
      console.error('Error al obtener datos:', error.message);
      throw error; // Propaga el error para que pueda ser manejado externamente si es necesario
    }
  }

  {#await obtenerDatos()}
    <p>Cargando datos...</p>
  {:then}
    <!-- Resto del componente que usa los datos -->
  {:catch error}
    <p>Error al cargar datos: {error.message}</p>
  {/await}
</script>
```

Aquí, si hay un error durante la obtención de datos, se activa el bloque `{:catch}` dentro de `{#await}` para manejar el error de manera adecuada.

#### **Mejora de la Experiencia del Usuario con `await` y `{#await}`**

La combinación de `await` y `{#await}` también permite proporcionar una experiencia de usuario informada durante la espera de una operación asíncrona. Mientras se espera la resolución de la promesa, puedes mostrar mensajes de carga para mantener a los usuarios informados:

```markup
<script>
  let datos;

  async function obtenerDatos() {
    const respuesta = await fetch('https://api.ejemplo.com/datos');
    datos = await respuesta.json();
  }

  {#await obtenerDatos()}
    <p>Cargando datos...</p>
  {:then}
    <!-- Resto del componente que usa los datos -->
  {:catch error}
    <p>Error al cargar datos: {error.message}</p>
  {/await}
</script>
```

En este caso, el bloque `{#await}` se activa mientras se espera la resolución de la promesa, mostrando un mensaje de "Cargando datos...". Una vez que la promesa se resuelve, el contenido dentro de `{#await}` se reemplaza por el resto del componente.

### `bind:`

Svelte, un marco de trabajo para construir aplicaciones web eficientes, presenta la directiva `bind` como una herramienta poderosa para gestionar el estado y las interacciones del usuario de manera elegante. A continuación, exploraremos diferentes aspectos de la directiva `bind` y cómo puede simplificar el desarrollo en Svelte.

#### Vinculación de Variables Entre `<script>` y HTML

En Svelte, la directiva `bind` facilita la vinculación bidireccional de variables entre el bloque `<script>` y el HTML del componente. Esto es particularmente útil para mantener una sincronización automática entre el estado de tu componente y la interfaz de usuario.

```markup
<script>
  // Declaración de una variable en el bloque <script>
  let nombre = "Usuario";
</script>

<!-- Vinculación bidireccional de la variable 'nombre' con un input -->
<input bind:value={nombre} />

<!-- Mostrar el valor actual de la variable -->
<p>Hola, {nombre}.</p>
```

En este ejemplo, cualquier cambio en el input actualizará automáticamente la variable `nombre`, y cualquier cambio en `nombre` se reflejará en el input y en el párrafo.

#### Uso con Eventos

La directiva `bind` también se puede utilizar con eventos, lo que te permite ejecutar funciones en respuesta a eventos específicos. Por ejemplo, puedes utilizar `bind:input` para ejecutar una función cuando el input cambie.

```markup
<script>
  let edad = 25;

  function handleEdadChange(event) {
    // Realizar acciones con el nuevo valor
    console.log("Nueva edad:", event.target.value);
  }
</script>

<!-- Vinculación de la variable 'edad' con un input y ejecución de la función 'handleEdadChange' -->
<input bind:value={edad} bind:input={handleEdadChange} />

<!-- Mostrar el valor actual de la variable -->
<p>Edad: {edad}</p>
```

En este caso, la función `handleEdadChange` se ejecutará cada vez que el valor del input cambie, permitiéndote realizar acciones personalizadas con el nuevo valor.

#### inculación con Elementos HTML

Puedes utilizar `bind` para vincular variables directamente con propiedades de elementos HTML, como clases o estilos.

```markup
<script>
  let isActive = false;
</script>

<!-- Vinculación de la variable 'isActive' con la clase 'active' de un elemento -->
<div class:active={isActive}>Elemento Activo</div>
```

En este ejemplo, la clase `active` se aplicará al `<div>` cuando `isActive` sea `true`.

Otro ejemplo tipico seria utilizando `bind:checked` que que nos permite realizar una accion cuando un casilla esta checked o no:

```markup
<script>
  let acepta = false;
</script>

{#if acepta}
<p>Ha dicho que si</p>
{:else}
<p>Ha dicho que no</p>

<input type="checkbox" bind:checked={acepta} />
```

#### Comunicación bidireccional

La directiva `bind` en Svelte permite la vinculación bidireccional de datos, conectando una variable en el componente padre con una propiedad en un componente hijo. Esto facilita la actualización automática de la interfaz de usuario en respuesta a cambios en el estado.

```markup
<!-- En el componente padre -->
<script>
  let count = 0;
</script>

<!-- Vinculación bidireccional con la directiva bind -->
<ComponenteHijo bind:valor={count} />
```

```markup
<!-- En el componente hijo -->
<script>
  export let valor;
</script>

<!-- Utilizando el valor vinculado en el componente hijo -->
<p>El valor vinculado es: {valor}</p>
```

Ahora, puedes usar la variable vinculada `valor` en la interfaz de usuario del componente hijo. Cualquier cambio en `count` en el componente padre actualizará automáticamente el valor en el componente hijo y se mostrará en la interfaz de usuario.

#### `bind:this`

La sintaxis `bind:this` en Svelte se utiliza para vincular una referencia a un elemento HTML dentro de un componente Svelte. Esta vinculación permite acceder y manipular directamente el elemento en el código del componente, facilitando la interacción dinámica con el DOM.

Aquí tienes un ejemplo básico para ilustrar cómo usar `bind:this`:

```markup
<script>
  let miElemento;

  function hacerAlgoConElElemento() {
    // Acceder y manipular el elemento directamente
    if (miElemento) {
      miElemento.style.backgroundColor = 'lightblue';
    }
  }
</script>

<!-- Vinculación de la referencia 'miElemento' con bind:this -->
<div bind:this={miElemento}>
  <p>¡Hola, Svelte!</p>
</div>

<!-- Botón para realizar acciones con el elemento vinculado -->
<button on:click={hacerAlgoConElElemento}>Modificar Elemento</button>
```

Es  recomendable checkear si la variable `miElemento` no es `null`, ya en el caso de que fuera `null` se romperia.
