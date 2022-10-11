# Listas Enlazadas

Las estrcuturas de datos son las distintas estructuras que utilizamos para representar la informacion en un ordenador, como una biblioteca. Un ejemplo de esto son los **arrays**, pero existen otro tipos de estructuras para guarda **informacion mas compleja.**

### **Listas enlazadas**

Las listas enlazadas permite representar un grupo de elementos presentados como una secuencia. Estas son colecciones de estructuras autorreferenciadas llamadas nodos. Con ellas podemos guardar y modificar datos en tiempo de ejecución y o es necesario definir cuantos espacios a a tener nuestra lista.

> &#x20;un **nodo** es un una estructura que se crea con memoria dinamica

En otras palabras, es una estuctura que contiene un miembro apuntador (**puntero**) el cual apunta a una estructura del mismo tipo.&#x20;

<figure><img src="../../.gitbook/assets/Screen Shot 2022-09-10 at 9.45.05 PM (1).png" alt=""><figcaption></figcaption></figure>

> Es un conjunto de nodos apuntados entre si

Las lista constan de dos partas, la cabeza, que es el primer elmento de la lista y la cola,  que son los nodos restantes. Ademas cada elemento de la cola es la cabeza de una lista.

El ultimo nodo de la lista apunta a una lista vacia, un valor NULL&#x20;

### Estructuras de la listas

La listas son estructuras que estan compuestas, por norma general, de una estructura con la **informacion** que deseamos guardar y otra variable que es un **puntero a otra estructura** del mismo tipo que nuestra lista (puntero al siguiente nodo). Para que quede mas aqui tines el siguiente ejemplo:

```
strcut Libro{
    char *titulo;
    char *escritor;
    char *fechaa_publicacion;
    
}

struct Lista{
    struct Libro libro;
    sruct Lista *sig;
}
```

Esta es la forma que normalmente se usa para guardar listas en lenguajes funcionales como por ejemplo list o haskell, pero existe una forma muchos mas simple de gaurdar elementos en una lista que es utilizando dos estruturas.&#x20;

Por un lado, una estructura llamada **nodo** que se compone de un elemento y un elemento siguiente; y una **lista** (estrutura) que lo unico que contiene es un puntero al primer nodo. Lo bueno de la lsita es que podemso introducirle mas metadoatos, como puede ser la longitud de esta.&#x20;

<pre><code><strong>typedef struct nodo{
</strong>    struct Libro libro;
    sruct nodo *sig;
} Nodo;

struct Lista{
    *nodo cabeza;
} Lista;</code></pre>

### Ventajas de una lista frente a un array

* Los nodos no tienen por que guardarse toso juntos en memoria, como ocurre con los arrays
* Pueden tener longitud variable
* Podemos agregar y quitar elementos en timepo de ejecucion

### Desventajas de una lista frente a un array

* Las listas no tienen nocion de indice, por lo que no podemos hacer accesos aleatorios
* Necesitan mas espacio en memoria ya ue tienes que aalmacenar punteros

### Crear y Eliminar nodos

Crear nuevo nodo a partir de datos deseados:

```
Nodo *crear_nodo(Libro *libro)
{
    Nodo *nodo = (Nodo *)malloc(sizeof(Nodo));
    strncpy(nodo->libro.titulo, libro->titulo, 50);
    strncpy(nodo->libro.autor, libro->autor, 50);
    strncpy(nodo->libro.isbn, libro->isbn, 13);
    nodo->siguiente = NULL;
    return nodo;
}
```

Mediante esta funcion generamos un nuevo nodo tipo "Nodo" mediante malloc y le asignamos los valores introducidos. Utilizamos las "->" para acceder a lso valores de las estructura nodo ("libro" o "sigiuente") y el " . " para acceder a los datos de la estructura de libro.

Para eliminar los datos es necesaria la utilizacion de free, para que no qqueden datos sueltos:

```
void eliminar_nodo(Nodo *nodo)
{
    free(nodo);
}
```

### Insertar nodos

Para **insertar un nodo al principio** de la lista  lo que hay que hacer es crea un nuevo nodo y al siguiente de este enlazarle lo que era antes la cabeza. En el caso de que tengas una lista que haga referencia a la cabeza asignarle a esta el nuevo nodo.

```
void insertar_al_principio(Lista *lista, Libro *libro)
{
    Nodo *nodo = crear_nodo(libro);
    nodo->sigueinte = lista->cabeza;
    lista->cabeza = nodo;
}
```

Para **insertar un nodo al final**, es necesario primero recorrer la lista y una vez este al final (puntero->siguiente == NULL) a este valor nulo hay que asignarle el nodo que que queramos poner al final. Para **recorrer la lista** es necesario hacerlo con un **puntero auxiliar** (puntero), para no perder los datos que se quedan atras.

En el caso de que de que la lista este vacia hay que asignar a la cabeza de esta el nuevo nodo.

```
void insertar_final(Lista *lista, Libro *libro)
{
    Nodo *nodo = crear_nodo(libro);
    if (lista->cabeza == NULL)
        lista->cabeza = nodo;
    else
    {
        Nodo *puntero = lista->cabeza;
        while (puntero->siguiente)
            puntero = puntero->siguiente;
        puntero->siguiente = nodo;
    }
}
```

Para **insertar un nodo depues de la posicion n**, hay que recorrer la lista mediante un puntero hasta llegar a la posicion deseada o al final de la lista. Una vez estemos en la posicion deseada apuntaremos el "sigueinte" del nuevo puntero al siguiente del del nodo en la posicion n. Por ulltimo haremos que el nodo n apunte al nuevo nodo.

<figure><img src="../../.gitbook/assets/Screen Shot 2022-10-10 at 6.39.27 PM.png" alt=""><figcaption></figcaption></figure>

Por ejemplo si queremos insertar un nuevo nodo depues de la posicion 19, recorreremos la lista hasta llegar a esta posicion. Una vez hecho, apuntaremos el nuevo nodo hacia el nodo "39" y el "19" al nuevo nodo "72", insertandolo asi entre medias.

```
void insertar_despues(int n, Lista *lista, Libro *libro)
{
    Nodo *nodo = crear_nodo(libro);
    if (lista->cabeza == NULL)
        lista->cabeza = nodo;
    else
    {
        Nodo *puntero = lista->cabeza;
        int posicion = 0;
        while (posicion++ < n && puntero->siguiente)
            puntero = puntero->siguiente;
        nodo->siguiente = puntero->sigueinte; //Apunta "72" a "39"
        puntero->sigueinte = nodo;            //Apunta "19" a "72"
    }
```

### Obtener Datos

Para **obtener los datos de un nodo n** es necesario recorrer la lista hasta esta posicion deseada o el final de la lista. Una vez estemos en el nodo adecuado habra que devovler la direcccion aa la informacion solicitada. En el caso de que la lista este vacia habra que devolver un valor nulo.

```
Libro *obtener_datos(int n, Lista *lista)
{
    if (lsitaa->cabeza == NULL)
        return (NULL);
    else
    {
        Nodo *puntero = lista->cabeza;
        int posicion = 0;
        while(posicion++ < n && puntero->siguiente)
            puntero = puntero->sigueinte;
        if (poiscion != n)
            return (NULL);
        else
            return (&puntero->libro);
    }
}
```

### Eliminar nodos

Para **eliminar el primer nodo de una lista** tan solo hay que acceder a este a traves de la estructura lista, que es la que almacena el primer elemento y eliminarlo mediante `eliminar_nodo`. Una vez eliminado habra que actualizar la cabeza de la lista para que apunte al siguiente elemento. Para no perder el siguiente nodo al primero, este habra que guardarlo en un auxiliar antes de eliminar la cabeza.

```
void eliminar_principio(Lista *lista)
{
    Nodo *eliminado = lista->cabeza;
    lista->cabeza = lista->cabeza->sigueinte;
    eliminar_nodo(eliminado);
}
```

Para **eliminar el ultimo nodo de una lista** hay que recorrer la lista hasta llegar al anteultimo nodo de esta, ya que lo que tenemos que eliminar es el puntero del ultimo nodo. En caso de que recorrieramos la lista hasta llegar al final, no podriamos eliminar este nodo, ya que `puntero-> siguiente` seria NULL. Por ello recorreremos la lsita mientras puntero->siguiente->siguiente.

Una vez estemos sobre el anteúltimo nodo, su `puntero->siguiente` lo asignaremos a NULL, ya que este ahora sera el ultimo nodo. Esos si, antes de esto, habra que guardar el ultimo nodo `puntero->siguiente->siguiente` en una variable auxiliar para su posterior eliminacion mediante `destruir_nodo`.&#x20;

```
void eliminar_ultimo(Lista *lista)
{
        if (lista->cabeza)
        {
        if (lista->cabeza
        Nodo *puntero = lista->cabeza;
        while (puntero->siguiente->siguiente)
                puntero = puntero->siguiente;
                Nodo *eliminado = puntero->siguiente;
            puntero->siguiente = NULL;
            destruir_nodo(eliminado)
        }
}
```

Para **eliminar un elemento n**, al igual que para eliminar el ultimo elemento, tenemnos que recorrer las lista hasta llegar al nodo (n - 1). Para asegurar que estamos en esa posicion y que no se ha acabado la lista antes de tiempo, hay que usar un contador. Una vez situado el el nodo indicado guardaremos el nodo n en una auxiliar para su poesteriro eliminacion y apuntaremos el nodo (n - 1) al nodo (n + 1).

<figure><img src="../../.gitbook/assets/Screen Shot 2022-10-11 at 2.52.45 PM.png" alt=""><figcaption></figcaption></figure>

En caso de que nos pida eliminar el primer elemento habra que hacer lo mismo que hacemos en la funcion `eliminar_principio`, para eliminar la cabeza de la lista.

```
void eliminar_elemento_n(int n, Lista *lista)
{
    if (lista->cabeza)
    {
        if (n == 0)
        {
            Nodo *eliminado = lista->cabeza;
            lista->cabeza = lista->cabeza->sigueinte;
            eliminar_nodo(eliminado);
        }
        else
        {
            Nodo *puntero = lista->cabeza;
            int posicion = 0;
            while (posicion++ < (n - 1) && puntero->siguiente->siguiente)
                puntero = puntero->siguiente;
            if (posicion == n -1)
            {
                Nodo *eliminado = puntero->siguiente;
                puntero->siguiente = eliminado->siguiente;
                destruir_nodo(eliminado);
            }
        }
    }
}
```

### Bibliografia

* [https://www.youtube.com/watch?v=oQ0WkIdr73E\&list=PLTd5ehIj0goMTSK7RRAPBF4wP-Nj5DRvT\&index=2](https://www.youtube.com/watch?v=oQ0WkIdr73E\&list=PLTd5ehIj0goMTSK7RRAPBF4wP-Nj5DRvT\&index=2)
* [https://es.stackoverflow.com/questions/46015/para-qu%C3%A9-se-usa-en-c-y-c-al-manejar-estructuras-de-datos](https://es.stackoverflow.com/questions/46015/para-qu%C3%A9-se-usa-en-c-y-c-al-manejar-estructuras-de-datos)

