# Formateo con {} y format()

El formateo de cadenas en Python es una técnica que permite insertar valores dinámicos en una cadena de texto. Esto es útil cuando queremos crear mensajes personalizados, informes, etc.

Hay varias formas de formatear cadenas en Python, pero la más común es utilizar la función `format()` y la notación de llaves `{}` como marcadores de posición. La notación de llaves permite especificar qué valor debe insertarse en esa posición en la cadena de texto.

La sintaxis básica para el formateo de strings con {} y format() es la siguiente:

```python
code"{} es un número".format(5)
```

Este código devolverá la cadena "5 es un número".

Se pueden especificar varios valores a formatear en una sola cadena, separados por comas dentro de los paréntesis de format(). Los valores se reemplazarán en el orden en que aparecen en la cadena:

```python
code"{} y {} son números".format(3, 5)
```

Este código devolverá la cadena "3 y 5 son números".

También es posible especificar una posición para cada valor a formatear dentro de la cadena utilizando los números 0, 1, 2, etc. para hacer referencia a su posición dentro de los paréntesis de format():

```python
code"{0} y {1} son números".format(3, 5)
```

Este código devolverá la misma cadena que el ejemplo anterior: "3 y 5 son números".

#### Caracter \`:\`

El carácter `:` en el formateo de cadenas en Python se utiliza para especificar opciones adicionales para el formato de los valores

### Insertar valores en una cadena

Se pueden insertar valores dinámicos en una cadena de texto utilizando la función format() y la notación de llaves {}.

```python
name = "John"
print("Hello, {}!".format(name))
# Output: Hello, John!
```

### Especificar el orden de los valores

Se puede especificar el orden de los valores insertados en la cadena utilizando números dentro de las llaves, como {0}, {1}, etc.

```python
name = "John"
age = 30
print("My name is {0} and I am {1} years old.".format(name, age))
# Output: My name is John and I am 30 years old.
```

### Insertar valores usando nombres de argumentos

En lugar de especificar el orden de los valores con números, se pueden especificar los valores utilizando nombres de argumentos, como {nombre}, {edad}, etc.

```python
name = "John"
age = 30
print("My name is {name} and I am {age} years old.".format(name=name, age=age))
# Output: My name is John and I am 30 years old.
```



### Alineación

Se pueden alinear los valores a la izquierda, derecha o al centro dentro de la cadena de texto.

```python
name = "John"
print("{:>10}".format(name)) # Alineado a la derecha
# Output:      John

print("{:<10}".format(name)) # Alineado a la izquierda
# Output: John     

print("{:^10}".format(name)) # Alineado al centro
# Output:    John   
```

El signo `<` alinea la salida a la izquierda, el signo `>` alinea la salida a la derecha, y el signo `^` centra la salida.

### Longitud total

Se puede especificar la longitud total de la cadena de texto y cómo deben rellenarse los valores que faltan para cumplir esa longitud.

```python
name = "John"
print("{:*^20}".format(name)) # Rellenado con asteriscos
# Output: *****John*****
```

### Formato de fechas

Se pueden formatear fechas y horas para mostrarlas en la forma deseada.

```python
from datetime import datetime
now = datetime.now()
print("The date is {:%Y-%m-%d %H:%M:%S}".format(now))
# Output: The date is 2022-12-30 10:30
```

### Formato para Números de Punto Flotante

```lua
luaCopy codeimport math
print("El valor de pi es {:.2f}".format(math.pi))
```

Este formato se utiliza para dar formato a números de punto flotante, donde `X` es el número de dígitos decimales que se deben mostrar después del punto decimal.

Salida: `El valor de pi es 3.14`

### Completar con ceros o espacios

```python
pythonCopy codeprint("{:04d}".format(42))
print("{:4d}".format(42))
print("{:04.2f}".format(3.14159265))
print("{:7.2f}".format(3.14159265))
```

El número dentro de las llaves especifica el número total de caracteres que se deben usar para mostrar el valor, incluyendo los ceros o espacios necesarios para completar la cantidad especificada.

Salida:

```bash
0042
  42
3.14
  3.14
```

### Especificación de tipo de conversión

```python
pythonCopy codeprint("{:b}".format(42))
print("{:c}".format(42))
print("{:d}".format(42))
print("{:x}".format(42))
print("{:X}".format(42))
print("{:.2e}".format(1234.56))
```

Las letras dentro de las llaves especifican el tipo de conversión que se debe usar:

* `b` convierte el número en su representación binaria.
* `c` convierte el número en el carácter correspondiente en la tabla Unicode.
* `d` convierte el número en un número decimal.
* `x` convierte el número en un número hexadecimal en minúsculas.
* `X` convierte el número en un número hexade
* `e` convierte el numero en exponencial

### Format con iteraciones

La función `format()` en Python también se puede utilizar con iteraciones dentro de su interior. Aquí hay un ejemplo para ilustrar esto:

```python
numbers = [1, 2, 3, 4, 5]

# Usando una iteración for dentro de la función format
formatted_numbers = ", ".join("The number is: {}".format(number) for number in numbers)
print(formatted_numbers)
```

El resultado será:

```python
The number is: 1, The number is: 2, The number is: 3, The number is: 4, The number is: 5
```

En este ejemplo, la función `format()` se utiliza dentro de una iteración `for`. Se recorre la lista `numbers` y se formatea cada número individualmente usando `format()`. Luego, se utiliza la función `join()` para unir todos los valores formateados en una sola cadena, separada por comas.

Esto es útil cuando se desea aplicar un formato similar a una serie de valores y mostrarlos en una sola cadena.
