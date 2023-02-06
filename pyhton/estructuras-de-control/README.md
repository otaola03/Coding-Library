# Estructuras de control

En Python, hay varias estructuras de control que se utilizan para controlar el flujo de ejecución de un programa. Aquí hay una descripción detallada de las estructuras de control en Python con ejemplos.

### if, elif, else

Gracias a esta estructuras de control, podemos **cambiar el flujo de ejecución de un programa**, haciendo que ciertos bloques de código se ejecuten si y solo si se dan unas condiciones particulares. Para eso se utilizan las estructuras `if`, `elif y else`.

```python
x = 3
if x > 5:
    print("x es mayor que 5")
elif x == 3:
    print("x es igual a 3")
else:
    print("x es menor que 3")
```

### while

El bucle while es un tipo de estructura de control en Python que permite repetir un bloque de código mientras se cumpla una condición determinada.

El formato básico de un bucle while es el siguiente:

```python
while condición:
    # bloque de código que se repetirá
    # mientras se cumpla la condición
```

Ejemplo:

```python
# Ejemplo de uso del bucle while

contador = 0

# La condición es que el contador sea menor a 5
while contador < 5:
    print(contador)
    contador += 1
```

En este ejemplo, el bucle while se ejecuta mientras `contador` sea menor a 5. Cada vez que se ejecuta el bucle, se imprime el valor de `contador` y se aumenta en 1. Una vez que `contador` sea igual a 5, la condición ya no se cumplirá y el bucle se detendrá.

#### Else y while <a href="#else-y-while" id="else-y-while"></a>

Algo no muy corriente en otros lenguajes de programación pero si en Python, es el uso de la cláusula `else` al final del `while`. Podemos ver el ejemplo anterior mezclado con el `else`. La sección de código que se encuentra dentro del `else`, se ejecutará cuando el bucle termine, pero solo si lo hace “por razones naturales”. Es decir, si el bucle termina porque la condición se deja de cumplir, y no porque se ha hecho uso del `break`.

```python
x = 5
while x > 0:
    x -=1
    print(x) #4,3,2,1,0
else:
    print("El bucle ha finalizado")
```

Podemos ver como **si el bucle termina por el `break`, el `print()` no se ejecutará**. Por lo tanto, se podría decir que si no hay realmente ninguna sentencia `break` dentro del bucle, tal vez no tenga mucho sentido el uso del `else`, ya que un bloque de código fuera del bucle cumplirá con la misma funcionalidad.

```python
x = 5
while True:
    x -= 1
    print(x) #4, 3, 2, 1, 0
    if x == 0:
        break
else:
    # El print no se ejecuta
    print("Fin del bucle")
```
