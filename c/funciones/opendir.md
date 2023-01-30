---
description: abrir, mostrar y cerrar directorios
---

# opendir

### opendir

`opendir` es una función en el lenguaje de programación C que se utiliza para abrir un directorio y acceder a sus archivos y subdirectorios.

La función `opendir` permite que un programa lea los archivos y subdirectorios de un directorio. Una vez que el directorio se ha abierto, puedes usar la función `readdir` para leer los archivos y subdirectorios uno por uno. Cuando ya no necesitas acceder al directorio, puedes cerrarlo con la función `closedir`.

La cabecera de la función `opendir` es:

```c
#include <dirent.h>
DIR *opendir(const char *dirname);
```

El argumento de `opendir` es el nombre del directorio que se desea abrir, en forma de una cadena de caracteres (`char *`).&#x20;

La función `opendir` devuelve un puntero a un tipo `DIR` que representa el directorio abierto. Si la apertura del directorio falla, la función devuelve `NULL`.

La estructura `DIR` es una estructura que representa un directorio abierto en el sistema operativo. Es una estructura interna que no se documenta públicamente y puede variar entre sistemas operativos y compiladores.

Sin embargo, en general, la estructura `DIR` contiene información sobre el directorio abierto, como la posición actual en el directorio y un puntero al archivo actual. Esta información es utilizada por la biblioteca de dirent para mantener un seguimiento de la lectura de los archivos y subdirectorios en el directorio abierto.

Es importante notar que no debes acceder directamente a los campos de la estructura `DIR`. En su lugar, debes usar las funciones proporcionadas por la biblioteca de dirent, como `opendir`, `readdir` y `closedir`, para trabajar con los directorios.

Ejemplo de uso:

```c
#include <dirent.h>
#include <stdio.h>

int main() {
    DIR *dir = opendir("/path/to/dir");
    if (dir == NULL) {
        printf("No se pudo abrir el directorio\n");
        return 1;
    }

    // leer los archivos y subdirectorios aquí

    closedir(dir);
    return 0;
}
```

### readdir
