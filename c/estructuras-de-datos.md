---
description: Principales tipos
---

# Estructuras de datos

Las estrcuturas de datos son las distintas estructuras que utilizamos para representar la informacion en un ordenador, como una biblioteca. Un ejemplo de esto son los **arrays**, pero existen otro tipos de estructuras para guarda **informacion mas compleja.**

### **Listas enlazadas**

Las listas enlazadas permite representar un grupo de elementos presentados como una secuencia. Estas son colecciones de estructuras autorreferenciadas llamadas nodos. Con ellas podemos guardar y modificar datos en tiempo de ejecución y o es necesario definir cuantos espacios a a tener nuestra lista.

> &#x20;un **nodo** es un una estructura que se crea con memoria dinamica

En otras palabras, es una estuctura que contiene un miembro apuntador (**puntero**) el cual apunta a una estructura del mismo tipo.&#x20;

<figure><img src="../.gitbook/assets/Screen Shot 2022-09-10 at 9.45.05 PM (1).png" alt=""><figcaption></figcaption></figure>

> Es un conjunto de nodos apuntados entre si

Las lista constan de dos partas, la cabeza, que es el primer elmento de la lista y la cola,  que son lso nodos restantes. Ademas cada elemento de la cola es la cabeza de una lista.

El ultimo nodo de la lista apunta a una lista vacia, un valor NULL&#x20;

#### Estrcuturas de la listas

La listas son estrcuturas que estan compuesats, por norma general, de una estrcutra con la informacion que deseamos guardar y otra variable que es un puntero a otra estrucutra del mismo tipo que nuestra lista (puntero al siguiente nodo). Para que quede mas aqui tines el sigueinte ejemplo:

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

```
struct nodo{
    struct Libro libro;
    sruct nodo *sig;
}

struct Lista{
    *nodo cabeza;
}
```

#### Ventajas de una lista frente a un array

* Los nodos no tienen por que guardarse toso juntos en memoria, como ocurre con los arrays
* Pueden tener longitud variable
* Podemos agregar y quitar elementos en timepo de ejecucion

#### Deventajas de una lista frente a un array

* Las listas no tienen nocion de indice, por lo que no podemos hacer accesos aleatorios
* Necesitan mas espacio en memoria ya ue tienes que aalmacenar punteros

#### Crear nodos



### Bibliografia

* [https://www.youtube.com/watch?v=oQ0WkIdr73E\&list=PLTd5ehIj0goMTSK7RRAPBF4wP-Nj5DRvT\&index=2](https://www.youtube.com/watch?v=oQ0WkIdr73E\&list=PLTd5ehIj0goMTSK7RRAPBF4wP-Nj5DRvT\&index=2)
* [https://es.stackoverflow.com/questions/46015/para-qu%C3%A9-se-usa-en-c-y-c-al-manejar-estructuras-de-datos](https://es.stackoverflow.com/questions/46015/para-qu%C3%A9-se-usa-en-c-y-c-al-manejar-estructuras-de-datos)

