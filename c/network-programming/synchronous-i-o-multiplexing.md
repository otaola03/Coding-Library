# Synchronous I/O Multiplexing



### poll()

La función `poll()` en C/C++ es una alternativa a `select()` y `epoll()` que se utiliza para monitorear múltiples descriptores de archivos, como sockets, para determinar si hay eventos esperando ser procesados. A diferencia de `select()`, `poll()` no tiene limitaciones en el número máximo de descriptores que puede manejar.

El plan general es mantener un array de estructuras `pollfd` con información sobre qué descriptores de socket queremos monitorear y qué tipo de eventos queremos observar. El sistema operativo se bloqueará en la llamada a `poll()` hasta que ocurra uno de esos eventos (por ejemplo, '¡socket listo para leer!') o hasta que ocurra un tiempo de espera especificado por el usuario.

**Sintaxis**

```cpp
#include <poll.h>

int poll(struct pollfd fds[], nfds_t nfds, int timeout);
```

* `fds[]`: Un arreglo de estructuras `pollfd` que especifican los descriptores que se deben monitorear y los eventos de interés.
* `nfds`: El número total de elementos en el arreglo `fds[]`.
* `timeout`: El tiempo máximo en milisegundos que `poll()` esperará por eventos. Un valor de `-1` indica que `poll()` esperará indefinidamente hasta que ocurra un evento.

La función `poll()` devuelve el número de descriptores de sockets que tienen eventos pendientes (listos para lectura, escritura, o errores) o 0 si ha expirado el tiempo de espera especificado. Si ocurre un error, devuelve -1 y establece `errno` para indicar el tipo de error.

#### struct pollfd

Esta es la estrucutra `pollfd`:

```cpp
struct pollfd {
    int fd;         // the socket descriptor
    short events;   // bitmap of events we're interested in
    short revents;  // when poll() returns, bitmap of events that occurred
};
```

* `fd`: Es el descriptor de archivo (por ejemplo, un socket) que se va a monitorear.
* `events`: Especifica los eventos que se deben monitorear en el descriptor `fd`. Puedes configurar varios eventos utilizando constantes como `POLLIN` para lectura, `POLLOUT` para escritura, etc. Puedes combinar múltiples eventos usando el operador OR bitwise (`|`).
* `revents`: Después de llamar a `poll()`, esta variable indica los eventos que han ocurrido en el descriptor `fd`. La función `poll()` llena este campo con los eventos que realmente han sucedido.

Así que vamos a tener un array de esas estructuras y estableceremos el campo `fd` para cada elemento a un descriptor de socket que nos interesa monitorear. Luego, configuraremos el campo `events` para indicar el tipo de eventos que nos interesan.

El campo `events` se puede rellenar con una de las siguientes macros:

| Macro     | Description                                                        |
| --------- | ------------------------------------------------------------------ |
| `POLLIN`  | Alert me when data is ready to `recv()` on this socket.            |
| `POLLOUT` | Alert me when I can `send()` data to this socket without blocking. |



### select()

La función `select()` en C/C++ se utiliza para monitorear múltiples descriptores de archivo (como sockets) y determinar cuáles de ellos están listos para lectura, escritura o si hay errores pendientes. Esta función es útil cuando necesitas manejar múltiples conexiones simultáneamente, como en servidores de chat o aplicaciones de red.

#### Sintaxis

```cpp
#include <sys/time.h>
#include <sys/types.h>
#include <unistd.h>

int select(int numfds, fd_set *readfds, fd_set *writefds,
           fd_set *exceptfds, struct timeval *timeout);
```

* `numfds`: El número máximo de descriptores de archivo en cualquier conjunto más uno.
* `readfds`, `writefds`, `exceptfds`: Conjuntos de descriptores de archivo para monitorear lectura, escritura y excepciones respectivamente.
* `timeout`: Estructura `struct timeval` que especifica el tiempo máximo que `select()` debe esperar por eventos. Si `timeout` es `NULL`, `select()` espera indefinidamente hasta que ocurra un evento.

La función `select()` devuelve el número total de descriptores de archivo en los conjuntos `readfds`, `writefds` y `exceptfds` que están listos para lectura, escritura o que tienen excepciones pendientes.

{% hint style="info" %}
A la hora de llamar a select es recomendable hacerlo con una copia del elemento `fd_set` que queiras oberservar, ya que reescribira este elemento guardando unicamente los `fd`s que estan disponibles para ser utilizados.
{% endhint %}

Si ocurre un error, `select()` devuelve -1 y establece `errno` para indicar el tipo de error. Si se agota el tiempo especificado en `timeout` sin que ocurran eventos en los descriptores de archivo, `select()` devuelve 0.

#### fd\_set

Los conjuntos de descriptores de archivo (`fd_set`) son conjuntos de bits, donde cada bit representa un descriptor de archivo. `fd_set` se utiliza para decirle a las funciones de monitoreo (como `select()` o `poll()`) qué descriptores de archivo deben ser monitoreados para eventos de lectura, escritura o excepciones.

Maramanipular estos `fd_set`s se utilizan las siguientes macros:

| Function                         | Description                              |
| -------------------------------- | ---------------------------------------- |
| `FD_SET(int fd, fd_set *set);`   | Añadir `fd` al `set`.                    |
| `FD_CLR(int fd, fd_set *set);`   | Eliminar `fd` del `set`.                 |
| `FD_ISSET(int fd, fd_set *set);` | Devuelve true si `fd` estan en el `set`. |
| `FD_ZERO(fd_set *set);`          | Elimina todos los elementos del `set`.   |

