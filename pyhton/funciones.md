# Funciones

Las funciones en Python son bloques de código que se pueden reutilizar para realizar tareas específicas. Las funciones se definen mediante la palabra clave `def`, seguida del nombre de la función y los argumentos de entrada entre paréntesis. La sintaxis básica de una función en Python es:

```python
def nombre_funcion(arg1, arg2, ...):
    # Código de la función
    # ...
    return resultado
```

* `nombre_funcion` es el nombre de la función que se define.
* `arg1, arg2, ...` son los argumentos de entrada de la función, que son valores o variables que se pasan a la función para su procesamiento.
* `resultado` es el resultado que se devuelve al final de la función. El valor devuelto se puede asignar a una variable o usar directamente.

Aquí hay un ejemplo de una función en Python que toma dos números como argumentos y devuelve su suma:

```python
def suma(a, b):
    result = a + b
    return result

# Llamar a la función
resultado = suma(1, 2)
print(resultado)  # 3
```

En Python, las funciones también pueden tener argumentos opcionales con valores predeterminados, que se proporcionan cuando la función se llama sin especificar ese argumento. La sintaxis para argumentos opcionales es:

```python
def nombre_funcion(arg1, arg2=valor_predeterminado):
    # Código de la función
    # ...
    return resultado
```

Aquí hay un ejemplo de una función que tiene un argumento opcional con un valor predeterminado:

```python
def saluda(nombre, mensaje="Hola"):
    print(mensaje, nombre)

# Llamar a la función sin especificar el mensaje
saluda("Juan")  # Hola Juan

# Llamar a la función con un mensaje especificado
saluda("Juan", "Buen día")  # Buen día Juan
```

## Args y Kwargs <a href="#args-y-kwargs-en-python" id="args-y-kwargs-en-python"></a>

Además de estos, existen también funciones con un número variable de argumentos, que se pueden pasar como una tupla o un diccionario. Para hacer esto se pueden utilizar los siguientes marcadores:

* `*args`: permite recibir un número variable de argumentos como una tupla.
* `**kwargs`: permite recibir un número variable de argumentos con nombre como un diccionario.

Aquí hay un ejemplo de una función que recibe un número variable de argumentos y los imprime:

```python
def imprimir_argumentos(*args):
    for arg in args:
        print(arg)

# Llamar a la función con diferentes argumentos
imprimir_argumentos(1, 2, 3)
# 1
# 2
# 3

imprimir_argumentos("Hola", "Mundo")
# Hola
# Mundo
```

Y aquí hay un ejemplo de una función que recibe un número variable de argumentos con nombre y los imprime:

```python
def imprimir_argumentos_nombre(**kwargs):
    for nombre, valor in kwargs.items():
        print(nombre, ":", valor)

# Llamar a la función con diferentes argumentos
imprimir_argumentos_nombre(a=1, b=2, c=3)
# a : 1
# b : 2
# c : 3

imprimir_argumentos_nombre(nombre="Juan", edad=30)
# nombre : Juan
# edad : 30
```

En resumen, las funciones son una herramienta fundamental en Python para escribir código modular y reutilizable. Pueden recibir y procesar argumentos de entrada y devolver resultados, lo que las hace muy útiles para organizar el código en tareas más pequeñas y manejables.

### Funciones Lambda

Las funciones lambda en Python son funciones anónimas que se definen en una sola línea y no tienen un nombre definido. Son útiles para crear funciones pequeñas y simples que se utilizan solo una vez en un programa y no es necesario definirlas formalmente.

Las funciones lambda se definen utilizando la palabra clave `lambda` seguida de una lista de argumentos separados por comas, seguida de dos puntos y una expresión que se evalúa y devuelve un valor. La sintaxis básica es la siguiente:

```python
lambda argument1, argument2, ... : expresion
```

Por ejemplo, para crear una función lambda que tome dos argumentos y los multiplique, podemos escribir:

```python
multiplicar = lambda x, y: x * y
```

Aquí, `multiplicar` es el nombre que se le asigna a la función lambda que acabamos de definir. La función toma dos argumentos, `x` e `y`, y devuelve su producto.

La función lambda se puede utilizar de la misma manera que cualquier otra función en Python. Por ejemplo, podemos llamar a la función `multiplicar` con los argumentos `2` y `3`:

```python
resultado = multiplicar(2, 3)
print(resultado)  # Imprime 6
```

También podemos pasar la función lambda como argumento a otras funciones, como la función `map()`, que aplica una función a cada elemento de una lista.

En resumen, las funciones lambda en Python son una forma de definir funciones pequeñas y simples en una sola línea sin necesidad de darles un nombre formal. Son útiles para crear funciones que se utilizan solo una vez en un programa y para pasar funciones como argumentos a otras funciones.
