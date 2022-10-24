---
description: Parar procesos
---

# Wait

Cuando un proceso crea un proceso secundario, a veces es necesario que el proceso principal se ejecute solo después de que el secundario haya terminado. La llamada al sistema wait() hace exactamente esto. Hace que el proceso principal espere a que finalice el proceso secundario y luego el padre continúa trabajando desde la declaración después de la wait().&#x20;

Para ser exactos, esperar hace que el padre espere a que el hijo cambie de estado. El cambio de estado puede ser:&#x20;

* el hijo ha terminado
* el hijo fue detenido por una señal
* el hijo fue retomado por una señal

<figure><img src="https://media.geeksforgeeks.org/wp-content/uploads/Wait_system_call_in_c.jpg" alt=""><figcaption></figcaption></figure>

### Sinopsis

```c
#include <sys/types.h>
#include <sys/wait.h>

pid_t wait(int *wstatus);
```

La llamada al sistema wait() toma solo un parámetro que **almacena la información de estado del proceso**. Pase NULL como valor si no desea conocer el estado de salida del proceso hijo y simplemente le preocupa hacer que el padre espere al hijo. En caso de éxito, la espera devuelve el PID del proceso secundario finalizado, mientras que en caso de error devuelve -1.

{% hint style="warning" %}
Se puede usar wait() para hacer que el padre espere a que el hijo termine (finalice) pero no al revés. wait devuelve el PID del proceso hijo terminado mientras que, en caso de falla, devuelve -1.
{% endhint %}

### Informacion sobre el estado del hijo&#x20;

La información de estado sobre el hijo reportada por wait es más que solo el estado de salida del niño, también incluye:

* terminación normal/anormal
* causa de terminación
* estado del exit (salida)

Para encontras mas iformacion sobre el estado del hijo se utilizan las macros `WIF`

| Macro                   | Descripcion                               |
| ----------------------- | ----------------------------------------- |
| WIFEXITED(status)       | El hijo se ejecuto con normalidad         |
| **WEXITSTATUS(status)** | reterna codigo cuando el hijo existe      |
| WIFSIGNALED(status)     | El hijo salió porque no se captó una seña |
| **WTERMSIG(status)**    | da el número de la señal de terminación   |
| WIFSTOPPED(status)      | El hijo ha sido detenido                  |
| **WSTOPSIG(status)**    | da el número de la señal de parada        |

### Ejemplo

```c
#include<unistd.h>
#include<sys/types.h>
#include<stdio.h>
#include<sys/wait.h>
int main()
{
pid_t p;
printf("before fork\n");
p=fork();
if(p==0)//child
{
printf("I am child having id %d\n",getpid());
printf("My parent's id is %d\n",getppid());
}
else//parent
{
wait(NULL);
printf("My child's id is %d\n",p);
printf("I am parent having id %d\n",getpid());
}
printf("Common\n");
}
```

output:

```
before fork
I am child having id 458
My parent's id is 457
Common
My child's id is 458
I am parent having id 457
Common
```

La ejecución comienza imprimiendo “antes del tenedor”. Luego, la llamada al sistema fork() crea un proceso secundario.&#x20;

La llamada al sistema wait() se agrega a la sección principal del código. Por lo tanto, en el momento en que el procesador comienza a procesar al padre, el proceso principal se suspende porque la primera declaración es esperar (NULL). Por lo tanto, primero, se ejecuta el proceso secundario y todas las líneas de salida corresponden al proceso secundario. Una vez que finaliza el proceso secundario, el padre reanuda e imprime todas sus instrucciones printf(). El NULL dentro de wait() significa que no estamos interesados ​​en conocer el estado de cambio de estado del proceso secundario.

### Bibliografia

* [https://dextutor.com/program-for-wait-system-call/](https://dextutor.com/program-for-wait-system-call/)
* [https://man7.org/linux/man-pages/man2/wait.2.html](https://man7.org/linux/man-pages/man2/wait.2.html)
* [https://linuxhint.com/wait-system-call-in-c/](https://linuxhint.com/wait-system-call-in-c/)
* [https://www.geeksforgeeks.org/wait-system-call-c/](https://www.geeksforgeeks.org/wait-system-call-c/)
* [https://www.delftstack.com/es/howto/c/wait-in-c/](https://www.delftstack.com/es/howto/c/wait-in-c/)
* [https://manpages.ubuntu.com/manpages/xenial/es/man2/wait.2.html](https://manpages.ubuntu.com/manpages/xenial/es/man2/wait.2.html)
