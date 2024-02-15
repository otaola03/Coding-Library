# Async/Await

Las funciones `async` y `await` son características de JavaScript que simplifican y mejoran la legibilidad del código asíncrono. Este post te guiará a través de qué son, cómo se utilizan y cómo pueden hacer que el manejo de operaciones asíncronas sea más claro y conciso.

{% embed url="https://www.youtube.com/watch?v=9j1dZwFEJ-c" %}

### ¿Qué son async y await?

Las palabras clave `async` y `await` fueron introducidas en ECMAScript 2017 (también conocido como ES8) para facilitar la escritura de código asíncrono en JavaScript.

* `async`: Se utiliza para declarar que una función retornará una promesa y permite el uso de `await` dentro de la función.
* `await`: Se utiliza dentro de una función declarada con `async` y pausa la ejecución de la función hasta que la promesa se resuelva. Permite trabajar con promesas de manera síncrona.

### Uso Básico

```javascript
// Función asincrónica con await
function obtenerDatos() {
  // Simulación de una operación asíncrona
  return new Promise(resolve => {
    setTimeout(() => resolve('Datos obtenidos'), 2000);
  });
}

// Uso de la función asincrónica
async function procesoPrincipal() {
  try {
    const datos = await obtenerDatos();
    console.log(datos);
    // Resto del código que depende de 'datos'
  } catch (error) {
    console.error('Error:', error);
  }
}

// Llamada a la función principal
procesoPrincipal();
```

En este ejemplo, `obtenerDatos` es una función asincrónica que retorna una promesa después de simular una operación asíncrona. La función `procesoPrincipal` utiliza `await` para esperar a que `obtenerDatos` se resuelva antes de continuar con el resto del código. Esto mejora la legibilidad y la estructura del código.
