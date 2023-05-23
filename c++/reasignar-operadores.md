# Reasignar operadores

La sobrecarga de operadores en C++ permite dar nuevos significados a los operadores existentes, como +, -, \*, /, etc., para trabajar con tipos de datos personalizados. Esto mejora la expresividad del código y nos permite utilizar los operadores de manera intuitiva con nuestros propios objetos. Es una característica importante que brinda flexibilidad y control en el diseño de nuestros programas.

### Sintaxis de la sobrecarga de operadores

La sobrecarga de operadores en C++ se realiza mediante la definición de funciones especiales llamadas "funciones de operador". Estas funciones tienen un nombre predefinido y siguen una sintaxis específica.

La sintaxis general para sobrecargar un operador es la siguiente:

```cpp
retorno operator operador (parámetros)
```

* `retorno`: especifica el tipo de dato que devuelve la función de operador.
* `operator`: es la palabra clave reservada que indica que se está sobrecargando un operador.
* `operador`: es el símbolo del operador que se va a sobrecargar, como +, -, \*, /, etc.
* `parámetros`: son los parámetros que toma la función de operador. Pueden ser de uno o más tipos, dependiendo del operador que se esté sobrecargando.

#### Explicación detallada de la sintaxis utilizada para sobrecargar operadores en C++

En C++, algunos operadores se pueden sobrecargar utilizando funciones de operador especiales. Estas funciones permiten definir cómo se comportará el operador cuando se aplique a objetos de un tipo personalizado.

Para sobrecargar un operador, debemos definir una función con el nombre y la firma adecuados. Por ejemplo, para sobrecargar el operador + para realizar una operación con un solo objeto de una clase personalizada, podríamos definir una función de operador de la siguiente manera:

```cpp
Clase operator+(const Clase& objeto) {
    // Implementación de la operación
}
```

En este ejemplo, `Clase` es el tipo de dato del objeto sobre el cual se aplica el operador +. La función de operador toma un único parámetro constante por referencia, que representa el objeto con el que se realizará la operación.

### Operadores aritméticos

Los operadores aritméticos en C++ se pueden sobrecargar para permitir operaciones personalizadas en clases personalizadas. A continuación, se describen los operadores aritméticos básicos y se muestran ejemplos de implementación para clases personalizadas.

La estructura de los operadores aritmeticos es de la siguiente manera:

```cpp
Clase operator+(const Clase& objeto) {
    // Implementación de la adición de objetos
}
```

Donde el operador puede ser:

* Operador de suma (+)
* Operador de resta (-)
* Operador de multiplicación (\*)
* Operador de división (/)

Aunque no haga falta, es buena practica crear por cada operador de asignnacion un metodo que realice esa operacion. Por ejemplo si queremos reasignar el `operador +`:

```cpp
struct Vector2
{
    float    x, y;
    
    Vector2(float x, float y) :x(x), y(y) {}
    
    Vector2 Add(const Vector2& other) const
    {
        return (Vector(x + other.x, y + other.y));
    }
    
    Vector2 operator+(const Vector2& other) const
    {
        return (Add(other));
    }
};
```

### Operadores de comparacion

En C++, los operadores de comparación se pueden sobrecargar para permitir comparaciones personalizadas entre objetos de clases personalizadas. A continuación, se describen los operadores de comparación comunes y se muestran ejemplos de su implementación para clases personalizadas.

La estructura de los operadores de comparacion es de la siguiente manera:

```cpp
bool operator==(const Clase& objeto) const {
    // Implementación de la comparación de igualdad
}
```

Donde el operador puede ser:

* Operador de igualdad (==)
* Operador de desigualdad (!=)
* Operador de menor que (<)
* Operador de mayor que (>)
* Operador de menor o igual que (<=)
* Operador de mayor o igual que (>=)

### Operadores de asignación

En C++, los operadores de asignación se pueden sobrecargar para permitir la asignación y operaciones de asignación personalizadas entre objetos de clases personalizadas. A continuación, se describen los operadores de asignación comunes y se muestran ejemplos de su implementación para clases personalizadas.

La estructura de los operadores aritmeticos es de la siguiente manera:

```cpp
Clase& operator=(const Clase& objeto) {
    // Implementación de la asignación
    return *this;
}
```

Donde el operador puede ser:

* Operador de asignacion (=)
* Operador de asignacion y suma (+=)
* Operador de asignacion y resta (-=)
* Operador de asignacion y multiplicación (\*=)
* Operador de asignacion y división (/=)

### Sobrecarga de operadores de incremento y decremento

Los operadores de incremento y decremento en C++ (`++` y `--`) se pueden sobrecargar para proporcionar un comportamiento personalizado en una clase. Aquí se explica cómo hacerlo:

**Operador de preincremento (++variable)**

La sobrecarga del operador de preincremento permite modificar el estado de un objeto antes de su uso.

```cpp
Tipo& operator++()
{
  // Implementación del preincremento
  // Modificar el estado del objeto
  return *this;
}
```

**Operador de postincremento (variable++)**

La sobrecarga del operador de postincremento devuelve una copia del objeto antes de incrementar su valor.

```cpp
Tipo operator++(int)
{
  Tipo copia = *this;
  // Implementación del postincremento
  // Modificar el estado del objeto
  return copia;
}
```

{% hint style="info" %}
En la sobrecarga del operador de postincremento (`variable++`), se le pasa un parámetro de tipo entero `int` para diferenciarlo del operador de preincremento (`++variable`).
{% endhint %}

**Operador de predecremento (--variable)**

La sobrecarga del operador de predecremento permite modificar el estado de un objeto antes de su uso.

```cpp
Tipo& operator--()
{
  // Implementación del predecremento
  // Modificar el estado del objeto
  return *this;
}
```

**Operador de postdecremento (variable--)**

La sobrecarga del operador de postdecremento devuelve una copia del objeto antes de decrementar su valor.

```cpp
Tipo operator--(int)
{
  Tipo copia = *this;
  // Implementación del postdecremento
  // Modificar el estado del objeto
  return copia;
}
```

Recuerda que al sobrecargar estos operadores, es importante seguir las convenciones y prácticas adecuadas, y garantizar un comportamiento consistente y predecible. Además, ten en cuenta las reglas de semántica de los operadores de incremento y decremento para asegurarte de que tu implementación cumpla con las expectativas.

### Operadores de entrada y salida

Los operadores de entrada (`>>`) y salida (`<<`) permiten la sobrecarga de los flujos de entrada y salida en C++. Estos operadores son especialmente útiles para trabajar con objetos personalizados y facilitar su lectura desde flujos de entrada o imprimir su representación en flujos de salida.

#### Sobrecarga del operador de entrada (`>>`)

La sintaxis para sobrecargar el operador de entrada es la siguiente:

```cpp
std::istream& operator>>(std::istream& is, Clase& objeto) {
    // Implementación de la lectura de datos desde el flujo de entrada
    return is;
}
```

En esta sintaxis, `std::istream&` representa una referencia al flujo de entrada, que generalmente es `std::cin`. `Clase& objeto` es una referencia al objeto de la clase que se va a leer desde el flujo de entrada.

Dentro de la implementación del operador de entrada, se deben leer los valores necesarios del flujo de entrada y asignarlos al objeto pasado como referencia (`objeto`). Esto puede implicar la lectura de diferentes tipos de datos y el manejo de errores de entrada incorrecta.

Al finalizar la lectura, se debe devolver la referencia al flujo de entrada (`is`) para permitir la encadenación de operaciones de entrada.

#### Sobrecarga del operador de salida (`<<`)

La sintaxis para sobrecargar el operador de salida es la siguiente:

```cpp
std::ostream& operator<<(std::ostream& os, const Clase& objeto) {
    // Implementación de la impresión del objeto en el flujo de salida
    // os << Accion
    return os;
}
```

En esta sintaxis, `std::ostream&` representa una referencia al flujo de salida, que puede ser `std::cout`, `std::cerr`, u otro flujo de salida personalizado. `const Clase& objeto` es una referencia constante al objeto de la clase que se va a imprimir en el flujo de salida.

Dentro de la implementación del operador de salida, se deben imprimir los valores relevantes del objeto en el flujo de salida. Esto puede implicar la impresión de diferentes tipos de datos y el formateo adecuado de la salida.

Al finalizar la impresión, se debe devolver la referencia al flujo de salida (`os`) para permitir la encadenación de operaciones de salida.

La sobrecarga de los operadores de entrada y salida permite una integración más fluida de los objetos personalizados con los flujos de entrada y salida estándar en C++. Esto facilita la lectura de objetos desde el usuario o la impresión de objetos en la consola o en archivos de salida.
