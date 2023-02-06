---
description: Arrays
---

# Listas

Las listas son una estructura de datos importante en Python que permite almacenar una secuencia ordenada de elementos. Las listas son mutables, lo que significa que se pueden agregar, eliminar o modificar elementos después de su creación.

Aquí hay un ejemplo de cómo crear una lista en Python:

```python
# Crear una lista
mi_lista = [1, 2, 3, 4, 5]
print(mi_lista)  # [1, 2, 3, 4, 5]
```

Algunas propiedades de las listas:

* Son **ordenadas**, mantienen el orden en el que han sido definidas
* Pueden ser formadas por tipos **arbitrarios**
* Pueden ser **indexadas** con `[i]`.
* Se pueden **anidar**, es decir, meter una dentro de la otra.
* Son **mutables**, ya que sus elementos pueden ser modificados.
* Son **dinámicas**, ya que se pueden añadir o eliminar elementos.

Las listas en Python pueden contener elementos de cualquier tipo, incluidos números, cadenas, funciones, otros objetos, etc. Incluso es posible tener una lista de listas.

```python
# Crear una lista de diferentes tipos de elementos
mi_lista = [1, "Hola", 3.14, True, [1, 2, 3]]
print(mi_lista)  # [1, "Hola", 3.14, True, [1, 2, 3]]
```

### Iterar listas <a href="#acceder-y-modificar-listas" id="acceder-y-modificar-listas"></a>

Las listas son objetos iterables, lo que significa que se pueden recorrer para acceder a cada uno de sus elementos. Aquí hay un ejemplo de cómo recorrer una lista:

```python
# Recorrer una lista
mi_lista = [1, 2, 3, 4, 5]
for elemento in mi_lista:
    print(elemento)
# 1
# 2
# 3
# 4
# 5
```

Si necesitamos un índice acompañado con la lista, que tome valores desde `0` hasta `n-1`, se puede hacer de la siguiente manera.

```python
lista = [5, 9, 10]
for index, l in enumerate(lista):
    print(index, l)
#0 5
#1 9
#2 10
```

O si tenemos dos listas y las queremos iterar a la vez, también es posible hacerlo.

```python
lista1 = [5, 9, 10]
lista2 = ["Jazz", "Rock", "Djent"]
for l1, l2 in zip(lista1, lista2):
    print(l1, l2)
#5 Jazz
#9 Rock
#10 Djent
```

Y por supuesto, también se pueden iterar las listas usando los índices como hemos visto al principio, y haciendo uso de `len()`, que nos devuelve la longitud de la lista.

```python
lista1 = [5, 9, 10]
for i in range(0, len(lista)):
    print(lista1[i])
#5
#9
#10
```

### Acceder y modificar valores

También se pueden acceder a los elementos de una lista por su índice, que es un número que indica su posición en la lista. Los índices en Python comienzan en 0. Esto es util para cambiar unicamente un solo elemento de la lista.

```python
# Acceder a un elemento por su índice
mi_lista = [1, 2, 3, 4, 5]
print(mi_lista[0])  # 1
mi_lista[2] = 4
```

En el caso de que quieras acceder al ultimo elementos puede utilizar el indice `-1`. De la misma manera, al igual que `[-1]` es el último elemento, podemos acceder a `[-2]` que será el penúltimo.

```python
a = [90, "Python", 3.87]
print(a[-1]) #3.87
```

{% hint style="info" %}
La asignacion de valores tambien se puede hacer mediante iteracion
{% endhint %}

### Sublistas

también es posible crear sublistas más pequeñas de una más grande. Para ello debemos de usar `:` entre corchetes, indicando a la izquierda el valor de inicio, y a la izquierda el valor final que no está incluido. Por lo tanto `[0:2]` creará una lista con los elementos `[0]` y `[1]` de la original.

```python
l = [1, 2, 3, 4, 5, 6]
print(l[0:2]) #[1, 2]
print(l[2:6]) #[3, 4, 5, 6]
```

Y de la misma manera podemos modificar múltiples valores de la lista a la vez usando `:`.

```python
l = [1, 2, 3, 4, 5, 6]
l[0:3] = [0, 0, 0]
print(l) #[0, 0, 0, 4, 5, 6
```

### Metodos

Hay muchos métodos disponibles en Python para trabajar con listas, aquí hay algunos de los más comunes:

#### `append(element)`

Agrega un elemento al final de la lista.

```python
mi_lista = [1, 2, 3, 4, 5]
mi_lista.append(6)
print(mi_lista)  # [1, 2, 3, 4, 5, 6]
```

#### `extend(list)`

Agrega los elementos de una lista a otra.

```python
mi_lista = [1, 2, 3, 4, 5]
otra_lista = [6, 7, 8]
mi_lista.extend(otra_lista)
print(mi_lista)  # [1, 2, 3, 4, 5, 6, 7, 8]
```

Esto tambien se puede hacer mediante el operador `+`&#x20;

```python
l = [1, 2, 3]
l += [4, 5]
print(l) #[1, 2, 3, 4, 5]
```

#### `insert(index, element)`

Agrega un elemento en una posición específica de la lista.

```python
scssCopy codemi_lista = [1, 2, 3, 4, 5]
mi_lista.insert(2, 6)
print(mi_lista)  # [1, 2, 6, 3, 4, 5]
```

#### `remove(element)`

Elimina el primer elemento con el valor especificado de la lista.

```python
scssCopy codemi_lista = [1, 2, 3, 4, 5]
mi_lista.remove(3)
print(mi_lista)  # [1, 2, 4, 5]
```

#### `pop(index)`

Elimina el elemento en una posición específica de la lista y devuelve su valor.

```python
scssCopy codemi_lista = [1, 2, 3, 4, 5]
elemento = mi_lista.pop(2)
print(mi_lista)  # [1, 2, 4, 5]
print(elemento)  # 3
```

#### `index(element)`

Devuelve la posición del primer elemento con el valor especificado en la lista.

```python
perlCopy codemi_lista = [1, 2, 3, 4, 5]
index = mi_lista.index(3)
print(index)  # 2
```

#### `count(element)`

Devuelve el número de veces que aparece un elemento en la lista.

```python
scssCopy codemi_lista = [1, 2, 3, 4, 3, 5]
count = mi_lista.count(3)
print(count)  # 2
```

#### `sort()`

Ordena los elementos de la lista en orden ascendente.

```python
scssCopy codemi_lista = [5, 3, 1, 4, 2]
mi_lista.sort()
print(mi_lista)  # [1, 2, 3, 4, 5]
```

#### `reverse()`

Invierte el orden de los elementos en la lista.

```python
scssCopy codemi_lista = [1, 2, 3, 4, 5]
mi_lista.clear()
print(mi_lista)  # []
```

#### `clear()`

Elimina todos los elementos de la lista.

```python
mi_lista = [1, 2, 3, 4, 5]
mi_lista.reverse()
print(mi_lista)  # [5, 4, 3, 2, 1]
```

Estos son solo algunos de los métodos más comunes para trabajar con listas en Python. Hay muchos otros disponibles y es posible crear sus propios métodos personalizados también.\
