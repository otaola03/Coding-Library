# access

La función `access` es una función en el lenguaje de programación C que se utiliza para verificar si un proceso tiene permisos para acceder a un archivo o directorio en el sistema operativo.

La cabecera de la función `access` es:

```c
#include <unistd.h>
int access(const char *pathname, int mode);
```

Los argumentos de la función `access` son:

* `pathname` es una cadena de caracteres que representa el nombre del archivo o directorio que se desea verificar.
* `mode` es un entero que indica los permisos que se desean verificar. Los valores comunes para `mode` incluyen `F_OK` para verificar la existencia del archivo, `R_OK` para verificar si se tiene acceso de lectura, `W_OK` para verificar si se tiene acceso de escritura y `X_OK` para verificar si se tiene acceso de ejecución.

La función `access` devuelve `0` si el proceso tiene los permisos especificados para el archivo o directorio, y `-1` si no los tiene. La función también puede devolver un valor `-1` si ocurre un error, por ejemplo, si el archivo o directorio no existe o si no se tienen los permisos necesarios para acceder a él.

Ejemplo de uso:

```c
#include <unistd.h>
#include <stdio.h>

int main() {
    if (access("/path/to/file", F_OK) == 0) {
        printf("El archivo existe\n");
    } else {
        printf("El archivo no existe\n");
    }

    if (access("/path/to/file", R_OK) == 0) {
        printf("Se tiene acceso de lectura\n");
    } else {
        printf("No se tiene acceso de lectura\n");
    }

    return 0;
}
```
