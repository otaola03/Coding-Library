# Iterar con zip

`zip` es una función en Python que se utiliza para combinar elementos de varias secuencias (por ejemplo, listas, tuplas, etc.) en una sola secuencia de tuplas. La cabecera de la función `zip` es la siguiente:

```python
zip(*iterables)
```

* `iterables`: Una secuencia o varias secuencias que se quieren combinar.

Ejemplo:

```python
colors = ['red', 'green', 'blue']
codes = [0xff0000, 0x00ff00, 0x0000ff]
color_codes = list(zip(colors, codes))
print(color_codes)

# Salida:
# [('red', 0xff0000), ('green', 0x00ff00), ('blue', 0x0000ff)]
```

En este ejemplo, estamos combinando los elementos de las listas `colors` y `codes` en una sola lista de tuplas `color_codes`.

Es importante destacar que `zip` genera un objeto de tipo `zip`, no una lista. Para convertirlo en una lista, se puede utilizar la función `list`.

Iterar con `zip` en Python es muy similar a iterar con `enumerate`, con la diferencia de que `zip` combina varias secuencias en lugar de mantener un registro del índice.

Ejemplo:

```python
colors = ['red', 'green', 'blue']
codes = [0xff0000, 0x00ff00, 0x0000ff]
for color, code in zip(colors, codes):
    print(color, code)

# Salida:
# red 0xff0000
# green 0x00ff00
# blue 0x0000ff
```

En este ejemplo, estamos iterando sobre las dos secuencias `colors` y `codes` utilizando `zip`. Cada iteración del bucle `for` asigna una tupla de elementos correspondientes a `color` y `code`.

{% hint style="info" %}
Si las secuencias que estás combinando con `zip` tienen diferentes longitudes, `zip` solo combinará los elementos hasta el final de la secuencia más corta.
{% endhint %}

### zip() con diccionarios <a href="#zip-con-diccionarios" id="zip-con-diccionarios"></a>

Hasta ahora nos hemos limitado a usar `zip` con listas, pero la función está definida para cualquier clase [iterable](https://ellibrodepython.com/iterator-python). Por lo tanto podemos usarla también con [diccionarios](https://ellibrodepython.com/diccionarios-en-python).

Si realizamos lo siguiente, `a,b` toman los valores de las key del [diccionario](https://ellibrodepython.com/diccionarios-en-python). Tal vez algo no demasiado interesante.

```python
esp = {'1': 'Uno', '2': 'Dos', '3': 'Tres'}
eng = {'1': 'One', '2': 'Two', '3': 'Three'}

for a, b in zip(esp, eng):
    print(a, b)

# 1 1
# 2 2
# 3 3
```

Sin embargo, si hacemos uso de la función [items](https://ellibrodepython.com/diccionarios-en-python#items), podemos acceder al _key_ y _value_ de cada elemento.

```python
esp = {'1': 'Uno', '2': 'Dos', '3': 'Tres'}
eng = {'1': 'One', '2': 'Two', '3': 'Three'}

for (k1, v1), (k2, v2) in zip(esp.items(), eng.items()):
    print(k1, v1, v2)

# 1 Uno One
# 2 Dos Two
# 3 Tres Three
```

Nótese que en este caso ambas _key_ `k1` y `k2` son iguales.

### Deshacer el zip() <a href="#deshacer-el-zip" id="deshacer-el-zip"></a>

Con un pequeño truco, es posible deshacer el `zip` en una sola línea de código. Supongamos que hemos usado `zip` para obtener `c`.

```python
a = [1, 2, 3]
b = ["One", "Two", "Three"]
c = zip(a, b)

print(list(c))
# [(1, 'One'), (2, 'Two'), (3, 'Three')]
```

¿Es posible obtener `a` y `b` desde `c`? Sí, tan sencillo como:

```python
c = [(1, 'One'), (2, 'Two'), (3, 'Three')]
a, b = zip(*c)

print(a)  # (1, 2, 3)
print(b)  # ('One', 'Two', 'Three')
```

Nótese el uso de `*c`, lo que es conocido como unpacking en Python.
