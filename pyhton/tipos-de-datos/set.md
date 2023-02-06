# Set

La función `set` en Python es una estructura de datos de tipo conjunto que permite almacenar elementos únicos y sin un orden definido. Esto significa que un conjunto no permite elementos repetidos y no mantiene ningún orden específico.

La cabecera de la función `set` es la siguiente:

```python
set(iterable)
```

* `iterable`: Una secuencia (por ejemplo, una lista, una tupla, etc.) que se quiere convertir en un conjunto.

Ejemplo:

```python
colors = ['red', 'green', 'blue', 'red', 'green']
color_set = set(colors)
print(color_set)

# Salida:
# {'blue', 'green', 'red'}
```

En este ejemplo, estamos creando un conjunto `color_set` a partir de la lista `colors`. Al hacer esto, los elementos repetidos se eliminan y solo se mantiene una copia de cada elemento único.

### Set Vs Listas

Las principales diferencias entre las listas y los conjuntos (`set`) en Python son las siguientes:

1. **Elementos únicos**: Los conjuntos no permiten elementos repetidos, mientras que las listas sí.
2. **Orden:** Los elementos en un conjunto no tienen un orden específico, mientras que los elementos en una lista sí tienen un orden.
3. **Búsqueda:** La búsqueda de un elemento en un conjunto es más rápida que en una lista, ya que los conjuntos utilizan una estructura de datos interna que permite realizar búsquedas en tiempo constante. En cambio, las búsquedas en una lista tienen un tiempo lineal en función de la longitud de la lista.
4. **Modificación**: Los conjuntos se pueden modificar (agregar o eliminar elementos), mientras que las listas también se pueden modificar.
5. **Operaciones de conjuntos:** Los conjuntos permiten realizar operaciones de conjuntos, como la unión, la intersección y la diferencia, de una manera fácil y eficiente.

En resumen, las listas son útiles cuando se requiere un orden y se pueden permitir elementos repetidos, mientras que los conjuntos son útiles cuando se requiere un conjunto de elementos únicos y no se necesita un orden específico.

### Métodos sets <a href="#metodos-sets" id="metodos-sets"></a>

Aquí hay una lista de los métodos más comunes en conjuntos (`set`) en Python y un ejemplo de cómo usarlos:

#### add

Este método agrega un elemento al conjunto. Si el elemento ya existe en el conjunto, no se agrega.

```python
# Crear un conjunto vacío
colores = set()

# Agregar elementos al conjunto
colores.add("rojo")
colores.add("verde")

# Imprimir el conjunto
print(colores)

# Salida: {'rojo', 'verde'}
```

#### remove

Este método elimina un elemento del conjunto. Si el elemento no existe en el conjunto, se genera una excepción `KeyError`.

```python
# Crear un conjunto de números
numeros = {1, 2, 3, 4, 5}

# Eliminar un elemento del conjunto
numeros.remove(3)

# Imprimir el conjunto
print(numeros)

# Salida: {1, 2, 4, 5}
```

#### `pop` <a href="#spop" id="spop"></a>

El método `pop()` elimina un elemento aleatorio del `set`.

```python
s = set([1, 2])
s.pop()
print(s) #{2}
```

#### union

Este método devuelve un nuevo conjunto que es la unión de dos conjuntos.

```python
# Crear dos conjuntos
conjunto1 = {1, 2, 3}
conjunto2 = {3, 4, 5}

# Unir los conjuntos
unido = conjunto1.union(conjunto2)

# Imprimir el conjunto unido
print(unido)

# Salida: {1, 2, 3, 4, 5}
```

El operador `|` nos permite realizar la **unión** de dos sets, lo que equivale a juntarlos. El equivalente es el método `union()` que vemos a continuación.

```python
s1 = set([1, 2, 3])
s2 = set([3, 4, 5])
print(s1 | s2) #{1, 2, 3, 4, 5}
```

#### intersection

Este método devuelve un nuevo conjunto que es la intersección de dos conjuntos.

```python
# Crear dos conjuntos
conjunto1 = {1, 2, 3}
conjunto2 = {2, 3, 4}

# Intersecar los conjuntos
intersectado = conjunto1.intersection(conjunto2)

# Imprimir el conjunto intersectado
print(intersectado)

# Salida: {2, 3}
```

#### difference

Este método devuelve un nuevo conjunto que es la diferencia de dos conjuntos.

```python
# Crear dos conjuntos
conjunto1 = {1, 2, 3}
conjunto2 = {2, 3, 4}

# Calcular la diferencia de los conjuntos
diferencia = conjunto1.difference(conjunto2)

# Imprimir la diferencia de los conjuntos
print(diferencia)

# Salida: {1}
```
