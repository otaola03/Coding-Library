---
description: Crear procesos
---

# Fork

La llamada al sistema de fork se usa para crear un nuevo proceso, que se llama _**child process**_ (proceso hijo), que se ejecuta simultáneamente con el proceso que realiza la llamada a la `fork()` (proceso principal). Después de que se crea un nuevo proceso secundario, ambos procesos ejecutarán la siguiente instrucción después de la llamada al sistema fork(). Un proceso hijo usa la misma computadora (contador de programa), los mismos registros de CPU, los mismos archivos abiertos que usa el proceso padre, basicamente es un **duplicado del proceso padre**.

```
pid_t fork(void)
```

### Retorno del fork

No toma parámetros y devuelve un valor entero. A continuación se muestran diferentes valores devueltos por fork().

| Case           | Return value                                      |
| -------------- | ------------------------------------------------- |
| Valor positivo | Si todo va bien, retorna al padre el PID del hijo |
| Zero (0)       | Si todo va bien returna 0 al hijo recien creado   |
| Valor negativo | Si la creación de un proceso hijo no tuvo éxito.  |

> Nota: fork() es una función basada en subprocesos, para obtener el resultado correcto, ejecute el programa en un sistema local.
