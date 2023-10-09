# Llamadas al sistema

### getaddrinfo()

La función `getaddrinfo` es una parte esencial del desarrollo de redes en C/C++. Permite a los programas resolver nombres de host y servicios, lo que significa que puede traducir un nombre de host (como www.ejemplo.com) a una dirección IP y viceversa. Esto es especialmente útil en situaciones en las que necesitas establecer una conexión de red y necesitas saber la dirección IP del host o el nombre del host a partir de una dirección IP.

Aun asi, su uso es bastante simple. Ayuda a configurar las estructuras que necesitará más adelante.

#### Sintaxis

```cpp
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>

int getaddrinfo(const char *node, const char *service,
                const struct addrinfo *hints, struct addrinfo **res);
```

* **`node`**: El nombre del host o la dirección IP que deseas resolver.
* **`service`**: El número del puerto o el nombre del servicio al que deseas conectarte.
* **`hints`**: Una estructura `addrinfo` que proporciona pistas sobre el tipo de conexión que estás buscando.
* **`res`**: Un puntero a un puntero de estructura `addrinfo` que se llenará con los resultados.

La función devuelve 0 si tiene éxito y un valor negativo si ocurre un error. El resultado de la función, es decir, la lista de estructuras `addrinfo`, se almacena en el puntero doble `res`. Es importante liberar esta memoria utilizando `freeaddrinfo()` una vez que ya no se necesite la lista de direcciones.

#### Uso basico

Aquí hay una llamada de ejemplo si usted es un servidor que desea escuchar en la dirección IP de su host, puerto 3490. Tenga en cuenta que esto en realidad no realiza ninguna escucha ni configuración de red; simplemente configura estructuras que usaremos más adelante:

```cpp
int status;
struct addrinfo hints;
struct addrinfo *servinfo;  // will point to the results

memset(&hints, 0, sizeof hints); // make sure the struct is empty
hints.ai_family = AF_UNSPEC;     // don't care IPv4 or IPv6
hints.ai_socktype = SOCK_STREAM; // TCP stream sockets
hints.ai_flags = AI_PASSIVE;     // fill in my IP for me

"

// servinfo now points to a linked list of 1 or more struct addrinfos

// ... do everything until you don't need servinfo anymore ....

freeaddrinfo(servinfo); // free the linked-list
```

`AI_PASSIVE` le dice a `getaddrinfo()` que asigne la dirección de mi host local a las estructuras de socket. Esto es conveniente porque así no tienes que codificarla directamente. (O puedes colocar una dirección específica como el primer parámetro de `getaddrinfo()` donde actualmente tengo NULL).

### socket()

La función `socket()` en C/C++ es una llamada al sistema que crea un nuevo socket, que es un punto de conexión de red utilizado para la comunicación entre diferentes máquinas o procesos en la misma máquina.

**Sintaxis**

```cpp
#include <sys/types.h>
#include <sys/socket.h>

int socket(int domain, int type, int protocol);
```

* **`domain`**: Especifica el dominio del socket. Puede ser `PF_INET` para IPv4, `PF_INET6` para IPv6 o `AF_UNIX` para comunicación local en el mismo sistema.
* **`type`**: Indica el tipo de socket, como `SOCK_STREAM` para TCP (orientado a conexión) o `SOCK_DGRAM` para UDP (sin conexión).
* **`protocol`**: Generalmente se establece en `0` para que el sistema seleccione el protocolo adecuado según el tipo de socket y el dominio.

La función devuelve un descriptor de socket si tiene éxito y -1 si ocurre un error.5

#### Uso basico

Lo que realmente quieres hacer es usar los valores de los resultados de la llamada a getaddrinfo() e introducirlos en socket() directamente de esta manera:

```cpp
int sockfd;
struct addrinfo hints, *res;

// do the lookup
// [pretend we already filled out the "hints" struct]
getaddrinfo("www.example.com", "http", &hints, &res);

// again, you should do error-checking on getaddrinfo(), and walk
// the "res" linked list looking for valid entries instead of just
// assuming the first one is good (like many of these examples do).
// See the section on client/server for real examples.
if ((sockfd = socket(p->ai_family, p->ai_socktype, p->ai_protocol)) == -1) {
    fprintf(stderr, "sockfd error: %s\n", gai_strerror(status));
    exit(1);
}

// resto of the code

close(serverSocket);
```

`socket()` simplemente le devuelve un descriptor de socket que puede usar en llamadas posteriores al sistema, o -1 en caso de error. La variable global `errno` se establece en el valor del error (consulte la página de manual de errno para obtener más detalles y una nota rápida sobre el uso de errno en programas multiproceso).

### bind()

La función `bind()` en C/C++ se utiliza para asociar un socket con una dirección IP y un número de puerto específicos en el sistema local. Esto es fundamental para los servidores que esperan conexiones entrantes en un puerto específico.

**Sintaxis**

```cpp
#include <sys/types.h>
#include <sys/socket.h>

int bind(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```

* **`sockfd`**: El descriptor de archivo del socket que se va a asociar.
* **`addr`**: Un puntero a una estructura `sockaddr` que contiene la dirección IP y el número de puerto.
* **`addrlen`**: La longitud de la estructura `sockaddr`.

La función `bind()` en C/C++ devuelve 0 en caso de éxito y -1 en caso de error.

#### Uso basico

Aqui tienes un ejemplo que vincula el socket al host en el que se ejecuta el programa, el puerto 3490:

```cpp
struct addrinfo hints, *res;
int sockfd;

// first, load up address structs with getaddrinfo():

memset(&hints, 0, sizeof hints);
hints.ai_family = AF_UNSPEC;  // use IPv4 or IPv6, whichever
hints.ai_socktype = SOCK_STREAM;
hints.ai_flags = AI_PASSIVE;     // fill in my IP for me

getaddrinfo(NULL, "3490", &hints, &res);

// make a socket:

sockfd = socket(res->ai_family, res->ai_socktype, res->ai_protocol);

// bind it to the port we passed in to getaddrinfo():
if (bind(sockfd, p->ai_addr, p->ai_addrlen) == -1) {
    close(sockfd);
    perror("server: bind");
    exit(1);
}
```

A veces, es posible que notes que intentas volver a ejecutar un servidor y `bind()` falla, indicando "Address already in use" (Dirección ya en uso). ¿Qué significa eso? Bueno, un pequeño fragmento de socket que estaba conectado todavía está presente en el kernel y está ocupando el puerto. Puedes esperar a que se libere (alrededor de un minuto) o agregar código a tu programa que le permita reutilizar el puerto, como se muestra a continuación:

```cpp
int yes = 1;
// Otra forma para personas que usan Solaris: char yes = '1';

// Elimina el molesto mensaje de error "Address already in use" (Dirección ya en uso)
if (setsockopt(listener, SOL_SOCKET, SO_REUSEADDR, &yes, sizeof yes) == -1) {
    perror("setsockopt");
    exit(1);
}
```

Un pequeño detalle adicional sobre `bind()`: hay momentos en los que no será absolutamente necesario llamarlo. Si te estás conectando (`connect()`) a una máquina remota y no te importa qué puerto local estás utilizando (como en el caso de `telnet` donde solo te importa el puerto remoto), puedes simplemente llamar a `connect()`. Esta función verificará si el socket no está vinculado (`bind()`) y lo vinculará a un puerto local no utilizado si es necesario.

### connect()

La función `connect()` en C/C++ se utiliza para establecer una conexión a un socket previamente creado y configurado. Esta función es comúnmente usada en clientes para conectarse a servidores.

**Sintaxis**

```cpp
int connect(int sockfd, const struct sockaddr *addr, socklen_t addrlen);
```

* **`sockfd`**: El descriptor de socket que se quiere conectar.
* **`addr`**: Un puntero a una estructura `sockaddr` que contiene la dirección del servidor al que se desea conectar.
* **`addrlen`**: El tamaño de la estructura `sockaddr`.

La función `connect()` devuelve un valor entero. En caso de éxito, devuelve `0`. Si falla, devuelve `-1` y establece la variable `errno` para indicar el tipo específico de error que ocurrió durante la conexión.

#### Uso basico

Tengamos un ejemplo en el que realizamos una conexión de socket a "www.example.com", puerto 3490:

```cpp
struct addrinfo hints, *res;
int sockfd;

// first, load up address structs with getaddrinfo():

memset(&hints, 0, sizeof hints);
hints.ai_family = AF_UNSPEC;
hints.ai_socktype = SOCK_STREAM;

getaddrinfo("www.example.com", "3490", &hints, &res);

// make a socket:

sockfd = socket(res->ai_family, res->ai_socktype, res->ai_protocol);

// connect!

if (connect(sockfd, res->ai_addr, res->ai_addrlen) == -1) {
    perror("Error al conectar con el servidor");
    close(sockfd);
    exit(-1);
}
```

### Listen()

La función `listen()` en C/C++ se utiliza en servidores para esperar conexiones entrantes de clientes. Después de crear un socket y conectarlo a una dirección, el servidor llama a `listen()` para comenzar a escuchar conexiones entrantes, que seran hacepatadas mediante `accept()`.

**Sintaxis**

```cpp
int listen(int sockfd, int backlog);
```

* `sockfd`: El descriptor de socket que se quiere escuchar.
* `backlog`: El número máximo de conexiones pendientes que el sistema permitirá en la cola de espera hasta que las `accept()`es

Nuevamente, como es habitual, `listen()` devuelve -1 y establece `errno` en caso de error. Devuelve 0 en caso de existo

#### Uso basico

Bien, como probablemente puedas imaginar, necesitamos llamar a `bind()` antes de llamar a `listen()` para que el servidor esté ejecutándose en un puerto específico. (¡Debes poder decirle a tus amigos a qué puerto conectarse!) Así que si vas a estar escuchando conexiones entrantes, la secuencia de llamadas al sistema que harás es:

```cpp
getaddrinfo();
socket();
bind();
listen();
/* accept() goes here */ 
```

\*Dejaré ese espacio como muestra de código, ya que es bastante autoexplicativo. (El código en la sección de accept(), a continuación, es más completo). La parte realmente complicada de todo este asunto es la llamada a `accept()`.llll

### accept()

La función `accept()` en C/C++ se utiliza para aceptar una conexión entrante en un socket previamente configurado. Es especialmente importante en el lado del servidor para manejar múltiples clientes.

Lo que va a pasar es esto: alguien muy, muy lejos intentará `connect()` a su máquina en un puerto en el que está `listen()`. Su conexión estará en cola esperando ser `accept()`. Llamas a `accept()` y le dices que obtenga la conexión pendiente.&#x20;

¡Le devolverá un nuevo file descriptor de archivo de socket para usar en esta única conexión! Así es, ¡de repente tienes dos descriptores de archivos de socket por el precio de uno! El original todavía está escuchando más conexiones nuevas y el recién creado finalmente está listo para `send()` y `recv()`.

**Sintaxis**

```cpp
int accept(int sockfd, struct sockaddr *addr, socklen_t *addrlen);
```

* `sockfd`: El descriptor de socket en el que se espera una conexión entrante.
* `addr`: Un puntero a una estructura `sockaddr` donde se almacenará la dirección del cliente.
* `addrlen`: Un puntero a un entero sin signo que indica el tamaño de la estructura `sockaddr`.

Nuevamente, como es habitual, `listen()` devuelve -1 y establece `errno` en caso de error. Devuelve 0 en caso de existo

#### Uso basico

Como antes, esto es un montón para absorber en una sola parte, así que aquí hay un fragmento de código de muestra para su lectura:

```cpp
#include <string.h>
#include <sys/types.h>
#include <sys/socket.h>
#include <netdb.h>

#define MYPORT "3490"  // the port users will be connecting to
#define BACKLOG 10     // how many pending connections queue will hold

int main(void)
{
    struct sockaddr_storage their_addr;
    socklen_t addr_size;
    struct addrinfo hints, *res;
    int sockfd, new_fd;

    // !! don't forget your error checking for these calls !!

    // first, load up address structs with getaddrinfo():

    memset(&hints, 0, sizeof hints);
    hints.ai_family = AF_UNSPEC;  // use IPv4 or IPv6, whichever
    hints.ai_socktype = SOCK_STREAM;
    hints.ai_flags = AI_PASSIVE;     // fill in my IP for me

    getaddrinfo(NULL, MYPORT, &hints, &res);

    // make a socket, bind it, and listen on it:

    sockfd = socket(res->ai_family, res->ai_socktype, res->ai_protocol);
    bind(sockfd, res->ai_addr, res->ai_addrlen);
    listen(sockfd, BACKLOG);

    // now accept an incoming connection:

    addr_size = sizeof their_addr;
    new_fd = accept(sockfd, (struct sockaddr *)&their_addr, &addr_size);

    // ready to communicate on socket descriptor new_fd!
```

Nuevamente, ten en cuenta que utilizaremos el descriptor de socket `new_fd` para todas las llamadas a `send()` y `recv()`. Si solo esperas una única conexión en todo momento, puedes cerrar el socket de escucha (`sockfd`) para evitar más conexiones entrantes en el mismo puerto, si así lo deseas.

### send() and recv()

Estas dos funciones son para comunicarse a través de sockets de flujo o sockets de datagramas conectados. Si deseas utilizar sockets de datagramas no conectados normales, deberás consultar la sección sobre `sendto()` y `recvfrom()`.

#### send()

La función `send()` en C/C++ se utiliza para enviar datos a través de un socket. Es comúnmente usada en aplicaciones de red para enviar información desde un cliente a un servidor o viceversa.

```cpp
size_t send(int sockfd, const void *buf, size_t len, int flags);
```

* `sockfd`: El descriptor de socket por el cual enviar los datos.
* `buf`: Puntero al búfer que contiene los datos a enviar.
* `len`: Tamaño de los datos a enviar, en bytes.
* `flags`: Opciones para el envío de datos.

`send()` devuelve el número de bytes realmente enviados! Esto podría ser menos que la cantidad que le indicaste que enviara. A veces le pides que envíe un montón de datos y simplemente no puede manejarlo. Enviará tanto de los datos como pueda y confiará en que enviarás el resto más tarde. Recuerda, si el valor devuelto por send() no coincide con el valor en len, depende de ti enviar el resto de la cadena.

En caso de error devuelve -1.

#### recv()

La función `recv()` en C/C++ se utiliza para recibir datos desde un socket. Es comúnmente usada en aplicaciones de red para recibir información desde un cliente o servidor. Esta función se utiliza en el lado del receptor para leer los datos enviados por el lado del remitente.

```cpp
size_t recv(int sockfd, void *buf, size_t len, int flags);
```

* `sockfd`: El descriptor de socket desde el cual recibir los datos.
* `buf`: Puntero al búfer donde se almacenarán los datos recibidos.
* `len`: Tamaño máximo de los datos que se pueden recibir, en bytes.
* `flags`: Opciones para la recepción de datos.

`recv()` devuelve el número de bytes realmente leídos en el búfer o -1 en caso de error (con errno establecido en consecuencia).

¡Espera! ¡`recv()` también puede devolver 0! Esto solo puede significar una cosa: ¡el lado remoto ha cerrado la conexión contigo! Un valor de retorno de 0 es la forma en que recv() te indica que esto ha ocurrido.

#### Uso basico

```cpp
char *msg = "Beej was here!";
int len, bytes_sent;
.
.
.
len = strlen(msg);
bytes_sent = send(sockfd, msg, len, 0);

```
