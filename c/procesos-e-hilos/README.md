# Procesos e Hilos

### **Procesos y Threads (hilos de ejecución)**

Si queremos que nuestro programa empiece a ejecutar varias cosas "a la vez", tenemos dos opciones. Por una parte podemos crear un nuevo proceso y por otra, podemos crear un nuevo hilo de ejecución (un thread). En realidad nuestro ordenador, salvo que tenga varias cpu, no ejecutará varias cosas a la vez. Cuando digo "a la vez", me refiero a que el sistema operativo irá ejecutando cachos de programa por turnos (por rodajas de tiempo) de forma muy rápida, dando la sensación de simultaneidad

### **Procesos**

Un **proceso** de unix es cualquier programa en ejecución y **es totalmente independiente de otros procesos**. El comando de unix `ps` nos lista los procesos en ejecución en nuestra máquina. Un proceso **tiene su propia zona de memoria y se ejecuta "simultáneamente" a otros procesos**. Es totalemente imposible en unix que un proceso se meta, a posta o por equivocación, en la zona de memoria de otro proceso. Esta es una de las caracteristicas que hace de unix un sistema fiable. Un programa chapucero o malintencionado no puede fastidiar otros programas en ejecución ni mucho menos a los del sistema operativo. Si el programa chapucero se cae, se cae sólo él.

La única forma que tiene el sistema para identificar un proceso es mediante un **identificador de proceso (PID)**, que es único en el sistema.

### Hilos

**Dentro de un proceso puede haber varios hilos** de ejecución (varios threads). Eso quiere decir que un proceso podría estar haciendo varias cosas "a la vez". **Los hilos** dentro de un proceso **comparten todos la misma memoria**. Eso quiere decir que si un hilo toca una variable, todos los demás hilos del mismo proceso verán el nuevo valor de la variable.&#x20;

Esto hace imprescindible el uso de [semáforos](https://www.chuidiang.org/clinux/ipcs/semaforo.php) o mutex (EXclusión MUTua, que en inglés es al revés, funciones **pthread\_mutex...**) para evitar que dos threads accedan a la vez a la misma estructura de datos. También hace que si un hilo "se equivoca" y corrompe una zona de memoria, todos los demás hilos del mismo proceso vean la memoria corrompida. Un fallo en un hilo puede hacer fallar a todos los demás hilos del mismo proceso.

### ¿Proceso o hilo?

&#x20;¿Qué elegimos? ¿Un proceso o un hilo?. Depende de muchos factores, pero yo (y es cosa mia, que tengo un PC obsoleto con linux), suelo elegir procesos cuando una vez lanzado el hijo no requiero demasiada comunicación con él. Elijo hilos cuando tienen que compartir y actualizarse datos.

Un proceso es más costoso de lanzar, ya que se necesita crear una copia de toda la memoria de nuestro programa. Los hilos son más ligeros.

En cuanto a complejidad, en los hilos, al compartir la memoria y los recursos, es casi obligado el uso de mutex o [semáforos](https://www.chuidiang.org/clinux/ipcs/semaforo.php), así que su programación suele ser más complicada y se necesita ser más cuidadoso. Un proceso, en el momento de lanzarlo, se hace independiente del nuestro, así que no deberíamos tener ningún problema, salvo que necesitemos comunicación entre ellos, que nos liaríamos a programar [memorias compartidas](https://www.chuidiang.org/clinux/ipcs/mem\_comp.php) (con sus correspondientes [semáforos](https://www.chuidiang.org/clinux/ipcs/semaforo.php)), [colas de mensajes](https://www.chuidiang.org/clinux/ipcs/colas.php), [sockets](https://www.chuidiang.org/clinux/sockets/sockets\_simp.php) o cualquier otro mecanismo de comunicación entre procesos unix.

Por ahí he leido que para gestionar entradas/salidas es mejor procesos (atender simultaneamente a varias entradas de sockets, por ejemplo) y que para hacer programas con muchos cálculos en paralelo con varias cpu es mejor hilos, siempre y cuando el sistema operativo sea capaz de repartir automáticamente los hilos en las distintas cpu en función de su carga de trabajo.
