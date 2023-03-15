# Decoradores

Los decoradores son una forma de modificar o extender la funcionalidad de una función en Python. Básicamente, un decorador es una función que toma otra función y la modifica sin cambiar el código fuente original.

Estos se utilizan para agregar funcionalidad a una función existente sin tener que modificar su código fuente original. Esto puede ser útil para agregar características como verificación de entrada, registro de llamadas o temporización a una función sin tener que agregar esta funcionalidad a la función en sí.

{% embed url="https://www.youtube.com/watch?v=FsAPt_9Bf3U" %}

### ¿Cómo se crean los decoradores?

Para crear un decorador en Python, simplemente definimos una función que tome otra función como argumento y devuelva una función modificada. Por ejemplo, si queremos crear un decorador que imprima un mensaje antes y después de la ejecución de una función, podemos hacerlo de la siguiente manera:

```python
def decorator(func):
    def wrapper(*args, **kwargs):
        # código que se ejecuta antes de la función original
        result = func(*args, **kwargs)
        # código que se ejecuta después de la función original
        return result
    return wrapper
```

En este ejemplo, el decorador "decorator" toma una función "func" como argumento. La función "wrapper" se define dentro del decorador y toma cualquier número de argumentos posicionales y de palabras clave. La función "wrapper" ejecuta algún código antes y después de llamar a la función original "func". La función "wrapper" devuelve el resultado de la función original.

Para aplicar este decorador a una función, simplemente coloque el símbolo "@" antes del nombre del decorador sobre la definición de la función:

```python
@decorator
def my_function():
    # código de la función original
```

Esta es la manera habitual en la que se aplica un decorador, sin embargo lo que esta aciendo internamente es asignar la funcion `wraper()` devuelta por el decorador `decorator()` a nuestra funcion `my_function()`. El sigueinte codigo hace los mimso que el mostrado anteriormente:

```python
my_function = decorator(my_function)
```

#### ¿Que es el wrapper?

El `wrapper` es una función que se utiliza en la creación de decoradores. Su función principal es envolver la función original, que se quiere decorar, dentro de otra función que agrega alguna funcionalidad adicional sin modificar la función original.

El `wrapper` es una función interna que se define dentro de la función decoradora y que tiene acceso a la función original y a los argumentos que se le pasan. Es decir, el `wrapper` es la función que se ejecuta antes y después de la función original, y puede hacer cualquier cosa que se necesite antes o después de la llamada a la función original

Por ejemplo, si se tiene el siguiente decorador que agrega una función adicional de impresión antes de la llamada a la función original:

```python
my_decorator(func):
    def wrapper(*args, **kwargs):
        print("Calling the function")
        return func(*args, **kwargs)
    return wrapper
```

En este caso, `wrapper` es la función interna que envuelve a la función original `func`. `*args` y `**kwargs` permiten que el decorador acepte cualquier número de argumentos y parámetros, lo que es útil en caso de que se quiera aplicar el decorador a una función con diferentes números de argumentos y parámetros.

En la última línea del decorador, la función `wrapper` se retorna para que se pueda hacer la reasginacion de la funcion de la que se ha hablado anteriormente

#### Decoradores con argumentos

Es importante tener en cuenta que los decoradores también pueden recibir argumentos. Para ello, debemos definir una función que devuelva el decorador deseado. Por ejemplo, si queremos un decorador que acepte un argumento entero y añada ese número de saltos de línea después de la ejecución de la función original, podemos definirlo de la siguiente manera:

```python
def newline_decorator(num_lines):
    def actual_decorator(func):
        def wrapper(*args, **kwargs):
            result = func(*args, **kwargs)
            print("\n" * num_lines)
            return result
        return wrapper
    return actual_decorator
```

Para utilizar este decorador con argumentos, simplemente debemos llamar a la función que devuelve el decorador con los argumentos deseados y colocar el resultado encima de la definición de la función que queremos decorar.

```python
@newline_decorator(3)
def my_function():
    print("Hello, world!")
```

En este caso, la función `my_function()` será decorada con un salto de línea de tres líneas después de su ejecución.

```python
>>> my_function()
Hello, world!



```

### Ejemplos de decoradores en Python

#### Decorador de temporización

Un decorador de temporización se puede utilizar para medir el tiempo de ejecución de una función. Por ejemplo, si queremos medir el tiempo que tarda una función en ejecutarse, podemos usar el siguiente decorador:

```python
import time

def temporizador(func):
    def wrapper(*args, **kwargs):
        inicio = time.time()
        resultado = func(*args, **kwargs)
        fin = time.time()
        print(f"La función {func.__name__} tardó {fin - inicio} segundos en ejecutarse.")
        return resultado
    return wrapper
```

Para aplicar este decorador a una función, podemos usar la sintaxis @temporizador antes de la definición de la función:

```ruby
@temporizador
def mi_funcion():
    # Código de la función
```

#### Decorador de registro de llamadas

Un decorador de registro de llamadas se puede utilizar para registrar todas las llamadas a una función. Por ejemplo, si queremos registrar todas las llamadas a una función y escribir las llamadas en un archivo de registro, podemos usar el siguiente decorador:

```python
def registro_de_llamadas(func):
    def wrapper(*args, **kwargs):
        resultado = func(*args, **kwargs)
        with open("registro.txt", "a") as f:
            f.write(f"{func.__name__} fue llamado con los siguientes argumentos: {args}, {kwargs}\n")
        return resultado
    return wrapper
```

Para aplicar el decorador a una función, simplemente debemos colocar el símbolo @ seguido del nombre del decorador encima de la definición de la función que queremos decorar. Por ejemplo:

```python
@my_decorator
def my_function():
    print("Hello, world!")
```

En este ejemplo, la función `my_function()` será decorada con el decorador `my_decorator`. Al llamar a `my_function()`, en realidad estaremos llamando a la función devuelta por el decorador, que a su vez llamará a la función original.

```python
>>> my_function()
Before the function runs
Hello, world!
After the function runs
```

Podemos ver que el decorador ha añadido funcionalidad antes y después de la ejecución de la función original.
