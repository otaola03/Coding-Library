# Iterar con enumerate

La función `enumerate` es una función integrada en Python que te permite iterar sobre un objeto iterable, al mismo tiempo que obtienes el índice y el valor correspondiente de cada elemento. La función devuelve un objeto de tipo `enumerate`, que contiene tuplas de dos elementos: el índice y el valor.

La sintaxis de la función `enumerate` es la siguiente:

```python
enumerate(iterable, start=0)
```

Donde:

* `iterable`: es el objeto iterable que quieres recorrer.
* `start`: es un argumento opcional que indica el valor inicial del índice. Por defecto es 0.

Veamos algunos ejemplos para entender mejor cómo funciona.

### Iterar sobre una lista con `enumerate`

Supongamos que tienes una lista de nombres, y quieres imprimir cada nombre junto con su índice correspondiente. Puedes hacerlo de la siguiente manera:

```python
nombres = ['Juan', 'María', 'Pedro', 'Ana']
for indice, nombre in enumerate(nombres):
    print(f'{indice}: {nombre}')
```

En este ejemplo, `enumerate` te devuelve una tupla de dos elementos en cada iteración, donde el primer elemento es el índice (0, 1, 2, 3) y el segundo elemento es el valor correspondiente de la lista (`'Juan'`, `'María'`, `'Pedro'`, `'Ana'`).

La salida de este código sería:

```python
0: Juan
1: María
2: Pedro
3: Ana
```

### Creacion de listas

Además de usar `enumerate` para iterar sobre objetos iterables, también puedes utilizarlo para crear listas de tuplas que contengan el índice y el valor correspondiente de cada elemento del objeto iterable.

Por ejemplo, supongamos que tienes una lista de nombres, y quieres crear una lista de tuplas que contenga el índice y el nombre correspondiente de cada elemento. Puedes hacerlo de la siguiente manera:

```python
nombres = ['Juan', 'María', 'Pedro', 'Ana']
lista_tuplas = list(enumerate(nombres))
print(lista_tuplas)
```

En este caso, `enumerate` te devuelve una tupla de dos elementos en cada iteración, donde el primer elemento es el índice (0, 1, 2, 3) y el segundo elemento es el valor correspondiente de la lista (`'Juan'`, `'María'`, `'Pedro'`, `'Ana'`). La función `list` se utiliza para convertir el objeto `enumerate` en una lista de tuplas.

La salida de este código sería:

```python
[(0, 'Juan'), (1, 'María'), (2, 'Pedro'), (3, 'Ana')]
```

De esta manera, puedes crear fácilmente una lista de tuplas que contenga el índice y el valor correspondiente de cada elemento de la lista original.

También puedes utilizar esta técnica para crear listas de tuplas a partir de otros objetos iterables, como diccionarios, conjuntos o incluso rangos de números. Solo debes asegurarte de utilizar el objeto iterable correcto como argumento de la función `enumerate`.

En resumen, `enumerate` es una función muy versátil en Python que te permite no solo iterar sobre objetos iterables, sino también crear listas de tuplas que contengan el índice y el valor correspondiente de cada elemento.
