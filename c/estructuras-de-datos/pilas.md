---
description: Stack
---

# Pilas

Una Pila es una clase especial de lista en la cual todas las inserciones y borrados tienen lugar en un extremo denominado _extremo, cabeza o tope._ otro nombre para las pilas son listas FIFO (último en entrar, primero en salir) o listas pushdown (empujadas hacia abajo). El modelo intuitivo de una pila es un conjunto de objetos apilados de forma que al añadir un objeto se coloca encima del ultimo añadido y para quitar un objeto del montón hay que quitar antes los que están por encima de él.

Un ejemplo practico que se suele utlizar para explicar este conceptos es una pila de platos. Mientras vamos lavando los platos, estos los vamos apilando y a la hora de utilizarlos el primero que cogemos es el ultimo que hemos lavado y colocado en la pila.



> Una pila tambien se puede implementar como una lista enlazada, aunque al igual que con las colas, las operaciones seran distintas.

<figure><img src="https://cdn.programiz.com/sites/tutorial2program/files/stack.png" alt=""><figcaption></figcaption></figure>

### Estructuras de las pilas

La estructura de una pila es muy simple, tan solo se compone de una estructura que contine un puntero hacia la cima de la pila. Para mayor comodidad se puede agregar un integrer con la longitud de la pila e ir aumentado o decreciendo este segun el tamaño de la pila.

```
typedef struct pila 
{
    Nodo *cima;
} Pila;
```

Para crear una pila de manera dinamica podemos hacerlo mediante una funcion utilizando malloc y una vez creada habra que asginar a la cima el valor NULL.

```
Pila *crear_pila()
{
    Pila *pila = (Pila *)malloc(sizeof(Pila));
    pila->cima = NULL;
    return (pila);
}
```

### Apilar (Push)

Apilar significa **introducir algo en la pila**. Este elemento sera introducido en el extremo de la pila, conocido como cima o Peek y para ello se puede utilizar la funcion [`insertar_principio`](listas-enlazadas.md#insertar-nodos). Aun asi este es un ejemplo de como apilar elementos en una pila:

Tan solo hay que crear un nuevo nodo con la informacion solicitada, apuntar su siguiente al la cima y establecer la nueva cima como el nodo creado.

```
void apilar(Pila *pila, URL url)
{
    Nodo *nodo = crear_nodo(url);
    nodo->sigueinte = pila->cima;
    pila->cima = nodo;
```



### Desapilar (Pop)

Desapilar significar **eliminar el ultimo elemento intruducido** en la pila, que es el elemento situado en la cima. Es decir si introducimos un elemento por por un extremo, tendremos que eliminarlo por ese mismo extremo. Para esto se puede utilizar la funcion [`eliminar_principio`](listas-enlazadas.md#eliminar-nodos). Aun asi este es un ejemplo de como desapilar elementos en una pila:

Antes que nada hay que comprobar la que la pila no este vacia. Una vez hecho guardaremos el primer nodo en una variable auxiliar, para su posterior eliminacion y depues estableceremos la cima como siguiente nodo del primero `pila->cima->siguiente`.

```
void desapilar(Pila *pila)
{
    if (pila->cima != NULL)
    {
        Nodo *eliminar = pila->cima;
        pila->cima = pila->cima->siguiente;
        destruir_nodo(eliminar);
    }
}
```

### Destruir Pilas

En el caso de hayas terminado de utilizar la pila y no sea necesaria su utilizacion, es recomendable eliminarla para evitar tener memoria en desuso. Para esto tan solo hay que ir sacando uno a uno los elementos de la pila y una vez vaciada hay que eliminar el espacio que ocupa la pila por si misma.

```
void destruir_pila(Pila *pila)
{
    while (pila->cima != NULL)
        Desapilar(pilar);
    free(pila);
}
```

