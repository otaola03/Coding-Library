# Herencia

La herencia es uno de los conceptos fundamentales de la programación orientada a objetos (POO) en Java, permitiendo la creación de jerarquías de clases donde una clase (subclase o clase derivada) hereda propiedades y comportamientos de otra clase (superclase o clase base). En este post, exploraremos los conceptos esenciales de la herencia en Java y cómo se utiliza para construir estructuras de clases reutilizables.

{% embed url="https://www.youtube.com/watch?v=ajOYOxCanhE&list=PLxvooGgpi4NeugSB4Pk546MXTPmGqPdc4&index=3" %}

### Conceptos Clave de la Herencia:

1. **Clase Base o Superclase:** Es la clase original de la cual otras clases derivan. Contiene propiedades y comportamientos comunes.

```java
public class Animal {
    protected String nombre;

    public Animal(String nombre) {
        this.nombre = nombre;
    }

    public void hacerSonido() {
        System.out.println("Haciendo un sonido");
    }
}
```

2. **Clase Derivada o Subclase:** Es la clase que hereda de otra clase. Puede añadir propiedades y comportamientos adicionales o modificar los existentes.

```java
public class Perro extends Animal {
    private String raza;

    public Perro(String nombre, String raza) {
        super(nombre);  // Llama al constructor de la superclase
        this.raza = raza;
    }

    // Puede añadir métodos adicionales
    public void ladrar() {
        System.out.println("¡Guau, guau!");
    }

    // Puede sobrescribir métodos de la superclase
    @Override
    public void hacerSonido() {
        System.out.println("El perro hace un ladrido");
    }
}
```

### Palabras Clave Relacionadas con la Herencia:

1. **`extends`:** Utilizada para declarar una clase como subclase de otra.

```java
public class Subclase extends Superclase {
    // Código de la subclase
}
```

2. **`super`:** Utilizada para llamar a los métodos o constructores de la superclase desde la subclase. Es para no tener que repetir el codigo y despues de llamar a `super()` agregas al construcotor las propiedades nuevas de la clase hijo.

```java
public class Subclase extends Superclase {
    public Subclase() {
        super();  // Llamada al constructor de la superclase
    }
}
```

3. **`@Override`:** Anotación que indica que un método en la subclase está sobrescribiendo un método en la superclase.

```java
public class Subclase extends Superclase {
    @Override
    public void metodoEspecifico() {
        // Implementación en la subclase
    }
}
```

### Sobrecarga

La sobrecarga, también conocida como "overloading" en inglés, es la capacidad de una clase de tener múltiples métodos con el mismo nombre pero con diferentes listas de parámetros. Esto permite a los programadores utilizar un nombre de método intuitivo y descriptivo para varias operaciones relacionadas.

#### Requisitos

Para sobrecargar un método, se deben cumplir uno o más de los siguientes requisitos:

* Cambiar el número de parámetros.
* Cambiar el tipo de parámetros.

#### Ejemplo de uso

```java
public class OperacionesMatematicas {

    // Sobrecarga del método sumar con diferentes tipos de parámetros
    public int sumar(int a, int b) {
        return a + b;
    }

    public double sumar(double a, double b) {
        return a + b;
    }

    // Sobrecarga del método sumar con un número variable de parámetros
    public int sumar(int... numeros) {
        int suma = 0;
        for (int num : numeros) {
            suma += num;
        }
        return suma;
    }

    // Otros métodos pueden coexistir con diferentes firmas
    public String sumar(String a, String b) {
        return a + b;
    }
}
```

Aqui podemos observar la sobrecarga del metodo `sumar` de tres formas distintas. Dos con el mimso numero de argumentos, pero de distinto tipo y un emtodo con mas de dos argumentos.

Al llamar a un método sobrecargado, el compilador determina cuál versión del método usar según el número y tipo de argumentos proporcionados.

```java
OperacionesMatematicas operaciones = new OperacionesMatematicas();

int resultado1 = operaciones.sumar(5, 3);          // Llama a sumar(int, int)
double resultado2 = operaciones.sumar(2.5, 3.5);   // Llama a sumar(double, double)
int resultado3 = operaciones.sumar(1, 2, 3, 4);    // Llama a sumar(int...)
String resultado4 = operaciones.sumar("Hola", " Java");  // Llama a sumar(String, String)
```

### Sobreescritura

Overriding o sobreescritura se refiere a la capacidad de una subclase para proporcionar una implementación específica de un método que ya está definido en su superclase. El método en la subclase tiene el mismo nombre, tipo de retorno y parámetros que el método en la superclase.

#### **Reglas y Consideraciones:**

* **Firma del Método:** El método en la subclase debe tener la misma firma que el método en la superclase (nombre, tipo de retorno, parámetros).
* **Visibilidad:** La visibilidad del método en la subclase no puede ser más restrictiva que la visibilidad del método en la superclase.
* **Excepciones:** La subclase no puede declarar excepciones más amplias que las declaradas por el método en la superclase. Puede declarar excepciones más específicas o ninguna excepción (solo si la superclase no declara ninguna).

#### Ejemplo

```java
class Animal {
    void hacerSonido() {
        System.out.println("Haciendo algún sonido");
    }
}

class Perro extends Animal {
    @Override
    void hacerSonido() {
        System.out.println("Guau guau");
    }
}
```

En este ejemplo la clase `Perro` hereda de `Animal` y reescribe el metodo `hacersonido()` para que realice una accion distinta.

#### **Anotación `@Override`**

La anotación `@Override` es opcional pero es una buena práctica utilizarla. Sirve para indicar explícitamente que el método en la subclase está destinado a sobrescribir un método en la superclase.

### Ventajas de la Herencia:

1. **Reutilización de Código:** Permite aprovechar la implementación existente de la superclase en la subclase.
2. **Jerarquías de Clases:** Facilita la organización de clases en jerarquías, reflejando relaciones del mundo real.
3. **Polimorfismo:** Permite tratar objetos de las subclases como objetos de la superclase, facilitando el polimorfismo.

### Consideraciones de Diseño:

1. **Jerarquía Lógica:** Diseña jerarquías de clases basadas en relaciones lógicas y comportamientos compartidos.
2. **Evitar Herencia Múltiple:** Java no admite herencia múltiple de clases. Utiliza interfaces si es necesario lograr múltiples herencias.

### Ejemplo de Uso:

```java
public class Main {
    public static void main(String[] args) {
        Perro miPerro = new Perro("Buddy", "Golden Retriever");
        miPerro.hacerSonido();  // Llama al método sobreescrito en la subclase
        miPerro.ladrar();       // Método específico de la subclase
    }
}
```

En este ejemplo, la clase `Perro` hereda de la clase `Animal`, aprovechando la propiedad y el método `hacerSonido()` de la superclase y añadiendo su propio método `ladrar()`.

La herencia en Java es una herramienta poderosa que promueve la reutilización de código y la construcción de jerarquías de clases lógicas. Al diseñar con herencia, es importante considerar la coherencia de la jerarquía y utilizarla de manera efectiva para crear un código modular y fácil de entender.
