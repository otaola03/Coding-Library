# Clases abstractas y Interfaces

Tanto las clases abstractas como las interfaces proporcionan una forma de establecer una interfaz común y definir comportamientos que deben ser implementados por las clases derivadas. Sin embargo, existen algunas diferencias clave entre estos dos conceptos.

### Clases virtuales puras

Las clases virtuales puras son clases que contienen al menos una función miembro virtual pura. Una función virtual pura se declara en la clase base pero no se implementa en ella.

La declaración de una función virtual pura se realiza agregando `= 0` al final de la declaración de la función en la clase base. Por ejemplo:

```cpp
class Base {
public:
    virtual void funcionPura() = 0;
};
```

El propósito principal de las clases virtuales puras es definir una interfaz común que las clases derivadas deben seguir. Estas clases proporcionan una estructura jerárquica y permiten el polimorfismo en el código.

Las clases virtuales puras no se pueden instanciar directamente, solo se utilizan como clases base para crear subclases que implementen las funciones virtuales puras. Las subclases deben proporcionar una implementación para todas las funciones virtuales puras de la clase base.

### Clases abstractas

En C++, una clase abstracta es una clase que contiene al menos una función virtual pura. Las clases abstractas se utilizan para crear una interfaz común que debe ser implementada por las clases derivadas.

#### Definición de una Clase Abstracta

Para definir una clase abstracta, se deben seguir los siguientes pasos:

1. Declarar al menos una función virtual pura en la clase base.
2. Evitar proporcionar una implementación para la función virtual pura en la clase base.
3. Utilizar la clase abstracta como base para derivar clases concretas.

Aquí hay un ejemplo de cómo se ve la definición de una clase abstracta en C++:

```cpp
class AbstractClass {
public:
    virtual void doSomething() = 0; // Función virtual pura
    virtual ~AbstractClass() {} // Destructor virtual (opcional)
};
```

#### Uso de Clases Abstractas

Las clases abstractas se utilizan como interfaces para garantizar una implementación coherente de ciertos métodos en las clases derivadas. Las clases que heredan de una clase abstracta deben proporcionar una implementación para todas las funciones virtuales puras heredadas.

Aquí hay un ejemplo que ilustra el uso de una clase abstracta:

```cpp
class Base {
public:
    virtual void print() = 0;
};

class Derived : public Base {
public:
    void print() override {
        std::cout << "Imprimiendo desde Derived" << std::endl;
    }
};

int main() {
    Derived d;
    d.print(); // Imprime: "Imprimiendo desde Derived"
    return 0;
}
```

{% hint style="info" %}
La palabra reservada `override` se utiliza para aportar clarided y esta solo disponible a partir de C++ 11
{% endhint %}

En este ejemplo, la clase `Base` es una clase abstracta con una función virtual pura `print()`. La clase `Derived` hereda de `Base` y proporciona una implementación concreta para `print()`. Al crear un objeto de `Derived` y llamar al método `print()`, se ejecutará la implementación definida en `Derived`.

#### Beneficios del Uso de Clases Abstractas

Las clases abstractas ofrecen varios beneficios en el diseño de programas en C++:

1. Permiten definir interfaces comunes: Las clases abstractas proporcionan una interfaz común que las clases derivadas deben implementar. Esto asegura que las clases derivadas cumplan con un conjunto específico de funciones.
2. Facilitan la extensibilidad: Al utilizar clases abstractas como interfaces, es más fácil agregar nuevas funcionalidades al sistema sin tener que modificar las clases existentes. Simplemente se crean nuevas clases derivadas que implementan la interfaz.
3. Promueven la modularidad: Al definir una clase abstracta, se establecen los requisitos mínimos para cualquier clase derivada. Esto fomenta la modularidad del código y facilita su mantenimiento.

Las clases abstractas proporcionan una forma de establecer una interfaz común y definir un conjunto de funciones que deben ser implementadas por las clases derivadas. Sin embargo, una clase abstracta **puede contener también funciones concretas que ya tienen una implementación**. Las clases derivadas de una clase abstracta heredarán tanto las funciones virtuales puras como las funciones concretas.

### Iterfaces

&#x20;Una interfaz es un conjunto de métodos abstractos que definen un contrato para las clases que la implementan. En C++, aunque no hay una construcción específica llamada "interfaz", podemos lograr el mismo concepto utilizando clases abstractas y funciones virtuales puras. En este artículo, exploraremos qué son las interfaces en C++ y cómo se utilizan.

#### Clases abstractas como interfaces&#x20;

En C++, una interfaz se puede lograr utilizando una clase abstracta. Una clase abstracta es una clase que contiene al menos una función virtual pura. Estas clases se utilizan para definir una interfaz común que varias clases pueden implementar. No se pueden instanciar directamente, solo se pueden utilizar como base para otras clases concretas.

#### Definiendo una interfaz

Para definir una interfaz en C++, creamos una clase abstracta que contiene funciones virtuales puras. Una función virtual pura se declara utilizando el modificador "virtual" y se le asigna el valor "0" al final de su declaración. Por ejemplo:

```cpp
cppCopy codeclass IShape {
public:
    virtual void draw() const = 0;
    virtual double getArea() const = 0;
};
```

En este caso, `IShape` se considera una interfaz que define los métodos `draw()` y `getArea()`. Las clases que implementen esta interfaz deberán proporcionar una implementación para estos métodos.

#### Beneficios de las interfaces (h2)

* **Abstracción y modularidad:** Las interfaces permiten definir contratos claros y abstractos para las clases. Esto promueve una separación clara de responsabilidades y facilita la modularidad en el diseño del código.
* **Polimorfismo:** Las interfaces permiten tratar objetos de diferentes clases pero que implementan la misma interfaz de manera uniforme. Esto facilita el uso de polimorfismo y el intercambio de objetos en tiempo de ejecución.
* **Flexibilidad y mantenibilidad:** Al programar con interfaces, se puede cambiar fácilmente la implementación de una clase sin afectar otras partes del código que dependen de la interfaz. Esto hace que el código sea más flexible y fácil de mantener.

### Diferencias entre Clases Abstractas e Interfaces (h2)

Aunque las clases abstractas y las interfaces tienen similitudes en términos de definir una interfaz común y establecer comportamientos que deben ser implementados, existen algunas diferencias importantes:

1. **Implementación**: Las clases abstractas pueden contener tanto funciones virtuales puras como funciones concretas, lo que les permite proporcionar una implementación por defecto para algunas funciones. Las interfaces, por otro lado, solo contienen funciones virtuales puras y no tienen implementaciones concretas.
2. **Herencia**: Una clase puede heredar de una sola clase abstracta, pero puede implementar múltiples interfaces. Esto significa que una clase puede tener una relación de herencia más específica con una clase abstracta y una relación de implementación con una o varias interfaces.
3. **Flexibilidad**: Las clases abstractas permiten definir comportamientos comunes y proporcionar implementaciones por defecto, lo que puede ser útil cuando se desea compartir código común entre las clases derivadas. Las interfaces, en cambio, se centran en definir una interfaz común y no proporcionan ninguna implementación por defecto.
4. **Uso**: Las clases abstractas se utilizan cuando se desea establecer una jerarquía de clases y compartir funcionalidad común. Las interfaces se utilizan cuando se desea definir una interfaz común que varias clases pueden implementar, independientemente de su jerarquía.
