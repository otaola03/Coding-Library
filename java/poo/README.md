# POO

La Programación Orientada a Objetos (POO) es un paradigma fundamental en el desarrollo de software que se centra en la creación y manipulación de objetos. Java, como lenguaje de programación, se basa en este paradigma, y a continuación, exploraremos los conceptos clave de la POO en Java:

* Clases
  * Modificadores de acceso
  * Objetos
* Metodos y paso de metodos
  * cosntructores y destructores
  * setters y getters
* Pilares de POO
  * Abstraccion
    * Interfaces
    * Clases abstractas
  * Encapsulamiento
  * Herencia
  * Polimorfismo
    * Polimorfismo en tiempo de compilacion
    * Polimorfismo en tiempo de ejecucion

<figure><img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/20190717114649/Object-Oriented-Programming-Concepts.jpg" alt=""><figcaption></figcaption></figure>

### Los 4 pilares

La Programación Orientada a Objetos (POO) se basa en cuatro pilares: encapsulamiento, herencia, polimorfismo y abstracción. Estos principios estructuran el diseño de software, permitiendo la encapsulación de datos, reutilización de código, flexibilidad con polimorfismo y simplificación conceptual mediante abstracción. Son fundamentales para construir sistemas eficientes en POO.

<figure><img src="https://miro.medium.com/v2/resize:fit:888/1*hXFebLehdhsUEP94jXIh7Q.png" alt=""><figcaption></figcaption></figure>

#### **Clases y Objetos**

En Java, todo se organiza en clases y objetos. Una clase es un plano o un modelo para crear objetos, y un objeto es una instancia específica de una clase.

```java
// Definición de una clase en Java
public class Coche {
    String marca;
    int anio;

    // Constructor
    public Coche(String m, int a) {
        marca = m;
        anio = a;
    }

    // Método
    public void conducir() {
        System.out.println("Conduciendo un coche de marca " + marca);
    }
}

// Creación de un objeto
Coche miCoche = new Coche("Toyota", 2022);
```

#### **Encapsulamiento:**

El encapsulamiento implica ocultar los detalles internos de una clase y exponer solo lo necesario. Los modificadores de acceso (`private`, `protected`, `public`) son esenciales para lograr el encapsulamiento.

```java
public class CuentaBancaria {
    private double saldo;

    public void depositar(double cantidad) {
        // Lógica para realizar el depósito
        saldo += cantidad;
    }

    public double obtenerSaldo() {
        return saldo;
    }
}
```

#### **Herencia:**

La herencia permite la creación de nuevas clases basadas en clases existentes, heredando sus propiedades y comportamientos. En Java, se utiliza la palabra clave `extends`.

```java
// Clase base
public class Animal {
    public void comer() {
        System.out.println("El animal come comida general.");
    }
}

// Clase derivada
public class Perro extends Animal {
    public void ladrar() {
        System.out.println("Guau, guau");
    }
}
```

#### **Polimorfismo**

El polimorfismo permite que un objeto pueda tomar muchas formas. En Java, el polimorfismo se logra mediante la sobrecarga de métodos y la implementación de interfaces.

```java
interface Forma {
    void dibujar();
}

class Circulo implements Forma {
    public void dibujar() {
        System.out.println("Dibujando un círculo");
    }
}

class Cuadrado implements Forma {
    public void dibujar() {
        System.out.println("Dibujando un cuadrado");
    }
}
```

#### **Abstracción**

La abstracción se refiere a la simplificación de conceptos complejos mediante la creación de clases abstractas e interfaces. Java permite la declaración de clases abstractas y la implementación de interfaces.

```java
// Clase abstracta
abstract class Figura {
    abstract void dibujar();
}

// Implementación de la clase abstracta
class Triangulo extends Figura {
    void dibujar() {
        System.out.println("Dibujando un triángulo");
    }
}
```

La POO en Java proporciona un marco sólido para el desarrollo de software, facilitando la modularidad, reutilización de código y mantenimiento. Al comprender estos conceptos, los programadores pueden diseñar sistemas más flexibles y escalables.
