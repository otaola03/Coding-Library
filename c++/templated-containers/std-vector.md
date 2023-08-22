# std::vector

El `std::vector` es una implementación de un arreglo dinámico que crece automáticamente según sea necesario. Combina la flexibilidad de un arreglo con la administración automática de memoria, lo que lo hace muy conveniente para muchas aplicaciones. Permite almacenar elementos de cualquier tipo y proporciona operaciones eficientes de inserción, eliminación y acceso.

### Uso Básico de `std::vector`

El contenedor `std::vector` es una herramienta esencial en la biblioteca estándar de C++ que proporciona un arreglo dinámico capaz de almacenar elementos de cualquier tipo.

#### Declaración y Creación de `std::vector`

Para utilizar un `std::vector`, primero debemos declararlo y crearlo. Podemos especificar el tipo de elementos que contendrá entre los corchetes angulares (`<>`). A continuación, se muestra cómo declarar y crear un `std::vector` de enteros y de cadenas:

```cpp
#include <iostream>
#include <vector>

int main() {
    // Declaración y creación de un std::vector de enteros
    std::vector<int> numeros;

    // Declaración y creación de un std::vector de cadenas
    std::vector<std::string> nombres;

    return 0;
}
```

#### Agregando Elementos a un `std::vector`

Una vez creado el `std::vector`, podemos agregar elementos utilizando el método `push_back()`. Esto agrega un elemento al final del `std::vector`. A continuación, se muestra cómo agregar elementos a un `std::vector` de enteros y de cadenas:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<std::string> nombres;
    nombres.push_back("Alice");
    nombres.push_back("Bob");

    return 0;
}
```

#### Accediendo a Elementos del `std::vector`

Para acceder a los elementos de un `std::vector`, podemos utilizar el operador de acceso `[]`. El índice se especifica entre los corchetes y comienza desde 0 para el primer elemento. A continuación, se muestra cómo acceder a elementos en un `std::vector` de enteros y de cadenas:

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros = {10, 20, 30};
    int primerElemento = numeros[0];  // Accede al primer elemento (10)
    int segundoElemento = numeros[1]; // Accede al segundo elemento (20)

    return 0;
}
```

#### Tamaño y Capacidad de un `std::vector`

Un `std::vector` tiene dos propiedades importantes: su tamaño actual y su capacidad. El tamaño se refiere al número de elementos almacenados, mientras que la capacidad es la cantidad total de elementos que puede almacenar antes de necesitar una realocación de memoria. Estos valores se obtienen utilizando los métodos `size()` y `capacity()`, respectivamente.

{% hint style="info" %}
La capacidad no necesariamente aumenta en un solo incremento; la implementación interna puede aumentar la capacidad en bloques más grandes para reducir las realocaciones frecuentes.
{% endhint %}

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros = {10, 20, 30};
    size_t tam = numeros.size();  // Tamaño actual (3)
    size_t capacidad = numeros.capacity();  // Capacidad actual (3 o más)

    return 0;
}
```

#### Eliminando Elementos de un `std::vector`

Para eliminar elementos de un `std::vector`, podemos utilizar los métodos `pop_back()` para eliminar el último elemento, y `erase()` para eliminar elementos en posiciones específicas.

```cpp
# include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros = {10, 20, 30};
    numeros.pop_back();  // Elimina el último elemento (30)
    numeros.erase(numeros.begin() + 1);  // Elimina el segundo elemento (20)

    return 0;
}
```

Para eliminar un elemnto de una posicion especifica medinate `erease()` es encesario indicarle el principio de la lista y a partir de ahí indicarle el elemento que desees borrar.

### Funciones Miembro y Métodos de `std::vector` en C++

El contenedor `std::vector` proporciona una variedad de funciones miembro y métodos que permiten realizar modificaciones, acceder a elementos y gestionar la capacidad del vector.

#### Modificación del Contenido

El método `push_back()` agrega un elemento al final del `std::vector`, mientras que `pop_back()` elimina el último elemento.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros;
    numeros.push_back(10);
    numeros.push_back(20);

    numeros.pop_back();  // Elimina el último elemento

    return 0;
}
```

#### Ajustando Tamaño y Capacidad

El método `resize()` ajusta el tamaño del `std::vector`, agregando o eliminando elementos según sea necesario. `reserve()` establece la capacidad mínima del `std::vector` sin cambiar su tamaño actual.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros = {10, 20, 30};

    numeros.resize(5);  // Aumenta el tamaño a 5, agregando elementos (0 por defecto)
    numeros.resize(2);  // Reduce el tamaño a 2, eliminando elementos extras

    numeros.reserve(10);  // Asegura capacidad para al menos 10 elementos

    return 0;
}
```

#### Accediendo a Elementos

Los métodos `front()` y `back()` permiten acceder al primer y último elemento del `std::vector`, respectivamente.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros = {10, 20, 30};

    int primerElemento = numeros.front();  // Accede al primer elemento (10)
    int ultimoElemento = numeros.back();   // Accede al último elemento (30)

    return 0;
}
```

#### Comprobando y Obtener Información

El método `empty()` verifica si el `std::vector` está vacío, mientras que `size()` devuelve el número de elementos almacenados.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros = {10, 20, 30};

    bool estaVacio = numeros.empty();  // Comprueba si está vacío (false)
    size_t tam = numeros.size();       // Obtiene el tamaño (3)

    return 0;
}
```

#### Intercambiando Contenido

El método `swap()` intercambia el contenido de dos `std::vector`, lo que puede ser útil para reorganizar o combinar datos.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> a = {1, 2, 3};
    std::vector<int> b = {4, 5, 6};

    a.swap(b);  // Intercambia el contenido entre a y b

    return 0;
}
```

#### Uso de `emplace_back()` y Constructores en Lugar de `push_back()`

`emplace_back()` permite construir elementos directamente en el `std::vector`, evitando copias innecesarias.

```cpp
#include <iostream>
#include <vector>

class Persona {
public:
    Persona(std::string nombre, int edad) : nombre_(nombre), edad_(edad) {}

private:
    std::string nombre_;
    int edad_;
};

int main() {
    std::vector<Persona> personas;
    personas.emplace_back("Alice", 25);  // Utiliza el constructor en lugar

    return 0;
}
```

Usa `push_back()` para agregar objetos ya construidos a un contenedor. Emplea `emplace_back()` para construir objetos directamente en el contenedor, evitando copias o movimientos, lo que puede ser más eficiente y cómodo en términos de rendimiento y uso de memoria.

\


### Gestión Eficiente de Memoria y Rendimiento en `std::vector`

La gestión eficiente de memoria es esencial para garantizar un buen rendimiento en tus programas. `std::vector` ofrece herramientas para controlar la asignación y liberación de memoria, lo que puede impactar significativamente en la velocidad y eficiencia de tus operaciones. En esta sección, exploraremos cómo `std::vector` gestiona la memoria, cómo evitar realocaciones innecesarias y cómo utilizar `reserve()` para optimizar la gestión de memoria.

#### Cómo `std::vector` Gestiona la Memoria

`std::vector` gestiona dinámicamente la memoria necesaria para almacenar sus elementos. Cuando se agrega un elemento a un `std::vector`, si no hay suficiente capacidad, se puede realizar una realocación de memoria para aumentar su tamaño y copiar los elementos existentes a la nueva ubicación. Esto puede ser costoso en términos de rendimiento, especialmente cuando se realizan muchas realocaciones.

#### Cómo Evitar Realocaciones Innecesarias

Para evitar realocaciones innecesarias, es importante estimar y reservar suficiente memoria desde el principio. Si tienes una idea aproximada del número de elementos que almacenarás, puedes reservar espacio utilizando `reserve()` antes de agregar elementos. Esto reduce la probabilidad de realocaciones posteriores.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros;
    numeros.reserve(1000);  // Reserva espacio para 1000 elementos

    // Agregar elementos a 'numeros' sin realocaciones
    for (int i = 0; i < 1000; ++i) {
        numeros.push_back(i);
    }

    return 0;
}
```

#### Uso de `reserve()` para Optimizar la Gestión de Memoria

La función `reserve()` es útil cuando tienes una idea clara del número máximo de elementos que contendrá el `std::vector`. Al reservar memoria de antemano, puedes minimizar las realocaciones y, por lo tanto, mejorar el rendimiento.

Es importante destacar que aunque `reserve()` reduce las realocaciones, no afecta al tamaño actual del `std::vector`. Para ajustar el tamaño actual y eliminar elementos adicionales, puedes usar `resize()` o `clear()` según sea necesario.

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> numeros;
    numeros.reserve(1000);  // Reserva espacio para 1000 elementos

    // Agregar elementos a 'numeros' sin realocaciones
    for (int i = 0; i < 1000; ++i) {
        numeros.push_back(i);
    }

    // Redefinir el tamaño y eliminar elementos adicionales
    numeros.resize(100);   // Ajusta el tamaño a 100
    numeros.clear();       // Elimina todos los elementos

    return 0;
}
```

Gestionar eficientemente la memoria es fundamental para el rendimiento de tus programas. Utilizando `reserve()` de manera estratégica en tu `std::vector`, puedes minimizar las realocaciones y mejorar el rendimiento general de tu código. Ten en cuenta el tamaño estimado de tu `std::vector` y ajusta la capacidad en consecuencia para lograr un equilibrio óptimo entre uso de memoria y velocidad
