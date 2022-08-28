---
description: Para tratar ficheros (contar)
---

# Wc

El programa **permite leer la entrada estándar o una lista concatenada, y genera una o más de las estadísticas siguientes: conteo de líneas, conteo de palabras y conteo de bytes**. Este comando puede aceptar uno o más nombres de archivos de entrada.

### Sintaxis

A continuación puede encontrar la sintaxis del comando:

```
wc [OPTION]... [FILE]...
```

Si pasamos **solo un nombre de archivo en el argumento obtendremos el conteo de líneas, de palabras y de bytes**. Además también **podemos pasar más de un nombre de archivo en el argumento del comando**

### Flags

Además de utilizar este comando como hemos visto hasta ahora, WC es un comando simple para trabajar y viene con sólo un puñado de opciones que pueden resultar interesantes de utilizar en algunas ocasiones:

| Flags                | Descripcion                                              |
| -------------------- | -------------------------------------------------------- |
| -l, -lines           | **imprime el número de líneas** presentes en el archivo. |
| -w, -words           | **imprime el número total de palabras** en el archivo.   |
| -m, -chars           | **imprime el número de caracteres** del archivo.         |
| -L, -max-line-lenght | **imprime el tamaño de la línea más larga** del archivo. |
| -c, -bytes           | **imprime el número total de bytes** en el archivo.      |

### Use el comando wc con tuberías

El comando wc se usa muy comúnmente con una combinación de diferentes comandos con tuberías. Veamos algunos ejemplos.

El siguiente comando de una sola línea contará el número de veces que aparece una palabra en un archivo:

```
$ cat file-name | grep -o 'word' | wc -l
```

Para contar el número de archivos y directorios en el directorio actual

```
$ ls -1 | wc -l
```

Para contar el número de archivos en el directorio actual.

```
$ find . -type f | wc -l
```

### Bibliografia

* [https://ubunlog.com/wc-un-comando-para-realizar-recuentos-en-gnu-linux/#Opciones\_de\_comando\_WC](https://ubunlog.com/wc-un-comando-para-realizar-recuentos-en-gnu-linux/#Opciones\_de\_comando\_WC)
* [https://conpilar.kryptonsolid.com/comando-wc-de-linux-para-contar-el-numero-de-lineas-palabras-y-caracteres/](https://conpilar.kryptonsolid.com/comando-wc-de-linux-para-contar-el-numero-de-lineas-palabras-y-caracteres/)
