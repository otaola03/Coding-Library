# Polimorfismo

El polimorfismo es uno de los conceptos fundamentales de la programación orientada a objetos (POO) en Java. Este principio permite que objetos de diferentes clases se utilicen de manera uniforme, proporcionando flexibilidad y extensibilidad en el código. En este post, exploraremos los aspectos clave del polimorfismo en Java y cómo se utiliza para crear aplicaciones más dinámicas y mantenibles.

{% embed url="https://www.youtube.com/watch?v=tIWm3I_Zu7I&list=PLxvooGgpi4NeugSB4Pk546MXTPmGqPdc4&index=4" %}

### ¿Que es el polimorfismo?

En programación, el polimorfismo es un concepto que nos permite tratar diferentes tipos de objetos de manera uniforme. Imagina tener una interfaz común para realizar ciertas acciones, como "hacer un sonido" o "nadar", independientemente de si estamos trabajando con un perro, un gato o un pez. El polimorfismo simplifica el código al permitir que objetos de clases distintas se utilicen de manera similar, ofreciendo flexibilidad y facilitando la gestión de diferentes tipos de datos.

> El polimorfisomo significa que dos clases sobreescriban una funcion heredada del mismo padre, es decir que dos funciones tengan la misma funcion, peor que haga distintas cosas.

{% embed url="https://miro.medium.com/v2/resize:fit:552/1*vVeUZJtM_W78OlmWbZUfWQ.png" %}

### **Concepto Fundamental del Polimorfismo:**

El polimorfismo significa "muchas formas". En Java, hay dos tipos principales de polimorfismo: polimorfismo de compilación (estático) y polimorfismo de ejecución (dinámico).

* **Polimorfismo de Compilación (Estático):**
  * Ocurre durante la compilación.
  * Se refiere al uso de sobrecarga de métodos y métodos estáticos.
* **Polimorfismo de Ejecución (Dinámico):**
  * Ocurre durante la ejecución.
  * Se refiere al uso de herencia y sobreescritura de métodos.

### **Polimorfismo con Herencia y Sobreescritura:**

```java
class Animal {
    void hacerSonido() {
        System.out.println("Haciendo un sonido");
    }
}

class Perro extends Animal {
    @Override
    void hacerSonido() {
        System.out.println("El perro hace un ladrido");
    }
}

class Gato extends Animal {
    @Override
    void hacerSonido() {
        System.out.println("El gato hace un maullido");
    }
}
```

En este ejemplo, las clases `Perro` y `Gato` heredan de la clase `Animal` y sobrescriben el método `hacerSonido()`. Por ende, a la hora de utilizarlas, cada una realizara un distinta accion, aunque sean invocadas de la misma manera:

```java
javaCopy codeAnimal miAnimal;

miAnimal = new Perro();
miAnimal.hacerSonido();  // Llama al método de la clase Perro

miAnimal = new Gato();
miAnimal.hacerSonido();  // Llama al método de la clase Gato
```

Aquí, `miAnimal` es una referencia polimórfica que puede apuntar a instancias de `Perro` o `Gato`. El método llamado dependerá del tipo real del objeto en tiempo de ejecución.

### **Interfaces y Polimorfismo:**

```java
interface Nadador {
    void nadar();
}

class Pato implements Nadador {
    @Override
    public void nadar() {
        System.out.println("El pato nada en el agua");
    }
}

class Pez implements Nadador {
    @Override
    public void nadar() {
        System.out.println("El pez nada con aletas");
    }
}
```

Las interfaces también permiten el polimorfismo, ya que las clases que implementan una interfaz pueden ser referenciadas a través de la interfaz.

### **Ventajas del Polimorfismo:**

1. **Flexibilidad:**
   * Permite el uso de un solo tipo de referencia para objetos de diferentes clases, facilitando la extensión y mantenimiento del código.
2. **Desacoplamiento:**
   * Reduce la dependencia entre clases, ya que las referencias pueden ser de tipo más general.
3. **Extensibilidad:**
   * Facilita la incorporación de nuevas clases sin afectar el código existente.

### **Consideraciones de Diseño:**

1. **Uso Responsable:**
   * Aplica polimorfismo de manera efectiva donde sea lógico y necesario.
2. **Sobreescritura Coherente:**
   * Al sobrescribir métodos, asegúrate de mantener la coherencia con el contrato de la superclase o interfaz.
