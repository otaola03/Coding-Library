# Semáforos

Los semáforos son un mecanismo de sincronización utilizado para controlar el acceso a un recurso compartido por varios procesos o hilos. Un semáforo es una variable entera que se puede incrementar (releasing) o decrementar (waiting) de manera atómica.

Los semáforos se utilizan para implementar bloqueos o mutexes, que permiten que solo un proceso o hilo tenga acceso a un recurso determinado en un momento dado. Esto es útil para evitar conflictos de acceso y garantizar la consistencia de los datos.

Existen dos variedades de semáforos: los semáforos tradicionales de System V y los semáforos POSIX, los más recientes. En este post, veremos los semáforos POSIX.

### Explicación sencilla

Los semáforos son una forma de controlar el acceso a un juguete o un juego que varios niños quieren usar al mismo tiempo. Cada vez que un niño quiere usar el juguete o juego, debe pedir permiso a un semáforo. Si el semáforo está en verde, significa que puede usar el juguete o juego. Si está en rojo, significa que otro niño está usándolo y debe esperar a que termine.

De esta manera, los semáforos ayudan a evitar peleas y conflictos entre los niños al jugar con los juguetes y aseguran que todos tengan una oportunidad justa de disfrutarlos.

### sem\_open

`sem_open` es la llamada para comenzar a utilizar un semáforo. `sem_open` abre un semáforo existente o crea un semáforo nuevo y lo abre para realizar operaciones adicionales.

```c
#include <semaphore.h>

sem_t *sem_open (const char *name, int oflag);
sem_t *sem_open (const char *name, int oflag, mode_t mode, unsigned int value);
```

#### name

El argumento "name" de la función `sem_open` es el nombre del semáforo que se está abriendo o creando. El nombre del semáforo es una cadena de caracteres que se utiliza para identificar al semáforo y permitir el acceso a él por diferentes procesos o hilos.

El nombre del semáforo se utiliza para crear un archivo en el sistema de archivos que representa al semáforo. Este archivo se encuentra en el directorio "/dev/shm" y tiene un prefijo "sem." seguido del nombre del semáforo. Por ejemplo, si se crea un semáforo con el nombre "/mysem", se creará un archivo con el nombre "/dev/shm/sem.mysem".

Es importante tener en cuenta que el nombre del semáforo es compartido entre todos los procesos o hilos que deseen utilizar el semáforo. Por lo tanto, es necesario utilizar nombres únicos para evitar conflictos con otros semáforos. Además, es importante recordar que el nombre del semáforo es una cadena de caracteres y no un número entero, por lo que no se puede utilizar como un identificador único para el semáforo.

Una manera visual de declarar el nombre de los semaforos es mediante macros:

```c
#define SEM_NAME "/mysem"
```

#### oflag

El segundo parámetro de la función `sem_open` es una cadena de banderas que indica cómo se deben abrir o crear el semáforo.

El parámetro "oflag" es una combinación de una o más banderas que se pueden utilizar para controlar el comportamiento de la función. Las banderas más comunes que se pueden utilizar en el parámetro "oflag" son:

* `O_CREAT`: Indica que el semáforo debe ser creado si no existe. Si se especifica esta bandera, se debe utilizar la segunda forma de la función `sem_open`, que incluye dos parámetros adicionales: "mode" y "value".
* `O_EXCL`: Indica que la llamada a `sem_open` debe fallar y establecer el valor de `errno` con el error "EEXIST" si el semáforo ya existe.
* `O_RDONLY`: Indica que el semáforo se abrirá en modo de lectura solamente.
* `O_WRONLY`: Indica que el semáforo se abrirá en modo de escritura solamente.
* `O_RDWR`: Indica que el semáforo se abrirá en modo de lectura y escritura.

En el caso de que no queda clara la diferencia entre `O_CREAT` y `O_RDWR`, la bandera `O_RDWR` indica el modo en que se abre el semáforo (lectura y escritura) mientras que la bandera `O_CREAT` indica que se debe crear el semáforo si no existe. Ambas banderas se pueden utilizar juntas para abrir o crear un semáforo en modo de lectura y escritura.

> `O_RDWR` abre un semáforo existente, y solo funciona si el samaforo ya ha sido creado. En cambio `O_CREAT` en el caso de que el semáforo no exista lo crea

Es importante tener en cuenta que la bandera `O_RDWR` no tiene ningún efecto si se utiliza sin la bandera `O_CREAT`, ya que el semáforo ya debe existir para poder abrirlo en modo de lectura y escritura. Por otro lado, la bandera `O_CREAT` sí puede utilizarse sin la bandera `O_RDWR`, en cuyo caso se creará el semáforo con permisos de lectura y escritura por defecto

Si un semáforo se abre con permisos de escritura, se podran aplicar las funciones sem\_wait y sem\_post sobre el. En cambio si solo tiene  permisos de lectura no se podra utilizar estas funciones y solo se podra ver su valor mediante sem\_getvalue.

En el caso de que tenga ambos permisos se podrán utilizar todas las funciones, como en el siguiente ejemplo:

```c
sem_t *sem = sem_open("/mysem", O_RDWR);
if (sem == SEM_FAILED) {
  // Error al abrir el semáforo
  return -1;
}

int value;
sem_getvalue(sem, &value);
printf("El valor actual del semáforo es %d\n", value);

sem_post(sem);
printf("Se ha incrementado el valor del semáforo\n");
```

#### mode

El tercer parámetro de la función `sem_open` es el parámetro `mode`, que especifica los permisos del semáforo. Este parámetro se utiliza solamente cuando se utiliza la bandera `O_CREAT` para crear un semáforo nuevo.

El parámetro "mode" es un valor entero que especifica los permisos de lectura, escritura y ejecución para el semáforo. El valor del parámetro "mode" se establece utilizando los [octales](../../linux/other-commands/chmod.md#agregar-y-quitar-permisos-con-el-metodo-octal) `rwx` para representar los permisos de lectura, escritura y ejecución, respectivamente. Los permisos se pueden establecer para el usuario dueño del semáforo, el grupo del usuario dueño y para el resto de usuarios.

Por ejemplo, el valor `0666` indica que el semáforo se debe crear con permisos de lectura y escritura para todos los usuarios. El valor `0600` indica que el semáforo se debe crear con permisos de lectura y escritura solamente para el usuario dueño.

#### value

El cuarto parámetro de la función `sem_open` es el parámetro "value", que especifica el valor inicial del semáforo. Este parámetro se utiliza solamente cuando se utiliza la bandera `O_CREAT` para crear un semáforo nuevo.

El parámetro "value" es un valor entero que especifica el valor inicial del semáforo. Este valor se utiliza para inicializar el semáforo cuando se crea por primera vez. El valor del parámetro "value" puede ser cualquier entero entero mayor o igual a 0.

Por ejemplo, el valor "1" indica que el semáforo se debe crear con un valor inicial de "1", lo que significa que se puede utilizar de inmediato para sincronizar un proceso o hilo. El valor "0" indica que el semáforo se debe crear con un valor inicial de "0", lo que significa que se debe bloquear un proceso o hilo hasta que el valor del semáforo sea incrementado por otro proceso o hilo.

#### Ejemplo

```c
sem_t *sem = sem_open("/mysem", O_CREAT | O_EXCL, 0666, 1);
if (sem == SEM_FAILED) {
  // Error al crear el semáforo
  return -1;
}
```

En el ejemplo anterior, se utiliza la bandera `O_CREAT` para indicar que el semáforo debe ser creado si no existe. También se especifica el parámetro "mode" con el valor "0666", que indica que el semáforo se debe crear con permisos de lectura y escritura para todos los usuarios. Si el semáforo ya existe, la llamada a `sem_open` **devolverá un puntero al semáforo** y no creará uno nuevo.

Como podeis ver, se pueden utilizar mas de una flag y en este caso tambien utilizamos la flag \
`O_EXCL`, para que en caso de que el semáforo ya exista el función `sem_open` nos devuelva un error.

### sem\_wait

La función `sem_wait` en C es una función de la biblioteca de semáforos de POSIX que se utiliza para bloquear a un proceso o hilo hasta que el valor de un semáforo sea mayor o igual que uno. La función tiene la siguiente forma:

```c
int sem_wait(sem_t *sem);
```

La función `sem_wait` toma como parámetro un apuntador a la estructura `sem_t` que representa el semáforo sobre el que se desea esperar. La función devuelve 0 en caso de éxito y -1 en caso de error, estableciendo el valor de la variable global `errno` con el código de error correspondiente.

La función `sem_wait` se utiliza para bloquear a un proceso o hilo hasta que el valor del semáforo sea mayor o igual que uno. Si el valor del semáforo es mayor o igual que uno antes de llamar a `sem_wait`, la función decrementará el valor del semáforo en una unidad y permitirá que el proceso o hilo continúe su ejecución. Si el valor del semáforo es menor que uno antes de llamar a `sem_wait`, la función bloqueará al proceso o hilo y lo pondrá en espera hasta que el valor del semáforo sea incrementado por otro proceso o hilo mediante una llamada a `sem_post`.

Ejemplo de código que utiliza la función `sem_wait` para bloquear a un proceso o hilo hasta que el valor del semáforo sea incrementado por otro proceso o hilo:

```c
sem_t *sem = sem_open("/mysem", O_CREAT, 0666, 0);
if (sem == SEM_FAILED) {
  // Error al crear el semáforo
  return -1;
}

// Bloquear al proceso o hilo hasta que el valor del semáforo sea incrementado
if (sem_wait(sem) == -1) {
  // Error al esperar en el semáforo
  return -1;
}
```

En el ejemplo anterior, se abre o crea un semáforo con un valor inicial de 0 utilizando la función `sem_open`. Luego, se llama a la función `sem_wait` para bloquear al proceso o hilo hasta que el valor del semáforo sea incrementado por otro proceso o hilo mediante una llamada a `sem_post`.&#x20;

Si el valor del semáforo es 0 antes de llamar a `sem_wait`, la función bloqueará al proceso o hilo y lo pondrá en espera hasta que otro proceso o hilo incremente el valor del semáforo mediante una llamada a `sem_post`. Una vez que el valor del semáforo es mayor o igual que uno, la función `sem_wait` decrementará el valor del semáforo en una unidad y permitirá que el proceso o hilo que había sido bloqueado continúe su ejecución.

### sem\_post

La función `sem_post` en C es una función de la biblioteca de semáforos de POSIX que se utiliza para incrementar el valor de un semáforo en una unidad. La función tiene la siguiente firma:

```c
int sem_post(sem_t *sem);
```

La función `sem_post` toma como parámetro un apuntador a la estructura `sem_t` que representa el semáforo al que se le desea incrementar el valor. La función devuelve 0 en caso de éxito y -1 en caso de error, estableciendo el valor de la variable global `errno` con el código de error correspondiente.

La función `sem_post` se utiliza para incrementar el valor del semáforo en una unidad. Si el valor del semáforo es 0 antes de llamar a `sem_post`, la función desbloqueará a un proceso o hilo que esté esperando en la llamada a `sem_wait` sobre el semáforo. Si el valor del semáforo es mayor que 0 antes de llamar a `sem_post`, la función simplemente incrementará el valor del semáforo en una unidad.

Ejemplo de código que utiliza la función `sem_post` para incrementar el valor de un semáforo y desbloquear a un proceso o hilo que esté esperando en una llamada a `sem_wait`:

```c
sem_t *sem = sem_open("/mysem", O_CREAT, 0666, 0);
if (sem == SEM_FAILED) {
  // Error al crear el semáforo
  return -1;
}

// Incrementar el valor del semáforo en una unidad
if (sem_post(sem) == -1) {
  // Error al incrementar el semáforo
  return -1;
}
```

En el ejemplo anterior, se abre o crea un semáforo con un valor inicial de 0 utilizando la función `sem_open`. Luego, se llama a la función `sem_post` para incrementar el valor del semáforo en una unidad. Si hay un proceso o hilo que esté esperando en una llamada a `sem_wait`.

### Ejemplo

```c
#include <stdio.h>
#include <stdlib.h>
#include <semaphore.h>
#include <unistd.h>
#include <sys/wait.h>

int main(void)
{
  // Abrir o crear un semáforo con un valor inicial de 1
  sem_t *sem = sem_open("/mysem", O_CREAT, 0666, 1);
  if (sem == SEM_FAILED) {
    perror("Error al crear el semáforo");
    return 1;
  }

  pid_t pid = fork();
  if (pid == -1) {
    perror("Error al crear el proceso hijo");
    return 1;
  }

  if (pid == 0) {
    // Proceso hijo
    printf("Hijo esperando en el semáforo\n");
    if (sem_wait(sem) == -1) {
      perror("Error al esperar en el semáforo");
      return 1;
    }
    printf("Hijo obtiene el semáforo\n");
    printf("Hijo accediendo al recurso compartido\n");
    sleep(1);
    printf("Hijo liberando el semáforo\n");
    if (sem_post(sem) == -1) {
      perror("Error al liberar el semáforo");
      return 1;
    }
  } else {
    // Proceso padre
    printf("Padre obtiene el semáforo\n");
    printf("Padre accediendo al recurso compartido\n");
    sleep(1);
    printf("Padre liberando el semáforo\n");
    if (sem_post(sem) == -1) {
      perror("Error al liberar el semáforo");
      return 1;
    }
    int status;
    waitpid(pid, &status, 0);
  }

  // Cerrar y eliminar el semáforo
  if (sem_close(sem) == -1) {
    perror("Error al cerrar el semáforo");
    return 1;
  }
  if (sem_unlink("/mysem") == -1) {
    perror("Error al eliminar el semáfor");
    return (1);
  }
  
  return (0);
}
```

En resumen, el código crea o abre un semáforo con un valor inicial de 1 mediante la función `sem_open`. Luego, crea un proceso hijo mediante la función `fork`. En el proceso hijo, se llama a la función `sem_wait` para bloquear al proceso hijo hasta que el valor del semáforo sea mayor o igual que uno. Mientras tanto, en el proceso padre, se obtiene el semáforo sin tener que esperar debido a que el valor del semáforo es inicialmente mayor o igual que uno.

Cuando el proceso hijo finalmente obtiene el semáforo, ambos procesos acceden al recurso compartido y luego liberan el semáforo mediante una llamada a `sem_post`. Gracias al uso del semáforo, se garantiza que el acceso al recurso compartido se realiza de manera sincronizada y que sólo un proceso puede acceder al recurso a la vez.
