# Promesas

Las promesas son una característica fundamental en JavaScript que permite manejar operaciones asíncronas de manera más legible y efectiva. Este post explorará qué son las promesas, cómo se utilizan y cómo pueden mejorar la gestión del código asíncrono en tus proyectos JavaScript.

{% embed url="https://www.youtube.com/watch?v=NOzi4wBHn0o" %}

### ¿Qué son las Promesas?

Una promesa en JavaScript es un objeto que representa la eventual finalización o el fracaso de una operación asíncrona. Proporciona una interfaz más clara y flexible para manejar flujos asíncronos en comparación con las devoluciones de llamada tradicionales.

### Creando una Promesa

```javascript
onst miPromesa = new Promise((resolve, reject) => {
  // Lógica asíncrona o tarea
  const exito = true;

  if (exito) {
    resolve('Operación exitosa');
  } else {
    reject('La operación ha fallado');
  }
});
```

En este ejemplo, creamos una promesa que representa una operación asíncrona. La función pasada como argumento tiene dos parámetros, `resolve` y `reject`, que se utilizan para indicar si la operación se completó con éxito o falló, respectivamente.

### Consumiendo Promesas

```javascript
miPromesa
  .then(resultado => console.log(resultado))
  .catch(error => console.error(error));
```

El método `then` se utiliza para manejar el caso de éxito de la promesa, mientras que `catch` maneja el caso de fallo. Esto mejora significativamente la legibilidad y el manejo de errores en comparación con las devoluciones de llamada anidadas.

### Promesas Encadenadas

```javascript
const obtenerDatos = () => {
  return new Promise((resolve, reject) => {
    // Lógica asíncrona para obtener datos
    const datos = 'Datos obtenidos correctamente';
    resolve(datos);
  });
};

obtenerDatos()
  .then(datos => {
    console.log(datos);
    return 'Datos procesados';
  })
  .then(datosProcesados => console.log(datosProcesados))
  .catch(error => console.error(error));
```

Las promesas permiten encadenar operaciones asíncronas de manera más clara y estructurada, facilitando la lectura del código. En este caso si funcion `obtenerDatos` funnciona como lo esperado el primer `then` devolvera un string que es guardado en la variable `datosProcesados` e impreso en el segundo `then`.

Este encadenamiento tambien se puede hacer con varias funciones:

```javascript
const obtenerDatos = () => {
  return new Promise((resolve, reject) => {
    // Lógica asíncrona para obtener datos
    const datos = 'Datos obtenidos correctamente';
    resolve(datos);
  });
};

const enviarDatos = () => {
  return new Promise((resolve, reject) => {
    // Lógica asíncrona para obtener datos
    const datos = 'Datos enviados correctamente';
    resolve(datos);
  });
};

obtenerDatos().then(datos => {console.log(datos); return enviarDatos()})
              .then(datos => {console.log(datos); console.log("Pirceso terminado")})
              .catch(error => console.error('Error: ', error);
```

### Promise.all y Promise.race

```javascript
const promesa1 = Promise.resolve('Primera promesa');
const promesa2 = new Promise((resolve) => setTimeout(() => resolve('Segunda promesa'), 2000));

Promise.all([promesa1, promesa2])
  .then(resultados => console.log(resultados))
  .catch(error => console.error(error));

Promise.race([promesa1, promesa2])
  .then(resultado => console.log(resultado))
  .catch(error => console.error(error));
```

`Promise.all` se resuelve cuando todas las promesas en el array han sido resueltas, mientras que `Promise.race` se resuelve o se rechaza tan pronto como una de las promesas en el array se resuelve o se rechaza.

\
