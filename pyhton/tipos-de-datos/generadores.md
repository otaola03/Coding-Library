# Generadores

En Python, un generador es una función que utiliza la sentencia `yield` en lugar de `return` para devolver valores. A diferencia de las funciones normales, que devuelven un valor y terminan, los generadores mantienen su estado y pueden generar múltiples valores a lo largo del tiempo, según sea necesario.

> Un generador es como una lista, pero que va creando los elementos de dicha lista a medida que se van solicitando

La principal ventaja de los generadores es que pueden ser mucho más eficientes en términos de memoria que las funciones normales, ya que solo generan valores a medida que se solicitan, en lugar de almacenar todos los valores en una lista o una matriz. Además, los generadores permiten procesar grandes cantidades de datos de manera eficiente, ya que pueden generar valores de manera continua sin necesidad de cargar todo el conjunto de datos en la memoria.

Veamos algun ejemplos para entender mejor cómo funcionan los generadores en Python:

```python
def letras_palabra(palabra):
    for letra in palabra:
        yield letra
```

Este generador devuelve una secuencia de letras a partir de una cadena dada. Cada vez que se llama a la función `next()` en el generador, se genera la siguiente letra en la secuencia. Por ejemplo:

```python
>>> letras = letras_palabra('hola')
>>> next(letras)
'h'
>>> next(letras)
'o'
>>> next(letras)
'l'
```

En el caso de no se queira utilizar next, tamben se podria utilizar de la siguiente manera:

```python
for palabra in generador_palabras_ordenadas(frase):
    print(palabra)
```

{% embed url="https://www.youtube.com/watch?v=bD05uGo_sVI" %}

### Ventajas

Los generadores tienen varias ventajas en Python:

1. Eficiencia en el uso de memoria: Los generadores son más eficientes en términos de memoria que las listas o las matrices, ya que solo generan valores a medida que se solicitan, en lugar de almacenar todos los valores en la memoria. Esto es especialmente importante cuando se trata de grandes conjuntos de datos.
2. Iteración personalizada: Los generadores permiten realizar iteraciones personalizadas, lo que significa que se pueden generar valores en función de una serie de condiciones o reglas, en lugar de simplemente iterar sobre una lista predefinida.
3. Velocidad de procesamiento: Los generadores pueden procesar grandes conjuntos de datos de manera eficiente, ya que pueden generar valores de manera continua sin necesidad de cargar todo el conjunto de datos en la memoria. Esto puede ser especialmente útil para aplicaciones que requieren procesamiento en tiempo real o en tiempo casi real.
4. Facilidad de uso: Los generadores son fáciles de implementar y utilizar en Python. Se definen utilizando la sentencia `yield` en lugar de `return`, lo que hace que su uso sea muy similar al de una función normal.
5. Compatibilidad con otras funciones: Los generadores son compatibles con muchas otras funciones de Python, como las funciones de la biblioteca `itertools`, lo que permite realizar operaciones avanzadas de iteración y filtrado de datos.

En resumen, los generadores son una herramienta muy útil en Python para procesar grandes cantidades de datos de manera eficiente y realizar iteraciones personalizadas. Su eficiencia en el uso de memoria, velocidad de procesamiento y facilidad de uso los convierten en una opción ideal para muchas aplicaciones de Python.

### Utilidad

Los generadores se utilizan comúnmente en las siguientes situaciones:

1. **Procesamiento de grandes conjuntos de datos:** cuando se trata de procesar grandes conjuntos de datos, los generadores pueden ser muy útiles, ya que evitan la necesidad de crear una lista completa en memoria. En lugar de eso, se pueden procesar los elementos de la secuencia uno por uno a medida que se necesitan.
2. **Generación de secuencias infinitas:** los generadores son ideales para la generación de secuencias infinitas, ya que no es necesario crear una lista completa de valores. En cambio, los valores se generan uno por uno según se solicitan.
3. **Procesamiento de archivos grandes:** cuando se trabaja con archivos grandes, los generadores pueden ser útiles para leer el archivo y procesar su contenido de manera eficiente, sin necesidad de cargar todo el archivo en memoria de una sola vez.
4. **Iteración sobre estructuras de datos complejas:** en algunos casos, como en el procesamiento de árboles o grafos, puede ser difícil o incluso imposible crear una lista completa de todos los nodos o elementos en memoria. En estos casos, los generadores pueden ser útiles para iterar sobre la estructura de datos de manera eficiente, generando los elementos uno por uno según sea necesario.

### Resumen

Un generador es una función especial que produce una serie de valores uno a la vez utilizando la palabra clave "yield". Cuando un generador se llama, no devuelve un valor inmediatamente como lo hace una función normal, en su lugar, devuelve un objeto generador que se puede utilizar para obtener los valores generados. Cada vez que se llama al objeto generador, el generador retoma donde se quedó la última vez y continúa generando valores hasta que se agoten todos los elementos o se detenga el proceso.

En resumen, un generador es una forma de generar una secuencia de valores bajo demanda y de manera eficiente sin tener que almacenar todos los valores en memoria al mismo tiempo.
