---
description: Parar procesos
---

# Wait

La función `wait` es una envoltura para la llamada al sistema compatible con POSIX, definida en el archivo de cabecera `<sys/wait.h>`. La función se utiliza para esperar los cambios de estado del programa en los procesos hijos y recuperar la información correspondiente. `wait` se llama normalmente después de la llamada al sistema `fork` que crea un nuevo proceso hijo. La llamada `wait` suspende el programa que llama hasta que uno de sus procesos hijos termine.

El usuario debe estructurar el código para que haya dos caminos diferentes para el proceso que llama y el proceso hijo. Normalmente se consigue con la sentencia `if...else` que evalúa el valor de retorno de la llamada a la función `fork`. Tenga en cuenta que `fork` devuelve el ID del proceso hijo, un entero positivo, en el proceso padre y devuelve 0 en el proceso hijo. `fork` devolverá -1 si la llamada falla.

**El proceso hijo puede terminar debido en cualquiera de estos casos:**

* Si se llama a la funcion `exit()`
* Devuelve un int desde el main
* Recibe una señal (del sistema operativo o de otro proceso) cuya acción predeterminada es terminar.

<figure><img src="https://media.geeksforgeeks.org/wp-content/uploads/Wait_system_call_in_c.jpg" alt=""><figcaption></figcaption></figure>

### Sintaxis

Si algún proceso tiene más de un proceso secundario, luego de llamar a `wait()`, el proceso principal debe estar en estado de espera si no finaliza ningún proceso secundario. Si solo se finaliza un proceso secundario, devolver una wait () devuelve el ID del proceso secundario terminado.

Si se finaliza más de un proceso secundario, wait() cosecha cualquier elemento secundario arbitrariamente y devuelve un ID de proceso de ese proceso secundario.&#x20;

Cuando wait () regresa, también definen el estado de salida (que le dice a nuestro proceso por qué terminó) a través del puntero, si el estado no es NULL. Si algún proceso no tiene un proceso secundario, wait () devuelve inmediatamente "-1".

> wait(): on success, returns the process ID of the terminated child;
>
> on failure, -1 is returned.

```
#include <sys/types.h>
#include <sys/wait.h>

pid_t wait(int *wstatus);
```

**Esperar hace que el padre espere a que el hijo cambie su estado**. El cambio de estado podría deberse a que el proceso secundario finalizó, se detuvo por una señal o se reanudó por una señal. En algunas circunstancias, cuando un proceso secundario se cierra o cambia de estado, se debe notificar al proceso padre sobre la alteración del estado o el estado de terminación del proceso secundario. En ese caso, el proceso principal usa funciones como `wait()` para consultar sobre la actualización en el estado del proceso secundario.

`Wait()` suspende el proceso de la persona que llama hasta que el sistema **recibe información sobre el estado final del hijo**. `Wait()` regresa instantáneamente si el sistema ya tiene información de estado sobre un proceso secundario terminado cuando se invoca. Si el proceso que llama recibe la señal con la acción de ejecutar un controlador de señales o finalizar el proceso, la espera () también finaliza.
