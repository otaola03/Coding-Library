---
description: For processes communication
---

# Signals

Las señales en C son un mecanismo de interrupción de la ejecución de un proceso para indicar un evento asociado con el proceso. Cuando se produce una señal, el sistema operativo interrumpe la ejecución del proceso y llama a una función de manejo de señal específica, si se ha registrado previamente.

Las señales se pueden generar de varias maneras, como una condición de error en el proceso, un timer que ha expirado o una entrada del usuario, como presionar Ctrl + C en la terminal.

El comportamiento por defecto de una señal puede ser ignorado o terminar el proceso. Sin embargo, un programador puede registrar su propia función de manejo de señal para realizar una acción personalizada en lugar del comportamiento predeterminado.

En resumen, las señales en C permiten a los procesos responder a eventos externos y tomar medidas adecuadas para manejarlos, lo que es esencial para la construcción de programas robustos y confiables.

La función `kill` en C permite enviar señales a procesos y `siagction` tiene como parametrso una de estas señales para establecer que se hara en caso de que el proceso reciba una de estas señales. Algunas de las señales más comunes que pueden ser enviadas son:

1. SIGABRT: esta señal se utiliza para indicar un error en la ejecución de un programa, como una llamada inválida a la función abort().
2. SIGFPE: esta señal se envía cuando se produce una excepción matemática, como una división por cero o una operación en punto flotante no válida.
3. SIGILL: esta señal se envía cuando el proceso intenta ejecutar un código ilegal o inválido.
4. SIGINT: esta señal se envía cuando se presiona CTRl + C en la línea de comandos.
5. SIGSEGV: esta señal se envía cuando un proceso intenta acceder a una dirección de memoria no válida o protegida.
6. SIGTERM: esta señal se envía para indicar una terminación normal del proceso, y puede ser generada por una llamada a la función kill().
7. SIGUSR1: esta señal especial puede ser generada y manejada por programas para cualquier propósito que el programador desee.
8. SIGUSR2: esta señal especial puede ser generada y manejada por programas para cualquier propósito que el programador desee.

### sigaction

La función `sigaction` en C es una función que se utiliza para especificar la acción que se tomará cuando se reciba una señal. Tiene la siguiente cabecera:

```c
#include <signal.h>
int sigaction(int signum, const struct sigaction *act, struct sigaction *oldact);
```

Los argumentos de la función `sigaction` son:

* `signum`: Es un entero que especifica el [número de la señal](https://man7.org/linux/man-pages/man7/signal.7.html) para la que se desea especificar la acción.&#x20;
* `act`: Es un puntero a una estructura `sigaction` que contiene la información sobre la acción que se tomará cuando se reciba la señal.
* `oldact`: Es un puntero a una estructura `sigaction` en la que se almacenará la acción anterior asociada con la señal.

La función `sigaction` funciona especificando la acción que se tomará cuando se reciba una señal determinada. La acción se especifica en la estructura `sigaction`, que contiene información sobre la acción que se tomará y cualquier máscara de señales adicional que deba establecerse durante la gestión de la señal.

La función `sigaction` se utiliza cuando se desea especificar una acción personalizada para una señal determinada. Por ejemplo, se puede usar para especificar una función de manejador de señales personalizada que se ejecutará cuando se reciba una señal determinada.

Aquí hay un ejemplo de código que ilustra el uso de la función `sigaction`:

```c
#include <signal.h>
#include <stdio.h>
#include <unistd.h>

void sigint_handler(int signum)
{
    printf("Recibí la señal %d\n", signum);
}

int main(void)
{
    struct sigaction sa;
    sa.sa_handler = sigint_handler;
    sigemptyset(&sa.sa_mask);
    sa.sa_flags = 0;

    if (sigaction(SIGINT, &sa, NULL) == -1)
    {
        perror("sigaction");
        return 1;
    }

    while (1)
    {
        printf("Esperando una señal...\n");
        sleep(1);
    }

    return 0;
}
```

En este ejemplo, se define una función `sigint_handler` que se utilizará como manejador de señales para la señal `SIGINT`. Luego, se establece la acción para `SIGINT` usando La función `sigaction` es utilizada para establecer la acción para la señal SIGINT. La primera entrada en `sigaction` es el número de la señal que se desea manejar (en este caso, `SIGINT`), la segunda entrada es una estructura `sigaction` que describe la acción a tomar cuando se reciba la señal y la tercer entrada es una estructura `sigaction` opcional que puede ser utilizada para guardar la acción anterior.

En este ejemplo, la estructura `sigaction` `sa` se inicializa con el manejador de señales `sigint_handler` y un conjunto de señales vacío en `sa_mask`. La bandera `sa_flags` se establece en `0` lo que significa que no hay banderas adicionales activas.

Después de establecer la acción para la señal SIGINT, el programa entra en un bucle infinito que imprime "Estoy en ejecución..." cada segundo. Si se presiona Ctrl + C mientras el programa está en ejecución, se generará la señal SIGINT, que será manejada por `sigint_handler` y un mensaje "Recibí la señal 2" será impreso.

### kill

La función `kill` en C es una función del sistema que permite enviar una señal a un proceso o a un grupo de procesos. Su cabecera es:

```c
cCopy codeint kill(pid_t pid, int sig);
```

Donde `pid` es el ID del proceso al que se desea enviar la señal y `sig` es el número de la señal que se desea enviar.

La función `kill` devuelve 0 si se ha enviado correctamente la señal y -1 en caso de error. En ese caso, la variable `errno` se establece con el código de error correspondiente.

La función `kill` se utiliza para enviar señales a otros procesos y controlar su comportamiento. Por ejemplo, la señal SIGTERM (número 15) se utiliza comúnmente para solicitar a un proceso que termine de manera limpia, mientras que la señal SIGKILL (número 9) se utiliza para terminar de manera forzada un proceso que no responde.

Aquí hay un ejemplo de código que envía la señal SIGTERM a un proceso con ID 12345:

```c
cCopy code#include <signal.h>
#include <unistd.h>
#include <stdio.h>

int main(void) {
    int result = kill(12345, SIGTERM);
    if (result == 0) {
        printf("Señal enviada exitosamente\n");
    } else {
        printf("Error al enviar la señal\n");
    }

    return 0;
}
```

Es importante tener en cuenta que la función `kill` solo puede enviar señales a procesos a los que el usuario que ejecuta el programa tenga acceso.
