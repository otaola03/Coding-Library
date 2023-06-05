# Shallow and deeps copies

En C++, cuando trabajamos con objetos y variables, es importante comprender cómo se copian y se manejan los datos. Uno de los conceptos clave en este sentido es la diferencia entre las copias superficiales (shallow copies) y las copias profundas (deep copies).

{% embed url="https://youtu.be/C_nLA3hfw8E" %}

### Shallow copies

En C++, si no definimos nuestro propio copy constructor, se proporciona uno por defecto. Lo mismo pasa con el operador de asignación.

Este copy constructor realiza una shallow copy de los miembros del objeto. Es decir, simplemente copia los valores de los miembros, incluidos los punteros, sin crear nuevas instancias ni duplicar los datos a los que apuntan los punteros.

{% hint style="info" %}
El Shallow copie es la misma operación por defecto que se realiza al asignar un integer a otro.&#x20;

El problema esta cuando las clases tienen punteros. Copia la misma dirección.
{% endhint %}

#### Ejemplo

```cpp
#include <iostream>

class Person {
public:
    std::string name;
    int* age;

    Person(const std::string& n, int a) : name(n), age(new int(a)) {}
    
    // Destructor para liberar la memoria del puntero age
    ~Person() {
        delete age;
    }
};

int main() {
    Person original("John", 30);
    Person shallowCopy = original;  // Realizando una shallow copy

    // Modificar el objeto shallowCopy
    *shallowCopy.age = 35;

    // Imprimir los valores
    std::cout << "Original: " << *original.age << std::endl;
    std::cout << "Shallow Copy: " << *shallowCopy.age << std::endl;

    return 0;
}
```

En este ejemplo, la clase `Person` tiene dos miembros: `name` de tipo `std::string` y `age` de tipo puntero a `int`. El constructor de `Person` asigna un nuevo espacio de memoria para `age` y copia el valor proporcionado. El destructor se encarga de liberar la memoria asignada para evitar fugas de memoria.

En el `main()`, creamos un objeto `original` con nombre "John" y edad 30. Luego, creamos un nuevo objeto `shallowCopy` y le asignamos `original`. Esto realiza una shallow copy, lo que significa que los miembros del objeto `shallowCopy` apuntarán a la misma dirección de memoria que `original`.

Si modificamos el valor de `*shallowCopy.age`, también afectará al objeto `original`, ya que ambos comparten la misma dirección de memoria para `age`.

La salida será:

```
Original: 35
Shallow Copy: 35
```

En cambio si cambiaramos la variable name no pasaria nada, ya que no es un puntero y estariamos cambiando otro espacio en memoria.

### Deep copy

En una copia profunda, se crean nuevas instancias de los datos miembro del objeto original. Esto significa que los datos se copian completamente y se asignan a nuevas ubicaciones de memoria en el objeto copiado. Cada objeto tiene su propia copia independiente de los datos.

{% hint style="info" %}
La tienes que hacer tu creando el constructor de copia y el operador de asignación.
{% endhint %}

#### Ejemplo

```cpp
#include <iostream>
#include <cstring>

class String {
public:
    char* data;

    // Constructor
    String(const char* str) {
        int length = std::strlen(str) + 1;
        data = new char[length];
        std::strcpy(data, str);
    }

    // Destructor
    ~String() {
        delete[] data;
    }

    // Constructor de copia
    String(const String& other) {
        int length = std::strlen(other.data) + 1;
        data = new char[length];
        std::strcpy(data, other.data);
    }
};

int main() {
    String original("Hello");
    String deepCopy = original;  // Realizando una deep copy

    // Modificar el objeto deepCopy
    deepCopy.data[0] = 'C';

    // Imprimir los valores
    std::cout << "Original: " << original.data << std::endl;
    std::cout << "Deep Copy: " << deepCopy.data << std::endl;

    return 0;
}
```

En este ejemplo, la clase `String` representa una cadena de caracteres y tiene un miembro `data` que es un puntero a un arreglo de caracteres.

Al realizar una deep copy al crear el objeto `deepCopy` a partir del objeto `original`, se crea una nueva instancia de `data` para el objeto copiado. Esto garantiza que ambos objetos tengan sus propias copias independientes de los datos.

Si modificamos el primer carácter de `deepCopy.data`, no afectará al objeto `original` ni a su miembro `data`, ya que tienen ubicaciones de memoria separadas.

La salida será:

```yaml
yamlCopy codeOriginal: Hello
Deep Copy: Cello
```

### Conclusión

En resumen, las shallow copies y deep copies son dos enfoques diferentes para copiar objetos en C++.&#x20;

Las shallow copies copian solo los miembros del objeto, manteniendo los punteros o referencias a los datos originales. Por otro lado, las deep copies copian tanto los miembros como los datos a los que hacen referencia los punteros o referencias, creando objetos independientes.
