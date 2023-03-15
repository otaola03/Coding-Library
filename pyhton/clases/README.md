# Clases

La Programación Orientada a Objetos (POO, por sus siglas en inglés) es un paradigma de programación que se basa en el uso de objetos y clases para representar conceptos y elementos del mundo real en el código. En la POO, se crean clases que actúan como plantillas para crear objetos que tienen atributos (datos) y métodos (funciones) que manipulan esos datos. Los objetos pueden interactuar entre sí y se pueden reutilizar en distintas partes del código.

El objetivo de la POO es hacer que el código sea más legible, mantenible y organizado. La abstracción y encapsulación son dos de las características más importantes de la POO, ya que permiten esconder la complejidad de los objetos y aislar las partes del código que cambian con frecuencia de las que no cambian.

En resumen, la POO es una manera de programar que hace que sea más fácil diseñar y mantener programas complejos, y que ayuda a los programadores a pensar en términos de objetos y conceptos reales en lugar de procedimientos y lógica.

{% embed url="https://www.youtube.com/playlist?list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc" %}

### Clases y instancias

La Programación Orientada a Objetos (POO) es un enfoque de programación que se basa en la idea de "objetos" como entidades independientes que contienen datos y funciones. En Python, estos objetos son definidos mediante clases.

La diferencia entre una clase y una instancia es que una clase es un modelo o plantilla para crear objetos con características similares. Por otro lado, una instancia es un objeto concreto creado a partir de una clase. En el ejemplo, la clase `Perro` es un modelo para crear objetos de tipo `Perro`, mientras que `perro_1` es una instancia de la clase `Perro`.

Aquí hay un ejemplo de cómo declarar una clase en Python 3.x:

```python
class Perro:
    pass:
```

En cambio en Python 2.x al crear una clase esta tiene que heredar de la clase `object`, que es la clase base de todas la clases.

En este ejemplo, hemos creado una clase llamada "Empleado" que define un objeto "Empleado". Esto se llama "herencia nueva", ya que permite a la clase heredar todas las características y métodos de la clase `object`. La notacion es la siguiente:

```python
class Perro(object):
    pass
```

{% hint style="info" %}
La sentencia `pass` sirve para poder declarar una clase, funcion... vacia
{% endhint %}

Una vez creada la clase, para crear una instancia de la clase "Perro", simplemente llamamos a la clase como si fuera una función:

```python
perro_1 = Perro()
```

#### Constructor

El método `__init__` es un método especial en Python que se llama automáticamente al crear una nueva instancia de una clase. Se conoce como constructor, y es una buena práctica inicializar los atributos de una clase en este método. Aquí hay un ejemplo para demostrar su uso:

```python
class Perro:
    def __init__(self, nombre, raza, edad):
        self.nombre = nombre
        self.raza = raza
        self.edad = edad

fido = Perro("Fido", "Labrador", 3)
```

En este ejemplo, creamos una clase `Perro` y definimos un método `__init__` que toma tres argumentos: `nombre`, `raza` y `edad`. Dentro de este método, inicializamos los atributos de la clase con los valores proporcionados en los argumentos. Luego, creamos una nueva instancia de la clase `Perro` y le asignamos valores a los atributos. Finalmente, imprimimos los valores de los atributos.

#### `__str__`

El método `__str__` es un método especial en Python que se utiliza para definir cómo se debe representar un objeto de una clase como una cadena de texto. Este método es llamado automáticamente por la función `str()` o por el operador `print` para mostrar una representación en forma de texto de un objeto de una clase.

El método `__str__` es opcional, pero es una buena práctica definirlo si se desea tener una representación legible y significativa de los objetos de una clase. Aquí hay un ejemplo de cómo se puede usar `__str__` en una clase:

```python
pythonCopy codeclass Persona:
    def __init__(self, nombre, edad):
        self.nombre = nombre
        self.edad = edad
        
    def __str__(self):
        return f"Persona({self.nombre}, {self.edad})"

p = Persona("Juan", 30)
print(p)  # Imprimirá: Persona(Juan, 30)
```

En este ejemplo, se ha definido una clase `Persona` con dos atributos `nombre` y `edad`. El método `__str__` se ha definido para devolver una representación en forma de texto de los objetos de la clase, en este caso en el formato `"Persona(nombre, edad)"`. Al llamar a `print(p)` o a `str(p)`, se llama automáticamente a `p.__str__()` y se muestra la representación en forma de texto correspondiente.

### Variables de clase y variables de instancia

Las variables de clase son aquellas que se declaran dentro de la clase y son compartidas por todas las instancias de la clase. Es decir, si una clase tiene una variable de clase, todas las instancias de la clase tendrán acceso a esa variable y su valor será compartido entre ellas.

Por otro lado, las variables de instancia son aquellas que se declaran dentro de los métodos de una clase y son únicas para cada instancia de la clase. Es decir, cada instancia de una clase tendrá su propia copia de las variables de instancia, y los cambios realizados a ellas sólo afectarán a esa instancia en particular.

Por ejemplo, considere la siguiente clase:

```python
class Perro:
    especie = "Canina"

    def __init__(self, nombre, raza):
        self.nombre = nombre
        self.raza = raza
```

Aquí, la variable de clase `especie` se define fuera de los métodos y es compartida por todas las instancias de la clase `Perro`. Por otro lado, las variables de instancia `nombre` y `raza` se definen dentro del método `__init__` y son únicas para cada objeto instanciado.

Podemos usar el método `__dict__` para ver la diferencia entre variables de clase y variables de instancia. Por ejemplo:

```python
perro_1 = Perro("Fido", "Labrador")
perro_2 = Perro("Max", "Bulldog")

print(perro_1.__dict__)
print(perro_2.__dict__)
```

El resultado sería:

```bash
{'nombre': 'Fido', 'raza': 'Labrador'}
{'nombre': 'Max', 'raza': 'Bulldog'}
```

Como puedes ver, las variables de instancia `nombre` y `raza` son diferentes para cada objeto, mientras que la variable de clase `especie` es la misma para ambos objetos. Es decir si ahora imprimimos la variable especia de cada perro y de la clase en si nos mostrara en todos lo mismo:

```python
print(Perro.especie)
print(perro_1.especie)
print(perro_1.especie)
```

El resultado seria:

```
Canina
Canina
Canina
```

Es decir si cambio la variable `especie` a la clase el cambio se aplicaria a todas las instancias al igual que a la clase. Sin embargo si el cambio lo aplico a una instancia el cambio tan solo se aplicara a esa instancia. Para poder aplicar este cambio a una uncia instancia python crea la variable `specie` en la instancia, como si se hubiera creado con el constructor.

```python
perro_1.especie = "felina"
```

Si ahora utilizamos el metodo `__dict__` observaremos que e a creado una nuva variable en `perro_1`:

```bash
{'especie': 'felina', 'nombre': 'Fido', 'raza': 'Labrador'}
```
