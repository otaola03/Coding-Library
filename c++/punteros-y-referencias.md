# Punteros y referencias

Los punteros y referencias son conceptos fundamentales en C++ que permiten manipular y acceder a datos de manera indirecta. En este post, exploraremos qué son los punteros y las referencias, cómo se utilizan y cuál es la diferencia entre ellos.

{% embed url="https://www.youtube.com/watch?v=sxHng1iufQE&ab_channel=PaulProgramming" %}

### Punteros

Un puntero en C++ es una variable especial que almacena la dirección de memoria de otro objeto. En otras palabras, un puntero "apunta" a la ubicación de memoria donde se encuentra almacenado otro objeto.

La sintaxis básica para declarar y utilizar un puntero en C++ es la siguiente:

```cpp
tipo_dato* nombre_puntero;
```

Donde `tipo_dato` es el tipo de dato al que apunta el puntero, y `nombre_puntero` es el nombre que se le da al puntero.

Para poder asignar la direccion de una variable a un puntero hay que utilizar el simboo &`:`

```cpp
int     num;
int*    ptr;

ptr = &num;
```

**Utilidad de los punteros**

Los punteros se utilizan para una variedad de tareas en C++, como:

* **Dinamicidad:** Permiten asignar y liberar memoria dinámicamente en tiempo de ejecución.
* **Manipulación de estructuras de datos complejas:** Los punteros permiten acceder y manipular estructuras de datos complejas, como arreglos y estructuras, de forma eficiente.
* **Paso de parámetros:** Los punteros se utilizan para pasar argumentos a funciones por referencia, lo que evita la copia de datos y permite modificar el valor del argumento original.

#### Referencias

Una referencia en C++ es otra forma de acceder a un objeto existente utilizando un alias o nombre alternativo. Una referencia se vincula a un objeto en el momento de la declaración y debe inicializarse con un objeto válido.

La sintaxis básica para declarar y utilizar una referencia en C++ es la siguiente:

```cpp
tipo_dato& nombre_referencia = objeto;
```

Donde `tipo_dato` es el tipo de dato del objeto y `nombre_referencia` es el nombre que se le da a la referencia. Con esto lee estamos asignando a la variable  `objeto` un nuevo nombre `nombre_referencia`.

{% hint style="info" %}
Una referencia es un nombre nuevo a una variable existente, por lo que a la hora de declararla es necesario asignarle una variable.
{% endhint %}

**Utilidad de las referencias**

Las referencias se utilizan principalmente para:

* **Aliasing:** Proporcionan un nombre alternativo para un objeto existente, lo que permite acceder y manipular ese objeto de manera más cómoda.
* **Paso de parámetros:** Las referencias se utilizan para pasar argumentos a funciones por referencia, lo que permite **modificar el valor del argumento** original **sin** necesidad de **utilizar punteros.**

### Diferencias entre punteros y referencias (continuación)

* **Operaciones aritméticas:** Los punteros admiten operaciones aritméticas, como incremento y decremento, para desplazarse en la memoria, mientras que las referencias no tienen esta capacidad.
* **Comprobación de nulidad:** Los punteros pueden ser verificados si son nulos antes de ser utilizados, lo que evita acceder a una dirección inválida de memoria. Las referencias, por otro lado, no requieren verificación de nulidad, ya que siempre se espera que estén vinculadas a un objeto válido.
* **Requerimientos de inicialización:** Las referencias deben ser inicializadas en el momento de la declaración y siempre deben referirse a un objeto válido. En cambio, los punteros pueden no ser inicializados en el momento de la declaración y pueden apuntar a objetos válidos o nulos.

### Elección entre punteros y referencias

La elección entre punteros y referencias depende del escenario y los requisitos específicos del programa. Algunos factores a considerar son:

* **Nulidad:** Si se necesita representar la ausencia de un objeto, se deben usar punteros.
* **Posibilidad de reasignación:** Si se requiere cambiar el objeto apuntado o referenciado, se deben usar punteros.
* **Sintaxis y legibilidad:** Las referencias pueden ofrecer una sintaxis más simple y legible, lo que las hace adecuadas en casos donde se busca un código más limpio y comprensible.

En general, se recomienda utilizar referencias cuando sea posible, ya que ofrecen mayor seguridad y facilidad de uso al garantizar la existencia de un objeto válido y evitar la necesidad de manejar nulidad.\
