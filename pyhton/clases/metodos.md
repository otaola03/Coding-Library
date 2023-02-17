# Metodos

En Python, los métodos son funciones que están definidas dentro de una clase y pueden ser llamadas en las instancias de esa clase. Los métodos son una forma de encapsular comportamientos y acciones que están relacionados con la clase en la que se definen.

### Métodos de instancia

Los métodos de instancia son aquellos que se definen dentro de la clase y actúan sobre una instancia de la misma. Esto significa que se pueden acceder a los atributos de instancia y modificarlos.

Un método de instancia se define de la misma manera que una función normal, pero se pasa la palabra clave `self` como primer argumento. `self` se refiere a la instancia que llama al método.

Aquí hay un ejemplo de cómo definir un método de instancia en una clase `Person`:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age
    
    def say_hello(self):
        print(f"Hello, my name is {self.name} and I'm {self.age} years old.")
```

En este ejemplo, `say_hello()` es un método de instancia que imprime un saludo con el nombre y la edad de la persona.

### Métodos de clase

Los métodos de clase son aquellos que se definen dentro de la clase, pero en lugar de actuar sobre una instancia, actúan sobre la clase en sí misma. Esto significa que no se puede acceder a los atributos de instancia en un método de clase.

Un método de clase se define utilizando la palabra clave `@classmethod` antes de su definición. El primer argumento de un método de clase es la clase misma, que se denota como `cls` por convención.

Aquí hay un ejemplo de cómo definir un método de clase en una clase `Person`:

```python
class Person:
    all_people = []
    
    def __init__(self, name, age):
        self.name = name
        self.age = age
        Person.all_people.append(self)
    
    @classmethod
    def count_people(cls):
        print(f"There are {len(cls.all_people)} people.")
```

En este ejemplo, `count_people()` es un método de clase que imprime el número de instancias de la clase `Person`.

#### Constructor alternativo

Para crear un constructor alternativo usando un `classmethod`, se debe usar el decorador `@classmethod` encima del método que se desea usar como constructor. Luego, se puede llamar al método directamente en la clase para crear una nueva instancia de la clase.

Aquí hay un ejemplo de cómo crear un constructor alternativo usando un `classmethod` en una clase `Person`:

```python
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    @classmethod
    def from_string(cls, person_str):
        name, age = person_str.split('-')
        return cls(name, age)

person1 = Person('John', 35)
person2 = Person.from_birth_year("Mike-35")

print(person1.name, person1.age)  # Output: John 35
print(person2.name, person2.age)  # Output: Mike 37
```

En este ejemplo se ha creado un constructor `from_string` que toma como argumento el un string que contiene el nombre y edad de una persona separado por un guion (`-`). Despues  llama al constructor principal usando la sintaxis `return cls(name, age)` para crear una nueva instancia de la clase `Person`.

Luego, se han creado dos instancias de la clase `Person`, una utilizando el constructor principal y la otra utilizando el constructor alternativo. Al imprimir los valores de `name` y `age` para cada instancia, se puede ver que los valores son correctos y que el constructor alternativo ha funcionado correctamente.

### Métodos estáticos

Los métodos estáticos son aquellos que se definen dentro de la clase, pero no actúan sobre la instancia ni sobre la clase. Esto significa que no se puede acceder a los atributos de instancia ni a los atributos de clase en un método estático.

Un método estático se define utilizando la palabra clave `@staticmethod` antes de su definición. A diferencia de los métodos de instancia y de clase, los métodos estáticos no toman `self` o `cls` como primer argumento.

Aquí hay un ejemplo de cómo definir un método estático en una clase `Math`:

```python
class Math:
    
    @staticmethod
    def add(a, b):
        return a + b
```

En este ejemplo, `add()` es un método estático que suma dos números.

### Métodos mágicos

Los métodos mágicos son aquellos que tienen nombres especiales y se utilizan para sobrecargar operadores o cambiar el comportamiento predeterminado de las operaciones en una clase.

Por ejemplo, el método `__init__()` que hemos visto anteriormente es un método mágico que se llama automáticamente cuando se crea una nueva instancia de la clase.

Para sobrecargar el operador de suma (`+`) en una clase `Point`, podemos definir el método especial `__add__` en la clase. Este método se llama cuando se usa el operador `+` en dos instancias de la clase `Point`.

Aquí está un ejemplo:

```python
class Point:
    def __init__(self, x, y):
        self.x = x
        self.y = y
    
    def __add__(self, other):
        new_x = self.x + other.x
        new_y = self.y + other.y
        return Point(new_x, new_y)

p1 = Point(1, 2)
p2 = Point(3, 4)
p3 = p1 + p2

print(p3.x, p3.y)  # Output: 4 6
```

En este ejemplo, definimos la clase `Point` con un constructor que toma dos argumentos, `x` e `y`, que representan las coordenadas del punto. Luego, definimos el método especial `__add__` que toma otro objeto `Point` como argumento y devuelve un nuevo objeto `Point` que es la suma de los dos puntos.

En la última línea del ejemplo, creamos dos instancias de la clase `Point` (`p1` y `p2`) y luego sumamos estas dos instancias usando el operador `+`. El resultado se almacena en la variable `p3`, que es otra instancia de la clase `Point`.

Finalmente, imprimimos las coordenadas de `p3` usando los atributos `x` e `y`.
