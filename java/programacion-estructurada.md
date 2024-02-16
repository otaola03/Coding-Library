# Programacion estructurada

En la programación, el control de flujo es esencial para tomar decisiones, repetir tareas y estructurar la lógica de un programa. En Java, disponemos de varias estructuras de control y bucles que nos permiten controlar el flujo de ejecución de nuestros programas de manera efectiva. En este artículo, exploraremos los principales tipos de bucles y estructuras de control en Java y cómo utilizarlos en tus proyectos.

{% embed url="https://coal-tuesday-a8b.notion.site/Programaci-n-estructurada-28abc066c7214f76952528413b714d47?pvs=25" %}

<details>

<summary>Programacion estructurada</summary>

[if-else](programacion-estructurada.md#estructura-de-control-if-else)

[while](programacion-estructurada.md#bucle-while)

[do-while](programacion-estructurada.md#bucle-do-while)

[for](programacion-estructurada.md#bucle-for)

[for-each](programacion-estructurada.md#bucle-for-each)

[switch](programacion-estructurada.md#estructura-switch)

</details>

### **Estructura de Control `if` - `else`**

La estructura **`if`** - **`else`** permite tomar decisiones basadas en una condición. Puedes ejecutar un bloque de código si la condición es verdadera (**`if`**) o un bloque alternativo si la condición es falsa (**`else`**).

```java
int edad = 18;
if (edad >= 18) {
    System.out.println("Eres mayor de edad.");
} else {
    System.out.println("Eres menor de edad.");
}
```

**Pseudocodigo**

```java
Si <condición> Entonces
	<Instrucciones>
Si no
	<Instrucciones>
Fin s
```

### **Bucle `while`**

El bucle **`while`** ejecuta un bloque de código repetidamente mientras una condición sea verdadera.

```java
int contador = 0;
while (contador < 5) {
    System.out.println("Contador: " + contador);
    contador++;
}
```

**Pseudocodigo**

```java
Mientras <condición> Hacer
	<instrucciones>
Fin mientras
```

### **Bucle `do-while`**

El bucle **`do-while`** es similar al **`while`**, pero garantiza que el bloque de código se ejecute al menos una vez, incluso si la condición es falsa posteriormente.

```java
int contador = 0;
do {
    System.out.println("Contador: " + contador);
    contador++;
} while (contador < 5);
```

**Pseudocodigo**

```java
Repetir
	<instrucciones>
Hasta que <condición >
```

### **Bucle `for`**

El bucle **`for`** proporciona una estructura compacta para repetir tareas. Tiene tres partes: inicialización, condición y actualización.

Ejemplo:

```java
for (int i = 0; i < 5; i++) {
    System.out.println("Iteración: " + i);
}
```

### **Bucle `for-each`**

El bucle **`for-each`** se utiliza para recorrer colecciones, como arreglos o listas, y ejecutar una acción en cada elemento sin necesidad de un contador.

```java
String[] colores = {"Rojo", "Verde", "Azul"};
for (String color : colores) {
    System.out.println("Color: " + color);
}
```

### **Estructura `switch`**

La estructura **`switch`** se utiliza para tomar decisiones basadas en el valor de una expresión. Puede tener múltiples casos y un caso predeterminado.

```java
int opcion = 2;
switch (opcion) {
    case 1:
        System.out.println("Opción 1 seleccionada.");
        break;
    case 2:
        System.out.println("Opción 2 seleccionada.");
        break;
    default:
        System.out.println("Opción no válida.");
}
```

**Pseudocodigo**

```java
Según sea <variable> Hacer
Caso valor 1:
<Instrucciones>
…
Fin según
```
