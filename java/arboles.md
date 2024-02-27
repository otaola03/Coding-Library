# Arboles

En informática, un **árbol** es una estructura de datos jerárquica compuesta por nodos interconectados, donde cada nodo tiene un nodo padre (excepto la raíz) y cero o más nodos hijos. Está diseñado para organizar datos eficientemente, facilitando la búsqueda y manipulación de información. Los árboles son fundamentales en la representación y estructuración de datos en algoritmos y aplicaciones informáticas.

### Conceptos básicos

Aquí, exploraremos los conceptos básicos de los árboles, sus elementos fundamentales y cómo se estructuran en la programación:

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

* El predecesor de cualquier elemento se denomina **padre** del elemento
* El  nodo que no tiene padre y predecesor de todos los elementos de denomina **raiz**
* Cada nodo puede tener 0 o mas hijos
* Todo hijo  es un **subarbol**
* Los nodos sin hijos se denominan **hojas**
* **Anchura (fan-out):** Maximo numero de hijos para un nodo cualquiera de un arbol
  * **Arbol-general:** tiene un fan-out acotado
  * **Arboles binarios:** Tiene un fan-out maximo de 2, es decir puede tener como maximo 2 hijos por cada nodo
* **Altura:** Distancia maxima desde la raiz a cualquiera de las hojas
* **Nivel:** Conjunto de nodos de un arbol que tienen la misma altura

### Tipos de recorrido

#### **Recorrido en Anchura (Breadth-First Traversal):**

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

El recorrido en anchura, también conocido como BFS, explora el árbol nivel por nivel. Comienza visitando la raíz y luego se mueve a sus nodos hijos antes de avanzar al siguiente nivel. Para implementarlo, utilizamos una cola para mantener un seguimiento del orden de visita. Este recorrido es eficaz para encontrar el camino más corto en un grafo no ponderado y garantiza que los nodos se visiten en el orden en que aparecen en cada nivel.

```
BFS(raiz):
    cola = nueva Cola()
    cola.encolar(raiz)

    mientras cola no esté vacía:
        nodo = cola.desencolar()
        imprimir nodo.valor

        si nodo.izquierdo no es nulo:
            cola.encolar(nodo.izquierdo)
        si nodo.derecho no es nulo:
            cola.encolar(nodo.derecho)
```

#### **Recorrido en Profundidad - Preorden (Preorder Traversal):**

<figure><img src="../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

En el recorrido en profundidad preorden, primero se visita el nodo actual, luego se realiza el mismo proceso en el subárbol izquierdo y, finalmente, en el subárbol derecho. Es útil para explorar la estructura del árbol antes de profundizar en niveles inferiores. Puede ser utilizado para crear una copia del árbol, imprimir una expresión aritmética en notación prefija o realizar cualquier acción que necesite procesar el nodo antes de sus hijos.

```
Preorden(raiz):
    si raiz no es nulo:
        imprimir raiz.valor
        Preorden(raiz.izquierdo)
        Preorden(raiz.derecho)
```

#### **Recorrido en Profundidad - Postorden (Postorder Traversal):**

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

En el recorrido en profundidad postorden comineza por las hojas, primero se visitan los nodos de los subárboles izquierdo y derecho y, finalmente, el nodo raiz. Este enfoque es útil para liberar la memoria ocupada por el árbol, ya que **libera los nodos de abajo hacia arriba**. También se utiliza para realizar operaciones que deben ocurrir después de procesar los nodos hijos, como evaluar expresiones aritméticas.

```
Postorden(raiz):
    si raiz no es nulo:
        Postorden(raiz.izquierdo)
        Postorden(raiz.derecho)
        imprimir raiz.valor
```

#### **Recorrido en Profundidad - Inoreden (Inorder Traversal):**

<figure><img src="../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

El recorrido inorden es un tipo de travesía en árboles que sigue el patrón de visitar primero el subárbol izquierdo, luego el nodo padre y, finalmente, el subárbol derecho. Es especialmente útil en árboles binarios de búsqueda, ya que este orden de recorrido produce una secuencia ordenada de los valores almacenados.

```
Inorden(nodo):
    si nodo no es nulo:
        Inorden(nodo.izquierdo)
        imprimir nodo.valor
        Inorden(nodo.derecho)
```

### Arboles de busqueda binaria

En esencia, un árbol de búsqueda binario es una estructura jerárquica que consta de nodos, cada uno con, como máximo, dos hijos: uno izquierdo y otro derecho. La clave de su eficacia radica en la organización de los datos:

* Los nodos izquierdos tiene un valor inferior que el nodo antedecesor
* Los nodos derechos tiene un valor mayor que el nodo antedecesor

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

#### Operacion de búsqueda

La operación de búsqueda en árboles de búsqueda binarios es una de las funcionalidades clave que hacen que esta estructura de datos sea tan eficiente. El proceso de búsqueda se inicia desde la raíz del árbol y avanza hacia abajo, comparando la clave de búsqueda con la clave del nodo actual.

1. **Inicio desde la Raíz:**
   * La búsqueda comienza en el nodo raíz del árbol. Se compara la clave de búsqueda con la clave del nodo actual.
2. **Descenso por el Árbol:**
   * Si la clave de búsqueda es menor que la clave del nodo actual, la búsqueda se dirige hacia el subárbol izquierdo. Si es mayor, se dirige hacia el subárbol derecho. Este proceso de comparación y descenso continúa hasta que se encuentra el nodo deseado o se llega a una hoja del árbol, indicando que el elemento no está presente.

```
Función BuscarEnArbolBinario(raiz, clave):
    Si raiz es nulo o raiz.clave es igual a clave:
        Devolver raiz
    
    Si clave < raiz.clave:
        Devolver BuscarEnArbolBinario(raiz.izquierdo, clave)
    
    Sino:
        Devolver BuscarEnArbolBinario(raiz.derecho, clave)
```

#### Operación de insercion

La operación de inserción en árboles de búsqueda binarios es esencial para construir y mantener la estructura del árbol de manera ordenada. Aquí tienes un pseudocódigo básico para la inserción en un árbol de búsqueda binario:

1. **Caso Base:**
   * Si la raíz es nula, significa que el árbol está vacío, por lo que el nuevo nodo se convierte en la raíz.
2. **Comparación de Claves:**
   * Se compara la clave del nuevo nodo con la clave del nodo actual. Dependiendo de la comparación, se decide si se inserta en el subárbol izquierdo o derecho.
3. **Recursividad:**
   * Si el subárbol correspondiente está vacío, se inserta el nuevo nodo en esa posición. Si no está vacío, se realiza la inserción de manera recursiva en el subárbol correspondiente.

```
Función InsertarEnArbolBinario(raiz, nuevoNodo):
    Si raiz es nula:
        raiz = nuevoNodo
    Sino Si nuevoNodo.clave < raiz.clave:
        Si raiz.izquierdo es nulo:
            raiz.izquierdo = nuevoNodo
        Sino:
            InsertarEnArbolBinario(raiz.izquierdo, nuevoNodo)
    Sino:
        Si raiz.derecho es nulo:
            raiz.derecho = nuevoNodo
        Sino:
            InsertarEnArbolBinario(raiz.derecho, nuevoNodo)
```

#### Operación de eliminiacion

La operación de eliminación en árboles de búsqueda binarios es un proceso más complejo que busca mantener la propiedad de orden del árbol mientras se elimina un nodo específico. Aquí tienes un pseudocódigo básico para la eliminación en un árbol de búsqueda binario:

1. **Casos Base:**
   * Si la raíz es nula, significa que el elemento no está presente en el árbol, por lo que no hay nada que eliminar.
2. **Recursividad:**
   * Se realiza la búsqueda del nodo a eliminar en el subárbol izquierdo o derecho según la comparación de claves.
3. **Caso 1: Nodo con un solo hijo o sin hijos:**
   * Si el nodo a eliminar tiene uno o ningún hijo, simplemente se reemplaza por su hijo (si existe) o se elimina directamente.
4. **Caso 2: Nodo con dos hijos:**
   * Si el nodo a eliminar tiene dos hijos, se encuentra el sucesor in-order (el nodo más pequeño en el subárbol derecho), se copia su clave en el nodo actual y luego se procede a eliminar el sucesor.
   * Es posible hacer lo mismo con el nodo mas grande en el subarbol izquierdo

```
Función EliminarEnArbolBinario(raiz, clave):
    Si raiz es nula:
        Devolver raiz
    
    Si clave < raiz.clave:
        raiz.izquierdo = EliminarEnArbolBinario(raiz.izquierdo, clave)
    
    Sino Si clave > raiz.clave:
        raiz.derecho = EliminarEnArbolBinario(raiz.derecho, clave)
    
    Sino:
        // Caso 1: Nodo con un solo hijo o sin hijos
        Si raiz.izquierdo es nulo:
            temp = raiz.derecho
            Eliminar(raiz)
            Devolver temp
        Sino Si raiz.derecho es nulo:
            temp = raiz.izquierdo
            Eliminar(raiz)
            Devolver temp
       
        // Caso 2: Nodo con dos hijos
        temp = EncontrarSucesorInOrder(raiz.derecho)
        raiz.clave = temp.clave
        raiz.derecho = EliminarEnArbolBinario(raiz.derecho, temp.clave)

    Devolver raiz

```

Este pseudocódigo asume funciones auxiliares como `Eliminar` para eliminar un nodo y `EncontrarSucesorInOrder` para encontrar el sucesor in-order en el subárbol derecho. Asegúrate de ajustar el pseudocódigo según la implementación específica de tu árbol binario. La eliminación en árboles de búsqueda binarios garantiza que el árbol siga siendo un BST después de la operación.
