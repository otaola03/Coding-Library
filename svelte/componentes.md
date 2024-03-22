# Componentes

Los componentes son unidades autónomas y reutilizables de código en el desarrollo de software. En el contexto del desarrollo web, los componentes son bloques de construcción de interfaces de usuario (UI) que encapsulan lógica, estilo y comportamiento específicos. Estos componentes permiten dividir una aplicación en partes más pequeñas y manejables, lo que facilita el desarrollo, la modificación y el mantenimiento del código.

### Estructura basica

En Svelte, un componente consta de tres partes principales: el script, la sección de estilo y la plantilla. Cada una de estas partes cumple una función específica y contribuye a la construcción del componente.

#### **Script (JavaScript/TypeScript):**

La sección de script es donde se define la lógica del componente utilizando JavaScript o TypeScript. Aquí se declaran variables, funciones y lógica de control de flujo. También es el lugar donde se gestionan los estados del componente y se realizan las operaciones necesarias.

```markup
<!-- Ejemplo de sección de script en Svelte -->
<script>
  let contador = 0;

  function incrementar() {
    contador += 1;
  }
</script>
```

#### **Estilo (CSS/SCSS):**

La sección de estilo permite aplicar estilos al componente. Puedes utilizar CSS, SCSS u otros preprocesadores de CSS para definir el aspecto visual del componente. Los estilos definidos aquí están encapsulados dentro del componente, evitando conflictos con estilos de otros componentes.

```markup
<!-- Ejemplo de sección de estilo en Svelte -->
<style>
  button {
    background-color: #3498db;
    color: #fff;
    padding: 10px 15px;
    border: none;
    cursor: pointer;
  }
</style>
```

#### **Plantilla (HTML):**

La sección de plantilla contiene el marcado HTML que define la estructura y presentación del componente. Svelte utiliza una sintaxis especial para las expresiones y directivas en el HTML, lo que facilita la manipulación del DOM y la actualización reactiva.

```markup
<!-- Ejemplo de sección de plantilla en Svelte -->
<button>
  Botom
</button>
```

Estas tres partes trabajan juntas para formar un componente completo en Svelte. El script maneja la lógica y el estado, la sección de estilo se encarga del aspecto visual, y la plantilla define la estructura y presentación de la interfaz de usuario. La integración de estas partes en un solo archivo facilita el desarrollo y mantenimiento de componentes reutilizables y claros.

### Binding

El binding en Svelte se refiere a la capacidad de establecer una conexión bidireccional entre una variable y un elemento en el DOM (Documento de Objetos del Modelo). Esto significa que los cambios en la variable se reflejan automáticamente en el DOM y viceversa. Svelte simplifica enormemente la gestión del estado y la manipulación de la interfaz de usuario mediante un sistema de binding intuitivo y potente.

#### Unidireccional

En el binding unidireccional, también conocido como "one-way binding", la información fluye en una dirección, desde el componente de Svelte hacia el DOM. Esto significa que cuando actualizas la variable en el componente, esos cambios se reflejarán en el DOM, pero no viceversa. Es decir, si el valor en el DOM cambia por alguna razón, no afectará directamente la variable en el componente.

```markup
<script>
  let message = "Hola, Mundo!";
</script>

<input bind:value={message}>
<p>{message}</p>
```

#### Bidireccional

En cambio, el binding bidireccional, también conocido como "two-way binding", permite que la información fluya en ambas direcciones, desde el componente hacia el DOM y viceversa. Si cambias la variable en el componente, se actualiza en el DOM, y si alguien modifica el valor directamente en el DOM, Svelte actualizará automáticamente la variable en el componente. Esto se puedo lograr mediante eventos.

```markup
<script>
  let count = 0;

  function increment() {
    count += 1;
  }
</script>

<button on:click={increment}>
  Haz clic para incrementar: {count}
</button><script>
  let count = 0;

  function increment() {
    count += 1;
  }
</script>

<button on:click={increment}>
  Haz clic para incrementar: {count}
</button>
```

### Anidacion de componentes

La anidación de componentes en Svelte se refiere a la práctica de colocar un componente dentro de otro. Esto permite construir estructuras jerárquicas donde los componentes más grandes contienen y gestionan componentes más pequeños. Este enfoque fomenta la modularidad y la reutilización del código.

Esto se logra de la siguiente manera:

```markup
<!-- Hijo.svelte -->
<p>Hola Mundo!</p>
```

```markup
<!-- Padre.svelte -->
<script>
  import Hijo from './Hijo.svelte';
</script>

<main>
  <Hijo />
</main>
```

En este ejemplo, el componente `Hijo` está anidado dentro del componente Padre. Este patrón de anidación permite la construcción de estructuras más complejas a medida que añadimos más componentes.

#### Comunicación entre Componentes Anidados (props)

```markup
<!-- Hijo.svelte -->
<script>
  export let mensajePadre;
</script>

<p>{mensajePadre}</p>
```

```markup
<!-- Padre.svelte -->
<script>
  import Hijo from './Hijo.svelte';

  let saludo = "¡Hola desde el componente padre!";
</script>

<main>
  <Hijo mensajePadre={saludo} />
</main>
```

Aquí, el componente Padre pasa una prop `mensajePadre` al componente Hijo, lo que facilita la comunicación de datos de un componente a otro. En ete ejemplo en el caso de que no establecieramos el contenido de `mensajePaadre`, este nos imprimiria `undefined`. Por lo que si queremos podermos establecer un valor por defecto:

```markup
<!-- Hijo.svelte -->
<script>
  export let mensajePadre = 'Hola Mundo';
</script>

<p>{mensajePadre}</p>
```

{% hint style="info" %}
En el caso de que el atributo del componte hijo se llame igual que una variabel del padre, se puede hacer de la siguiente manera:

`<Hijo {mensaje} />`
{% endhint %}

#### spread props

La propagación de propiedades, comúnmente conocida como "spread props" o "spread attributes", es una característica en Svelte que te permite pasar todas las propiedades de un objeto a un componente de manera fácil y concisa. Esto es útil cuando deseas pasar múltiples propiedades a un componente sin tener que enumerarlas individualmente.

Supongamos que tienes un componente llamado `MiComponente` que acepta varias propiedades:

```markup
<!-- MiComponente.svelte -->
<script>
  export let nombre;
  export let edad;
  export let ciudad;
</script>

<p>{nombre} tiene {edad} años y vive en {ciudad}.</p>
```

En el componente padre, puedes utilizar "spread props" para pasar todas las propiedades de un objeto al componente hijo:

```markup
<!-- App.svelte -->
<script>
  import MiComponente from './MiComponente.svelte';

  let datosPersona = {
    nombre: 'Juan',
    edad: 25,
    ciudad: 'Ciudad de Ejemplo'
  };
</script>

<MiComponente {...datosPersona} />
```

En este ejemplo, `{...datosPersona}` está propagando todas las propiedades del objeto `datosPersona` al componente `MiComponente`. Esto es equivalente a pasar cada propiedad individualmente como:

```markup
<MiComponente nombre={datosPersona.nombre} edad={datosPersona.edad} ciudad={datosPersona.ciudad} />
```

Usar "spread props" es particularmente útil cuando tienes un objeto con muchas propiedades y deseas pasarlas todas a un componente de manera más limpia y eficiente.

Ten en cuenta que "spread props" no solo funciona con objetos. También puedes aplicarlo a otros elementos, como arrays:

```markup
<script>
  let colores = ['rojo', 'verde', 'azul'];
</script>

<MiComponente colores={...colores} />
```

En este caso, cada elemento del array se pasa como una propiedad individual al componente `MiComponente`.
