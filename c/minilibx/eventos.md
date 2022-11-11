# Eventos

Los eventos son la base para escribir aplicaciones interactivas en MiniLibX. Todos los hooks en MiniLibX no son más que una función que se llama cada vez que se dispara un evento.&#x20;

Tanto X-Window como MacOSX son sistemas gráficos bidireccionales. Por un lado, el programa envía órdenes a la pantalla para mostrar píxeles, imágenes, etc. Por otro lado, puede obtener información del teclado y del ratón asociada a la pantalla. Para ello, el programa recibe "eventos" del teclado o del ratón.

### AppleScript key codes

Todo accion realizada a traves del teclado o el mouse tiene  un numero de referencia, de esta manera mediante los eventos que nos facilita MiniLibX podremos saber en todo momento que informacion no esta enviando el usuario de nuestro programa. Para asi si lo deseasmos estabelcerle a ciertas acciones una funcion o accion corespondiente.

La key codes del teclado de mac son las [siguientes](https://eastmanreference.com/complete-list-of-applescript-key-codes):

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-11 at 8.12.36 PM.png" alt=""><figcaption></figcaption></figure>

### Tipos de eventos

Para que podamos registrar eventos, el minilibx nos proporciona un conjunto de funciones llamadas hooks que podremos utilizar para registrar eventos antes de que se llame a `mlx_loop`. Esta funcion deja el programa en un bucle infinito, para asi poder recibir los datos de entrada a traves del teclado y asi ejecutar las funciones correspodientes.

```c
int    mlx_loop ( void *mlx_ptr );
```

la fucnio principal para la utilizacion de evenetos es mlx\_hook, este nos permite especifciar que eventos queremos&#x20;
