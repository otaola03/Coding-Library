# Structs

### struct addrinfo

`addrinfo` es una estructura utilizada en programación de sockets para almacenar información sobre direcciones de red y servidores. Esta estructura es útil cuando estás escribiendo código que necesita configurar sockets de red, como crear un servidor o un cliente, y deseas almacenar toda la información relevante en un solo lugar.

```c
struct addrinfo {
    int              ai_flags;      // Opciones para la búsqueda
    int              ai_family;     // Familia de direcciones (IPv4 o IPv6 o AF_UNSPEC)
    int              ai_socktype;   // Tipo de socket (SOCK_STREAM o SOCK_DGRAM)
    int              ai_protocol;   // Protocolo utilizado (e.g., IPPROTO_TCP)
    size_t        ai_addrlen;    // Longitud de la dirección
    struct sockaddr *ai_addr;       // Puntero a la dirección
    char            *ai_canonname;  // Nombre canónico del host
    struct addrinfo *ai_next;       // Puntero al siguiente nodo en la lista
};
```

* **`ai_flags`**: Se utiliza para especificar opciones adicionales durante la resolución de direcciones mediante `getaddrinfo`.
  * `AI_PASSIVE`: Para usar con servidores, indica que la dirección IP del host local debe asignarse a las estructuras de socket.&#x20;
  * `AI_CANONNAME`: Para obtener el nombre canónico del host.&#x20;
  * `AI_NUMERICHOST`: Para evitar la resolución de nombres de dominio, si ya se tiene una dirección IP numérica.&#x20;
  * `AI_NUMERICSERV`: Similar a AI\_NUMERICHOST, pero para el número de puerto
* **`ai_family`**: Especifica la familia de direcciones, como `AF_INET` para IPv4 o `AF_INET6` para IPv6.
  * `AF_UNSPEC`: No especifica IPv4 o IPv6, permitiendo cualquiera.
  * `AF_INET`: Para IPv4.
  * `AF_INET6`: Para IPv6.
* **`ai_socktype`**: Especifica el tipo de socket, como `SOCK_STREAM` para sockets TCP o `SOCK_DGRAM` para sockets UDP.
  * `SOCK_STREAM`: Para sockets de flujo (TCP).
  * `SOCK_DGRAM`: Para sockets de datagramas (UDP).
* **`ai_protocol`**: Especifica el protocolo a utilizar, como `IPPROTO_TCP` para TCP o `IPPROTO_UDP` para UDP.
  * `IPPROTO_TCP`: Para el protocolo TCP.
  * `IPPROTO_UDP`: Para el protocolo UDP.
* **`ai_addr`**: Un puntero a una estructura `sockaddr` que contiene la información de dirección.
* **`ai_addrlen`**: La longitud de la estructura `sockaddr`.
* **`ai_canonname`**: Un nombre canónico asociado con la dirección.
* **`ai_next`**: Un puntero al siguiente elemento en la lista enlazada de `addrinfo`. Esto es útil cuando `getaddrinfo()` devuelve múltiples resultados.

Es posible que no necesites escribir en estas estructuras con frecuencia; en muchos casos, una llamada a `getaddrinfo()` para completar tu `struct addrinfo` será todo lo que necesites. Sin embargo, antes de realizar la llamada a `getaddrinfo()` es recomendable vaciar completamente la estructura mediante `memset()`.

```cpp
struct addrinfo hints;
memset(&hints, 0, sizeof hints);
getaddrinfo(NULL, PORT, &hints, &servinfo)
```

<figure><img src="../../.gitbook/assets/Untitled (2).png" alt=""><figcaption></figcaption></figure>

### struct sockaddr

`struct sockaddr` es una estructura que actúa como un tipo de dato genérico para representar direcciones de red en la programación de sockets en C. Puede adaptarse tanto a direcciones IPv4 como a direcciones IPv6, lo que la hace versátil y esencial en el desarrollo de aplicaciones de red.

> La estructura `struct sockaddr` almacena información de dirección de socket para varios tipos de sockets.

```c
struct sockaddr {
    unsigned short sa_family; // Familia de direcciones, AF_xxx
    char sa_data[14];         // Almacena la dirección (y otros datos en algunos casos)
};
```

`sa_family` puede ser una variedad de cosas, pero en este documento será `AF_INET` (IPv4) o `AF_INET6` (IPv6) para todo lo que hacemos. `sa_data` contiene una dirección de destino y un número de puerto para el socket. Esto puede ser un tanto engorroso ya que no deseas empaquetar manualmente la dirección en `sa_data`.

#### struct sockaddr\_in (IPv4)

Para lidiar con `struct sockaddr`, los programadores crearon una estructura paralela: `struct sockaddr_in` ("in" de "Internet") para usar con IPv4.

Y aquí está la parte importante: un puntero a una `struct sockaddr_in` se puede convertir en un puntero a una `struct sockaddr` y viceversa. Entonces, incluso si `connect()` requiere un `struct sockaddr*`, todavía puedes usar una `struct sockaddr_in` y convertirla en el último momento.

<pre class="language-c"><code class="lang-c"><strong>// Solo IPv4
</strong><strong>struct sockaddr_in {
</strong>    short int          sin_family;  // familia de direcciones, AF_INET
    unsigned short int sin_port;    // número de puerto
    struct in_addr     sin_addr;    // dirección de Internet
    unsigned char      sin_zero[8]; // mismo tamaño que struct sockaddr
};
</code></pre>

Esta estructura facilita la referencia a los elementos de la dirección del socket. Ten en cuenta que `sin_zero` (que se incluye para rellenar la estructura al tamaño de una `struct sockaddr`) debe configurarse con todos los ceros utilizando la función `memset()`. Además, observa que `sin_family` corresponde a `sa_family` en una `struct sockaddr` y debe configurarse como 'AF\_INET'. Finalmente, el `sin_port` debe estar en Network Byte Order (utilizando `htons()`).

Observa que el campo `sin_addr` es una estructura `struct in_addr`. ¿Qué es eso? Bueno, sin dramatizar demasiado, es uno de los unions más impresionantes de todos los tiempos

```c
// (IPv4 only--see struct in6_addr for IPv6)

// Internet address (a structure for historical reasons)
struct in_addr {
    uint32_t s_addr; // that's a 32-bit int (4 bytes)
};
```

¡Vaya! Bueno, solía ser un union, pero parece que esos días han quedado atrás. Menos mal. Entonces, si has declarado 'ina' como del tipo `struct sockaddr_in`, entonces 'ina.sin\_addr.s\_addr' hace referencia a la dirección IP de 4 bytes (en Network Byte Order). Ten en cuenta que incluso si tu sistema aún utiliza el unión espantoso para `struct in_addr`, aún puedes hacer referencia a la dirección IP de 4 bytes de exactamente la misma manera que mencioné anteriormente (esto se debe a las definiciones con '#defines').

#### sockaddr\_in6 (IPv6)

`sockaddr_in6` es una estructura utilizada en programación de sockets para representar direcciones de red en el contexto de IPv6. A diferencia de la estructura `sockaddr_in`, que se utiliza para direcciones IPv4, `sockaddr_in6` está diseñada específicamente para IPv6.

```c
// (IPv6 only--see struct sockaddr_in and struct in_addr for IPv4)

struct sockaddr_in6 {
    u_int16_t       sin6_family;   // address family, AF_INET6
    u_int16_t       sin6_port;     // port number, Network Byte Order
    u_int32_t       sin6_flowinfo; // IPv6 flow information
    struct in6_addr sin6_addr;     // IPv6 address
    u_int32_t       sin6_scope_id; // Scope ID
};

struct in6_addr {
    unsigned char   s6_addr[16];   // IPv6 address
};
```

Observa que IPv6 tiene una dirección IPv6 y un número de puerto, al igual que IPv4 tiene una dirección IPv4 y un número de puerto.

#### struct sockaddr\_storage

`struct sockaddr_storage` está diseñada para ser lo suficientemente grande como para contener tanto estructuras IPv4 como IPv6. Verás, en algunas llamadas, a veces no sabes de antemano si se completará tu `struct sockaddr` con una dirección IPv4 o IPv6. Por lo tanto, pasas esta estructura paralela, muy similar a `struct sockaddr` pero más grande, y luego la conviertes al tipo que necesitas.

```c
struct sockaddr_storage {
    sa_family_t  ss_family;     // address family

    // all this is padding, implementation specific, ignore it:
    char      __ss_pad1[_SS_PAD1SIZE];
    int64_t   __ss_align;
    char      __ss_pad2[_SS_PAD2SIZE];
};
```

Lo importante es que puedes ver la familia de direcciones en el campo `ss_family`. Verifícalo para ver si es `AF_INET` o `AF_INET6` (para IPv4 o IPv6). Luego puedes convertirlo en `struct sockaddr_in` o `struct sockaddr_in6` si así lo deseas.
