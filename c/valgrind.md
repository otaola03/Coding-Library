---
description: Memory Leaks
---

# Valgrind

### ¿Que es un Memory Leak?

Una fuga de memoria es un error de software que ocurre cuando un bloque de memoria reservada no es liberada en un programa de computación. Comúnmente ocurre porque se pierden todas las referencias a esa área de memoria antes de haberse liberado. Es decir que ocurre cuando se gestiona mal la memoria.

Un caso tipico es la utilizacion de malloc para la reserva de memoria, pero sin la utilizacion de free para posteriormente liberarla. O la mala utilizacion de estos dos.

### ¿Que es valgrind?

Valgrind es un conjunto de herramientas libres que ayuda en la depuración de problemas de memoria y rendimiento de programas. La herramienta más usada es Memcheck.

### Guia basica de Valgrind

Esta guía brinda la información mínima que necesita para comenzar a detectar errores de memoria en su programa con Memcheck.

Para acceder a la La guía oficial de inicio rápido de Valgrind aqui tienes el [enlace](https://valgrind.org/docs/manual/quick-start.html).

#### 1. Preparando tu programa

Compile su programa con -g para incluir información de depuración para que los mensajes de error de Memcheck incluyan números de línea exactos. Usar -O0 también es una buena idea, si puede tolerar la desaceleración. Con -O1, los números de línea en los mensajes de error pueden ser inexactos, aunque, en términos generales, ejecutar Memcheck en código compilado en -O1 funciona bastante bien, y la mejora de la velocidad en comparación con la ejecución de -O0 es bastante significativa. No se recomienda el uso de -O2 y superior, ya que Memcheck ocasionalmente informa errores de valores no inicializados que en realidad no existen.

#### 2. Ejecutando el programa bajo Memcheck

Normalmente ejecutas los programas asi:

```
./a.out arg1 arg2
```

Utiliza esta linea de comando

```
valgrind --leak-check=yes ./a.out arg1 arg2
```

Memcheck es la herramienta predeterminada. La opción --leak-check activa el detector detallado de fugas de memoria.

El programa se ejecutará mucho más lento (por ejemplo, de 20 a 30 veces) de lo normal y usará mucha más memoria. Memcheck emitirá mensajes sobre errores de memoria y leaks que detecte.

#### 3. Interpretar la salida de Memcheck

Aquí hay un programa C de ejemplo, en un archivo llamado a.c, con un error de memoria y una fuga de memoria.

```c
#include <stdlib.h>

  void f(void)
  {
     int* x = malloc(10 * sizeof(int));
     x[10] = 0;        // problem 1: heap block overrun
  }                    // problem 2: memory leak -- x not freed

  int main(void)
  {
     f();
     return 0;
  }
```

La mayoría de los mensajes de error son similares a los siguientes, que describen el problema 1, el desbordamiento del bloque de almacenamiento dinámico:

```
==19182== Invalid write of size 4
==19182==    at 0x804838F: f (example.c:6)
 ==19182==    by 0x80483AB: main (example.c:11)
 ==19182==  Address 0x1BA45050 is 0 bytes after a block of size 40 alloc'd
 ==19182==    at 0x1B8FF5CD: malloc (vg_replace_malloc.c:130)
 ==19182==    by 0x8048385: f (example.c:5)
 ==19182==    by 0x80483AB: main (example.c:11)
```

Cosas a notar:

* Hay mucha información en cada mensaje de error; léelo cuidadosamente.
* El 19182 es el ID del proceso; por lo general no es importante.
* La primera línea ("Escritura no válida...") le dice qué tipo de error es. Aquí, el programa escribió en alguna memoria que no debería haber debido a un desbordamiento del bloque de almacenamiento dinámico.
* Debajo de la primera línea hay un seguimiento de la pila que le indica dónde ocurrió el problema. Los seguimientos de pila pueden ser bastante grandes y confusos, especialmente si está utilizando C++ STL. Leerlos de abajo hacia arriba puede ayudar. Si el seguimiento de la pila no es lo suficientemente grande, use la opción `--num-callers` para hacerlo más grande.
* Las direcciones de código (por ejemplo, 0x804838F) generalmente no son importantes, pero en ocasiones son cruciales para rastrear errores más extraños.
* Algunos mensajes de error tienen un segundo componente que describe la dirección de memoria involucrada. Este muestra que la memoria escrita acaba de pasar el final de un bloque asignado con malloc() en la línea 5 del ejemplo.c.

Vale la pena **corregir los errores en el orden en que se notifican**, ya que los errores posteriores pueden deberse a errores anteriores. No hacer esto es una causa común de dificultad con Memcheck.&#x20;

Los mensajes leak se ven así:

```
  ==19182== 40 bytes in 1 blocks are definitely lost in loss record 1 of 1
  ==19182==    at 0x1B8FF5CD: malloc (vg_replace_malloc.c:130)
  ==19182==    by 0x8048385: f (a.c:5)
  ==19182==    by 0x80483AB: main (a.c:11)
```

El seguimiento de la stack le indica dónde se asignó la memoria perdida. Desafortunadamente, Memcheck no puede decirle por qué se filtró la memoria. (Ignore el "vg\_replace\_malloc.c", que es un detalle de implementación).

Hay varios tipos de fugas; Las dos categorías más importantes son:

* "definitivamente perdido": su programa está perdiendo memoria, ¡arréglelo!
* "probablemente perdido": su programa está perdiendo memoria, a menos que esté haciendo cosas raras con los punteros (como moverlos para que apunten al centro de un bloque de montón).

Memcheck también informa sobre los usos de valores no inicializados, más comúnmente con el mensaje "Conditional jump or move depends on uninitialised value(s)". Puede ser difícil determinar la causa raíz de estos errores. Intente usar `--track-origins=yes` para obtener información adicional. Esto hace que Memcheck funcione más lento, pero la información adicional que obtiene a menudo ahorra mucho tiempo para averiguar de dónde provienen los valores no inicializados.

#### Video orientativo

{% embed url="https://www.youtube.com/watch?v=NMmK8o_BZ7M" %}

### Flags

Para poder tener un mejor informe de los problemas, se pueden agregar flags a la ejecución de la herramienta en el programa. Por ejemplo:

```
valgrind --leak-check=full --track-origins=yes --show-reachable=yes ./ejectuableErrores tipicos de Valgrind
```

A continuación describimos los flags utilizados:

|                        |                                                                                                                                                                      |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| --leak check = full    | Mostrar en detalle cada perdida, en lugar de un resumen.                                                                                                             |
| --track origins = yes  | Mostrar donde se originaron los valores no inicializados.                                                                                                            |
| --show reachable = yes | Para mostrar todo tipo de “memory leaks”, incluso los que al terminar la ejecución, el sistema operativo se encarga de arreglar (estos también hay que corregirlos). |

### Errores tipicos de Valgrind

* **Memory leak:** Ocurre cuando no liberamos la memoria que reservamos (con malloc), de forma tal que se pierde la referencia a la misma. Esto provoca que partes de la memoria en desuso no puedan ser utilizados por otros programas y/o procesos.
* **Invalid Free:** Ocurre cuando se vuelve a liberar un bloque de memoria ya liberado, o cuando el mismo no fue reservado previamente.
* **Invalid read of size \<A>:** Ocurre cuando se intenta leer un bloque de memoria de \<A> bytes, que no esta reservado previamente (ya sea no declarando la variable, o no usando malloc).
* **Invalid write of size \<A>:** Ocurre cuando se intenta escribir un bloque de memoria de \<A> bytes, que no esta reservado previamente (ya sea no declarando la variable, o no usando malloc). Por ejemplo si un array creado con malloc tiene n espacios,  dara error al intentar escribir en la posicion n + 1
* **Conditional jump or move depends on uninitialized value(s):** Ocurre cuando se evaluá la condición de un salto (por ejemplo, “if (\<condicion>) {...}” ), en la cual esta depende de una o mas variables no inicializadas. Esto quiere decir, que el valor que se evalua, es un valor que depende del asignado por otros programas y/o procesos que fueron ejecutados previamente, a la dirección de memoria en cuestión. Por ejemplo cuando utilizas una variable sin inicializar.

### Bibliografia

* [Debugging con Valgrind (Parte 1)](https://youtu.be/pfjjSL9sp3w)
* [Debugging con Valgrind (Parte 2)](https://youtu.be/Vqr75HSe3kk)
* [Cómo utilizar Valgrind para perfilar el uso de memoria](https://access.redhat.com/documentation/es-es/red\_hat\_enterprise\_linux/6/html/performance\_tuning\_guide/s-memory-valgrind)
