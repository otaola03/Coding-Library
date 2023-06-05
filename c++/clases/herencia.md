# Herencia

La herencia es uno de los conceptos fundamentales en la programación orientada a objetos (POO) y desempeña un papel crucial en el lenguaje de programación C++. Permite la creación de relaciones entre clases, lo que a su vez promueve la reutilización de código y facilita la organización y el mantenimiento del software.

### Sintaxis de la herencia en C++

La sintaxis para definir una clase derivada en C++ es la siguiente:

```cpp
class ClaseDerivada : public ClaseBase {
    // Definición de miembros y funciones de la clase derivada
};
```

La palabra clave `public` indica que la clase derivada hereda públicamente de la clase base. Esto significa que los miembros públicos y protegidos de la clase base se mantienen accesibles en la clase derivada.

#### Herencia mutliple

En C++, la herencia múltiple nos permite crear una clase derivada que hereda de múltiples clases base. Esto nos brinda la capacidad de combinar características y comportamientos de varias clases en una sola clase derivada. La sintaxis para heredar de múltiples clases base es la siguiente:

```cpp
class ClaseDerivada : public ClaseBase1, public ClaseBase2, ...
{
    // Cuerpo de la clase derivada
};
```

### Acceso a miembros heredados

En una relación de herencia, los miembros heredados se comportan de diferentes formas en función de su nivel de acceso en la clase base:

* Los miembros **públicos** de la clase base son accesibles directamente desde la clase derivada y también desde el código externo.
* Los miembros **protegidos** de la clase base son accesibles desde la clase derivada, pero no son accesibles desde el código externo.
* Los miembros **privados** de la clase base no son accesibles desde la clase derivada ni desde el código externo.

### Nivel de acceso en la declaración de la clase derivada

Cuando declaramos una clase derivada en C++, utilizamos `public`, `private` o `protected` para especificar el nivel de acceso a la clase base. Esto determina cómo los miembros heredados serán tratados en la clase derivada:

> Establece el nivel de proteccion que se le aplicara a los miembros heredados.

* `public` mantiene los miembros públicos de la clase base como públicos en la clase derivada, permitiendo el acceso desde la clase derivada y el código externo.
* `private` convierte los miembros públicos y protegidos de la clase base en miembros privados en la clase derivada, restringiendo el acceso solo a la clase derivada.
* `protected` convierte los miembros públicos de la clase base en miembros protegidos en la clase derivada, limitando el acceso a la jerarquía de clases derivadas.

La elección del nivel de acceso en la declaración de la clase derivada es importante para controlar la visibilidad y el alcance de los miembros heredados, y garantizar una encapsulación adecuada en el diseño de la clase derivada.

### Los Problemas del Diamante en la Herencia Múltiple

La herencia múltiple en C++ permite que una clase derivada herede de dos o más clases base. Sin embargo, esta característica puede dar lugar a dos problemas comunes conocidos como el problema de llamada a funciones ambigua y el problema de la doble instancia. Exploraremos estos problemas en detalle y cómo se pueden resolver.

```
        ClaseBase
       /         \
ClaseDerivada1   ClaseDerivada2
       \         /
        ClaseFinal
```

#### El Problema de Llamada a Funciones Ambigua

El problema de llamada a funciones ambigua ocurre cuando una clase derivada hereda de dos o más clases base que tienen una función con el mismo nombre. Esto crea una ambigüedad en la llamada a la función desde la clase derivada. Veamos un ejemplo:

```cpp
class ClaseBase
{
public:
    void MiFuncion() { /* Implementación en ClaseBase */ }
};

class ClaseDerivada1 : public ClaseBase
{
public:
    // ...
};

class ClaseDerivada2 : public ClaseBase
{
public:
    // ...
};

class ClaseFinal : public ClaseDerivada1, public ClaseDerivada2
{
public:
    void Ejemplo()
    {
        // Ambigüedad: ¿Cuál función MiFuncion se debe llamar?
        MiFuncion();
    }
};
```

En este caso, la clase `ClaseFinal` hereda de `ClaseDerivada1` y `ClaseDerivada2`, ambas a su vez heredan de `ClaseBase` y tienen una función llamada `MiFuncion()`. Al intentar llamar a `MiFuncion()` desde `ClaseFinal`, se produce una ambigüedad.

Para resolver este problema, se puede especificar el alcance de la clase base al llamar a la función. En el ejemplo anterior, podemos utilizar `ClaseBase::MiFuncion()` dentro de `ClaseFinal` para indicar al compilador cuál versión de la función debe ser llamada y así evitar la ambigüedad.

```cpp
class ClaseFinal : public ClaseDerivada1, public ClaseDerivada2
{
public:
    void Ejemplo()
    {
        ClaseDerivada1::MiFuncion(); // Acceso a la versión de ClaseDerivada1
    }
};
```

#### El Problema de la Doble Instancia

El problema de la doble instancia ocurre cuando una clase derivada hereda de dos o más clases base que comparten una misma clase base común. Esto resulta en la creación de múltiples instancias de la clase base en la clase derivada, lo que puede llevar a errores y problemas de duplicación de datos. Veamos un ejemplo:

```cpp
class ClaseBase
{
    int datos;
public:
    // ...
};

class ClaseDerivada1 : public ClaseBase
{
    // ...
};

class ClaseDerivada2 : public ClaseBase
{
    // ...
};

class ClaseFinal : public ClaseDerivada1, public ClaseDerivada2
{
    // ...
};
```

En este caso, `ClaseFinal` hereda tanto de `ClaseDerivada1` como de `ClaseDerivada2`, ambas a su vez heredan de `ClaseBase`. Debido a esta estructura, `ClaseFinal` contiene dos instancias separadas de `ClaseBase`, lo que puede ocasionar problemas al acceder a los datos y comportamientos heredados de `ClaseBase`.

Para resolver este problema, se utiliza la técnica de **herencia virtual**. Al declarar la herencia de la clase base como virtual en las clases derivadas, se evita la duplicación de instancias de la clase base. La herencia virtual se realiza de la siguiente manera:

```cpp
class ClaseBase
{
    // ...
};

class ClaseDerivada1 : public virtual ClaseBase
{
    // ...
};

class ClaseDerivada2 : public virtual ClaseBase
{
    // ...
};

class ClaseFinal : public ClaseDerivada1, public ClaseDerivada2
{
    // ...
};
```

Con el uso de la herencia virtual, `ClaseFinal` contendrá una única instancia de `ClaseBase`, resolviendo los problemas del diamante y permitiendo un acceso correcto a los miembros heredados.
