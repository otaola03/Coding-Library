# Clases

En el mundo de la programación orientada a objetos, las clases son un pilar fundamental. En Java, un lenguaje de programación orientado a objetos robusto, las clases desempeñan un papel esencial en la creación y organización del código. Este post explora las clases en Java, desde su definición básica hasta su implementación y uso en aplicaciones del mundo real.

### Definición de Clases en Java

En Java, una clase es una plantilla o un modelo que define el comportamiento y las propiedades de los objetos. Los objetos son instancias de clases, y estas definen los atributos y métodos que los objetos pueden tener. Una clase en Java se define mediante la palabra clave `class`. Aquí tienes un ejemplo básico:

```java
public class MiClase {
    // Atributos
    private int numero;
    private String texto;

    // Constructor
    public MiClase(int numero, String texto) {
        this.numero = numero;
        this.texto = texto;
    }

    // Métodos
    public void mostrarInformacion() {
        System.out.println("Número: " + numero);
        System.out.println("Texto: " + texto);
    }
}
```

### Atributos, Constructores y Métodos

#### **Atributos**

Los atributos de una clase representan las características o datos que describen el estado de los objetos creados a partir de esa clase. En el ejemplo de la clase `MiClase`, los atributos son `numero` y `texto`. Pueden ser de diferentes tipos de datos, como enteros, cadenas, booleanos, entre otros. El acceso a estos atributos se puede controlar mediante modificadores de acceso, como `private` en este caso.

```java
public class MiClase {
    // Atributos
    private int numero;
    private String texto;
    // Resto de la clase...
}
```

#### **Constructores**

Un constructor es un método especial que se utiliza para inicializar los atributos de un objeto cuando se crea una instancia de la clase. En el ejemplo, el constructor de `MiClase` toma dos parámetros (`numero` y `texto`) y asigna estos valores a los atributos correspondientes.

```java
// Constructor
public MiClase(int numero, String texto) {
    this.numero = numero;
    this.texto = texto;
}
```

La palabra clave `this` se utiliza para referenciar los atributos de la instancia actual de la clase, distinguiéndolos de los parámetros del constructor.

#### **Métodos**

Los métodos definen el comportamiento de la clase. Pueden realizar operaciones, manipular datos y devolver resultados. En el ejemplo, la clase `MiClase` tiene un método llamado `mostrarInformacion()` que imprime en la consola la información almacenada en los atributos.

```java
// Método
public void mostrarInformacion() {
    System.out.println("Número: " + numero);
    System.out.println("Texto: " + texto);
}
```

Los métodos también pueden tener parámetros y valores de retorno, lo que agrega flexibilidad y funcionalidad a la clase.

Para usar un metodo tan solo tienes que llamarlo a traves de un objeto:

```java
public class Main {
    public static void main(String[] args) {
        Persona persona = new Persona();
        persona.mostrarInformacion();
    }
}
```

### Creación de Objetos

Una vez que se ha definido una clase, puedes crear objetos utilizando el operador `new`. Aquí está cómo se crea un objeto de la clase `MiClase`:

```java
MiClase miObjeto = new MiClase(42, "Hola, Mundo!");
miObjeto.mostrarInformacion();
```

### Encapsulamiento y Modificadores de Acceso

Java utiliza conceptos como encapsulamiento para controlar el acceso a los atributos y métodos de una clase. Los modificadores de acceso como `public`, `private` y `protected` definen la visibilidad de estos elementos.

#### **Getters (Métodos de Obtención):**

Los getters son métodos diseñados para recuperar o obtener el valor de un atributo privado. Siguen una convención de nomenclatura que comienza con la palabra "get", seguida del nombre del atributo con la primera letra en mayúscula.

```java
public class Persona {
    private String nombre;

    // Getter para el atributo 'nombre'
    public String getNombre() {
        return nombre;
    }
}
```

#### **Setters (Métodos de Establecimiento):**

Los setters son métodos utilizados para modificar o establecer el valor de un atributo privado. Siguen una convención de nomenclatura que comienza con la palabra "set", seguida del nombre del atributo con la primera letra en mayúscula. Los setters a menudo incluyen un parámetro que representa el nuevo valor que se asignará al atributo.

```java
public class Persona {
    private String nombre;

    // Setter para el atributo 'nombre'
    public void setNombre(String nuevoNombre) {
        this.nombre = nuevoNombre;
    }
}
```

### Herencia y Polimorfismo

Java admite herencia, permitiendo que una clase herede atributos y métodos de otra. Además, el polimorfismo permite que un objeto se comporte como su clase base o como una de sus clases derivadas.

### Clases estaticas

\
En Java, una clase estática es una clase que tiene miembros (métodos o campos) que se pueden acceder directamente, sin necesidad de crear una instancia de la clase. Las clases estáticas se declaran utilizando la palabra clave `static`. Aquí hay algunas características y conceptos clave sobre las clases estáticas:

1.  **Campo Estático:**

    * Un campo estático es una variable que pertenece a la clase y no a las instancias individuales de esa clase. Todos los objetos de esa clase comparten el mismo campo estático.
    * Se accede a un campo estático a través del nombre de la clase en lugar de a través de una instancia del objeto.

    ```java
    public class Ejemplo {
        // Campo estático
        public static int contador;

        // Otros miembros de la clase...
    }
    ```
2.  **Método Estático:**

    * Un método estático es un método que pertenece a la clase y no a una instancia específica de la clase.
    * Puedes llamar a un método estático directamente a través del nombre de la clase, sin crear una instancia de la clase.

    ```java
    public class Ejemplo {
        // Método estático
        public static void imprimirMensaje() {
            System.out.println("¡Hola, soy un método estático!");
        }

        // Otros miembros de la clase...
    }
    ```
3. **Bloque de Inicialización Estático:**
   * En Java, un bloque de inicialización estático es un bloque de código dentro de una clase que se ejecuta solo una vez cuando la clase se carga en la memoria. Este bloque de código se denota con la palabra clave `static` y se utiliza para realizar operaciones de inicialización que deben llevarse a cabo antes de que se creen instancias de la clase o se llamen a otros métodos estáticos.

<pre class="language-java"><code class="lang-java"><strong>public class OtraClase {
</strong>    static {
        // Código de inicialización estática
    }
}
</code></pre>

#### Como utilizar

5. **Uso Común:**
   * Las clases estáticas son útiles cuando se tiene funcionalidad que pertenece a la clase en su conjunto y no a una instancia específica.
   * A menudo se utilizan para agrupar métodos relacionados que no dependen del estado de una instancia.
6. **Ejemplo de Uso:**
   * Un ejemplo común de uso de clases estáticas es la clase `Math` en Java, que contiene métodos y campos estáticos para operaciones matemáticas.

```java
double resultado = Math.sqrt(25);
```

En resumen, las clases estáticas proporcionan un enfoque para organizar y acceder a funcionalidades compartidas en una clase sin la necesidad de crear instancias. Son útiles para agrupar métodos y campos relacionados que no dependen del estado de una instancia particular.
