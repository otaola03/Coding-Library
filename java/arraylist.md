# ArrayList

n el mundo de la programación en Java, la manipulación de colecciones es una habilidad crucial. El `ArrayList` es una de las estructuras de datos más versátiles y ampliamente utilizadas en Java, que forma parte del paquete `java.util`. En este post, exploraremos a fondo el `ArrayList` y aprenderemos a aprovechar al máximo sus características.

### ¿Qué es ArrayList?

`ArrayList` es una implementación de la interfaz `List` en Java. A diferencia de los arrays convencionales, `ArrayList` es dinámico, lo que significa que puede cambiar su tamaño durante la ejecución del programa. Esto proporciona una flexibilidad significativa al manipular conjuntos de datos.

{% embed url="https://www.youtube.com/watch?v=NbYgm0r7u6o" %}

### Declaración y Creación

Para utilizar un `ArrayList`, primero necesitamos importar la clase desde el paquete `java.util`. Luego, podemos declarar e inicializar un `ArrayList` de la siguiente manera:

```java
import java.util.ArrayList;

// Crear un ArrayList vacio
ArrayList<String> listaNombres = new ArrayList<>();

// Crearn un ArrayList con elemntos en su interior
ArrayList<String> listaNombres2 = new ArrayList<>(Arrays.asList("Jhon", "Crhis"));
```

### Operaciones sobre ArrayList

#### Añadir Elementos

Podemos agregar elementos al `ArrayList` utilizando el método `add()`:

```java
listaNombres.add("Alice");
listaNombres.add("Bob");
listaNombres.add("Charlie");
```

#### Acceder a Elementos

Para acceder a un elemento en un `ArrayList`, utilizamos el método `get()` junto con el índice:

```java
String primerNombre = listaNombres.get(0);
System.out.println("Primer nombre: " + primerNombre);
```

#### Eliminar Elementos

Podemos eliminar elementos por índice o directamente por valor:

```java
listaNombres.remove(1); // Elimina el elemento en el índice 1
listaNombres.remove("Charlie"); // Elimina el elemento con el valor "Charlie"
```

#### Iteración con Iteradores

Podemos usar un bucle `for` o un iterador para recorrer todos los elementos en el `ArrayList`:

```java
for (String nombre : listaNombres) {
    System.out.println(nombre);
}
```

#### Tamaño y Comprobaciones

Podemos obtener el tamaño del `ArrayList` y comprobar si está vacío:

```java
int tamaño = listaNombres.size();
boolean estaVacio = listaNombres.isEmpty();
```

### Array Vs ArrayList

En Java, tanto los arrays como los ArrayList son herramientas para almacenar datos, pero sus diferencias son clave en el diseño de programas. Los arrays son estáticos y requieren un tamaño fijo, mientras que los ArrayList son dinámicos y pueden cambiar de tamaño durante la ejecución del programa. La elección entre ellos depende de las necesidades específicas del proyecto y del nivel de flexibilidad requerido para manejar datos de manera eficiente.

1. **Tamaño Dinámico:**
   * **Array:** Su tamaño es fijo y se determina en el momento de la creación. No puede cambiar una vez que se ha definido.
   * **ArrayList:** Tiene un tamaño dinámico que puede cambiar durante la ejecución del programa, ya que se ajusta automáticamente según sea necesario.
2. **Tipos de Datos:**
   * **Array:** Puede contener tipos de datos primitivos o objetos.
   * **ArrayList:** Solo puede contener objetos. Si necesitas almacenar tipos de datos primitivos, debes utilizar sus equivalentes clases envolventes (por ejemplo, `Integer` en lugar de `int`).
3. **Sintaxis de Declaración e Inicialización:**
   * **Array:** Se declara y se inicializa con un tamaño específico en el momento de la creación, como `int[] miArray = new int[5];`.
   * **ArrayList:** Se declara e inicializa de manera más flexible sin la necesidad de especificar un tamaño inicial, como `ArrayList<Integer> miArrayList = new ArrayList<>();`.
4. **Manipulación:**
   * **Array:** Manipular el tamaño de un array requiere crear uno nuevo con el tamaño deseado y luego copiar los elementos del array original al nuevo.
   * **ArrayList:** Puede cambiar dinámicamente su tamaño con métodos como `add()`, `remove()`, etc.
5. **Eficiencia:**
   * **Array:** Puede ser más eficiente en términos de memoria y rendimiento para tamaños fijos, ya que no tiene el sobrecoste de gestionar un tamaño dinámico.
   * **ArrayList:** Ofrece mayor flexibilidad, pero puede tener un ligero sobrecoste en términos de rendimiento y memoria debido a su capacidad dinámica.

#### **Recomendaciones:**

* **Arrays:** Son más adecuados cuando conoces el tamaño fijo de tus datos y no necesitas cambiarlo durante la ejecución.
* **ArrayList:** Son más flexibles y convenientes cuando necesitas un tamaño dinámico y operaciones frecuentes de inserción o eliminación de elementos.

En general, la elección entre Arrays y ArrayList depende de las necesidades específicas de tu programa. Si la flexibilidad y la manipulación dinámica del tamaño son importantes, opta por ArrayList. Si el tamaño es fijo y conocido de antemano, un array puede ser más eficiente.

> Aun asi, en la mayoria de los casos siempre va a ser mas recomendable utilizar `ArrayList`, gracias a todas su opciones. Pocas veces vas a ver una gran deferencia en terminos de eficiencia al usar `Array` en vez de `ArrayList`.

