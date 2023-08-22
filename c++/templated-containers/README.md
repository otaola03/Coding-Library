# Templated Containers

Los contenedores templados, o _templated containers_, son una característica esencial en C++ que te permite crear estructuras de datos genéricas capaces de almacenar diferentes tipos de elementos. Estos contenedores son parte de la librería estándar de C++ y son fundamentales para escribir código eficiente y reutilizable.

### Definición y Utilidad de los Templated Containers

Los templated containers son clases genéricas que pueden almacenar objetos de cualquier tipo, proporcionando una capa de abstracción sobre la gestión de memoria y manipulación de datos. Estos contenedores se implementan utilizando plantillas, lo que permite la creación de estructuras de datos flexibles y eficientes que pueden ser adaptadas a diferentes necesidades.

### Tipos de Templated Containers

En la librería estándar de C++, existen varios tipos de templated containers que se adaptan a diferentes casos de uso. Algunos de los más comunes incluyen:

#### **std::vector:**

Un contenedor de tipo arreglo dinámico que crece automáticamente a medida que se agregan elementos. Es útil para almacenar y gestionar colecciones de datos de tamaño variable.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros;
    numeros.push_back(10);
    numeros.push_back(20);
    numeros.push_back(30);

    for (int num : numeros) {
        std::cout << num << " ";
    }

    return 0;
}
```

#### **std::list:**

Una lista doblemente enlazada que permite la inserción y eliminación eficiente de elementos en cualquier posición. Es ideal para situaciones en las que se requiere un acceso rápido a los elementos interiores de la lista.

```cpp
#include <iostream>
#include <list>
#include <string>

int main() {
    std::list<std::string> listaTareas;
    listaTareas.push_back("Completar informe");
    listaTareas.push_back("Enviar correo electrónico");

    for (const std::string& tarea : listaTareas) {
        std::cout << tarea << std::endl;
    }

    return 0;
}
```

#### **std::map:**

Un contenedor asociativo que almacena pares clave-valor, donde las claves están ordenadas. Es perfecto para la búsqueda rápida de valores basados en una clave.

```cpp
#include <iostream>
#include <map>
#include <string>

int main() {
    std::map<std::string, std::string> directorio;
    directorio["Juan"] = "555-1234";
    directorio["María"] = "555-5678";

    std::string nombre = "Juan";
    std::cout << "Número de teléfono de " << nombre << ": " << directorio[nombre] << std::endl;

    return 0;
}
```

### &#x20;Tipos de Contenedores en la STL de C++

Los contenedores en la Standard Template Library (STL) de C++ se agrupan en varias categorías para adaptarse a diferentes necesidades de programación. A continuación, exploraremos los tipos de contenedores disponibles y sus subcategorías.

#### **Sequence Containers** (Contenedores Secuenciales):

Los "Sequence Containers" (Contenedores de Secuencia) en C++ son una categoría de contenedores que almacenan y gestionan elementos en un orden específico. Estos contenedores mantienen la secuencia de inserción de elementos y permiten el acceso, la modificación y la eliminación de elementos en función de su posición en la secuencia.

Algunos ejemplos de Sequence Containers en C++ son:

1. **std::vector:** Almacena elementos en una matriz dinámica que se puede redimensionar. Ofrece acceso rápido a los elementos y permite la inserción y eliminación en cualquier posición.
2. **std::list:** Implementa una lista doblemente enlazada, permitiendo inserción y eliminación eficientes en cualquier posición, pero con un mayor costo en el acceso aleatorio a los elementos.
3. **std::deque:** Abreviatura de "double-ended queue" (cola de doble final), proporciona inserción y eliminación eficiente tanto en el frente como en la parte posterior de la secuencia.
4. **std::array:** Representa una matriz de tamaño fijo con acceso directo a sus elementos. La ventaja principal es que tiene un tamaño fijo y conocido en tiempo de compilación.
5. **std::forward\_list:** Similar a `std::list`, pero implementa una lista simplemente enlazada, lo que la hace más eficiente en términos de memoria y velocidad, pero sacrificando la capacidad de acceso inverso.

#### **Associative Containers** (Contenedores Asociativos)

Los "Associative Containers" (Contenedores Asociativos) en C++ son una categoría de contenedores que almacenan elementos en pares clave-valor, donde cada elemento se asocia con una clave única. Estos contenedores permiten el acceso y la búsqueda eficiente de elementos utilizando las claves en lugar de las posiciones.

1. **std::map:** Almacena pares clave-valor, donde las claves se mantienen ordenadas y únicas. Permite una búsqueda rápida de valores basada en las claves.
2. **std::multimap:** Similar a `std::map`, pero permite claves duplicadas. Los valores se ordenan según las claves y permiten búsquedas eficientes.
3. **std::set:** Almacena valores únicos ordenados. Permite la búsqueda rápida de valores y también es útil para verificar si un valor específico existe en el conjunto.
4. **std::multiset:** Similar a `std::set`, pero permite valores duplicados.
5. **std::unordered\_map:** Almacena pares clave-valor en un orden no determinístico, pero ofrece búsquedas rápidas utilizando tablas hash.
6. **std::unordered\_multimap:** Similar a `std::unordered_map`, pero permite claves duplicadas.
7. **std::unordered\_set:** Almacena valores únicos en un orden no determinístico, utilizando tablas hash para búsquedas rápidas.
8. **std::unordered\_multiset:** Similar a `std::unordered_set`, pero permite valores duplicados.

#### **Unordered Containers** (Contenedores No Ordenados):

Los "Unordered Containers" (Contenedores Desordenados) en C++ son una categoría de contenedores que almacenan elementos en una estructura de datos hash, lo que permite un acceso y búsqueda muy eficientes.&#x20;

A diferencia de los "Associative Containers", los Unordered Containers no mantienen un orden específico de elementos. Estos contenedores se basan en tablas hash para almacenar y recuperar datos de manera rápida utilizando una función de hash para calcular posiciones de almacenamiento.

{% hint style="info" %}
Una **tabla hash** es una forma rápida de almacenar y buscar datos usando claves. Utiliza una función matemática para asignar claves a ubicaciones de almacenamiento.
{% endhint %}

Algunos ejemplos de Unordered Containers en C++ son:

* **std::unordered\_map:** Almacena pares clave-valor utilizando una tabla hash. Permite una búsqueda rápida de valores basada en las claves, pero no mantiene ningún orden específico.
* **std::unordered\_multimap:** Similar a `std::unordered_map`, pero permite claves duplicadas.
* **std::unordered\_set:** Almacena valores únicos utilizando una tabla hash. Permite búsquedas rápidas, pero no mantiene ningún orden específico.
* **std::unordered\_multiset:** Similar a `std::unordered_set`, pero permite valores duplicados.

#### **Container Adapters** (Adaptadores de Contenedores)

Los "Container Adapters" (Adaptadores de Contenedores) en C++ son clases que proporcionan interfaces específicas para acceder y manipular contenedores ya existentes de la Biblioteca Estándar de C++. Estos adaptadores permiten una funcionalidad más especializada y limitada en comparación con los Sequence Containers o los Associative Containers.

Existen tres tipos principales de Container Adapters:

* **std::stack:** Implementa una estructura de datos de pila (LIFO - Last In, First Out) utilizando un contenedor subyacente (por defecto, `std::deque`). Proporciona operaciones como `push`, `pop` y `top`, lo que permite agregar y eliminar elementos solo desde la parte superior de la pila.
* **std::queue:** Implementa una estructura de datos de cola (FIFO - First In, First Out) utilizando un contenedor subyacente (por defecto, `std::deque`). Ofrece operaciones como `push`, `pop` y `front`, lo que permite agregar elementos al final de la cola y eliminarlos desde el frente.
* **std::priority\_queue:** Implementa una cola de prioridad utilizando un contenedor subyacente (por defecto, `std::vector`). Los elementos se almacenan en un orden específico según una función de comparación definida. Proporciona operaciones para agregar elementos y obtener el elemento más prioritario.

Este tipo de contenedores son una plantilla de la biblioteca estándar que proporcionan una interfaz de pila sobre un contenedor subyacente, es decir son clases heredadas. Sin embargo ocultan ciertos metodos de sus clases padres.

Normalmente no vas a necesitar los metodos de las clases padres, ya que de sera asi tal vez no este usando el contenedor apropiado. Sin embargo, en algunas situaciones puede ser útil acceder al contenedor subyacente para realizar operaciones más avanzadas. Esto se puede lograr de dos maneras, con `std::stack::container_type` y con `std::stack::c`.

Cuando usas `std::stack<T>::container_type`, estás accediendo al tipo de ese contenedor subyacente. Por ejemplo:

```cpp
cppCopy code#include <iostream>
#include <stack>

int main() {
    std::stack<int>::container_type myContainer;  // Declara una variable del tipo del contenedor subyacente
    // Aquí podrías usar myContainer como si fuera el contenedor directamente

    return 0;
}
```

Por otro lado, cuando usas `std::stack<T>::c`, estás accediendo al contenedor subyacente real. Por ejemplo:

```cpp
cppCopy code#include <iostream>
#include <stack>

int main() {
    std::stack<int> myStack;
    std::stack<int>::container_type& myContainer = myStack.c;  // Obtén una referencia al contenedor subyacente
    // Ahora myContainer es el contenedor subyacente real

    return 0;
}
```

### Ventajas de Utilizar Templated Containers

* **Flexibilidad**: Los templated containers se adaptan automáticamente a diferentes tipos de datos, lo que proporciona una gran flexibilidad en la manipulación de datos.
* **Reutilización de Código**: Puedes escribir algoritmos genéricos que funcionen con cualquier tipo de templated container, lo que fomenta la reutilización de código.
* **Eficiencia**: Los templated containers están optimizados para un rendimiento eficiente y una gestión de memoria adecuada.
