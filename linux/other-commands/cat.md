---
description: Ver contenido
---

# Cat

El comando cat en Linux es uno de los más útiles que puedes aprender. Deriva su nombre de la palabra concatenar y te permite crear, fusionar o imprimir archivos en la pantalla de salida estándar o en otro archivo y mucho más.

### Sintaxis

El comando toma un nombre de archivo como argumento junto con opciones para especificar operaciones particulares.

```
cat [OPTION] [FILE]
```

### Flags

Como la mayoría de líneas de comando, Linux Cat **se controla por parámetros opcionales cuando se reproduce**. Estas opciones siguen al nombre del comando. Debes tener en cuenta que hay que distinguir entre mayúsculas y minúsculas. Normalmente hay dos notaciones para la mayoría de las opciones:

| Flag       | Descripcion                                                                              |
| ---------- | ---------------------------------------------------------------------------------------- |
| -h, --help | Ayuda a mostrar el comando Linux Cat                                                     |
| -n         | Enumera las líneas de salida                                                             |
| -s         | Combina varias líneas en blanco en una sola (eliminar lineas en blanco, saltos de linea) |
| -b         | Combina varias líneas en blanco en una sola                                              |
| -v         | Emite caracteres invisibles                                                              |
| -e         | Igual que -v, pero incluyendo el marcador de fin de línea                                |
| -t         | Igual que -v, pero incluyendo el marcador de pestañas                                    |
| et         | Combinación de -e y -t; emite todos los caracteres invisibles                            |

### Ver el contenido de un archivo con el comando cat

Este es uno de los usos más básicos del comando cat. Sin necesidad de ninguna opción, el comando leerá el contenido de un archivo y lo mostrará en la consola.

```
cat filename.txt
```

Para evitar desplazarse por archivos muy grandes, puedes agregar la opción **| more** ver la pantalla de menos o más:

```
cat filename.txt | more
```

También puedes mostrar el contenido de más de un archivo. Por ejemplo, para mostrar el contenido de todos los archivos de texto, usa el siguiente comando en el terminal:

```
cat *.txt
```

### Como se utiliza Cat en la pracica

La mayoría de los escenarios de aplicación resultan de la **encadenación de la orden con otros comandos**. Con ello, se utilizan redireccionamientos de la entrada y salida estándar. En concreto, se trata de las llamadas tuberías y redireccionamientos. Estos son proporcionados por el shell (también llamado “intérprete de comandos”) y su uso se extiende a todos los comandos:



<table data-header-hidden><thead><tr><th width="176"></th><th width="117"></th><th></th><th></th></tr></thead><tbody><tr><td><strong>Desviación</strong></td><td><strong>Símbolo</strong></td><td><strong>Aplicación</strong></td><td><strong>Explicación</strong></td></tr><tr><td>Pipe</td><td>|</td><td>cmd1 | cmd2</td><td>  Reenvía la salida del comando cmd1 a la entrada del comando cmd2</td></tr><tr><td>Input-Redirect</td><td>&#x3C;</td><td>cmd &#x3C; data</td><td>Lee los datos de entrada del comando cmd del archivo</td></tr><tr><td>Output-Redirect</td><td>></td><td>cmd > data</td><td>Escribe los datos de salida del comando cmd en el archivo; si es necesario, se sobrescribe el archivo ya existente</td></tr><tr><td>Output-Redirect</td><td>>></td><td>cmd >> data</td><td>Escribe los datos de salida del comando cmd en el archivo; si es necesario, se amplía el archivo ya existente</td></tr></tbody></table>

Linux Cat **suele comenzar con una sucesión de otros comandor Linux**. Aquí te mostramos los más usados:



| **Comando Linux**                                                                                                                                                         | **Explicación**                                                     |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------- |
| split                                                                                                                                                                     | Divide el archivo en trozos; la operación se puede invertir con cat |
| uniq                                                                                                                                                                      | Elimina las líneas de entrada que aparecen más de una vez           |
| sort                                                                                                                                                                      | Ordena las líneas de entrada de forma alfanumérica                  |
| [head](https://www.ionos.es/digitalguide/servidores/configuracion/linux-head/), [tail](https://www.ionos.es/digitalguide/servidores/configuracion/comando-tail-de-linux/) | Limita la salida a las líneas al principio/final                    |

### Redirigir contenido usando el comando cat <a href="#h-redirigir-contenido-usando-el-comando-cat" id="h-redirigir-contenido-usando-el-comando-cat"></a>

En lugar de mostrar el contenido de un archivo en la consola, puedes redirigir la salida a otro archivo usando la opción **>**. La línea de comando se vería así:

```
cat source.txt > destination.txt
```

Si el archivo de destino no existe, el comando lo creará o sobrescribirá uno existente con el mismo nombre.

Para agregar el contenido del archivo destino, usa la opción **>>** junto con el comando cat:

```
cat source.txt >> destination.txt
```

### Concatenar archivos con el comando cat de Linux <a href="#h-concatenar-archivos-con-el-comando-cat-de-linux" id="h-concatenar-archivos-con-el-comando-cat-de-linux"></a>

Este comando también te permite concatenar múltiples archivos en uno solo. En esencia, funciona exactamente como la función de redireccionamiento anterior, pero con múltiples archivos fuente.

```
cat source1.txt source2.txt > destination.txt
```

Como antes, el comando anterior creará el archivo de destino si no existe, o sobrescribirá uno existente con el mismo nombre.

### Marcar el final de las líneas con el comando Cat <a href="#h-marcar-el-final-de-las-l-neas-con-el-comando-cat" id="h-marcar-el-final-de-las-l-neas-con-el-comando-cat"></a>

El comando cat también puede marcar los extremos de las líneas mostrando el caracter **$** al final de cada línea. Para usar esta función, usa la opción **-E** junto con el comando cat:

```
cat -E filename.txt
```

### Mostrar un archivo en orden inverso con el comando Cat <a href="#h-mostrar-un-archivo-en-orden-inverso-con-el-comando-cat" id="h-mostrar-un-archivo-en-orden-inverso-con-el-comando-cat"></a>

Para ver el contenido de un archivo en orden inverso, comenzando con la última línea y terminando con la primera, simplemente usa el comando **tac**, que es **cat** invertido:

```
tac filename.txt
```

### Bibliografia

* [https://www.hostinger.es/tutoriales/comando-cat-linux](https://www.hostinger.es/tutoriales/comando-cat-linux)
* [https://www.ionos.es/digitalguide/servidores/configuracion/linux-cat/](https://www.ionos.es/digitalguide/servidores/configuracion/linux-cat/)
