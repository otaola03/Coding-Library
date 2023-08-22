# Iterators

Los iteradores son herramientas esenciales en C++ que permiten acceder y recorrer los elementos de contenedores y secuencias de datos de manera eficiente. Proporcionan una abstracción que facilita la manipulación de datos sin preocuparse por los detalles internos de la estructura de datos. Los iteradores permiten recorrer los elementos en cualquier dirección (adelante o atrás) y son una parte fundamental de la Biblioteca Estándar de C++.

### Tipos de Iteradores

En C++, existen varios tipos de iteradores, cada uno diseñado para trabajar con diferentes tipos de contenedores y sus características. Los tipos más comunes son:

#### **Iteradores de Contenedor**

Los iteradores de contenedor permiten recorrer y acceder a los elementos de contenedores como vectores, listas y mapas. Proporcionan formas de acceder al principio, final y otros puntos en el contenedor para realizar operaciones en los elementos.

* **begin:** Apunta al primer elemento del contenedor.
* **end:** Apunta a una posición más allá del último elemento del contenedor.
* **rbegin:** Apunta al último elemento del contenedor.
* **rend:** Apunta a una posición antes del primer elemento del contenedor al revés.

```cpp
std::vector<int> numbers = {1, 2, 3, 4, 5};
for (auto it = numbers.begin(); it != numbers.end(); ++it) {
    std::cout << *it << " ";
}
```

#### **Iteradores de Flujo**

Los iteradores de flujo simplifican la lectura y escritura de datos a través de flujos de entrada y salida, como la entrada estándar y la salida estándar. Facilitan la interacción con flujos al proporcionar una forma de acceder y operar en datos en un estilo similar al de los contenedores.

* **istream\_iterator:** Lee valores de entrada de flujo.
* **ostream\_iterator:** Escribe valores en un flujo de salida.

```cpp
std::vector<int> numbers;
std::istream_iterator<int> input_it(std::cin);
std::copy(input_it, std::istream_iterator<int>(), std::back_inserter(numbers));
```

Este código crea un vector de enteros llamado `numbers`. Luego, utiliza un iterador de flujo `input_it` para leer enteros de la entrada estándar (`std::cin`). Mediante la función `std::copy`, los valores leídos se insertan en el vector `numbers` usando `std::back_inserter`. Esto permite llenar el vector con valores ingresados desde la entrada estándar.

### Uso de Iteradores&#x20;

Los iteradores permiten recorrer y manipular elementos en contenedores de manera uniforme. Pueden usarse en bucles para realizar operaciones en cada elemento o acceder a un elemento específico.

```cpp
std::list<std::string> words = {"hello", "world", "example"};
std::list<std::string>::iterator it = words.begin();
std::advance(it, 2); // Avanzar 2 posiciones
std::cout << *it << std::endl; // Imprime "example"
```
