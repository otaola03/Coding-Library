# Diccionarios

Un diccionario es una estructura de datos en Python que permite almacenar información de manera ordenada y eficiente. A diferencia de las listas, que se indexan con números enteros, los diccionarios se indexan con claves (`key`), que pueden ser de cualquier tipo inmutable, como cadenas, números y tuplas.

Algunas propiedades de los diccionario en Python son las siguientes:

* Son **dinámicos**, pueden crecer o decrecer, se pueden añadir o eliminar elementos.
* Son **indexados**, los elementos del diccionario son accesibles a través del `key`.
* Y son **anidados**, un diccionario puede contener a otro diccionario en su campo `value`.

### Crear diccionarios

En Python, existen varias formas de crear un diccionario, las cuales se detallan a continuación:

```python
d1 = {
  "Nombre": "Sara",
  "Edad": 27,
  "Documento": 1003882
}
print(d1)
#{'Nombre': 'Sara', 'Edad': 27, 'Documento': 1003882}
```

Otra forma equivalente de crear un diccionario en Python es usando `dict()` e introduciendo los pares `key: value` entre paréntesis.

```python
d2 = dict([
      ('Nombre', 'Sara'),
      ('Edad', 27),
      ('Documento', 1003882),
])
print(d2)
#{'Nombre': 'Sara', 'Edad': '27', 'Documento': '1003882'}
```

También es posible usar el constructor `dict()` para crear un diccionario.

```python
d3 = dict(Nombre='Sara',
          Edad=27,
          Documento=1003882)
print(d3)
#{'Nombre': 'Sara', 'Edad': 27, 'Documento': 1003882}
```

### Acceder al diccionario

Para acceder a un valor en un diccionario, puedes usar su clave dentro de corchetes `[]`. Por ejemplo, si tienes un diccionario `d` con una clave `'nombre'`, puedes acceder a su valor de la siguiente manera:

```python
pythonCopy coded = {'nombre': 'Juan', 'edad': 30}
print(d['nombre'])  # imprime 'Juan'
```

Para cambiar el valor de una clave existente en un diccionario, simplemente asigna un nuevo valor a esa clave. Por ejemplo:

```python
d = {'nombre': 'Juan', 'edad': 30}
d['edad'] = 31  # cambia el valor de la clave 'edad'
print(d)  # imprime {'nombre': 'Juan', 'edad': 31}
```

En el caso de que no exista dicha key, python agregara automaticamente la key al diccionario y le asignara el valor especificado.

En el caso de que desees acceder a las keys y no a el valor de lass keys tienes acceder a las `keys` utilizando el metodo `keys()` y convertirlas en una lista para luego poder acceder a ellas mediante un indice.

```python
print(list(d.keys())[0])    #Imprime 'nombre'
```

Iterar diccionarios

Los diccionarios se pueden iterar de manera muy similar a las listas u otras estructuras de datos. Para imprimir los `key`.

```python
# Imprime los key del diccionario
for x in d1:
    print(x)
#Nombre
#Edad
#Documento
#Direccion
```

Se puede imprimir también solo el `value`.

```python
# Impre los value del diccionario
for x in d1:
    print(d1[x])
#Laura
#27
#1003882
#Calle 123
```

O si queremos imprimir el `key` y el `value` a la vez.

```python
# Imprime los key y value del diccionario
for x, y in d1.items():
    print(x, y)
#Nombre Laura
#Edad 27
#Documento 1003882
#Direccion Calle 123
```

### Metodos

#### Claves (keys)

El método `keys()` devuelve una vista de todas las claves del diccionario.

```python
pythonCopy coded = {"a": 1, "b": 2, "c": 3}
print(d.keys())  # dict_keys(['a', 'b', 'c'])
```

#### Valores (values)

El método `values()` devuelve una vista de todos los valores del diccionario.

```python
d = {"a": 1, "b": 2, "c": 3}
print(d.values())  # dict_values([1, 2, 3])
```

#### Ítems (items)

El método `items()` devuelve una vista de tuplas (clave, valor) para cada par clave-valor del diccionario.

```python
d = {"a": 1, "b": 2, "c": 3}
print(d.items())  # dict_items([('a', 1), ('b', 2), ('c', 3)])
```

#### Acceder a un valor (get)

El método `get()` devuelve el valor correspondiente a una clave. Si la clave no existe, devuelve un valor predeterminado.

```python
d = {"a": 1, "b": 2, "c": 3}
print(d.get("a"))  # 1
print(d.get("x", 0))  # 0
```

#### Eliminar un elemento (pop)

El método `pop()` elimina y devuelve el valor correspondiente a una clave. Si la clave no existe, lanza una excepción.

```python
d = {"a": 1, "b": 2, "c": 3}
print(d.pop("b"))  # 2
```

#### Agregar o actualizar un elemento (update)

El método `update()` agrega o actualiza elementos de un diccionario con elementos de otro diccionario.

```python
d1 = {"a": 1, "b": 2}
d2 = {"c": 3, "d": 4}
d1.update(d2)
print(d1)  # {'a': 1, 'b': 2, 'c': 3, 'd': 4}
```
