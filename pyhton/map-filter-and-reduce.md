# Map, Filter and Reduce

### Map

La función `map()` es una función incorporada en Python que se utiliza para aplicar una función a cada elemento de una lista o iterador y devolver un nuevo objeto iterable con los resultados.

**Sintaxis**

La sintaxis básica de la función map() es la siguiente:

```scss
map(function, iterable, ...)
```

Donde:

* `function`: es la función que se aplicará a cada elemento del iterable.
* `iterable`: es el iterable al que se aplicará la función.

Podemos proporcionar uno o más iterables como argumentos adicionales. En este caso, la función que se aplica a cada elemento debe aceptar tantos argumentos como iterables se hayan proporcionado.

**Ejemplos**

1. Aplicar una función a cada elemento de una lista:

Supongamos que tenemos una lista de números y queremos calcular el cuadrado de cada número. Podemos usar la función `map()` junto con una función lambda para lograr esto de la siguiente manera:

```python
nums = [1, 2, 3, 4, 5]
squares = list(map(lambda x: x**2, nums))
print(squares)  # Output: [1, 4, 9, 16, 25]
```

En este ejemplo, pasamos una función lambda que eleva cada elemento al cuadrado como el primer argumento de la función `map()`. Luego, pasamos la lista de números como el segundo argumento. Finalmente, usamos la función `list()` para convertir el objeto map en una lista.

2. Aplicar una función a dos o más listas:

También podemos aplicar una función a elementos correspondientes de dos o más listas. En este caso, la función debe aceptar tantos argumentos como iterables se hayan proporcionado. Supongamos que tenemos dos listas y queremos calcular la suma de los elementos correspondientes. Podemos hacerlo de la siguiente manera:

```python
a = [1, 2, 3, 4, 5]
b = [10, 20, 30, 40, 50]
sums = list(map(lambda x, y: x + y, a, b))
print(sums)  # Output: [11, 22, 33, 44, 55]
```

En este ejemplo, pasamos una función lambda que toma dos argumentos (x e y) y devuelve su suma. Luego, pasamos las dos listas como argumentos adicionales.

3. Aplicar una función a una cadena:

También podemos aplicar una función a cada carácter de una cadena. En este caso, la función debe aceptar un solo argumento. Supongamos que tenemos una cadena y queremos convertir cada carácter a su correspondiente valor entero en la tabla ASCII. Podemos hacerlo de la siguiente manera:

```python
string = 'hello'
ascii_vals = list(map(ord, string))
print(ascii_vals)  # Output: [104, 101, 108, 108, 111]
```

En este ejemplo, pasamos la función `ord()` que convierte cada carácter a su valor entero en la tabla ASCII como el primer argumento de la función `map()`. Luego, pasamos la cadena como el segundo argumento. Finalmente, usamos la función `list()` para convertir el objeto map en una lista.

### Filter

En Python, la función `filter()` se utiliza para filtrar elementos de una secuencia según una función dada. La función `filter()` devuelve un objeto de tipo iterador que contiene los elementos de la secuencia para los cuales la función dada devuelve `True`.

La sintaxis básica de la función `filter()` es la siguiente:

```python
filter(función, secuencia, ...)
```

donde `función` es la función que se aplicará a cada elemento de la `secuencia`, y `secuencia` es la secuencia que se desea filtrar. La función `función` debe tomar un argumento y devolver `True` o `False` según se desee incluir o excluir el elemento de la secuencia.

#### Ejemplo de uso de la función Filter

Supongamos que se desea filtrar una lista de números para obtener solo los números pares. Se puede utilizar la función `filter()` junto con una función lambda (función anónima) para lograr esto:

```python
numeros = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
pares = list(filter(lambda x: x % 2 == 0, numeros))
print(pares) # Output: [2, 4, 6, 8, 10]
```

En este ejemplo, la función lambda `lambda x: x % 2 == 0` toma un argumento `x` y devuelve `True` si `x` es par y `False` en caso contrario. La función `filter()` aplica esta función a cada elemento de la lista `numeros` y devuelve un iterador que contiene solo los números pares.

#### Usando filter() con Funciones definidas por el usuario

También se puede utilizar una función definida por el usuario en lugar de una función lambda con la función `filter()`. Por ejemplo, supongamos que se desea filtrar una lista de cadenas para obtener solo las que contienen un carácter determinado:

```python
def contiene_letra(letra, cadena):
    return letra in cadena

palabras = ['hola', 'adios', 'python', 'programacion']
con_h = list(filter(lambda x: contiene_letra('h', x), palabras))
print(con_h) # Output: ['hola']
```

En este ejemplo, la función `contiene_letra()` toma dos argumentos, `letra` y `cadena`, y devuelve `True` si la letra se encuentra en la cadena y `False` en caso contrario. La función `filter()` aplica esta función a cada elemento de la lista `palabras` y devuelve un iterador que contiene solo las palabras que contienen la letra 'h'.

#### Conclusión

La función `filter()` es una herramienta poderosa para filtrar elementos de una secuencia según una función dada. Se puede utilizar una función lambda o una función definida por el usuario para especificar la condición de filtrado. La función `filter()` devuelve un iterador que contiene solo los elementos de la secuencia que cumplen la condición.
