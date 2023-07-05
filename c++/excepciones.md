# Excepciones

En la programación, las excepciones son situaciones inesperadas o errores que ocurren durante la ejecución de un programa. C++ proporciona un mecanismo para manejar estas excepciones, permitiendo al programador capturar y manejar los errores de manera controlada. En este post, exploraremos el concepto de excepciones en C++ y cómo se utilizan para el manejo de errores.

{% embed url="https://www.youtube.com/watch?v=5nCXSDv6e4I" %}

### Excepciones en C++

Las excepciones en C++ son objetos que se lanzan cuando se produce un error o una situación excepcional durante la ejecución de un programa. Estas excepciones se pueden lanzar en cualquier parte del código y se pueden capturar y manejar en bloques específicos.

Para lanzar una excepción en C++, se utiliza la palabra clave `throw`, seguida de un objeto que representa la excepción. Por ejemplo:

```cpp
throw MiExcepcion("Ocurrió un error");
```

En este ejemplo, se lanza una excepción de tipo `MiExcepcion` con un mensaje de error específico.

### Captura y manejo de excepciones

Para capturar y manejar una excepción en C++, se utiliza la estructura `try-catch`. El bloque `try` se utiliza para envolver el código que puede lanzar una excepción, mientras que el bloque `catch` se utiliza para capturar y manejar la excepción lanzada.

La sintaxis básica de `try-catch` en C++ es la siguiente:

```cpp
try {
    // Código que puede lanzar una excepción
}
catch (TipoExcepcion& e) {
    // Manejo de la excepción
}
```

En este ejemplo, el bloque `try` contiene el código que puede lanzar una excepción. Si se produce una excepción del tipo especificado en el bloque `catch`, el control del programa se transfiere al bloque `catch` correspondiente, donde se puede manejar la excepción de acuerdo a los requerimientos del programa.

### Clases de excepciones predefinidas

C++ proporciona una serie de clases de excepciones predefinidas que se pueden utilizar para representar diferentes tipos de errores. Algunas de las clases de excepciones más comunes son:

* `std::exception`: Clase base para todas las excepciones.
* `std::runtime_error`: Excepción que representa errores en tiempo de ejecución.
* `std::logic_error`: Excepción que representa errores lógicos o de programación.
* `std::out_of_range`: Excepción que se lanza cuando se intenta acceder a un índice fuera de rango.
* `std::bad_alloc`: Excepción que se lanza cuando hay problemas de asignación de memoria dinámica.

Estas clases de excepciones predefinidas se pueden utilizar tal como están o se pueden heredar para crear clases de excepciones personalizadas que se ajusten a las necesidades específicas del programa.

#### Jerarquia de excepciones

La jerarquía de excepciones en C++ se refiere a la organización de las excepciones en una estructura de árbol, donde las excepciones más generales se encuentran en la parte superior y las más específicas se encuentran en niveles inferiores. Esta jerarquía permite capturar y manejar diferentes tipos de excepciones de manera más precisa.

<figure><img src="../.gitbook/assets/Screen Shot 2023-06-11 at 6.22.50 PM.png" alt=""><figcaption></figcaption></figure>

La ventaja de tener una jerarquía de excepciones es que podemos capturar y manejar excepciones de manera más granular. Podemos capturar excepciones específicas en primer lugar y luego capturar excepciones más generales si es necesario. Esto nos permite tomar acciones diferentes según el tipo de error que se haya producido.

{% hint style="info" %}
Si hay una excepción de mayor jerarquia antes de cualquier otra, terminará siempre por entar en ese `catch`,  ya que engloba todos lo errores.
{% endhint %}

Por ejemplo:

```cpp
try {
    // Código que puede lanzar excepciones
} catch (const std::invalid_argument& e) {
    // Manejo de excepción de argumento inválido
} catch (const std::runtime_error& e) {
    // Manejo de excepción de tiempo de ejecución
} catch (const std::exception& e) {
    // Manejo de excepción genérica
} catch (...) {
    // Manejo de cualquier otra excepción no especificada
}
```

En este ejemplo, se capturan excepciones específicas primero, como `std::invalid_argument` y `std::runtime_error`, y luego se captura una excepción más genérica `std::exception` en caso de que no se haya capturado ninguna excepción específica.

La jerarquía de excepciones en C++ nos permite estructurar nuestro código de manejo de errores de manera más organizada y responder adecuadamente a diferentes situaciones de error.

### Excepciones personalizadas

Aunque C++ proporciona excepciones predefinidas, también es posible crear excepciones personalizadas para abordar situaciones específicas y mejorar la legibilidad y el mantenimiento del código.

#### **Creación de una excepción personalizada**

En C++, se pueden crear excepciones personalizadas mediante la creación de una clase que herede de la clase base `std::exception` o de una de sus subclases derivadas, como `std::runtime_error` o `std::logic_error`.

<pre class="language-cpp"><code class="lang-cpp">#include &#x3C;exception>
#include &#x3C;string>

class MiExcepcion : public std::exception
{
<strong>    public:
</strong>        const char* what() const throw() {return ("Excecpion Nº1");}
};
</code></pre>

En este ejemplo, hemos creado una excepción personalizada llamada `MiExcepcion` que hereda de `std::exception`. La función `what()` se sobrescribe para devolver el mensaje de la excepción cuando se produce un error.

{% hint style="info" %}
En la cabecera de la función `what()`, el `throw() e` una especificación opcional y su objetivo es indicar que la función `what()` no lanzará excepciones durante su ejecución.
{% endhint %}

En el caso de que qieras crear un tipo de excepcion que requeira de argumentos tendras que crear el constructor y destructor:

```cpp
#include <exception>
#include <string>

class MiExcepcion : public std::exception
{
    private:
        std::string mensaje;
    public:
        MiExcepcion(const std::string& nombre)
        {
            mensaje = "Error: " + nombre + " no existe";
        }
    
        const char* what() const throw()
        {
            return mensaje_.c_str();
        }
};
```

A la hora de crear el `mensaje` es necesario hacerlo en el constructor por que si intenamtos hacerlo en la funcion `what()` esta devovlera un puntero que se destruira nada mas terminar la funcion, pro lo que devlvera basura.

En el caso de que en el erro tan solo queiras devovelr el valor paso al cosntrutor el cosntrucotre se puede declarar de la siguiente manera:

```cpp
MiExcepcion(const std::string& mensaje): mensaje(mensaje) {}
```

#### **Lanzamiento y captura de una excepción personalizada**

Una vez que se ha creado una excepción personalizada, se puede lanzar utilizando la palabra clave `throw`. A continuación, se muestra un ejemplo de cómo lanzar y capturar una excepción personalizada:

```cpp
try
{
    x = 0;
    if (x == 0)
        throw ErrorDeDivision("Dvidir entre 0");
    int resultado = dividir(10, x);
}
catch (const ErrorDeDivision& e)
{
    std::cout << "Se produjo una excepción: " << e.what() << std::endl;
}
```

En este ejemplo, se intenta realizar una división por cero en la función `dividir()`. Si ocurre una excepción de tipo `MiExcepcion`, se captura en el bloque `catch` correspondiente y se muestra el mensaje de la excepción utilizando la función `what()`.
