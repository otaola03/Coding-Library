# Estructura sigaction

La estructura `sigaction` en C es una estructura que se utiliza para especificar el manejo de una señal en un programa. Esta estructura se utiliza en la función `sigaction` para registrar un manejador de señal personalizado.

Es importante destacar que el uso de la estructura `sigaction` es opcional, ya que también se pueden manejar señales usando funciones simples, como `signal()`, que solo requieren un puntero a función y un número de señal. Sin embargo, la estructura `sigaction` ofrece un mayor control y flexibil

La estructura `sigaction` tiene la siguiente forma:

```c
struct sigaction {
    void     (*sa_handler)(int);
    void     (*sa_sigaction)(int, siginfo_t *, void *);
    sigset_t   sa_mask;
    int        sa_flags;
    void     (*sa_restorer)(void);
};
```

### `sa_handler`:

`sa_handler` es una variable de la estructura `struct sigaction` que se utiliza para especificar una función que será llamada cuando se reciba una señal determinada. Esta función se conoce como manejador de señales y su objetivo es realizar una acción específica en respuesta a la recepción de una señal.

La cabecera de la función que se especifica como manejador de señales es la siguiente:

```c
void funcion_manejadora (int signum);
```

Donde `signum` es el número de la señal que se ha recibido.

Ejemplo:

```c
#include <signal.h>
#include <stdio.h>
#include <unistd.h>

void manejador_SIGINT (int signum) {
    printf("Se ha recibido la señal SIGINT con número %d\n", signum);
}

int main () {
    struct sigaction accion;
    accion.sa_handler = manejador_SIGINT;
    sigemptyset(&accion.sa_mask);
    accion.sa_flags = 0;
    
    sigaction(SIGINT, &accion, NULL);
    
    while (1) {
        sleep(1);
    }
    
    return 0;
}
```

En este ejemplo, se define una función `manejador_SIGINT` que se utilizará como manejador de señales para la señal `SIGINT`. Luego, se establece la acción para `SIGINT` usando `sigaction` y especificando `manejador_SIGINT` como `sa_handler`.

### `sa_sigaction`

`sa_sigaction` es un puntero a una función que actúa como manejador de señales. Es una variable en la estructura `sigaction` que describe la acción a tomar cuando se reciba una señal específica.

La cabecera de la función apunta a una función con el siguiente prototipo:

```c
void (*sa_sigaction)(int signum, siginfo_t *info, void *context);
```

`sa_sigaction` toma tres argumentos:

1. `signum`: es el número de señal que ha sido recibida.
2. `info`: es un puntero a una estructura `siginfo_t` que proporciona información adicional sobre la señal.
3. `context`: es un puntero a una estructura que contiene información sobre el contexto en el momento en quese recibió la señal.

Aquí hay un ejemplo de código que muestra cómo utilizar `sa_sigaction` para manejar la señal `SIGINT`:

```c
#include <signal.h>
#include <stdio.h>
#include <unistd.h>

void sigint_handler(int signum, siginfo_t *info, void *context)
{
  printf("Recibí la señal %d\n", signum);
}

int main()
{
  struct sigaction sa;
  sa.sa_sigaction = sigint_handler;
  sa.sa_flags = SA_SIGINFO;
  sigemptyset(&sa.sa_mask);

  if (sigaction(SIGINT, &sa, NULL) == -1)
  {
    perror("sigaction");
    return 1;
  }

  while (1)
  {
    printf("Estoy en ejecución...\n");
    sleep(1);
  }

  return 0;
}
```

En este ejemplo, la función `sigint_handler` se establece como el manejador de señales para la señal `SIGINT` usando la estructura `sigaction` `sa`. La bandera `sa_flags` se establece en `SA_SIGINFO` para que la función `sa_sigaction` reciba información adicional sobre la señal. Finalmente, se establece la acción para `SIGINT` utilizando la función `sigaction`. Si se presiona Ctrl + C mientras el programa está en ejecución, se generará la señal SIGINT, que será manejada por `sigint_handler` y un mensaje "Recibí la señal 2" será impreso.

### `sa_mask`

La máscara de señales `sa_mask` en la estructura `sigaction` se utiliza para especificar qué señales deben bloquearse durante la ejecución del manejador de señales. Es decir, cuando se recibe una señal y se activa el manejador de señales, se pueden bloquear otras señales específicas para evitar que se manejen simultáneamente.

El manejo de `sa_mask` se realiza mediante las funciones `sigemptyset`, `sigfillset`, `sigaddset`, `sigdelset` y `sigismember`. Estas funciones se utilizan para manipular la máscara de señales en la estructura `sigaction`.

* `sigemptyset` se utiliza para inicializar una máscara de señales como un conjunto vacío.
* `sigfillset` se utiliza para inicializar una máscara de señales como un conjunto lleno, lo que significa que todas las señales están incluidas en la máscara.
* `sigaddset` se utiliza para agregar una señal a una máscara de señales existente.
* `sigdelset` se utiliza para eliminar una señal de una máscara de señales existente.
* `sigismember` se utiliza para determinar si una señal está incluida en una máscara de señales.

Aquí hay un ejemplo de código en C que ilustra el uso de la máscara de señales:

```c
cCopy code#include <signal.h>
#include <unistd.h>
#include <stdio.h>

void signal_handler(int signum)
{
    printf("Recibida la señal %d\n", signum);
    sleep(3);
}

int main(void)
{
    struct sigaction act;
    act.sa_handler = signal_handler;
    sigemptyset(&act.sa_mask);
    sigaddset(&act.sa_mask, SIGINT);
    act.sa_flags = 0;

    if (sigaction(SIGUSR1, &act, NULL) < 0)
    {
        perror("sigaction");
        return 1;
    }

    printf("Presione Ctrl+Z para enviar la señal SIGUSR1\n");

    while (1)
    {
        printf("Esperando...\n");
        sleep(1);
    }

    return 0;
}
```

En este ejemplo, se establece un manejador de señal para la señal `SIGUSR1` mediante la función `sigaction`. La estructura `sigaction` incluye el manejador de señal en el campo `sa_handler`, y una máscara de señales que incluye la señal `SIGINT` en el campo `sa_mask`.

El código ejecuta un bucle infinito que solo imprime "Esperando..." y luego se bloquea por un segundo usando la función `sleep`. Si se presiona `Ctrl+Z` mientras el código está en el bucle, se enviará la señal `SIGUSR1` al proceso, interrumpiendo la función `sleep` y activando el manejador de señales.

El manejador de señales imprime un mensaje y luego se bloquea por tres segundos usando la función `sleep`. Durante este tiempo, la señal `SIGINT` está bloqueada, por lo que si se presiona `Ctrl+C`, no se enviará la señal al proceso.

Este ejemplo ilustra cómo la máscara de señales `sa_mask` se puede usar para controlar qué señales deben bl

### `sa_flags`

Este es un conjunto de banderas que controlan el comportamiento del manejador de señal. Algunas banderas comunes incluyen:

* `SA_NOCLDSTOP`: Esta bandera indica que no se debe enviar una señal `SIGCHLD` cuando un proceso hijo se detiene o termina.
* `SA_SIGINFO`: Esta bandera indica que se debe utilizar `sa_sigaction` en lugar de `sa_handler` para manejar la señal.
* `SA_RESTART`: Esta bandera indica que las operaciones bloqueadas por la señal deben ser automáticamente restauradas después de que el manejador de señal haya finalizado.

Aquí hay un ejemplo simple de código en C que demuestra el uso de la bandera `SA_RESTART`:

```c
#include <signal.h>
#include <unistd.h>
#include <stdio.h>

void signal_handler(int signum)
{
    printf("Recibida la señal %d\n", signum);
}

int main(void)
{
    struct sigaction act;
    act.sa_handler = signal_handler;
    sigemptyset(&act.sa_mask);
    act.sa_flags = SA_RESTART;

    if (sigaction(SIGINT, &act, NULL) < 0)
    {
        perror("sigaction");
        return 1;
    }

    printf("Presione Ctrl+C para enviar la señal SIGINT\n");

    while (1)
    {
        printf("Esperando...\n");
        sleep(1);
    }

    return 0;
}
```

En este ejemplo, se establece un manejador de señal para la señal `SIGINT` (la señal generada por `Ctrl+C`) mediante la función `sigaction`. La estructura `sigaction` incluye el manejador de señal en el campo `sa_handler`, la máscara de señales vacía en el campo `sa_mask`, y la bandera `SA_RESTART` en el campo `sa_flags`.

El código ejecuta un bucle infinito que solo imprime "Esperando..." y luego se bloquea por un segundo usando la función `sleep`. Si se presiona `Ctrl+C` mientras el código está en el bucle, se enviará la señal `SIGINT` al proceso, interrumpiendo la función `sleep`.

Sin la bandera `SA_RESTART`, la función `sleep` no sería reanudada después de manejar la señal, y el proceso simplemente volvería al inicio del bucle. Sin embargo, con la bandera `SA_RESTART`, la función `sleep` será automáticamente reanudada después de manejar la señal, permitiendo que el proceso continúe su ejecución sin interrupciones.

Este ejemplo muestra cómo la bandera `SA_RESTART` puede simplificar el código y asegurar un comportamiento más consistente en el proceso.
