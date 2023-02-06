# Iterar con For

El bucle `for` en Python es una estructura de control que se utiliza para repetir un bloque de código varias veces. Se utiliza para iterar sobre un objeto iterable, como una lista, una tupla, un diccionario, un conjunto, etc.

La sintaxis del bucle `for` en Python es la siguiente:

```python
variable in objeto_iterable:
    # bloque de código a repetir
```

Donde `variable` es una variable que se asigna a cada elemento del objeto iterable en cada iteración del bucle, y `objeto_iterable` es un objeto que contiene elementos que se deben iterar.

Aquí hay un ejemplo de código que muestra cómo usar un bucle `for` para imprimir los números en una lista:

```python
numbers = [1, 2, 3, 4, 5]
for num in numbers:
    print(num)
```

Iterando cadena al revés. Haciendo uso de `[::-1]` se puede iterar la lista desde el último al primer elemento.&#x20;

```python
texto = "Python"
for i in texto[::-1]:
    print(i) #n,o,h,t,y,P
```

Itera la cadena saltándose elementos. Con `[::2]` vamos tomando un elemento si y otro no.

```python
texto = "Python"
for i in texto[::2]:
    print(i) #P,t,o
```

#### range

`range` es una función en Python que se utiliza para generar una secuencia de números, por lo general con fines de iteración. La cabecera de la función `range` es la siguiente:

```python
range(start, stop, step)
```

Ejempo:

```python
# Genera una secuencia de números del 0 al 9 (10 números)
for i in range(10):
    print(i)

# Genera una secuencia de números del 2 al 9 (7 números)
for i in range(2, 10):
    print(i)

# Genera una secuencia de números del 2 al 12, saltando de 2 en 2 (5 números)
for i in range(2, 13, 2):
    print(i)
```

Es importante destacar que `range` genera un objeto de tipo `range`, no una lista. Para convertirlo en una lista, se puede utilizar la función `list`.

#### iterables

Un iterable en Python es un objeto que contiene una secuencia de elementos y se puede recorrer en un bucle. Los iterables son una parte fundamental de la programación en Python y se usan ampliamente en muchas tareas.

Algunos ejemplos de iterables en Python incluyen listas, tuplas, diccionarios, conjuntos, cadenas de texto, archivos y objetos personalizados que implementan el método `__iter__` o el protocolo de iteración.

Para recorrer un iterable, se puede usar el bucle `for`. La sintaxis para hacer una iteración sobre un iterable es la siguiente:

```python
for elemento in iterable:
    # hacer algo con el elemento
```

Donde `iterable` es el objeto iterable que se va a recorrer y `elemento` es una variable que se asigna a cada elemento del iterable en cada iteración.

Tiene bastante sentido, porque si queremos iterar una variable, esta variable debe ser **iterable**, todo muy lógico. Pero llegados a este punto, tal vez de preguntes ¿pero cómo se yo si algo es iterable o no?. Bien fácil, con la siguiente función `isinstance()` podemos saberlo. No te preocupes si no entiendes muy bien lo que estamos haciendo, fíjate solo en el resultado, `True` significa que es iterable y `False` que no lo es.

```python
from collections import Iterable
lista = [1, 2, 3, 4]
cadena = "Python"
numero = 10
print(isinstance(lista, Iterable))  #True
print(isinstance(cadena, Iterable)) #True
print(isinstance(numero, Iterable)) #False
```

Por lo tanto las listas y las cadenas son iterables, pero `numero`, que es un entero no lo es. Es por eso por lo que no podemos hacer lo siguiente, ya que daría un error. De hecho el error sería `TypeError: int' object is not iterable`.

#### iteradores

Un iterador en Python es un objeto que permite recorrer y acceder secuencialmente a los elementos de una colección, como una lista o una tupla. Un iterador es similar a un iterable, pero tiene algunas diferencias clave.

Una de las principales diferencias es que un iterador solo permite acceder a sus elementos una vez, y no se puede volver a utilizar después de haber recorrido la colección completa. Esto se conoce como iteración única.

Otra diferencia es que los iteradores se pueden crear a partir de un iterable usando la función `iter`:

```python
snumbers = [1, 2, 3, 4, 5]
numbers_iterator = iter(numbers)
print(it)       #<list_iterator object at 0x106243828>
print(type(it)) #<class 'list_iterator'>
```

Una vez que se tiene un iterador, se puede acceder a sus elementos usando la función `next`:

```python
print(next(numbers_iterator))  # imprime 1
print(next(numbers_iterator))  # imprime 2
```

Dado que el iterador hace referencia a nuestra lista, si llamamos más veces a `next()` que la longitud de la lista, se nos devolverá un error `StopIteration`. Lamentablemente no existe ninguna opción de volver al elemento anterior.

Los iteradores son útiles porque permiten recorrer y acceder a los elementos de una colección de manera eficiente y controlada. Algunas de las utilidades principales de los iteradores incluyen:

1. Ahorro de memoria: Los iteradores permiten recorrer una colección un elemento a la vez, en lugar de almacenar todos los elementos en la memoria a la vez. Esto es especialmente útil cuando se trabaja con colecciones muy grandes.
2. Control de la iteración: Los iteradores permiten controlar la iteración sobre una colección, ya sea recorriendo la colección de manera secuencial o saltándose elementos específicos.
3. Mejor rendimiento: Al trabajar con colecciones muy grandes, los iteradores pueden mejorar el rendimiento de su código, ya que permiten recorrer la colección de manera eficiente.
4. Reutilizabilidad: Los iteradores pueden ser reutilizados en diferentes partes de su código, lo que puede ayudar a mantener su código limpio y organizado.

Es perfectamente posible tener diferentes iteradores para la misma lista, y serán totalmente independientes. Tan solo dependerán de la lista, como es evidente, pero no entre ellos.

```python
lista = [5, 6, 7]
it1 = iter(lista)
it2 = iter(lista)
print(next(it1)) #5
print(next(it1)) #6
print(next(it1)) #7
print(next(it2)) #5
```

#### enumerate

`enumerate` es una función en Python que se utiliza para iterar sobre una secuencia (como una lista, una cadena, etc.) y además mantener un registro del índice del elemento actual. La cabecera de la función `enumerate` es la siguiente:

```python
enumerate(iterable, start=0)
```

* `iterable`: La secuencia que se quiere iterar.
* `start` (opcional): El índice inicial. Por defecto es 0.

Ejemplo:

```python
# Enumerar los elementos de una lista
colors = ['red', 'green', 'blue']
for i, color in enumerate(colors):
    print(i, color)

# Salida:
# 0 red
# 1 green
# 2 blue
```

En un bucle `for`, `enumerate` permite iterar sobre los elementos de una secuencia mientras se mantiene un registro del índice de cada elemento. Esto es útil en muchos casos, por ejemplo, para imprimir tanto el elemento como su índice o para acceder a elementos específicos de una secuencia basados en su índice.

Por último, es importante notar que su uso no se limita únicamente a bucles `for`. Podemos convertir el tipo `enumerate` en una lista de tuplas, donde cada una contiene un elemento de la colección inicial y el índice asociado.

```python
lista = ["A", "B", "C"]

en = list(enumerate(lista))
print(en)

# Salida;
# [(0, 'A'), (1, 'B'), (2, 'C')]
```
