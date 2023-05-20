# Punteros a funciones

Los punteros a funciones, también conocidos como punteros a métodos, son una característica poderosa de C++ que permite almacenar y manipular direcciones de funciones.

Un puntero a función es una variable que almacena la dirección de una función en memoria. Al igual que los punteros a variables, los punteros a funciones nos permiten acceder y llamar a una función indirectamente.

La sintaxis básica para declarar un puntero a función es la siguiente:

```cpp
tipo_retorno (*nombre_puntero)(tipo_parametros);
```

Donde `tipo_retorno` es el tipo de dato que devuelve la función y `tipo_parametros` son los tipos de datos de los parámetros que recibe la función. `nombre_puntero` es el nombre que se le da al puntero a función.

### Uso de punteros a funciones

**Asignación de una función a un puntero**

Para asignar una función a un puntero a función, se puede utilizar el nombre de la función directamente, ya que el nombre de una función es en sí mismo un puntero a esa función.

```cpp
tipo_retorno funcion(tipo_parametros); // Declaración de una función
tipo_retorno (*puntero)(tipo_parametros) = funcion; // Asignación de la función al puntero
```

**Invocación de una función a través de un puntero**

Para invocar una función a través de un puntero a función, se utiliza el operador de invocación de función `()`.

```cpp
(*puntero)(argumentos); // Invocación de la función a través del puntero
```

**Uso de typedef para simplificar la sintaxis**

La sintaxis para declarar punteros a funciones puede volverse compleja. Para simplificarla, se puede utilizar el `typedef` para definir un nombre de tipo para el puntero a función.

```cpp
typedef tipo_retorno (*nombre_tipo)(tipo_parametros); // Definición de un nombre de tipo para el puntero
nombre_tipo puntero = funcion; // Asignación de la función al puntero
```

#### Ejemplo

```cpp
#include <iostream>

void Funcion(int valor) {
    std::cout << "El valor es: " << valor << std::endl;
}
int main() {
    void (*punteroSinTypedef)(int) = Funcion;
    (*punteroSinTypedef)(5);

    typedef void (*PunteroConTypedef)(int);
    PunteroConTypedef punteroConTypedef = Funcion;
    (*punteroConTypedef)(10);

    return 0;
}
```

En este ejemplo, declaramos un puntero a función llamado `punteroSinTypedef` sin utilizar typedef, y otro puntero a función llamado `punteroConTypedef` utilizando typedef.

Luego, definimos una función `Funcion` que será llamada a través de los punteros a función. En el `main`, asignamos la dirección de la función a cada puntero y los llamamos pasando un valor.

Ambos punteros a función se comportan de la misma manera y permiten llamar a la función `Funcion`. La única diferencia radica en la forma en que se declaran y utilizan.

### Punteros a metodos

Un puntero a método es una variable que almacena la dirección de un método de una clase en memoria. Al igual que los punteros a funciones, los punteros a métodos nos permiten acceder y llamar a un método indirectamente.

{% hint style="info" %}
Cuando el puntero a un método es parte de la clase, no es necesario crear un objeto adicional para asignarle un método.

Sin embargo, si el puntero no es parte de la clase, se requerirá un objeto válido de esa clase para asignarle un método.
{% endhint %}

La sintaxis básica para declarar un puntero a método es la siguiente:

```cpp
tipo_retorno (Clase::*nombre_puntero)(tipo_parametros);
```

Donde `tipo_retorno` es el tipo de dato que devuelve el método, `Clase` es el nombre de la clase a la que pertenece el método, `tipo_parametros` son los tipos de datos de los parámetros que recibe el método y `nombre_puntero` es el nombre que se le da al puntero a método.

{% hint style="info" %}
`Clase::*` es el tipo, es decir especifica que es una variable que guarda un puntero a una funcion de la clase `Clase.`
{% endhint %}

**Asignación de un método a un puntero**

Para asignar un método a un puntero a método, se utiliza la sintaxis `&Clase::nombre_metodo`. El operador `&` se utiliza para obtener la dirección del método.

```cpp
Clase objeto; // Creación de un objeto de la clase
tipo_retorno (Clase::*puntero)(tipo_parametros) = &Clase::nombre_metodo; // Asignación del método al puntero
```

**Invocación de un método a través de un puntero**

Para invocar un método a través de un puntero a método, se utiliza el operador `.*`. Se debe tener un objeto válido para poder llamar al método.

```cpp
(objeto.*puntero)(argumentos); // Invocación del método a través del puntero y el objeto
```
