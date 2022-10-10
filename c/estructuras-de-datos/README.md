# Estructuras de datos

### Estructuras de datos en programacion

Las estructuras de datos es una rama de las ciencias de la computación que estudia y aplica diferentes formas de organizar información dentro de una aplicación, para manipular, buscar e insertar estos datos de manera eficiente.

**Depende que algoritmo queramos ejecutar**, habrá veces que sea mejor utilizar una estructura de datos u otra estructura que nos permita más velocidad.

Por este motivo es interesante conocer algo más que simplemente los arrays o los hashmaps que casi todo el mundo conoce.

### ¿Para qué sirven las estructuras de datos? <a href="#c2-bfpara-qu-c3-a9-sirven-las-estructuras-de-datos" id="c2-bfpara-qu-c3-a9-sirven-las-estructuras-de-datos"></a>

En el ámbito de la informática, las **estructuras de datos** son aquellas que nos permiten, como desarrolladores, organizar la información de manera eficiente, y en definitiva diseñar la solución correcta para un determinado problema.

Ya sean las más utilizadas comúnmente -como las **variables**, **arrays**, **conjuntos** o **clases**- o las diseñadas para un propósito específico -**árboles**, **grafos**, **tablas**, etc.-, una **estructura de datos** nos permite trabajar en un algo nivel de abstracción almacenando información para luego acceder a ella, modificarla y manipularla.

### Arrays <a href="#arrays" id="arrays"></a>

¿Qué es un array en programación? Un **array** es un tipo de **dato estructurado** que permite almacenar un conjunto de datos homogéneo y ordenado, es decir, todos ellos del mismo tipo y relacionados. Su condición de _homogéneo_, indica que sus elementos están compuestos por el mismo tipo de dato, y su condición de _ordenado_ hace que se pueda identificar del primer al último elemento que lo compone.

<figure><img src="https://dc722jrlp2zu8.cloudfront.net/media/cache/15/0d/150d76f956d52bc2c4e7ac1556c67808.webp" alt=""><figcaption></figcaption></figure>

Constan de un **índice** para acceder a una posición concreta y del valor que el mismo almacena.

### Estructura de datos dinámicas <a href="#estructura-de-datos-din-c3-a1micas" id="estructura-de-datos-din-c3-a1micas"></a>

Por otro lado, vimos que en programación existen **estructuras de datos dinámicas**, es decir, una colección de elementos -nodos- que normalmente se utilizan para dejar asentados registros. A diferencia de un **array** que contiene espacio para almacenar un número fijo de elementos, una **estructura dinámica de datos** se amplía y contrae durante la ejecución del programa. Veamos algunos casos:

#### Estructura de datos lineales <a href="#estructura-de-datos-lineales" id="estructura-de-datos-lineales"></a>

Las **estructuras de datos lineales** son aquellas en las que los elementos ocupan lugares sucesivos en la estructura y cada uno de ellos tiene un único sucesor y un único predecesor, es decir, sus elementos están ubicados uno al lado del otro relacionados en forma lineal.

Hay tres tipos de **estructuras de datos lineales**:

* Listas enlazadas
* Pilas
* Colas

### **Listas enlazadas**

En las **estructuras de datos**, las listas enlazadas se construyen con elementos que están ubicados en una secuencia. Aquí, cada elemento se conecta con el siguiente a través de un enlace que contiene la posición del siguiente elemento. De este modo, teniendo la referencia del principio de la lista podemos acceder a todos los elementos de la misma.

Estas listas se componen de `nodos` los cuales tienen dos atributos: el primero es el item o elemento que va a contener este nodo y el segundo atributo es una referencia al siguiente elemento de la lista.

<figure><img src="https://blog.soyhenry.com/content/images/size/w1600/2022/02/LISTA-ENLAZADA.png" alt=""><figcaption></figcaption></figure>

### **Pila (Stack)**

La pila es un tipo especial de **lista lineal** dentro de las **estructuras de datos dinámicas** que permite almacenar y recuperar datos, siendo el modo de acceso a sus elementos de tipo LIFO (del inglés _Last In, First Out_, es decir, _último en entrar, primero en salir_). ¿Cómo funciona? A través de dos operaciones básicas: apilar (push), que coloca un objeto en la pila, y su operación inversa, desapilar (pop), que retira el último elemento apilado.

Las pilas son un tipo de listas que tienen la particularidad de sólo poder eliminar o insertar en la `cima` de la lista.

<figure><img src="https://cdn.programiz.com/sites/tutorial2program/files/stack.png" alt=""><figcaption></figcaption></figure>

### Colas

Esta estructura es otro tipo de lista que nos permite emular el comportamiento de una fila o cola de la vida real donde el primer elemento en ingresar a la fila es el primero en salir, lo que quiere decir que las inserciones (Encolar) se realizan al final y las extracciones (Desencolar) se realizan al frente de la cola, lo cual se conoce como FIFO (First in First out).

Es otra estructura de datos muy útil, que sirve, entre otras cosas, para implementar una cola o para comunicar procesos asíncronos.

<figure><img src="https://upload.wikimedia.org/wikipedia/commons/b/bb/Cola.svg" alt=""><figcaption></figcaption></figure>

### Estructura de datos no lineales <a href="#estructura-de-datos-no-lineales" id="estructura-de-datos-no-lineales"></a>

Las **estructuras de datos no lineales**, también llamadas multienlazadas, son aquellas en las que cada elemento puede estar enlazado a cualquier otro componente. Es decir, cada elemento puede tener varios sucesores o varios predecesores.

Existen dos tipos:

* Árboles
* Grafos

### **Árboles**

En **estructura de datos**, los árboles consisten en una **estructura no lineal** que se utiliza para representar datos con una relación jerárquica en la que cada elemento tiene un único antecesor y puede tener varios sucesores.

Los mismos se encuentran clasificados en: **árbol general**, un árbol donde cada elemento puede tener un número ilimitado de sub árboles y **árboles binarios**, que son una estructura de datos homogénea, dinámica y no lineal en donde a cada elemento le pueden seguir como máximo dos nodos.

Una característica esencial de los arboles binarios es que la inserción de sus elementos se realizan siguiendo un criterio, si el item del nodo a insertar es menor a su nodo padre, la inserción se realiza por la izquierda y en caso contrario la inserción se realiza por el lado derecho. Como consecuencia de esto, nuestro arbol siempre estara organizado de tal manera que los hijos izquierdos de cada nodo seran menores a el y los derechos seran mayores, lo cual nos permite realizar búsquedas muy eficientes debido a la organización de esta información donde para buscar un elemento solo es necesario ir comparando el valor a buscar con el valor del nodo actual y asi tomar la decisión si ir por la izquierda o por la derecha, ahorrandonos las búsquedas por el otro lado del arbol.

Es una forma de guardar los datos de tal manera, que, aunque no estén ordenados, se puedan retirar de ese conjunto datos **de forma ordenada**.

Esto permite una **gran velocidad**, por ejemplo, a la hora de implementar una cola de prioridades donde queremos que cada elemento que insertemos, si insertamos de repente muchos elementos con una prioridad, el primero que se coja sea el que tenga más o menos prioridad, depende del **tipo de montículo**.

<figure><img src="http://www.oscarblancarteblog.com/wp-content/uploads/2014/08/subarbol.png" alt=""><figcaption></figcaption></figure>

### **Grafos**

Otro tipo de **no lineal** de **estructura de datos en programación**, son los **grafos**. Se trata de una estructura matemática formada por un conjunto de puntos —una estructura de datos— y un conjunto de líneas, cada una de las cuales une un punto a otro. Los puntos se llaman nodos o vértices del grafo y las líneas se llaman aristas o arcos.

<figure><img src="https://blog.soyhenry.com/content/images/size/w1600/2022/02/GRAFOS.png" alt=""><figcaption></figcaption></figure>

### Bibliografia

* [https://openwebinars.net/blog/que-son-las-estructuras-de-datos-y-por-que-son-tan-utiles/](https://openwebinars.net/blog/que-son-las-estructuras-de-datos-y-por-que-son-tan-utiles/)
* [https://blog.soyhenry.com/que-es-una-estructura-de-datos-en-programacion/](https://blog.soyhenry.com/que-es-una-estructura-de-datos-en-programacion/)
* [https://ed.team/blog/estructuras-de-datos](https://ed.team/blog/estructuras-de-datos)
