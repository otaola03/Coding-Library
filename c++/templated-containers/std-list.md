# std::list

El contenedor `std::list` en la Standard Template Library (STL) de C++ es una opción poderosa para almacenar y manipular datos en forma de lista doblemente enlazada.

### Sintaxis y Declaración

Para empezar a trabajar con `std::list` en C++, es importante comprender cómo incluir la librería necesaria, cómo declarar un objeto `std::list` y cómo insertar elementos en él utilizando las funciones `push_back()` y `push_front()`. Aquí te mostraremos paso a paso cómo hacerlo.

#### Inclusión de la Librería

Antes de poder utilizar `std::list`, debes incluir la librería adecuada en tu programa. Agrega la siguiente línea al principio de tu archivo de código:

```cpp
#include <list>
```

Esta línea permite que el compilador reconozca y use la definición de `std::list` y otras funcionalidades relacionadas con la STL.

#### Declaración de un `std::list`

La declaración de un objeto `std::list` es similar a la declaración de cualquier otro tipo de variable en C++. Puedes declarar un `std::list` para almacenar elementos de un tipo específico de la siguiente manera:

```cpp
std::list<int> numeros;  // Declaración de un std::list de enteros
std::list<std::string> palabras;  // Declaración de un std::list de cadenas
```

Aquí, hemos declarado dos objetos `std::list`: uno para almacenar enteros y otro para almacenar cadenas. Puedes cambiar el tipo de datos según tus necesidades.

#### Inserción de Elementos con `push_back()` y `push_front()`

Una vez que has declarado un `std::list`, puedes agregar elementos utilizando las funciones `push_back()` y `push_front()`. Estas funciones te permiten insertar elementos al final o al principio de la lista, respectivamente.

**`push_back()`**

```cpp
numeros.push_back(10);  // Agrega el número 10 al final de la lista
numeros.push_back(20);  // Agrega el número 20 al final de la lista
```

**`push_front()`**

```cpp
numeros.push_front(5);  // Agrega el número 5 al principio de la lista
```

Con estas operaciones, puedes construir y poblar tu `std::list` con los elementos que necesites.

### &#x20;Métodos Más Utilizados en `std::list`

A continuación, exploraremos algunos de los métodos más utilizados en `std::list`, junto con una breve explicación de lo que hace cada método y fragmentos de código que ilustran su uso para realizar operaciones esenciales en la manipulación de elementos.

#### Inserción y Eliminación de Elementos

**`push_back()` y `push_front()`**

El método `push_back(valor)` agrega el valor especificado al final de la lista. Por otro lado, `push_front(valor)` agrega el valor al principio de la lista.

```cpp
estd::list<int> numeros;
numeros.push_back(10);  // Agrega 10 al final de la lista
numeros.push_front(5);  // Agrega 5 al principio de la lista
```

**`pop_back()` y `pop_front()`**

`pop_back()` elimina el último elemento de la lista, mientras que `pop_front()` elimina el primer elemento.

```cpp
numeros.pop_back();  // Elimina el último elemento de la lista
numeros.pop_front(); // Elimina el primer elemento de la lista
```

**`insert(iterador, valor)` y `erase(iterador)`**

El método `insert(iterador, valor)` inserta el valor en la posición indicada por el iterador. `erase(iterador)` elimina el elemento apuntado por el iterador.

```cpp
auto it = std::next(numeros.begin());  // Iterador al segundo elemento
numeros.insert(it, 7);  // Inserta 7 después del primer elemento

it = std::next(numeros.begin(), 2);  // Iterador al tercer elemento
numeros.erase(it);  // Elimina el tercer elemento
```

#### Acceso a Elementos

`front()` devuelve una referencia al primer elemento de la lista, mientras que `back()` devuelve una referencia al último elemento.

```cpp
int primerElemento = numeros.front();  // Acceso al primer elemento
int ultimoElemento = numeros.back();   // Acceso al último elemento
```

#### Iteradores y Recorrido

Puedes utilizar un bucle `for` y un iterador para recorrer la lista y operar en cada elemento.

```cpp
for (std::list<int>::iterator it = lista.begin(); it != lista.end(); ++it) {
        std::cout << *it << " ";
    }
```

&#x20;La elección entre `++it` y `it++` en un bucle `for` cuando se trabaja con iteradores puede tener un impacto en el rendimiento y en algunos casos en el comportamiento del programa.

En la mayoría de los casos, ambos enfoques funcionan de manera similar y la elección entre `++it` y `it++` no tendrá un impacto significativo. Sin embargo, algunos casos particulares, como iteradores a contenedores grandes o situaciones donde el rendimiento es crítico, podrían beneficiarse de usar `++it` por su mayor eficiencia.

**Uso de Iteradores**

Los iteradores permiten recorrer la lista y acceder a sus elementos uno por uno.

```cpp
auto it = numeros.begin();
while (it != numeros.end()) {
    int valor = *it;  // Accede al valor a través del iterador
    // Realiza operaciones con 'valor'
    ++it;
}
```

#### Tamaño y Comprobaciones

`size()` devuelve el número de elementos en la lista, mientras que `empty()` verifica si la lista está vacía.

```cpp
size_t tamano = numeros.size();   // Obtiene el tamaño de la lista
bool estaVacia = numeros.empty();  // Verifica si la lista está vacía
```

Estos fragmentos de código ejemplifican cómo se utilizan los métodos más comunes en `std::list` para realizar operaciones de inserción, eliminación, acceso y recorrido. Comprender y aplicar estos métodos te permitirá trabajar eficientemente con `std::list` en tus proyectos.
