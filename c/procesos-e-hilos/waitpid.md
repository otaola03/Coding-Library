---
description: Monitorear estados de proceso
---

# Waitpid

La llamada del sistema `wait` tiene múltiples limitaciones y, para cubrir funciones más avanzadas, es necesario utilizar la función `waitpid`. Es decir, si un proceso crea varios hijos y el padre necesita supervisar a un hijo específico, solo `waitpid` puede hacer esto.

### Syntaxis

```c
pid_t waitpid(pid_t pid, int *status, int options);
```

El `waitpid` toma tres argumentos, el primero de los cuales es el número de identificación del proceso (pid). PID puede tener múltiples valores prediseñados con diferentes efectos:

* **< -1** --> Espere cualquier proceso secundario cuyo ID de grupo de procesos sea igual al valor absoluto de `pid`
* **-1** --> se puede pasar para monitorear cualquier proceso hijo que cambie su estado primero, que se usa para implementar la funcionalidad `wait`.
* **0** --> Espere cualquier proceso secundario cuyo ID de grupo de procesos sea igual al del proceso que llama
* **>0** --> implica que el valor debe ser el ID de proceso real que se devolvió desde la función `fork`, que a su vez se usa para monitorear solo un proceso hijo específico

&#x20;El segundo argumento es de tipo puntero `int` y debemos declarar una variable entera para pasar su dirección a la función. `waitpid`, por otro lado, almacenará la información del estado del niño en la variable `int` dada, que luego se puede decodificar usando las macros predefinidas.

El último argumento es de tipo `int`, y se usa para especificar ciertos eventos de proceso hijo a monitorear además de los predeterminados.

### Utilice macros para mostrar el estado de espera del proceso secundario en C

El ID del proceso del hijo que terminó, o cero si se utilizó WNOHANG y no hay hijo disponible, o -1 en caso de error (en este caso, errno se pone a un valor apropiado).

* **WNOHANG** --> significa que vuelve inmediatamente si ningún hijo ha terminado.
* **WUNTRACED** --> que significa que también vuelve si hay hijos parados (pero no rastreados), y de cuyo estado no ha recibido notificación. El estado para los hijos rastreados que están parados también se proporciona sin esta opción.
* **WCONTINUED** --> También devolver si un hijo detenido ha sido retomado por entrega de `SIGCONT`.



### Bibliografia

* [https://www.delftstack.com/es/howto/c/waitpid-in-c/](https://www.delftstack.com/es/howto/c/waitpid-in-c/)
* [https://stackoverflow.com/questions/21248840/example-of-waitpid-in-use](https://stackoverflow.com/questions/21248840/example-of-waitpid-in-use)
* [https://linux.die.net/man/2/waitpid](https://linux.die.net/man/2/waitpid)
* [https://manpages.ubuntu.com/manpages/xenial/es/man2/wait.2.html](https://manpages.ubuntu.com/manpages/xenial/es/man2/wait.2.html)
* [https://ciksiti.com/es/chapters/9183-waitpid-syscall-in-c](https://ciksiti.com/es/chapters/9183-waitpid-syscall-in-c)
