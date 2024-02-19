# Encapsulacion

La encapsulación es uno de los principios fundamentales de la programación orientada a objetos (POO) en Java, que se centra en la ocultación de los detalles internos de un objeto y la exposición controlada de su funcionalidad. Este concepto permite la creación de código modular, mantenible y seguro. A continuación, exploraremos qué es la encapsulación, por qué es importante en Java y cómo implementarla.

### ¿Qué es la Encapsulación?

La encapsulación implica agrupar los datos (variables) y los métodos (funciones) relacionados dentro de una unidad, es decir, una clase en el contexto de Java. Además, se busca restringir el acceso directo a los detalles internos del objeto desde fuera de la clase, fomentando el principio de "ocultar la implementación, mostrar la interfaz".

{% embed url="https://www.youtube.com/watch?v=sNKKxc4QHqA&list=PLxvooGgpi4NeugSB4Pk546MXTPmGqPdc4&index=6" %}

### Beneficios de la Encapsulación:

1. **Seguridad del Objeto:** Evita el acceso no autorizado y modificación de los datos internos de un objeto, mejorando la integridad del objeto.
2. **Flexibilidad de Implementación:** Permite realizar cambios en la implementación interna de la clase sin afectar el código que utiliza la clase.
3. **Modularidad y Mantenibilidad:** Facilita la organización modular del código al agrupar funciones relacionadas, mejorando la mantenibilidad y la comprensión del código.

### Implementación de Encapsulación en Java:

1. **Uso de Modificadores de Acceso:** Utiliza modificadores de acceso (`private`, `protected`, `public`) para controlar la visibilidad de las variables y métodos.

```java
public class Persona {
    private String nombre;  // Variable encapsulada
    private int edad;       // Variable encapsulada

    // Métodos de acceso (getters y setters)
    public String getNombre() {
        return nombre;
    }

    public void setNombre(String nombre) {
        this.nombre = nombre;
    }

    public int getEdad() {
        return edad;
    }

    public void setEdad(int edad) {
        if (edad >= 0) {
            this.edad = edad;
        }
    }
}
```

1. **Métodos de Acceso (Getters y Setters):** Proporciona métodos de acceso para leer (`get`) y modificar (`set`) los valores de las variables privadas.
2. **Validaciones y Lógica Interna:** Incorpora lógica interna dentro de los métodos de acceso, como validaciones para asegurar la consistencia de los datos.

### Ejemplo de Uso:

```java
public class Main {
    public static void main(String[] args) {
        Persona persona = new Persona();
        persona.setNombre("Juan");
        persona.setEdad(25);

        System.out.println("Nombre: " + persona.getNombre());
        System.out.println("Edad: " + persona.getEdad());
    }
}
```

En este ejemplo, la clase `Persona` encapsula las variables `nombre` y `edad` y proporciona métodos de acceso (`getters` y `setters`). El código fuera de la clase no puede acceder directamente a las variables, mejorando la seguridad y la flexibilidad.

La encapsulación en Java es esencial para construir software robusto y mantenible. Al aplicar este principio, se mejora la seguridad, flexibilidad y organización del código, contribuyendo a un desarrollo de software eficiente y confiable.

### Metodos de acceso

En Java, los modificadores de acceso son palabras clave que determinan la visibilidad y accesibilidad de las clases, variables, métodos y constructores en el código. Estos modificadores permiten establecer niveles de encapsulación, es decir, controlar qué partes del código pueden acceder a ciertos elementos y cuáles no. En este post, exploraremos los principales modificadores de acceso en Java y cómo se utilizan para gestionar la visibilidad de los miembros de una clase.

#### Public, Protected, Default y Private: Un Vistazo Rápido

1. **Public (public):**
   * Accesible desde cualquier clase y paquete.
   * No hay restricciones en la visibilidad.
   * Puede ser utilizado libremente en cualquier parte del programa.
2. **Protected (protected):**
   * Accesible dentro del mismo paquete y por subclases (incluso si están en paquetes diferentes).
   * Proporciona un nivel intermedio de visibilidad.
   * Permite la herencia y extensión de clases, restringiendo el acceso desde clases no relacionadas.
3. **Default (Sin Modificador):**
   * Accesible solo dentro del mismo paquete.
   * No se utiliza una palabra clave específica; es el nivel predeterminado si no se especifica ningún modificador.
   * Conocido como "paquete-privado" o "package-private".
4. **Private (private):**
   * Accesible solo dentro de la misma clase.
   * Proporciona el mayor nivel de encapsulación.
   * Oculta la implementación interna de la clase y restringe el acceso a otras clases.

<figure><img src="../../.gitbook/assets/photo_2024-02-14_17-49-43 (1).jpg" alt=""><figcaption></figcaption></figure>

#### Ejemplos de Uso:

```java
// Ejemplo de clase con diferentes modificadores de acceso
public class Ejemplo {

    public int variablePublica;  // Accesible desde cualquier clase

    protected int variableProtegida;  // Accesible dentro del mismo paquete y por subclases

    int variableDefault;  // Accesible solo dentro del mismo paquete

    private int variablePrivada;  // Accesible solo dentro de la misma clase

    // Métodos con diferentes modificadores de acceso
    public void metodoPublico() {
        // Código del método
    }

    protected void metodoProtegido() {
        // Código del método
    }

    void metodoDefault() {
        // Código del método
    }

    private void metodoPrivado() {
        // Código del método
    }
}
```

#### Consideraciones de Diseño:

1. **Principio de Menor Visibilidad:**
   * Apunta a utilizar el modificador de acceso más restrictivo posible para limitar la visibilidad y prevenir el acceso no autorizado.
2. **Encapsulación:**
   * Utiliza `private` para variables y métodos que deben ser exclusivamente internos a la clase, fortaleciendo la encapsulación.
3. **Interacción entre Clases:**
   * Utiliza `public` y `protected` con precaución para exponer solo lo necesario para la interacción con otras clases.

#### Ventajas de Utilizar Modificadores de Acceso:

1. **Seguridad y Control:**
   * Permite controlar quién puede acceder y modificar los miembros de una clase.
2. **Encapsulación:**
   * Favorece la encapsulación, protegiendo la implementación interna de una clase.
3. **Mantenibilidad:**
   * Mejora la mantenibilidad del código al facilitar futuras modificaciones y actualizaciones.
