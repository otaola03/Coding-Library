# Templates

normales, array, funciones, clases

Las plantillas son una característica clave en lenguajes de programación como C++, Java y Python. Permiten escribir funciones y clases que pueden trabajar con tipos de datos genéricos en lugar de tipos específicos. Esto significa que puedes escribir código que funcione para diferentes tipos de datos sin tener que duplicar el código.

### Sintaxis

Las plantillas se definen usando la palabra clave `template` seguida de una lista de parámetros de plantilla entre ángulos (`<>`). Aquí tienes un ejemplo básico:

```cpp
template <typename T>
T Suma(T a, T b) {
    return a + b;
}
```

#### Parámetros de Plantilla: `typename` vs. `class`

En la definición de plantillas, puedes usar las palabras clave `typename` o `class` para indicar que un identificador es un parámetro de plantilla. Ambos cumplen la misma función y se pueden usar indistintamente en la mayoría de los casos. Por ejemplo, las siguientes dos definiciones son equivalentes:

```cpp
template <typename T>
void MiFuncion(T parametro) {
    // Código de la función
}
```

```cpp
template <class T>
void MiFuncion(T parametro) {
    // Código de la función
}
```

#### Plantillas con Varios Tipos de Datos

Las plantillas en C++ no se limitan a trabajar con un solo tipo de dato. Puedes ampliar su potencia utilizando plantillas con múltiples parámetros, lo que te permite crear código genérico que funciona con varios tipos de datos de manera simultánea.

```cpp
template <typename Tipo1, typename Tipo2, ...>
```

### Plantillas de Funciones

Las plantillas de funciones son una característica esencial en C++ que te permiten crear funciones genéricas capaces de trabajar con diferentes tipos de datos.

#### Creación y Uso de Funciones de Plantilla

Crear una función de plantilla es similar a crear una función normal, pero en lugar de un tipo de dato específico, utilizamos un parámetro de plantilla. Esto nos permite trabajar con múltiples tipos de datos sin tener que duplicar el código. Aquí tienes la estructura básica de una función de plantilla:

```cpp
template <typename Tipo>
Tipo MiFuncion(Tipo parametro) {
    // Código de la función
}
```

Luego, puedes usar la función de plantilla con diferentes tipos de datos según sea necesario:

```cpp
int resultadoEntero = MiFuncion(5);
double resultadoFlotante = MiFuncion(3.14);
```

#### Especialización de Plantillas de Funciones

En ciertos casos, puedes necesitar proporcionar una implementación especializada de una función de plantilla para un tipo de dato específico. Esto se llama especialización de plantillas. Por ejemplo:

```cpp
template <>
int Maximo<int>(int a, int b) {
    return (std::abs(a) > std::abs(b)) ? a : b;
}
```

Esta especialización de la función `Maximo` permite encontrar el valor absoluto máximo en lugar del valor numérico máximo.

### Plantillas de Clases

Las plantillas de clases son una característica poderosa en C++ que te permiten crear estructuras de datos y abstracciones genéricas capaces de trabajar con varios tipos de datos.

Al igual que con las funciones de plantilla, las clases de plantilla se definen utilizando la palabra clave `template` seguida de uno o más parámetros de plantilla. Estos parámetros pueden ser tipos de datos o valores no tipo. Aquí tienes la estructura básica de una clase de plantilla:

```cpp
template <typename Tipo>
class MiClase {
public:
    // Métodos y miembros de la clase
};
```

#### Ejemplos de Clases que Trabajan con Tipos Genéricos

```cpp
cppCopy codetemplate <typename T>
class Pila {
public:
    Pila() : tope(-1) {}

    void Empujar(T elemento) {
        elementos[++tope] = elemento;
    }

    T Sacar() {
        return elementos[tope--];
    }

private:
    T elementos[100];
    int tope;
};

int main() {
    Pila<int> pilaEnteros;
    pilaEnteros.Empujar(5);

    Pila<double> pilaFlotantes;
    pilaFlotantes.Empujar(3.14);

    return 0;
}
```

Como puedes observar a la hora de crear la clase es necesario especificar el tipo de dato que se va a utilizar en la plantilla. Con las funciones tambien se puede hacer, pero no es necesario.

#### Especialización de Plantillas de Clases

En ciertos casos, es posible que desees proporcionar una implementación especializada de una clase de plantilla para un tipo de dato específico. Esto se llama especialización de plantillas de clases. Por ejemplo:

```cpp
template <typename T>
class MiClase {
public:
    void Mostrar() {
        std::cout << "Valor genérico: " << valor << std::endl;
    }

private:
    T valor;
};

template <>
class MiClase<int> {
public:
    void Mostrar() {
        std::cout << "Valor especializado para enteros: " << valor << std::endl;
    }

private:
    int valor;
};
```

La clase `MiClase` tiene una versión genérica que puede manejar cualquier tipo de dato, y una versión especializada específica para enteros.

### Especialización de Plantillas (h2)

La especialización de plantillas es una característica avanzada en C++ que te permite proporcionar una implementación específica de una plantilla para un tipo de dato particular. Esto es útil cuando deseas ajustar el comportamiento de una plantilla para un caso específico o cuando necesitas optimizar el código para ciertos tipos de datos.

```cpp
template <typename T>
T Maximo(T a, T b) {
    return (a > b) ? a : b;
}

template <>
int Maximo<int>(int a, int b) {
    return (std::abs(a) > std::abs(b)) ? a : b;
}

int main() {
    int resultado = Maximo(5, -10); // Devuelve -10 debido a la especialización
    return 0;
}
```

#### Cómo y Cuándo Especializar Plantillas

La especialización de plantillas se logra al proporcionar una implementación alternativa de una plantilla para un tipo de dato específico. Puedes especializar tanto funciones como clases de plantilla. Para especializar una plantilla, debes seguir estos pasos:

1. Utiliza la palabra clave `template<>` para indicar que estás haciendo una especialización.
2. Especifica el tipo de dato para el que estás haciendo la especialización.
3. Proporciona la implementación especializada.

#### Especialización Parcial vs. Completa

La especialización puede ser parcial o completa:

* **Especialización Parcial**: Proporcionas una implementación especializada para algunos parámetros de plantilla mientras mantienes la implementación genérica para otros. Por ejemplo, puedes especializar una función de plantilla solo para tipos numéricos.
* **Especialización Completa**: Proporcionas una implementación especializada para un tipo de dato específico, reemplazando completamente la implementación genérica.

La elección entre especialización parcial y completa depende de tu necesidad. La especialización parcial puede ser útil cuando deseas ajustar ciertos aspectos del comportamiento de la plantilla, mientras que la especialización completa es apropiada cuando el comportamiento debe ser completamente diferente para un tipo de dato específico.

### Parámetros No Tipo en Plantillas (h2)

En el contexto de las plantillas en C++, es posible utilizar valores no tipo como parámetros, lo que amplía la versatilidad y capacidad de personalización de las plantillas. A diferencia de los parámetros de tipo, los parámetros no tipo permiten la inclusión de valores constantes como argumentos de plantilla.

#### Uso de Parámetros No Tipo en Plantillas

Los parámetros no tipo son constantes definidas en tiempo de compilación que actúan como argumentos de plantilla. Pueden ser utilizados para especificar tamaños de arreglos, valores constantes, y más.

Para usar un valor no tipo como parámetro de plantilla, declaramos el parámetro utilizando la palabra clave `typename` o `class`, seguido del tipo de valor no tipo deseado:

```cpp
template <int Potencia>
double PotenciaNumero(double base) {
    double resultado = 1.0;
    for (int i = 0; i < Potencia; ++i) {
        resultado *= base;
    }
    return resultado;
}
```

#### Aplicación de Parámetros No Tipo y Constantes

Los parámetros no tipo también pueden ser utilizados como constantes en el código, lo que permite realizar optimizaciones y tomar decisiones en tiempo de compilación. A continuación, se muestra un ejemplo:

```cpp
template <int Tam>
struct Contenedor {
    int datos[Tam];

    Contenedor() {
        for (int i = 0; i < Tam; ++i) {
            datos[i] = 0;
        }
    }
};
```

En este caso, `Tam` es un parámetro no tipo utilizado para determinar el tamaño del arreglo en la estructura `Contenedor`. Esto permite que el tamaño del arreglo sea conocido en tiempo de compilación y optimiza la creación del objeto `Contenedor`.
