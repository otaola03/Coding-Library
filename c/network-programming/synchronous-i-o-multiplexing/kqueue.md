# kqueue

**kqueue** es un mecanismo de notificación de eventos disponible en sistemas operativos tipo UNIX, como FreeBSD y macOS. Se utiliza para monitorear varios tipos de eventos en descriptores de archivos, como sockets, archivos regulares, pipes y más.

### **Eventos**

En kqueue, los **eventos** son notificaciones asincrónicas que indican cambios en los descriptores de archivos o en otros recursos del sistema operativo. Estos eventos son fundamentales para el desarrollo de aplicaciones eficientes y receptivas en sistemas tipo UNIX, como FreeBSD y macOS.

#### struct kevent

**`struct kevent`** es una estructura de datos esencial en la interfaz de programación de aplicaciones (API) de kqueue en sistemas tipo UNIX, como FreeBSD y macOS. Esta estructura se utiliza para especificar y recibir información sobre eventos que deben ser monitoreados o que han ocurrido en descriptores de archivos.

La estructura `kevent` tiene la siguiente definición:

```c
struct kevent {
    uintptr_t ident;  // Identificador del objeto (por ejemplo, descriptor de archivo o identificador de proceso)
    short     filter; // Tipo de evento a ser monitorizado (por ejemplo, EVFILT_READ para eventos de lectura)
    u_short   flags;  // Varios flags que modifican el comportamiento del evento
    u_int     fflags; // Flags específicos del filtro
    intptr_t  data;   // Datos asociados con el evento
    void      *udata; // Puntero a datos de usuario (puede ser NULL)
};
```

* **`ident`**: Especifica el identificador del objeto que se está monitoreando, como un descriptor de archivo o un identificador de proceso.
* **`filter`**: Indica el tipo de evento que se está monitoreando, como `EVFILT_READ` para eventos de lectura o `EVFILT_WRITE` para eventos de escritura.
* **`flags`**: Representa varios flags que modifican el comportamiento del evento. Algunos ejemplos de flags son:
  * **`EV_ADD`**: Agrega un evento al conjunto de eventos monitoreados.
  * **`EV_DELETE`**: Elimina un evento del conjunto de eventos monitoreados.
  * **`EV_ENABLE`**: Activa un evento previamente desactivado.
  * **`EV_DISABLE`**: Desactiva un evento sin eliminarlo del conjunto de eventos monitoreados.
* **`fflags`**: Contiene flags específicos del filtro. Por ejemplo, para eventos de archivo, puede contener `NOTE_DELETE` para eventos de eliminación de archivo.
* **`data`**: Almacena datos asociados con el evento, como el número de bytes disponibles para leer o escribir en un descriptor de archivo.
* **`udata`**: Es un puntero a datos de usuario asociados con el evento. Puede ser utilizado para almacenar información adicional sobre el evento.

#### Pares

Un kevent está identificado por un par `<ident, filter>.` El identificador puede ser un descriptor (archivo, socket, flujo), un ID de proceso o un número de señal, según lo que queremos monitorear. El filtro identifica el filtro del kernel utilizado para procesar el evento respectivo. Existen algunos filtros predefinidos del sistema, como `EVFILT_READ` o `EVFILT_WRITE`, que se activan cuando existen datos para una operación de lectura o cuando es posible una operación de escritura, respectivamente.

Por ejemplo, si queremos ser notificados cuando haya datos disponibles para leer en un socket, tenemos que especificar un kevent en la forma `<sockfd, EVFILT_READ>`, donde `sockfd` es el descriptor de archivo asociado con el socket. Si quisiéramos monitorear la actividad de un proceso, necesitaríamos una tupla `<pid, EVFILT_PROC>`. Ten en cuenta que **solo puede haber un kevent con el mismo `<ident, filter>` en nuestro kqueue**.

#### Filters

Después de haber diseñado un kevent, debemos decidir si queremos agregarlo a nuestro kqueue. Para este propósito, establecemos el miembro de los flags como EV\_ADD. También podríamos eliminar uno existente estableciendo EV\_DELETE o simplemente deshabilitarlo con EV\_DISABLE.

### kevent()

En sistemas UNIX como FreeBSD y macOS, `kqueue` proporciona una interfaz de eventos altamente eficiente. La función `kevent()` es fundamental para el monitoreo y manejo de eventos asincrónicos, permitiendo que las aplicaciones reaccionen a cambios en tiempo real en los descriptores de archivos, procesos y otros recursos del sistema.

#### Sintaxis de `kevent()`

La función `kevent()` tiene la siguiente sintaxis:

```c
int kevent(int kq, const struct kevent *changelist, int nchanges, struct kevent *eventlist, int nevents, const struct timespec *timeout);
```

* `kq`: Descriptor de kqueue en el cual se están monitoreando eventos.
* `changelist`: Lista de eventos que se están agregando, modificando o eliminando.
* `nchanges`: Número de eventos en la lista `changelist`.
* `eventlist`: Lista de eventos de retorno, donde se colocarán los eventos que han ocurrido.
* `nevents`: Número máximo de eventos que pueden ser colocados en `eventlist`.
* `timeout`: Período de tiempo durante el cual la función esperará eventos antes de regresar (`NULL` para esperar indefinidamente).

#### Agregar y Monitorear Eventos con `kevent()`

```c
int kq = kqueue();
int sockfd = socket(AF_INET, SOCK_STREAM, 0);

struct kevent event;
EV_SET(&event, sockfd, EVFILT_READ, EV_ADD, 0, 0, NULL);

if (kevent(kq, &event, 1, NULL, 0, NULL) == -1) {
    perror("Error al agregar evento de lectura al kqueue");
}
```

En este ejemplo, se crea un descriptor de kqueue (`kq`) y un socket (`sockfd`). Se configura un evento de lectura en el socket usando `EV_SET()` y luego se agrega al kqueue usando `kevent()`.

**Esperar Eventos con `kevent()`**

```c
struct kevent events[10];
int nevents;

while (1) {
    nevents = kevent(kq, NULL, 0, events, 10, NULL);
    if (nevents == -1) {
        perror("Error al esperar eventos en kqueue");
        break;
    }

    for (int i = 0; i < nevents; ++i) {
        if (events[i].filter == EVFILT_READ) {
            printf("Evento de lectura detectado en el descriptor %d\n", events[i].ident);
            // Realizar acciones basadas en el evento de lectura
        }
    }
}
```

En este bucle, `kevent()` espera eventos en el kqueue y los almacena en `events`. Luego, se procesan los eventos, en este caso, se imprime un mensaje cuando ocurre un evento de lectura en un descriptor de archivo.

