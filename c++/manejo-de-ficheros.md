---
description: Libreria fstream
---

# Manejo de ficheros

La librería fstream en C++ proporciona una interfaz para manejar archivos de forma flexible y eficiente. Se incluye de la sigueinte manera:

```cpp
#include <fstream>
```

Permite la lectura y escritura de datos en archivos, lo que resulta útil para realizar operaciones de entrada y salida en aplicaciones. En este artículo, exploraremos las principales características y funcionalidades de la librería fstream.

### Abriendo y cerrando archivos

La librería fstream ofrece diversas funciones para abrir y cerrar archivos. Al abrir un archivo, se puede especificar el modo de apertura, que puede ser de lectura, escritura o ambas.&#x20;

Para evitar tener que utilizar open existen dos tipos de datos predefinidios `std::ifstream` y `std::ofstream` que abren el fichero en modo de lectura o escirtura.

```cpp
std::ifstream archivoEntrada("archivo.txt"); //Modo de apertura de lectura
std::ofstream archivoSalida("archivo.txt"); //Modo de apertura de escritura
```

Tambien es posible pasarles el modo apertura a sus constructores, aunque no es tan comun:

```cpp
std::ifstream archivoEntrada("archivo.txt", std::ifstream::in);
```

#### Open

`Open()` permite abrir archivos con diferentes modos de apertura y realizar operaciones de lectura y escritura en ellos.

```cpp
void open(const char* filename, ios_base::openmode mode = ios_base::in | ios_base::out);
```

El método `open()` toma como primer parámetro el nombre del archivo que se va a abrir, especificado como una cadena de caracteres (`const char*`). El segundo parámetro, `mode`, es opcional y permite especificar el modo de apertura del archivo. Por defecto, se asume que el archivo se abrirá en modo de lectura y escritura.

#### Modos de apertura

Aquí tienes algunos de los modos de apertura más comunes que se utilizan al abrir un archivo con `ofstream` en C++:

1. **`std::ios::out`**: Abre el archivo en modo de escritura. Si el archivo no existe, se crea. Si el archivo ya existe, se sobrescribe su contenido.
2. **`std::ios::app`**: Abre el archivo en modo de escritura al final. Si el archivo no existe, se crea. Los datos nuevos se agregarán al final del archivo existente sin eliminar el contenido previo.
3. **`std::ios::trunc`**: Abre el archivo en modo de escritura y trunca su contenido existente. Si el archivo no existe, se crea. Si el archivo ya existe, se eliminará su contenido anterior antes de comenzar a escribir nuevos datos.
4. **`std::ios::binary`**: Abre el archivo en modo binario en lugar de modo de texto. Esto permite escribir y leer datos binarios, como imágenes o estructuras de datos personalizadas.
5. **`std::ios::in`**: Abre el archivo en modo de lectura. Permite leer datos del archivo. Si el archivo no existe, se producirá un error al intentar abrirlo.

#### Comprobar apertura

Después de abrir un archivo, es importante comprobar si el archivo se abrió correctamente. Esto se puede hacer utilizando el siguiente enfoque:

```cpp
if (!archivo.is_open())
{
    // Error al abrir el archivo
}
```

La función `is_open()` devuelve `true` si el archivo se abrió correctamente y `false` en caso contrario. Si el archivo no se abrió correctamente, se puede manejar el error de acuerdo con los requisitos de la aplicación.

### Metodos de Lectura

#### **Método: `get()`**&#x20;

El método `get()` se utiliza para leer un solo carácter del archivo. Retorna el carácter leído como un objeto de tipo `int` o `EOF` (End-Of-File) en caso de alcanzar el final del archivo.

```cpp
std::fstream archivo("datos.txt", std::ios::in);

char c;
archivo.get(c);  // Lee un solo carácter del archivo
if (archivo.good()) {
    std::cout << "Carácter leído: " << c << std::endl;
}
```

#### **Método: `getline()`**

El método `getline()` se utiliza para leer una línea completa del archivo y almacenarla en un objeto de tipo `std::string`. Permite especificar un delimitador opcional para determinar el final de la línea.

```cpp
std::fstream archivo("datos.txt", std::ios::in);

std::string linea;
std::getline(archivo, linea);  // Lee una línea completa del archivo
if (!linea.empty()) {
    std::cout << "Línea leída: " << linea << std::endl;
}
```

Permite especificar un delimitador opcional para determinar el final de la lectura.

```cpp
std::getline(archivo, cadena, ',');  // Lee una cadena hasta encontrar una coma
```

#### **Método: `read()`**

El método `read()` se utiliza para leer una cantidad específica de caracteres desde el archivo y almacenarlos en un búfer. Puedes especificar la cantidad de caracteres a leer y la ubicación de almacenamiento mediante un puntero.

```cpp
cppCopy codestd::fstream archivo("datos.txt", std::ios::in);

char buffer[256];
archivo.read(buffer, 255);  // Lee hasta 255 caracteres del archivo
buffer[255] = '\0';  // Agrega un terminador nulo
```

#### **Método: `operator>>`**

El operador de extracción `>>` se utiliza para leer datos numéricos desde un archivo. Puede ser utilizado con diferentes tipos de datos, como `int`, `float`, `double`, entre otros. Los datos leídos son asignados directamente a las variables proporcionadas.

```cpp
cppCopy codestd::fstream archivo("datos.txt", std::ios::in);

int numero;
archivo >> numero;  // Lee un número entero del archivo
if (archivo.good()) {
    std::cout << "Número leído: " << numero << std::endl;
}
```





### Metodos de escritura









### Manipulación de la posición de lectura/escritura

Cuando trabajas con archivos utilizando la clase `std::fstream` en C++, puedes manipular la posición de lectura y escritura en el archivo. Esto te permite desplazarte dentro del archivo para leer o escribir datos en ubicaciones específicas.

**seekg() - Establecer la posición de lectura**

El método `seekg()` se utiliza para establecer la posición de lectura en el archivo. Puedes especificar la posición a la que deseas desplazarte utilizando un desplazamiento relativo o absoluto. Aquí tienes un ejemplo:

```cpp
std::fstream archivo("datos.txt", std::ios::in);

// Desplazarse a la posición absoluta 50
archivo.seekg(50);

// Desplazarse 10 posiciones hacia adelante desde la posición actual
archivo.seekg(10, std::ios::cur);

// Desplazarse 20 posiciones hacia atrás desde el final del archivo
archivo.seekg(-20, std::ios::end);
```

En el ejemplo anterior, `seekg()` se utiliza para establecer la posición de lectura en diferentes ubicaciones del archivo. El primer argumento especifica el desplazamiento, mientras que el segundo argumento (opcional) indica desde dónde se realiza el desplazamiento (principio, posición actual o final del archivo).

**tellg() - Obtener la posición de lectura actual**

El método `tellg()` se utiliza para obtener la posición de lectura actual en el archivo. Devuelve un valor que representa la posición en bytes desde el principio del archivo. Aquí tienes un ejemplo:

```cpp
std::fstream archivo("datos.txt", std::ios::in);

// Obtener la posición de lectura actual
std::streampos posicion = archivo.tellg();

// Convertir la posición a un valor entero
int posicionEntera = static_cast<int>(posicion);
```

En el ejemplo anterior, `tellg()` se utiliza para obtener la posición de lectura actual en el archivo. Luego, se puede convertir la posición a un valor entero si es necesario.

**seekp() - Establecer la posición de escritura**

El método `seekp()` se utiliza para establecer la posición de escritura en el archivo. Funciona de manera similar a `seekg()`, pero se aplica a la posición de escritura en lugar de la posición de lectura. Aquí tienes un ejemplo:

```cpp
std::fstream archivo("datos.txt", std::ios::out);

// Desplazarse a la posición absoluta 100
archivo.seekp(100);

// Desplazarse 50 posiciones hacia adelante desde la posición actual
archivo.seekp(50, std::ios::cur);

// Desplazarse 10 posiciones hacia atrás desde el final del archivo
archivo.seekp(-10, std::ios::end);
```

En el ejemplo anterior, `seekp()` se utiliza para establecer la posición de escritura en diferentes ubicaciones del archivo.

**tellp() - Obtener la posición de escritura actual**

El método `tellp()` se utiliza para obtener la posición de escritura actual en el archivo. Funciona de manera similar a `tellg()`, pero se aplica a la posición de escritura en lugar de la posición de lectura. Aquí tienes un ejemplo:

```cpp
std::fstream archivo("datos.txt", std::ios::out);

// Obtener la posición de escritura actual
std::streampos posicion = archivo.tellp();

// Convertir la posición a un valor entero
int posicionEntera = static_cast<int>(posicion);
```

En el ejemplo anterior, `tellp()` se utiliza para obtener la posición de escritura actual en el archivo. Luego, se puede convertir la posición a un valor entero si es necesario.

#### Moverse a destiempo

Por defecto, el puntero de lectura (`get pointer`) y el puntero de escritura (`put pointer`) se encuentran en la misma posición al abrir un archivo en modo de lectura/escritura (`std::ios::in | std::ios::out`). Esto significa que, al realizar operaciones de lectura o escritura, ambas posiciones se actualizan automáticamente.

Sin embargo, puedes manipular los punteros de forma independiente utilizando los métodos `seekg()` y `seekp()` para establecer la posición de lectura y escritura respectivamente.
