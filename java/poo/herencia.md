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
javaCopy codepublic class Subclase extends Superclase {
    @Override
    public void metodoEspecifico() {
        // Implementación en la subclase
    }
}
```

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
