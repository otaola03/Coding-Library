# Abstraccion

La abstracción es un principio fundamental en la Programación Orientada a Objetos (POO) que permite representar conceptos complejos de manera simplificada en el código. En lugar de tratar con todos los detalles y complejidades de un objeto del mundo real, la abstracción se centra en identificar las características esenciales y modelarlas a través de clases y objetos en el código.

{% embed url="https://www.youtube.com/watch?v=L1-zCdrx8Lk&list=PLxvooGgpi4NeugSB4Pk546MXTPmGqPdc4&index=5" %}

### **Características Clave de la Abstracción**

1. **Identificación de Características Esenciales:** La abstracción implica identificar las propiedades y comportamientos esenciales de un objeto, dejando de lado los detalles menos relevantes.
2. **Creación de Modelos Conceptuales:** A través de clases y objetos, se crean modelos conceptuales que representan entidades del mundo real de manera simplificada.
3. **Ocultamiento de Detalles de Implementación:** Los detalles internos de implementación se ocultan, permitiendo a los desarrolladores interactuar con los objetos a través de interfaces claras y bien definidas.

En resumen, la astraccion se encarga de simplificar los conceptos de manera modular para que asi a la hora de utulizar uno de estos modulos tan solo te tengas que saber cual es el input y el ouput del modulo, si necesidad de entender su funcionamiento interno.

### Clases Abstractas

Las clases abstractas son un tipo de clases que proporcionan una forma de abstraer conceptos y definir comportamientos comunes, fomentando la reutilización de código en el diseño de software. Estas, a diferencia de las clases normales, no pueden se instanciadas y se delcaran añadiendo la palabra `abstract` a la declaracion de la clase.

#### **Características Clave de Clases Abstractas:**

1. **Métodos Abstractos:** Las clases abstractas pueden contener métodos abstractos, que son declarados pero no implementados en la clase abstracta. Las clases derivadas deben proporcionar implementaciones concretas para estos métodos.
2. **Métodos Concretos:** Además de los métodos abstractos, las clases abstractas pueden contener métodos concretos (implementados), proporcionando funcionalidades compartidas que las clases derivadas pueden heredar.
3. **No se Pueden Instanciar Directamente:** Una clase abstracta no puede ser instanciada directamente. Debe ser subclasificada, y sus métodos abstractos deben ser implementados en las clases derivadas antes de poder crear objetos de esas clases.

#### Ejemplo

```java
// Clase abstracta Animal
public abstract class Animal {
    private String nombre;

    // Constructor
    public Animal(String nombre) {
        this.nombre = nombre;
    }

    // Método abstracto que debe ser implementado por las clases derivadas
    abstract void hacerSonido();

    // Método concreto
    public void saludar() {
        System.out.println("Hola, soy un animal llamado " + nombre);
    }
}

// Clase derivada Gato
public class Gato extends Animal {
    // Constructor que invoca al constructor de la clase base (Animal)
    public Gato(String nombre) {
        super(nombre);
    }

    // Implementación del método abstracto hacerSonido
    void hacerSonido() {
        System.out.println("Miau, miau");
    }
}

// Clase principal para probar el código
public class Main {
    public static void main(String[] args) {
        // Crear un objeto de la clase Gato
        Gato miGato = new Gato("Pelusa");

        // Llamar a métodos de la clase Gato
        miGato.saludar();
        miGato.hacerSonido();
    }
}
```

En este ejemplo, la clase `Animal` es abstracta y contiene un método abstracto `hacerSonido()`, que debe ser implementado por cualquier clase que herede de ella. La clase derivada `Gato` extiende `Animal` y proporciona una implementación específica para el método abstracto. La clase principal (`Main`) crea un objeto `Gato`, llama a sus métodos y también trata el objeto como un `Animal` para demostrar la polimorfia.

#### Abstraccion y clases abstractas

Es importante aclarar la diferencia entre el concepto de abstracción en la Programación Orientada a Objetos (POO) y una clase abstracta, ya que no son lo mismo.

* **Abstracción en POO:**
  * La abstracción en POO se refiere al proceso de simplificar y modelar conceptos del mundo real en términos de clases y objetos. Se trata de identificar las características esenciales de un objeto y representarlas en el código sin preocuparse por los detalles de implementación.
  * Ejemplo: Tener una clase `Vehiculo` para representar el concepto abstracto de un vehículo, sin especificar si es un automóvil, una bicicleta o un avión.
* **Clase Abstracta:**
  * Una clase abstracta en POO es una clase que no puede ser instanciada directamente y puede contener tanto métodos abstractos (sin implementación) como métodos concretos (con implementación).
  *   Ejemplo:

      ```java
      abstract class Animal {
          abstract void hacerSonido();
          void dormir() {
              System.out.println("El animal está durmiendo");
          }
      }
      ```

En resumen, mientras que la abstracción en POO es un concepto más amplio que implica simplificar y modelar conceptos, una clase abstracta es una implementación específica en la que se pueden tener tanto métodos abstractos como concretos para representar un nivel intermedio entre una interfaz y una clase concreta.

### Interfaces

Las interfaces son un componente clave de la Programación Orientada a Objetos (POO) en Java, ofreciendo una manera de definir metodos predefinidos (sin implementar) para las clases que las implementen. Es decir, es una manera de lograr que varias clases tengas los mismos metodos y variables.

#### **Características Clave de las Interfaces:**

1. **Declaración de Métodos Abstractos:** Las interfaces permiten la declaración de métodos abstractos, que deben ser implementados por cualquier clase que las implemente. (Todos sus metodos son `abstract`, no hace falta especificarlo)
2. **Constantes:** Además de los métodos, las interfaces pueden contener constantes (variables con valores que no cambian), que son implícitamente `public`, `static`, y `final`.
3. **Implementación por Múltiples Clases:** Una clase puede implementar múltiples interfaces. Esto permite que una clase adquiera múltiples comportamientos sin necesidad de herencia múltiple.

#### **Ejemplo Práctico:**

Supongamos que estamos modelando vehículos con la interfaz `Vehiculo`:

```java
// Interfaz Vehiculo
public interface Vehiculo {
    void acelerar();  // Método abstracto
    void frenar();    // Método abstracto

    // Constantes
    int VELOCIDAD_MAXIMA = 120;
    String TIPO_COMBUSTIBLE = "Gasolina";
}

// Clase que implementa la interfaz Vehiculo
public class Automovil implements Vehiculo {
    // Implementación de los métodos de la interfaz
    @Override
    public void acelerar() {
        System.out.println("Automóvil acelerando");
    }

    @Override
    public void frenar() {
        System.out.println("Automóvil frenando");
    }

    // Puede tener sus propios métodos y atributos
    public void encenderLuces() {
        System.out.println("Luces encendidas");
    }
}
```

La anotación `@Override` ayuda a prevenir errores y mejorar la legibilidad del código al indicar claramente que se está sobrescribiendo un método de la interfaz.

#### **Ventajas de las Interfaces:**

* **Desacoplamiento:** Permiten el desacoplamiento entre las interfaces y las implementaciones, facilitando cambios sin afectar otras partes del código.
* **Reusabilidad del Código:** Dado que una clase puede implementar múltiples interfaces, se facilita la reutilización de código y la adición de nuevas funcionalidades.
* **Flexibilidad:** Proporcionan una manera flexible de definir comportamientos compartidos por diferentes clases, permitiendo una fácil extensión.

### Clases Abstractas Vs Interfaces

Las clases abstractas e interfaces en Java son elementos fundamentales de la programación orientada a objetos que permiten definir contratos y abstracciones en el código. A continuación, se presentan las diferencias clave entre ellas, teniendo en cuenta tanto los métodos como las variables.

#### Clases Abstractas:

1. **Métodos:**
   * Pueden contener tanto métodos abstractos (sin implementación) como métodos concretos (con implementación).
   * Permiten proporcionar funcionalidades por defecto a través de los métodos concretos.

```java
abstract class ClaseAbstracta {
    abstract void metodoAbstracto();  // Método abstracto
    void metodoConcreto() { }  // Método concreto
}
```

2. **Constructores:** Pueden tener constructores, lo que facilita la inicialización de estados y otras acciones al crear instancias de la clase abstracta.
3. **Herencia:** Permite la herencia única. Una clase puede heredar de una sola clase abstracta.
4. **Variables:** Pueden contener variables de instancia y de clase con diversos modificadores de acceso.

```java
abstract class ClaseAbstracta {
    int variableInstancia;  // Variable de instancia
    static int variableClase;  // Variable de clase (static)
}
```

#### Interfaces

1. **Métodos:** Contienen únicamente métodos abstractos (hasta Java 8), pero pueden incluir métodos por defecto y estáticos desde Java 8.

```java
interface MiInterfaz {
    void metodoAbstracto();  // Método abstracto
    default void metodoConcreto() { }  // Método concreto por defecto
    static void metodoEstatico() { }  // Método estático
}
```

2. **Constructores:** No pueden tener constructores. Las interfaces están diseñadas para definir comportamientos, no para instanciarse directamente.
3. **Herencia:** Permite la implementación múltiple. Una clase puede implementar múltiples interfaces.
4. **Variables:** Contienen variables constantes (public, static, final) que representan valores invariables compartidos por las implementaciones.

```java
interface MiInterfaz {
    int CONSTANTE = 42;  // Variable constante
}
```

**Consideraciones de Diseño:**

* **Cuando Usar Clases Abstractas:**
  * Cuando se desea proporcionar una base común para clases relacionadas.
  * Cuando se necesita compartir código común a través de métodos concretos.
* **Cuando Usar Interfaces:**
  * Cuando se busca lograr una implementación de contrato sin preocuparse por la herencia de clases.
  * Cuando una clase puede cumplir múltiples contratos (interfaces).

La elección entre clases abstractas e interfaces dependerá de la naturaleza del diseño y los requisitos específicos de la aplicación. En muchos casos, se pueden utilizar de manera complementaria para lograr un diseño más flexible y modular.
