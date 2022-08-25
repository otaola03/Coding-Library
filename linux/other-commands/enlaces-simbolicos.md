---
description: Enlaces duros y Enlaces simbolicos
---

# Ln

Un **symlink** (también llamado enlace simbólico) es un tipo de archivo en Linux que apunta a otro archivo o una carpeta en tu computador. Los enlaces simbólicos son similares a los accesos directos en Windows.

Algunas personas llaman a los enlaces simbólicos "soft links" - un tipo de enlace en los sistemas Linux/UNIX - opuestos a los "hard links".

### ¿Qué son los enlaces duros?

1. Los enlaces duros tienen el mismo número de inodos.
2. El comando ls -l muestra todos los enlaces con la columna de enlace que muestra el número de enlaces.
3. Los enlaces tienen contenido de archivo real
4. Eliminar cualquier enlace, solo reduce el número de enlaces pero no afecta a los otros enlaces.
5. No puede crear un vínculo físico para un directorio.
6. Incluso si se elimina el archivo original, el enlace seguirá mostrando el contenido del archivo.

En pocas palabras, un enlace físico es solo un nombre adicional para un archivo ya existente en sistemas basados ​​en UNIX

### ¿Qué son los enlaces suaves?

1. Los enlaces blandos tienen diferentes números de inodos.
2. El comando ls -l muestra todos los enlaces con el valor de la segunda columna 1 y el enlace apunta al archivo original.
3. Soft Link contiene la ruta del archivo original y no el contenido.
4. La eliminación del enlace flexible no afecta nada, pero cuando se elimina el archivo original, el enlace se convierte en un enlace «colgante» que apunta a un archivo inexistente.
5. Un Soft Link puede enlazar a un directorio.

En términos simples, un enlace flexible suele ser un alias para el archivo original que redirige al archivo o directorio de destino cuando se accede a través de la ruta especificada en el asunto del enlace flexible. Es similar a la opción de acceso directo en los sistemas operativos Windows.

### Cómo crear un enlace simbólico para un archivo <a href="#c-mo-crear-un-enlace-simb-lico" id="c-mo-crear-un-enlace-simb-lico"></a>

La sintaxis para crear un enlace simbólico es:

```
ln -s <ruta del archivo o carpeta> <ruta del enlace que se creará>
```

`ln` es el comando de enlace. La bandera `-s` especifica que el enlace debe ser soft. Las `-s` también pueden ser introducidas como `-symbolic`.

Por defecto, el comando `ln` crea hard links. El siguiente argumento es la `ruta del archivo (o carpeta)` que quieres enlazar. (Es decir, el archivo o carpeta para el acceso directo que quieres crear).

El último argumento es la `ruta para enlazarse` a sí mismo (el acceso directo).

Para que quede calor aqui tienes un ejemplo en el que se crea un enlace simbolico al fichero `/home/Desktop/fichero.txt` y se le da el nombre `enlace.txt`.

```
ln -s /home/Desktop/fichero.txt enlace.txt
```

En el caso de qu quiereas ubicarlo en otra carpeta y no en el direcotrio actual:

```
ln -s /home/Desktop/fichero.txt /home/Documents/enlace.txt
```

### Cómo crear un enlace simbólico para una carpeta <a href="#c-mo-crear-un-enlace-simb-lico" id="c-mo-crear-un-enlace-simb-lico"></a>

Al igual que para los arhcivos usaremos:

```
ln -s /home/mis-cosas /home/Desktop/mis-cosas
```

Esto crearía una carpeta simbólica llamada `mis cosas` en el escritorio que contendría el contenido de `/home/mis-cosas`. Cualquier cambio en esta carpeta vinculada también afectará a la carpeta original.

### Flags de ln

Las opciones de enlace simbólico se denominan switches de línea de comando. Aquí están los más comunes y sus descripciones:



| **Flags**            | **Descripción**                                              |
| -------------------- | ------------------------------------------------------------ |
| -backup\[=CONTROL]   | copia de seguridad de cada archivo de destino existente      |
| -d, -F, –directory   | el superusuario puede intentar un enlace duro                |
| -f, –force           | se elimina el archivo de destino existente                   |
| -I, –interactive     | preguntar antes de eliminar archivos de destino              |
| -L, –logical         | objetivos de deferencia que son enlaces simbólicos           |
| -n, –non-dereference | los enlaces simbólicos al directorio se tratan como archivos |
| -P, –physical        | convierte enlaces duros directamente a enlaces simbólicos    |
| -r, –relative        | crea enlaces simbólicos relativos a la ubicación del enlace  |
| -s, -symbol          | hacer enlaces simbólicos en lugar de enlaces duros           |
| -S, –suffix=SUFFIX   | anula el sufijo de copia de seguridad habitual               |
| -v, –verbose         | imprime el nombre de cada archivo vinculado                  |

### Cómo usar unlink para eliminar un enlace simbólico <a href="#c-mo-usar-unlink-para-eliminar-un-enlace-simb-lico" id="c-mo-usar-unlink-para-eliminar-un-enlace-simb-lico"></a>

La sintaxis es:

```shell
unlink <ruta-enlace-simbolico>
```

### Cómo usar rm para remover un symlink <a href="#c-mo-usar-rm-para-remover-un-symlink" id="c-mo-usar-rm-para-remover-un-symlink"></a>

Como hemos visto, un enlace simbólico es sólo otro archivo o carpeta que apunta a un archivo o carpeta original. Para eliminar esa relación, tú puedes eliminar el archivo enlazado.

Por lo tanto, la sintaxis es:

```shell
rm <ruta-enlace-simbolico>
```

En el caso de los direcotrios, si estos tiene  contenido en su interior, el comando te dara error y por ello deveras uilizar los flags -rf. Para mas informacion, puedes acceder al apartado de [rm](../basic-commands.md#5-.rm).

```
rm -rf <ruta-enlace-simbolico>
```

### Cómo encontrar y eliminar los enlaces rotos <a href="#c-mo-encontrar-y-eliminar-los-enlaces-rotos" id="c-mo-encontrar-y-eliminar-los-enlaces-rotos"></a>

Los enlaces rotos se producen cuando el archivo o la carpeta a la que apunta un enlace simbólico cambia de ruta o se elimina. Enotnces siempre que intentes acceder a ese enlace te dara un error de "No existe tal archivo o directorio". Esto se debe a que el enlace no tiene contenido propio.

Cuando tú descubras enlaces rotos, tú puedes borrar el archivo fácilmente. Una forma fácil de encontrar enlaces simbólicos rotos es:

```shell
find /home/Desktop -xtype l
```

Esto listará todos los enlaces simbólicos rotos en el directorio `Desktop` - desde los archivos a los directorios y sub-directorios.

Con en flag `-d` o -delete podras borrarlos:

```shell
find /home/Desktop -xtype l -delete
```

### Bibliografia

* [https://www.hostinger.es/tutoriales/crear-enlace-simbolico-linux](https://www.hostinger.es/tutoriales/crear-enlace-simbolico-linux)
* [https://www.freecodecamp.org/espanol/news/tutorial-de-enlace-simbolico-en-linux-como-crear-y-remover-un-enlace-simbolico/](https://www.freecodecamp.org/espanol/news/tutorial-de-enlace-simbolico-en-linux-como-crear-y-remover-un-enlace-simbolico/)
* [https://es.sawakinome.com/articles/software/unassigned-2417.html](https://es.sawakinome.com/articles/software/unassigned-2417.html)
