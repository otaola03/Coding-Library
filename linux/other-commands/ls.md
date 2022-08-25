---
description: Para listar el contenido de un directorio
---

# Ls

### ¿Para qué sirve el comando ls <a href="#para-que-sirve-el-comando-ls" id="para-que-sirve-el-comando-ls"></a>

```
ls
```

El contenido se mostrará todo en una sola línea, en mi caso se ve algo así pero dependiendo de la distribución Linux que utilices y que archivos o directorios hayas creado esta salida será diferente.

```
Descargas  Documentos  Escritorio  Imágenes  Música  Plantillas  Público  Vídeos
```

### ¿Como listar archivos ocultos?

```
ls -a
```

### Como listar directorios con informacion detallada

Si lo que deseamos es **ver una lista mas detallada** aun, es decir con información relevante a cada uno de los archivos usamos…

```
ls -l
```

Esto mostrara lo siguiente:

```
-rw-r--r-- 1 jperez jperez 18355 ago 22 21:07 comandos.txt
drwxr-xr-x 2 jperez jperez  4096 ago 22 21:18 Folder
```

* La primera columna de contiene información del **tipo nodo (filenode)** como si estamos lidiando con un archivo o un directorio y los permisos de este. En el siguiente ejemplo vemos que empieza con una **d**, esto quiere decir que es un directorio, por el contrario la segunda línea inicia con un **-**, esto quiere decir que es un archivo normal.
  * Para mas informacion sobre los permisos ve a este aparrtado
* La segunda columna indica la **cantidad de** **vinculos** que existen en este archivo (1)
* La tercer columna que indica quien es el **owner (dueño)** del archivo o directorio (jperez).
* La cuarta columna que indica el **filesize (tamaño de archivo en bytes)** (jdoe).
* La quinta columna muestra la **fecha de creación del archivo o directorio** (ago 22 21:07)
* La última columna muestra el **nombre del archivo o directorio** (Folder)

### Parametros adicionales

| Parámetro | Descripcion                                                      |
| --------- | ---------------------------------------------------------------- |
| -r        | Ordena en orden inverso el listado de archivos                   |
| -t        | Ordena el listado de archivos conforme el mas reciente al inicio |
| -l@       | Para ver permisos especiales                                     |

### Bibliografia

* [https://apuntes.de/linux-certificacion-lpi/ls/#gsc.tab=0](https://apuntes.de/linux-certificacion-lpi/ls/#gsc.tab=0)
* [https://linuxhint.com/what-does-ls-l-command-do-in-linux/ ](https://linuxhint.com/what-does-ls-l-command-do-in-linux/)
