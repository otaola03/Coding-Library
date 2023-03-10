# Herencia

La herencia de clases es un concepto fundamental en la programación orientada a objetos. En Python, una clase puede heredar atributos y métodos de otra clase existente, y luego agregar o modificar sus propios atributos y métodos. La clase base se llama clase padre o superclase, y la clase que hereda de ella se llama clase hija o subclase.

La sintaxis para definir una clase hija es la siguiente:

```python
class Hija(Padre):
    pass
```

Aquí, `Hija` es la subclase que hereda de `Padre` la cual es la superclase. Todos los atributos y métodos definidos en la clase padre se heredan automáticamente en la clase hija. La clase hija puede entonces agregar nuevos atributos y métodos, o modificar los existentes.

### Sintaxis

La sintaxis para la herencia en Python es bastante sencilla. Para declarar una clase hija que herede de una clase padre, simplemente se indica el nombre de la clase padre entre paréntesis después del nombre de la clase hija. Por ejemplo:

```python
class Animal:
    def __init__(self, name):
        self.name = name

    def talk(self):
        pass

class Dog(Animal):
    def talk(self):
        return "Woof!"
```

En este ejemplo, se define una clase `Animal` que tiene un método constructor que toma un argumento `name` y un método `talk` que no hace nada. Luego se define una clase `Dog` que hereda de `Animal`. `Dog` redefine el método `talk` para devolver "Woof!".

En la declaración de la clase `Dog`, la clase padre `Animal` se indica entre paréntesis. Esto indica que `Dog` hereda de `Animal`. Cuando se invoca al constructor de la clase `Dog`, también se invoca al constructor de la clase `Animal` automáticamente. Es decir, se puede llamar al constructor de la clase padre usando `super()`, que es una referencia a la clase padre. Por ejemplo:

<pre class="language-python"><code class="lang-python">class Animal:
    def __init__(self, name):
        self.name = name

<strong>class Dog(Animal):
</strong>    def __init__(self, name, breed):
        super().__init__(name)
        self.breed = breed
</code></pre>

En este ejemplo, se define una clase `Dog` que también hereda de `Animal`. `Dog` redefine el constructor `__init__` para tomar dos argumentos: `name` y `breed`. La primera línea del constructor de la clase `Dog` llama al constructor de la clase `Animal` utilizando `super()`, pasándole el argumento `name`. Luego, se define un nuevo atributo `breed` en la clase `Dog`.

Esto puede ser util cuando estamos heredando de tan solo una clase. En cambio si nuestra nueva calse hereda de mas de una clase tnedremos que hacer referencia a esa clase para inicializarla. Esto se hace de la sigueinte manera:

```python
class Dog(Animal, Canine):
    def __init__(self, name, breed, breed):
        Animal.__init__(name)
        Canine.__init__(breed)
        self.breed = breed
```
