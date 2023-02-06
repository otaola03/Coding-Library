# Scripts

Un script de Python es un archivo de texto plano que contiene código escrito en el lenguaje de programación Python. Se puede ejecutar en un intérprete de Python o en un entorno de desarrollo integrado (IDE) y su propósito principal es automatizar tareas o resolver problemas específicos.

Los scripts de Python pueden contener una combinación de sentencias, funciones, clases y otros elementos de programación, y pueden acceder a bibliotecas externas de Python o a otras aplicaciones.

Para ejecutar un script de Python, se puede abrir una terminal o una línea de comandos y escribir `python nombre_del_script.py`. También se puede hacer clic en el archivo desde el sistema de archivos o abrirlo desde un IDE y presionar una tecla de atajo para ejecutarlo.

Los scripts de Python son muy útiles para automatizar tareas repetitivas, procesar archivos de texto, realizar cálculos y visualizaciones de datos, entre muchas otras aplicaciones.



### **\_\_main\_\_**

`__name__==__main__` es una verificación utilizada en Python para determinar si un módulo o script se está ejecutando como programa principal o se está importando como módulo en otro programa.

En Python, `__name__` es una variable predefinida que contiene el nombre del módulo o script actual. Cuando se ejecuta un programa principal, `__name__` se establece en `"__main__"`. Por lo tanto, la verificación `__name__==__main__` se usa para verificar si el módulo o script se está ejecutando como programa principal.

Aquí hay un ejemplo de código que utiliza `__name__==__main__`:

```python
def suma(a, b):
    return a + b

if __name__ == '__main__':
    x = 3
    y = 4
    resultado = suma(x, y)
    print("La suma de", x, "y", y, "es", resultado)
```

En este ejemplo, la función `suma` se puede usar tanto como un módulo importado en otro programa como como programa principal. Si el módulo se importa en otro programa, no se ejecutará el código dentro de `if __name__ == '__main__':`. Sin embargo, si se ejecuta como programa principal, se ejecutará el código dentro de la estructura&#x20;

Es recomendable incluir la verificación `if __name__ == '__main__'` en tus scripts o módulos en Python cuando deseas tener control sobre código que solo se ejecuta cuando el archivo se está ejecutando como programa principal y no cuando se importa como módulo en otro programa. De esta manera, puedes evitar ejecutar código que no es relevante o que puede causar problemas al importar el módulo en otro programa.

Sin embargo, si tienes un archivo que es solo un script y no se va a importar como módulo en otro programa, no es necesario incluir la verificación `if __name__ == '__main__'`. En este caso, puedes ejecutar todo el código en el archivo sin ningún problema.

En resumen, la verificación `if __name__ == '__main__'` es una buena práctica y se recomienda su uso en la mayoría de los casos para mejorar la portabilidad y mantenibilidad de tus scripts y módulos de Python.

### \_\_doc\_\_

`.__doc__` es un atributo especial en Python que se puede utilizar para acceder a la documentación de un objeto. La documentación se puede escribir en el cuerpo de una función, clase, módulo, etc. utilizando una cadena de documentación o un comentario multilínea. La cadena de documentación se almacena en el atributo `.__doc__` del objeto y se puede acceder desde el código.

Por ejemplo, si tienes una función llamada `mi_funcion` con una cadena de documentación, puedes acceder a la documentación de la siguiente manera:

```python
pythonCopy codedef mi_funcion():
    """Esta es la documentación de mi función."""
    # Código de la función

print(mi_funcion.__doc__)
# Salida: 'Esta es la documentación de mi función.'
```

Es importante tener en cuenta que las cadenas de documentación son opcionales y no son necesarias para el funcionamiento del código. Sin embargo, son muy útiles para proporcionar información sobre el propósito, los argumentos, los valores de retorno, etc. de un objeto y para hacer más legible y comprensible el código.

También es posible acceder a la documentación de módulos, clases, atributos, etc. de la misma manera, utilizando el atributo `.__doc__` del objeto correspondiente.
