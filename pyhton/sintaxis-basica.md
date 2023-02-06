# Sintaxis basica

### Tipos de datos

Los tipos en Python son categorías que se utilizan para clasificar los valores. Cada valor en Python tiene un tipo que indica qué operaciones se pueden realizar con ese valor. Algunos de los tipos más comunes en Python son:

* **int:** Entero, un número sin parte decimal (ej. 1, 2, 3, -10)
* **float**: Punto flotante, un número con parte decimal (e.g. 1.0, -0.5, 3.14)
* **str:** Cadena de caracteres, una secuencia de texto encerrada entre comillas (ej. "Hola", "perro", "123")
* **bool:** Valor booleano, que puede ser True o False
* l**ist:** Lista, una colección ordenada de valores de cualquier tipo (ej. \[1, 2, 3], \["Hola", "Mundo"], \[1, "dos", 3.0])
* **tuple:** Tupla, similar a la lista pero inmutable (es decir, no se pueden cambiar los elementos una vez definidos) (ej. (1, 2, 3), ("Hola", "Mundo"), (1, "dos", 3.0))
* **set:** Conjunto, una colección sin orden y sin elementos repetidos (ej. {1, 2, 3}, {"Hola", "Mundo"}, {1, "dos", 3.0})
* **dict:** Diccionario, una colección de pares clave-valor (ej. {'nombre': 'Juan', 'edad': 30}, {1: 'Hola', 2: 'Mundo'})

<figure><img src="../.gitbook/assets/Screen Shot 2023-01-31 at 1.39.01 PM.png" alt=""><figcaption></figcaption></figure>

Python es un lenguaje dinámico, lo que significa que **no es necesario especificar el tipo de una variable cuando se declara**. Python asignará el tipo adecuado a la variable en función del valor que se le asigne.

{% hint style="info" %}
Para poder ver de que tipo es una variable se puede utilizar la funcion `type`. Por ejemplo:&#x20;

`type(numero)` nos devolvera `<class 'str'>`
{% endhint %}

### Operadores

Los operadores son símbolos especiales en Python que realizan operaciones matemáticas o lógicas con los valores (o variables que contienen valores).

<figure><img src="../.gitbook/assets/Screen Shot 2023-01-31 at 1.44.01 PM.png" alt=""><figcaption></figcaption></figure>

Además de los operadores aritméticos, de asignación, de comparación y lógicos que mencioné en mi respuesta anterior, hay otros operadores especiales en Python que se utilizan en diferentes situaciones:

* Operadores de pertenencia:
  * in: Verifica si un elemento está en una secuencia (por ejemplo, una lista o una cadena).
  * not in: Verifica si un elemento no está en una secuencia.
* Operadores de identidad:
  * is: Verifica si dos variables son el mismo objeto en la memoria.
  * is not: Verifica si dos variables no son el mismo objeto en la memoria.

### print

La función `print` es una función incorporada en Python que se utiliza para imprimir información en la consola o en un archivo. La sintaxis general de la función `print` es:

```python
print(*objects, sep=' ', end='\n', file=sys.stdout, flush=False)
```

* `objects`: Son los objetos que se van a imprimir. Puede haber uno o más objetos separados por comas.
* `sep`: Especifica el separador que se utilizará entre los objetos impresos. Por defecto, el separador es un espacio en blanco.
* `end`: Especifica el carácter o cadena que se agregará al final de la impresión. Por defecto, se agrega un salto de línea ('\n').
* `file`: Especifica el archivo donde se escribirá la salida. Por defecto, la salida se escribe en la consola (`sys.stdout`).
* `flush`: Especifica si se debe forzar un vaciado del buffer de salida después de escribir. Por defecto, `flush` es `False`.

Aquí hay algunos ejemplos de uso de la función `print` en Python:

```python
# Imprimir una cadena
print("Hola mundo")

# Imprimir un número
print(123)

# Imprimir varios objetos separados por una coma
print("El número es", 123)

# Imprimir varios objetos separados por un espacio
print("El número es", 123, sep=" ")

# Imprimir varios objetos separados por un guión
print("El número es", 123, sep="-")

# Imprimir varios objetos sin salto de línea al final
print("El número es", 123, end="")
```

Es importante tener en cuenta que la función `print` convierte automáticamente los objetos en cadenas antes de imprimirlos, por lo que es posible imprimir cualquier tipo de objeto en Python, incluidos números, listas, diccionarios, etc.
