---
description: Principales tipos
---

# Estructuras de datos

Las estrcuturas de datos son las distintas estructuras que utilizamos para representar la informacion en un ordenador, como una biblioteca. Un ejemplo de esto son los **arrays**, pero existen otro tipos de estructuras para guarda **informacion mas compleja**

La listas enlazadas&#x20;

### Listas enlazadas

Las listas enlazadas permite representar un grupo de elementos presentados como una secuencia. Estas son colecciones de estructuras autorreferenciadas llamadas nodos. Con ellas podemos guardar y modificar datos en tiempo de ejecución y o es necesario definir cuantos espacios a a tener nuestra lista.

```
struct nodo{
    char *nombre;
    sruct nodo *sig;
}
```

En otras palabras, es una estuctura que contiene un miembro apuntador (**puntero**) el cual apunta a una estructura del mismo tipo.&#x20;

<figure><img src="../.gitbook/assets/Screen Shot 2022-09-10 at 9.45.05 PM (1).png" alt=""><figcaption></figcaption></figure>

> Es un conjunto de nodos apuntados entre si

Las lista constan de dos partas, la cabeza, que es el primer elmento de la lista y la cola,  que son lso nodos restantes. Ademas cada elemento de la cola es la cabeza de una lista.

El ultimo nodo de la lista apunta a una lista vacia, un valor NULL&#x20;

#### Ventajas de una lista frente a un array

* Los nodos no tienen por que guardarse toso juntos en memoria, como ocurre con los arrays
* Pueden tener longitud variable
* Podemos agregar y quitar elementos en timepo de ejecucion

#### Deventajas de una lista frente a un array

* Las listas no tienen nocion de indice, por lo que no podemos hacer accesos aleatorios
* Necesitan mas espacio en memoria ya ue tienes que aalmacenar punteros

### Estructura autorreferenciada



&#x20;un nodo es un una estructura que se crea con memoria dinamica
