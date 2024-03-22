# Reactividad

En Svelte, la reactividad significa que cuando una variable cambia, la interfaz de usuario se actualiza automáticamente para reflejar ese cambio. No necesitas escribir código extra para manejar estas actualizaciones; Svelte se encarga de eso por ti, simplificando el desarrollo de aplicaciones interactivas.

### Eventos

El manejo de eventos en Svelte es esencial para construir aplicaciones interactivas y dinámicas. Este post te guiará a través de las diversas formas en que Svelte maneja eventos, desde eventos de usuario hasta eventos personalizados, proporcionando una base sólida para crear experiencias de usuario envolventes y receptivas.

En Svelte, el manejo de eventos de usuario es intuitivo y directo. Puedes reaccionar a eventos como clics, cambios, y más, de manera fácil y legible. Tan solo tines que hacer uso del atributo on:

```markup
<script>
  function handleClick() {
    alert('¡Hiciste clic!');
  }
</script>

<button on:click={handleClick}>Haz clic</button>
```

Otro ejemplo simeple es el siguiente:

```markup
<script>
  let contador = 0;
</script>

<button on:click={() => contador += 1}>
  Haz clic: {contador}
</button>
```

### Variables reactivas

Las declaraciones reactivas en Svelte son una parte fundamental de la reactividad en la interfaz de usuario. Permiten que los componentes respondan dinámicamente a los cambios en las variables o expresiones que han sido marcadas como reactivas. Las declaraciones reactivas se crean utilizando el modificador `$:`.

* Las declaraciones reactivas se inician con `$:` seguido de una expresión o bloque de código.
* La expresión o bloque de código se evalúa de manera reactiva, lo que significa que **cualquier cambio en las variables referenciadas provocará la reevaluación de la expresión**.
* Svelte realiza el seguimiento automático de las dependencias dentro de las declaraciones reactivas, por lo que no es necesario especificar manualmente qué variables deben ser rastreadas.

#### Uso basico

Puedes usar declaraciones reactivas en expresiones para calcular valores de manera dinámica basándote en otras variables reactivas.

```markup
<script>
  let a = 5;
  let b = 10;
  $: suma = a + b;
</script>

<p>La suma de a y b es: {suma}</p>
```

Además de expresiones simples, puedes usar bloques de código más complejos.

```markup
<script>
  let contador = 0;
  $: {
    console.log('El contador ha cambiado:', contador);
    if (contador > 5) {
      console.log('¡Contador superó 5!');
    }
  }
</script>

<button on:click={() => contador += 1}>Incrementar</button>
```

### Arrays reactivos

Esto se debe a que Svelte aplica su reactividad mediant la asgignsciones, por lo que si no hay asignacion de un valor a una variable el cambio no se aplciara. Por ejemplo este cambio no se aplicaria:

```markup
<script>
let miArray = [1, 2, 3];

function addNumber() {
    numbers.push(numbers.length + 1);
}
</script>

<button on:click={agregarElemento}>Agregar Elemento</button>

{#each miArray as elemento (elemento)}
  <p>{elemento}</p>
{/each}
```

En cambio si lo hacemos de la ssiguiente manera, el cambio si se aplicarar:

```javascript
function addNumber() {
    numbers.push(numbers.length + 1);
    numbers = numbers;
}
```

Es decir, para actualizar un array de manera reactiva, se debe crear un nuevo array en lugar de modificar el existente directamente. Esto tambien puedes lograrlo utilizando la función `array.concat` o el operador de propagación (`...`). Aquí tienes un ejemplo:

```javascript
let miArray = [1, 2, 3];

function agregarElemento() {
    miArray = [...miArray, 4]; // Crea un nuevo array con el nuevo elemento
}
```

En este ejemplo, cada vez que se hace clic en el botón, se agrega un nuevo elemento al array `miArray` utilizando el operador de propagación (`...`). Esto asegura que se cree un nuevo array, lo que activa la reactividad y actualiza automáticamente la interfaz de usuario.

### **Objetos reactivos**

Al igual que con los arrays, para actualizar un objeto de manera reactiva, debes crear un nuevo objeto en lugar de modificar el existente directamente. Puedes lograr esto utilizando la función `Object.assign` o el operador de propagación (`...`). Aquí tienes un ejemplo:

```markup
<script>
  let miObjeto = { nombre: 'Juan', edad: 25 };

  function actualizarEdad() {
    miObjeto = { ...miObjeto, edad: 26 }; // Crea un nuevo objeto con la edad actualizada
  }
</script>

<button on:click={actualizarEdad}>Actualizar Edad</button>

<p>Nombre: {miObjeto.nombre}, Edad: {miObjeto.edad}</p>
```

En este ejemplo, cada vez que se hace clic en el botón, se actualiza la propiedad `edad` del objeto `miObjeto` creando un nuevo objeto con el operador de propagación (`...`).

Es importante tener en cuenta que estas técnicas de actualización son necesarias para mantener la reactividad en Svelte. Si intentas modificar un array u objeto directamente, Svelte puede no detectar el cambio y no actualizará la interfaz de usuario de manera automática.

\
