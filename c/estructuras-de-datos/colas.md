# Colas

Una cola es una estructura de datos, caracterizada por ser una secuencia de elementos en la que la operación de inserción _push_ se realiza por un extremo y la operación de extracción _pop_ por el otro. También se le llama estructura [FIFO](https://www.ecured.cu/index.php?title=FIFO\&action=edit\&redlink=1) (del inglés First In First Out), debido a que el primer elemento en entrar será también el primero en salir.

Las colas de estructuras de datos son como las de la vida real, los datos se incoirpaoran al final de estas y van avanzando poco a poco hasta llegar a la cabeza de la cola.

### Estructuras de las colas

Estas son estructuras que se componen de dos elementos, la **cabeza**, que es un puntero al primer elemento; y el **final**, que es un puntero al ultimo nodo de la cola. El tener un puntero al final de la cola hace que no haya que recorrer todo el rato la lista cuando queramos agregar un elemento.

```
typedef strcut Cola
{
    nodo_pedido *primero;
    nodo_pedido *ultimo;
}
```

<figure><img src="https://miro.medium.com/max/732/1*2jbpFradIkDF9677ws3sVA.png" alt=""><figcaption></figcaption></figure>

### Propiedades

* Una colas se puede componer a partir de una lista enlazada
* Unimos nodos desde el principio hasta el final por medio de punteros
* Solo que las operaciones son esencialmente distintas

### Encolar

Encolar significa introducir un nodo en la cola y este se introducen en la cola por el final. Como las colas son parecidas a la listas para agregar nodos podemos reutilizar la funcion de las listas enlazadas [`"insertar_final"`](listas-enlazadas.md#insertar-nodos).&#x20;

### Procesar (Consultar)

Consultar significa obtener el siguiente elemento de la cola. Por ejemplo cuando tenemso una cola de pagos, procesar el pago que tenemos ahora msimo en la cabeza de la cola, que seria el siguiente, que sera el que esta en la cabeza de la cola. Es decir que para procesar el valor de una cola tan solo hay que consultar el nodo que esta en la cabeza de la cola.

Eliminar elementos

Una vez procesado el elemento el elemento procesado hay que eliminarlo. Es decir eliminar la cabeza de la lista. Para esto podemos aprovechar la funcion utilizada al menajar estructuras de datos "eliminar\_principio".

### Despachar

Extraer el pimer elemento de la cola, eliminarlo y devolver para que se procese.
