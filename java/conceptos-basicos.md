# Conceptos basicos

{% embed url="https://coal-tuesday-a8b.notion.site/Conceptos-basicos-6f00995932ea41839fe79a0cbc9229e7" %}



<details>

<summary>Conceptos Básicos</summary>

[Variables](conceptos-basicos.md#variables)

[Tipso de datos](conceptos-basicos.md#tipos-de-datos)

[Tipos de operadores](conceptos-basicos.md#tipos-de-operadores)

[Casteos](conceptos-basicos.md#casteos)

[Arrays](conceptos-basicos.md#arrays)

[Imprimir en consola](conceptos-basicos.md#imprimir-en-consola)

[Recibir datos por consola](conceptos-basicos.md#recibir-datos-por-consola)

</details>

### Variables

Una variable es un contenedor para almacenar datos. Piensa en ellas como cajas etiquetadas donde puedes guardar y manipular información en tu programa. Cada variable tiene un nombre único y un tipo de dato que especifica qué tipo de información puede contener.

En Java, existen varios tipos de variables, pero los principales son:

1. **Variables Locales:** Definidas dentro de un método o bloque y solo son visibles en ese ámbito.
2. **Variables de Instancia:** Pertenecen a una instancia específica de una clase y se declaran en la clase pero fuera de cualquier método.
3. **Variables Estáticas (o Globales):** Pertenecen a la clase en lugar de una instancia específica y se declaran con la palabra clave **`static`**.

{% embed url="https://coal-tuesday-a8b.notion.site/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2F072431b7-a9e6-4f2f-9065-a7c8fa12a257%2Fab645f01-e029-4ff8-ae8d-bc07c5cc55ad%2FUntitled.png?table=block&id=bcce3d42-9043-42b0-ba56-74bb770044c0&spaceId=072431b7-a9e6-4f2f-9065-a7c8fa12a257&width=1590&userId=&cache=v2" %}

### Tipos de datos

```java
public class TiposDeDatos {
    public static void main(String[] args) {
        // Tipos de datos primitivos
        char miCaracter = 'A'; // 1 byte
        short miShort = 1000; // 2 bytes
        int miEntero = 42; // 4 bytes
        long miLargo = 1234567890L; // 4 bytes
        float miFlotante = 3.14f; // 4 bytes
        double miDoble = 2.71828; // 8 bytes
        boolean esVerdadero = true;

        // Tipos de datos no primitivos
        String miCadena = "Hola, Mundo!";
        MiClase miObjeto = new MiClase();
        int[] miArreglo = new int[5];
        MiInterfaz miInterfaz = new MiImplementacion();
        Día diaDeLaSemana = Día.LUNES;
        Integer miEnteroObjeto = new Integer(42);
    }
}
```

### Tipos de operadores

Los operadores son símbolos que realizan operaciones en variables y valores. Algunos operadores comunes en Java incluyen:

* Operadores aritméticos (+, -, \*, /, %)
* Operadores de comparación (==, !=, <, >, <=, >=)
* Operadores lógicos (&&, ||, !)
* Operadores de asignación (=, +=, -=, \*=, /=, %=)
* Operadores de incremento/decremento (++, --)

### Casteos

El casteo (casting) se refiere a la conversión de un tipo de dato a otro. Puedes realizar casteo explícito e implícito. Por ejemplo:&#x20;

```java
double numeroDouble = 10.5;
int numeroEntero = (int) numeroDouble; // Casteo explícito
```

### Arrays

Un arreglo o array en Java es una estructura de datos que permite almacenar múltiples valores del mismo tipo bajo un solo nombre. Los arreglos son muy utilizados en programación para trabajar con colecciones de datos, como listas de números, cadenas de texto u objetos. Aquí hay algunos conceptos clave sobre los arreglos en Java:

#### **Declaración de arreglos**

Puedes declarar un arreglo especificando el tipo de datos que contendrá, seguido del nombre del arreglo y corchetes **`[]`** para indicar que es un arreglo. Por ejemplo:

```java
int[] numeros; // Declaración de un arreglo de enteros
String[] nombres; // Declaración de un arreglo de cadenas
```

También puedes declarar arreglos de otros tipos de datos, como **`double`**, **`char`**, **`boolean`**, o incluso arreglos de objetos personalizados.

#### **Inicialización de arreglos**

Una vez declarado un arreglo, debes inicializarlo para asignarle un tamaño específico. Puedes hacerlo de varias maneras:

Inicialización en línea:

```java
int[] numeros = {1, 2, 3, 4, 5}; // Inicializa un arreglo de enteros con valores
```

Inicialización mediante la palabra clave **`new`**:

```java
int[] numeros = new int[5]; // Inicializa un arreglo de enteros con 5 elementos, todos inicializados a 0
```

#### **Acceso a elementos**

Para acceder a elementos individuales de un arreglo, utiliza su índice (posición), comenzando desde 0 para el primer elemento. Por ejemplo:

```java
int tercerNumero = numeros[2]; // Accede al tercer elemento del arreglo (índice 2)
```

#### **Longitud de arreglos**

Puedes obtener la longitud (cantidad de elementos) de un arreglo utilizando la propiedad **`length`**. Por ejemplo:

```java
int longitud = numeros.length; // Obtiene la longitud del arreglo 'numeros'
```

#### **Iteración a través de arreglos**

Puedes recorrer un arreglo utilizando bucles **`for`** o **`foreach`** (disponible a partir de Java 5). Aquí hay un ejemplo con un bucle **`for`**:

```java
for (int i = 0; i < numeros.length; i++) {
    System.out.println(numeros[i]);
}
```

#### **Arreglos multidimensionales**

Java permite crear arreglos multidimensionales, como matrices. Puedes tener arreglos de arreglos o matrices de varias dimensiones. Por ejemplo, una matriz bidimensional:

```java
int[][] matriz = {{1, 2, 3}, {4, 5, 6}, {7, 8, 9}};
```

### Imprimir en consola

Para imprimir en la consola en Java, puedes utilizar la clase **`System`** y su método **`out`** junto con el método **`println()`** para mostrar contenido en una nueva línea o **`print()`** para imprimir en la misma línea. Aquí tienes ejemplos de cómo hacerlo:

#### **Usando `println()` para imprimir en una nueva línea:**

```java
javaCopy code
System.out.println("Hola, Mundo!"); // Imprime y agrega una nueva línea
System.out.println("¡Bienvenido a Java!");
```

La salida será:

```css
Hola, Mundo!
¡Bienvenido a Java!
```

#### Usando `print()` para imprimir en la misma línea:

```java
System.out.print("Hola, "); // Imprime sin cambiar de línea
System.out.println("Mundo!"); // Imprime y agrega una nueva línea
```

La salida será:

```
Hola, Mundo!
```

#### Usando formato con printf():

Puedes utilizar el método **`printf()`** para imprimir con formato, similar a **`printf`** en C o C++. Por ejemplo:

```java
String nombre = "Juan";
int edad = 30;
System.out.printf("Hola, %s. Tienes %d años.%n", nombre, edad);
```

La salida será:

```css
Hola, Juan. Tienes 30 años.
```

Ten en cuenta que **`%s`** se usa para cadenas de texto, **`%d`** para números enteros y **`%n`** para una nueva línea.

#### **Imprimir variables**

Puedes imprimir el valor de una variable de la siguiente manera:

```java
int numero = 42;
System.out.println("El valor de la variable 'numero' es: " + numero);
```

La salida será:

```arduino
El valor de la variable 'numero' es: 42
```

Estas son algunas de las formas más comunes de imprimir en la consola en Java. Puedes elegir el método que mejor se adapte a tus necesidades de salida y formato.

### Recibir datos por consola

Sí, puedes utilizar **`System.in`** para recibir datos por consola en Java. Para hacerlo, necesitas utilizar la clase **`Scanner`**, que te permite leer datos de la entrada estándar (teclado) de manera sencilla. Aquí te muestro cómo puedes utilizar **`Scanner`** para recibir datos desde la consola:

Primero, debes importar la clase **`Scanner`** al principio de tu programa Java:

```java
import java.util.Scanner;
```

Luego, puedes crear un objeto **`Scanner`** para leer datos de la entrada estándar (**`System.in`**), como se muestra a continuación:

```java
Scanner scanner = new Scanner(System.in);
```

Después de crear el objeto **`Scanner`**, puedes utilizar sus métodos para recibir datos del usuario. Aquí tienes algunos ejemplos:

#### **Leer una cadena de texto:**

```java
System.out.print("Ingresa tu nombre: ");
String nombre = scanner.nextLine();
System.out.println("Hola, " + nombre);
```

Este código muestra un mensaje al usuario, espera a que el usuario ingrese una línea de texto y almacena esa línea en la variable **`nombre`**.

#### Leer un caracter:

```java
System.out.print("Ingresa un caracter: ");
char caracter = scanner.next().charAt(0);
System.out.println("Caracter: " + caracter);
```

Este código muestra un mensaje al usuario, espera a que el usuario ingrese un caracter y almacena esa línea en la variable **`caracter`**.

A diferencia del metodo `nextLine`, el metodo `next` no guarda una linea entera (hasta el salto de linea), sino que guarda un string desde el inicio hasta el primer espacio.

#### **Leer un número entero:**

```java
System.out.print("Ingresa un número entero: ");
int numero = scanner.nextInt();
System.out.println("El número que ingresaste es: " + numero);
```

Este código muestra un mensaje al usuario, espera a que el usuario ingrese un número entero y almacena ese número en la variable **`numero`**.

#### **Leer un número decimal (punto flotante):**

```java
System.out.print("Ingresa un número decimal: ");
double decimal = scanner.nextDouble();
System.out.println("El número decimal que ingresaste es: " + decimal);
```

Este código muestra un mensaje al usuario, espera a que el usuario ingrese un número decimal y almacena ese número en la variable **`decimal`**.

Es importante mencionar que **`Scanner`** se utiliza para leer datos en el formato en el que el usuario los ingrese. Por lo tanto, debes asegurarte de que la entrada coincida con el tipo de dato que estás tratando de leer. Además, es una buena práctica cerrar el objeto **`Scanner`** cuando hayas terminado de usarlo:

```java
scanner.close();
```

Esto libera los recursos asociados con la lectura de entrada estándar.
