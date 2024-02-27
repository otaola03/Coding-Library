# Excepciones

En Java, las excepciones son objetos que representan situaciones excepcionales que pueden surgir durante la ejecución del programa. Estas situaciones pueden ser errores en tiempo de ejecución, como la división por cero o el acceso a un índice fuera de los límites de un array.

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

### **Tipos de Excepciones en Java**

Java clasifica las excepciones en dos tipos principales: Excepciones verificadas (checked) y Excepciones no verificadas (unchecked).

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

#### **Excepciones Verificadas (Checked Exceptions)**

Estas son excepciones que deben ser manejadas explícitamente mediante un bloque `try-catch` o especificando que el método las arrojará (`throws`).

```java
java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class ManejoExcepciones {
    public static void main(String[] args) {
        try {
            BufferedReader reader = new BufferedReader(new FileReader("archivo.txt"));
            String linea = reader.readLine();
            System.out.println(linea);
            reader.close();
        } catch (IOException e) {
            System.out.println("Excepción IO: " + e.getMessage());
        }
    }
}
```

#### **Excepciones No Verificadas (Unchecked Exceptions)**

Estas son excepciones que no requieren un manejo explícito y generalmente son errores en tiempo de ejecución.

Ejemplo:

```java
public class ManejoExcepciones {
    public static void main(String[] args) {
        int[] array = {1, 2, 3};
        System.out.println(array[5]); // Esto generará una ArrayIndexOutOfBoundsException
    }
}
```

### **Bloques Finally**

El bloque `finally` se utiliza para contener código que debe ejecutarse siempre, independientemente de si se produce una excepción o no.

```java
public class ManejoExcepciones {
    public static void main(String[] args) {
        try {
            // Código que podría generar una excepción
        } finally {
            // Código que se ejecutará siempre
        }
    }
}
```

El bloque `finally` se ejecuta después de que se completa el bloque `try` y, opcionalmente, después de que se maneje cualquier excepción con el bloque `catch`. En otras palabras, el orden de ejecución sería:

1. El código dentro del bloque `try` se ejecuta.
2. Si se lanza una excepción dentro del bloque `try`, se busca un bloque `catch` correspondiente. Si se encuentra, se ejecuta el código dentro del bloque `catch`.
3. Después de que se completa el bloque `try` y, en su caso, el bloque `catch`, el bloque `finally` se ejecuta, independientemente de si se lanzó una excepción o no.

```java
try {
    // Código en el bloque try
} catch (Exception e) {
    // Manejo de excepción en el bloque catch (si es necesario)
} finally {
    // Código en el bloque finally, que se ejecutará siempre
}
```

### **Try-With-Resources**

Java 7 introdujo el bloque `try-with-resources` para gestionar automáticamente los recursos, como cerrar un archivo o una conexión, sin necesidad de un bloque `finally`.

```java
try (BufferedReader reader = new BufferedReader(new FileReader("archivo.txt"))) {
    String linea = reader.readLine();
    System.out.println(linea);
} catch (IOException e) {
    System.out.println("Excepción IO: " + e.getMessage());
}
```

### **Creación de Excepciones Personalizadas**

En algunas situaciones, es posible que desees crear tus propias excepciones personalizadas para manejar casos específicos en tu aplicación.

```java
public class MiExcepcion extends Exception {
    public MiExcepcion(String mensaje) {
        super(mensaje);
    }
}
```
