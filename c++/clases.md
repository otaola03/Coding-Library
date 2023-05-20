# Clases

Las clases en C++ son un concepto fundamental en la programación orientada a objetos (POO). Proporcionan una forma estructurada de definir objetos que encapsulan datos y comportamiento relacionados. En este post, exploraremos las clases en C++ y aprenderemos cómo utilizarlas de manera efectiva.

### Definición de una clase en C++

Una clase en C++ se define utilizando la palabra clave `class` seguida del nombre de la clase. Aquí tienes un ejemplo básico de cómo se ve la definición de una clase en C++:

```cpp
class MiClase {
  // Miembros de la clase
};
```

Dentro de las clases podemos declarar tanto variables como funciones, aunque a las funciones. se les suelen llamar métodos. Aunque se puede definer el código y valores de las variables dentro de la clase es buena practica hacerlo en su correspondiente `.cpp`.

Es buena practica declarar las variables privadas de la clase con una barra baja, para poder diferecniarlas de l rresto de las variables.

```cpp
class MiClase {
  private:
    int  _name;
}; 
```

### Modificadores de acceso

Estos modificadores determinan la accesibilidad de los miembros (variables y funciones) de una clase y ayudan a establecer los niveles de encapsulamiento y protección en el código.

#### Modificador de acceso `public`

El modificador de acceso `public` permite que los miembros de una clase sean accesibles desde cualquier parte del programa, ya sea dentro o fuera de la clase. Esto significa que los miembros públicos son visibles para todos y pueden ser accedidos y modificados directamente.

> Los miembros públicos son accesibles desde cualquier parte del programa, tanto dentro como fuera de la clase.

```cpp
class MiClase {
public:
  int variablePublica;    // Variable miembro pública

  void funcionPublica() {
    // Código de la función miembro pública
  }
};
```

En este ejemplo, `variablePublica` es una variable miembro pública que se puede acceder y modificar directamente desde fuera de la clase. `funcionPublica` es una función miembro pública que también se puede llamar desde fuera de la clase.

El modificador de acceso `public` es útil cuando queremos permitir un acceso amplio a los miembros de la clase o cuando necesitamos que los miembros sean utilizados por otros componentes del programa.

#### Modificador de acceso `private`

El modificador de acceso `private` restringe el acceso a los miembros de una clase solo a la propia clase. Los miembros privados no pueden ser accedidos o modificados directamente desde fuera de la clase.

> Los miembros privados solo son accesibles desde dentro de la propia clase y no se pueden acceder directamente desde fuera de la clase

```cpp
class MiClase {
private:
  int variablePrivada;    // Variable miembro privada

  void funcionPrivada() {
    // Código de la función miembro privada
  }
};
```

En este ejemplo, `variablePrivada` es una variable miembro privada que solo puede ser accedida y modificada desde dentro de la clase. `funcionPrivada` es una función miembro privada que solo puede ser llamada desde dentro de la clase.

El modificador de acceso `private` es útil cuando queremos ocultar los detalles internos de una clase y restringir el acceso directo a los miembros. Esto nos permite tener un mayor control sobre cómo se manipulan los datos y evita modificaciones inapropiadas desde fuera de la clase.

#### Modificador de acceso `protected`

El modificador de acceso `protected` es similar al modificador `private`, ya que restringe el acceso a los miembros de una clase. Sin embargo, a diferencia de `private`, los miembros protegidos también pueden ser accedidos por las clases derivadas.

> Los miembros protegidos son accesibles desde dentro de la propia clase y en las clases derivadas, pero no se pueden acceder directamente desde fuera de la jerarquía de clases.

```cpp
class ClaseBase {
protected:
  int variableProtegida;  // Variable miembro protegida

  void funcionProtegida() {
    // Código de la función miembro protegida
  }
};

class ClaseDerivada : public ClaseBase {
public:
  void funcionDerivada() {
    variableProtegida = 10;  // Acceso a la variable protegida en la clase derivada
    funcionProtegida();      // Llamada a la función protegida en la clase derivada
  }
};
```

En este ejemplo, `variableProtegida` es una variable miembro protegida que puede ser accedida y modificada en la clase derivada `ClaseDerivada`, ya que se hereda de `ClaseBase`.

### Constructores y destructores

Los constructores y destructores son métodos especiales de una clase en C++ que se utilizan para inicializar y liberar recursos de un objeto, respectivamente.

#### Cosntructores y destructors predefinidios

Si no se proporciona un constructor personalizado, se generará automáticamente un constructor predeterminado sin parámetros. Este constructor simplemente inicializa las variables miembro con valores predeterminados.

Aun así, es buena practica declarar el constructor vacio, al igual que el destructor:

```cpp
class MiClase 
{
  public:
    MiClase()
    {
    }
    ~MiClasse()
    {
    }
};
```

#### Constructores y Destructores Personalizados en C++

Un constructor, al contrario que un destructor, puede tener parámetros, lo que nos permite inicializar las variables miembro con valores específicos al crear un objeto.

También Es posible definir un destructor personalizado para realizar tareas de limpieza específicas antes de que un objeto se destruya. Esto es especialmente útil cuando se han asignado recursos que deben ser liberados adecuadamente.

```cpp
class MiClase
{
  public:
    MiClase(int valorInicial)
    {
      // Código del constructor con parámetros
    }
    ~MiClase() {
    // Código del destructor personalizado
  }
};
```

### Getters y Setters

Los getters y setters son métodos utilizados para acceder y modificar los valores de variables miembro de una clase desde fuera de la misma. Proporcionan un mecanismo para encapsular el acceso a los datos y mantener el principio de ocultamiento de información en la programación orientada a objetos.

#### Getters

Un getter es un método que se utiliza para obtener el valor de una variable miembro de una clase. Su nombre suele comenzar con la palabra "get" seguida del nombre de la variable miembro.

```cpp
class MiClase {
private:
  int miVariable;

public:
  // Getter
  int getMiVariable() {
    return miVariable;
  }
};
```

En este ejemplo, se define un getter llamado `getMiVariable()` que devuelve el valor de la variable miembro `miVariable`.

#### Setters

Un setter es un método que se utiliza para modificar el valor de una variable miembro de una clase. Su nombre suele comenzar con la palabra "set" seguida del nombre de la variable miembro.

```cpp
class MiClase {
private:
  int miVariable;

public:
  // Setter
  void setMiVariable(int valor) {
    miVariable = valor;
  }
};
```

En este ejemplo, se define un setter llamado `setMiVariable()` que recibe un parámetro `valor` y asigna ese valor a la variable miembro `miVariable`.

### Static

La palabra clave `static` se utiliza en C++ para declarar elementos que son compartidos por todas las instancias de una clase en lugar de ser específicos de cada objeto individual. Estos elementos se asocian con la clase en sí y no con las instancias de la clase.

#### Variables estáticas

Una variable estática se declara utilizando la palabra clave `static` en el contexto de una clase. Estas variables existen en un solo lugar en la memoria, independientemente del número de objetos que se creen.

> Una variable estática es una variable global que se comparte entre todos los objetos y a al que puedes acceder sin haber declarado ningún objeto.

<pre class="language-cpp"><code class="lang-cpp">class MiClase {
<strong>private:
</strong>  static int contador;

public:
  // ...
};
</code></pre>

En este ejemplo, se declara una variable estática llamada `contador` dentro de la clase `MiClase`.

Las variables estáticas se acceden utilizando el nombre de la clase seguido del operador de resolución de ámbito (`::`). No es necesario crear una instancia de la clase para acceder a ellas.

```cpp
int MiClase::contador = 0; // Inicialización de la variable estática

// Acceso a la variable estática
int valor = MiClase::contador;
```

En este ejemplo, se inicializa y se accede a la variable estática `contador` de la clase `MiClase`.

#### Métodos estáticos

Un método estático es aquel que se declara utilizando la palabra clave `static`. Estos métodos no operan sobre objetos individuales, sino que se asocian con la clase en sí y no pueden acceder a variables miembro no estáticas.

```cpp
class MiClase {
public:
  static void metodoEstatico() {
    // Código del método estático
  }
};
```

En este ejemplo, se define un método estático llamado `metodoEstatico()` en la clase `MiClase`.

Los métodos estáticos se invocan utilizando el nombre de la clase seguido del operador de resolución de ámbito (`::`). No es necesario crear una instancia de la clase para invocarlos.

```cpp
MiClase::metodoEstatico(); // Invocación del método estático
```

En este ejemplo, se invoca el método estático `metodoEstatico()` de la clase `MiClase`.

\
