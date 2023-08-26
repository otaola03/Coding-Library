# std::map

`std::map` es un contenedor asociativo proporcionado por la Biblioteca Estándar de C++ que almacena pares clave-valor en un orden específico. Cada clave en un `std::map` se asocia con un único valor, y las claves se almacenan en orden ascendente por defecto. Es una estructura de datos eficiente para realizar búsquedas y acceso rápido a valores basados en claves.

Para crear y utilizar un `std::map` en C++, sigue esta sintaxis:

```cpp
#include <map>

int main() {
    std::map<KeyType, ValueType> myMap; // Declaración del std::map
    // ... operaciones con el std::map ...
    return 0;
}
```

`KeyType` representa el tipo de dato de las claves y `ValueType` es el tipo de dato de los valores asociados.

### Operaciones Básicas con std::map

#### Inserción de Elementos Clave-Valor

Puedes insertar elementos en un `std::map` utilizando la función `insert()` o mediante el operador de índice `[]`:

```cpp
std::map<std::string, int> ageMap;

// Usando insert()
ageMap.insert(std::make_pair("Alice", 25));
ageMap.insert(std::make_pair("Bob", 30));

// Usando el operador []
ageMap["Charlie"] = 28;
```

#### Acceso a Elementos Mediante Claves

Puedes acceder a los valores en el `std::map` mediante sus claves utilizando el operador `[]`:

```cpp
int aliceAge = ageMap["Alice"]; // Acceso al valor asociado con la clave "Alice"
```

Es importante destacar que si la clave no existe, se creará una nueva entrada con la clave y un valor predeterminado (0 para tipos numéricos).

#### Inserción y Acceso de Elementos

Puedes insertar elementos clave-valor en un `std::map` utilizando la función `insert()` o el operador de índice `[]`, como se mencionó anteriormente:

```cpp
std::map<std::string, int> scores;

scores.insert(std::make_pair("Alice", 95));
scores["Bob"] = 88;
```

Para acceder a los valores asociados con las claves, simplemente utiliza el operador de índice `[]`:

```cpp
int aliceScore = scores["Alice"]; // Devuelve 95
int jamesScore = scores["James"]; //Crea James y deueleve un elemnto vacio
```

Al utilizar `[]` en el caso de que no exista la clave buscada sera creada y devolvera un value vacio o nulo dependiendo del tipo que sea. Esto la mayoria de las veces, o muy a mendo no es conveniente y para evitarlo se utiliza el metodo `.at()`.

Este metodo proporciona una forma segura de acceso, ya que verifica si la clave existe antes de devolver el valor correspondiente. Si la clave no está presente en el mapa, el operador lanzará una excepción `std::out_of_range`.

Aquí tienes un ejemplo de cómo usar el operador `.at()`:

```cpp
#include <iostream>
#include <map>

int main() {
    std::map<std::string, int> scores;
    scores["Alice"] = 95;
    scores["Bob"] = 88;

    try {
        // Acceso seguro utilizando .at()
        int aliceScore = scores.at("Alice");
        int charlieScore = scores.at("Charlie");  // Lanza std::out_of_range
    } catch (const std::out_of_range& e) {
        std::cout << "Clave no encontrada en el mapa." << std::endl;
    }

    return 0;
}
```

En este ejemplo, el intento de acceder a `"Alice"` utilizando `.at()` tiene éxito y devuelve el valor `95`. Sin embargo, el intento de acceder a `"Charlie"` lanza una excepción ya que esa clave no está presente en el mapa.

#### Verificación de la Existencia de Claves

Puedes verificar si una clave existe en el `std::map` utilizando la función `find()` o la función `count()`:

```cpp
if (scores.find("Alice") != scores.end()) {
    // La clave "Alice" existe en el std::map
}

if (scores.count("Bob") > 0) {
    // La clave "Bob" existe en el std::map
}
```

#### Eliminación de Elementos

Para eliminar un elemento específico por su clave, utiliza la función `erase()`:

```cpp
scores.erase("Alice"); // Elimina el elemento con la clave "Alice"
```

También puedes utilizar la función `clear()` para eliminar todos los elementos del `std::map`:

```cpp
scores.clear(); // Elimina todos los elementos del std::map
```

### Orden y Comparación en std::map

#### Orden por Defecto y Personalización

`std::map` mantiene sus elementos en orden ascendente según las claves. Esto significa que las claves se organizan automáticamente en orden creciente cuando se insertan elementos en el mapa. Por lo tanto, al recorrer el `std::map`, los elementos se presentarán en orden ascendente de las claves.

#### Uso de Comparadores Personalizados

Puedes personalizar el orden de los elementos en un `std::map` utilizando comparadores personalizados. Los comparadores son funciones que determinan el orden de dos elementos en función de criterios específicos.

Por ejemplo, si deseas ordenar un `std::map` en orden descendente en función de las claves, puedes usar un comparador personalizado:

```cpp
struct CompareDescending {
    bool operator()(const KeyType& a, const KeyType& b) const {
        return a > b; // Orden descendente
    }
};

std::map<KeyType, ValueType, CompareDescending> descendingMap;
```

Aquí, `CompareDescending` es una estructura que sobrecarga el operador `()` para definir un comparador personalizado.

Recuerda que cuando utilices comparadores personalizados, asegúrate de que sigan las reglas de orden y no generen inconsistencias.

### Iteración en std::map

Puedes recorrer los elementos de un `std::map` utilizando iteradores. Cada iterador apunta a un par clave-valor en el mapa. Los pares clave-valor están representados como objetos `std::pair`, donde `first` es la clave y `second` es el valor asociado.

#### Iteradores y Bucles for

Para recorrer un `std::map` utilizando bucles for y sus iteradores, puedes hacer lo siguiente:

```cpp
#include <map>

int main() {
    std::map<std::string, int> scores;
    scores["Alice"] = 95;
    scores["Bob"] = 88;
    scores["Charlie"] = 75;

    // Recorrido utilizando bucle for y iteradores
    for (auto it = scores.begin(); it != scores.end(); ++it) {
        const std::string& name = it->first;   // Clave
        int score = it->second;                // Valor
        // ... haz algo con name y score ...
    }

    return 0;
}
```

También puedes utilizar bucles for-each (C++11 en adelante) para simplificar el recorrido:

```cpp
for (const auto& entry : scores) {
    const std::string& name = entry.first;   // Clave
    int score = entry.second;                // Valor
    // ... haz algo con name y score ...
}
```

### Uso de Tipos Personalizados en std::map

#### Utilización de Clases como Claves

En un `std::map`, puedes utilizar clases personalizadas como claves en lugar de tipos de datos simples. Esto te permite organizar y acceder a datos de manera más específica y contextual.

Supongamos que tienes una clase `Person` con un nombre y una edad, y deseas utilizar esta clase como clave en un `std::map`:

```cpp
#include <map>
#include <string>

class Person {
public:
    std::string name;
    int age;

    // Constructor
    Person(const std::string& n, int a) : name(n), age(a) {}

    // Operador de comparación para ordenar personas por nombre
    bool operator<(const Person& other) const {
        return name < other.name;
    }
};

int main() {
    std::map<Person, int> ageMap;

    // Insertar elementos utilizando objetos Person como claves
    ageMap[Person("Alice", 30)] = 30;
    ageMap[Person("Bob", 25)] = 25;

    // Acceder a elementos utilizando objetos Person como claves
    int age = ageMap[Person("Alice", 30)]; // Devuelve 30

    return 0;
}
```

Para utilizar clases personalizadas como claves en un `std::map`, debes proporcionar una función de comparación para determinar el orden de las claves. En el ejemplo anterior, se sobrecarga el operador `<` en la clase `Person` para ordenar personas por nombre.

Asegúrate de que la función de comparación cumpla con las reglas de orden requeridas por `std::map`.

#### Trabajando con Unordered Maps y Hashing

Si estás interesado en utilizar clases personalizadas como claves en un contenedor más orientado a hash, como `std::unordered_map`, tendrás que proporcionar también una función de hash para esa clase. Esto permite al contenedor calcular el hash de la clave personalizada y realizar búsquedas y accesos de manera eficiente.

```cpp
#include <unordered_map>
#include <string>

class Student {
public:
    std::string name;
    int studentId;

    // Constructor y operador de comparación (como en el ejemplo anterior)

    // Función de hash personalizada
    struct HashFunction {
        std::size_t operator()(const Student& s) const {
            return std::hash<int>()(s.studentId);
        }
    };
};

int main() {
    std::unordered_map<Student, int, Student::HashFunction> studentScores;

    // Insertar y acceder a elementos (similar a std::map)

    return 0;
}
```

En este ejemplo, la función `HashFunction` se encarga de calcular el hash basado en el número de identificación del estudiante. Esto permite utilizar objetos `Student` como claves en un `std::unordered_map` de manera eficiente.

En resumen, cuando trabajas con clases personalizadas como claves en contenedores, el operador de comparación es necesario en `std::map` para el ordenamiento, y una función de hash es necesaria en `std::unordered_map` para el hashing eficiente.
