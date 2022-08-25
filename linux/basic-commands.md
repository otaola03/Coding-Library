# Basic Commands

### ¿Que es y para que srive linux?

Resultado de imagen de que es linux Linux® es un sistema operativo open source. En 1991, Linus Torvalds lo diseñó y creó a modo de pasatiempo. Mientras estaba en la universidad, Linus intentó crear una versión open source, alternativa y gratuita del sistema operativo MINIX, que a su vez se basaba en los principios y el diseño de Unix.

<details>

<summary>Comandos</summary>

1. [Man](basic-commands.md#1.-man)
2. [pwd](basic-commands.md#2.-pwd)
3. [touch](basic-commands.md#3.-touch)
4. [mkdir](basic-commands.md#4.-mkdir)
5. [rm](basic-commands.md#5-.rm)
6. [cd](basic-commands.md#6.-cd)
7. [tar](basic-commands.md#7.-tar)

[Otros comandos](basic-commands.md#otros-comandos)

</details>

### Comandos basicos para desarrolladores

#### 1. Man

Con él podemos conocer el uso de todos los comandos de Linux, mostrando una vista con información como nombre, sinopsis, descripción, opciones, estado de salida, valores de devolución, errores, archivos, versiones, ejemplos, etc.

```
man [command/tool name]
```

#### 2. pwd

El comando **`pwd`** se usa para localizar la ruta del directorio de trabajo en el que te encuentras. Por ejemplo, si mi nombre de usuario es «jperez» y estoy en mi directorio Documentos, la ruta absoluta sería: /home/jperez/Documents.

```
pwd [OPTION]...
```

#### 3. touch

Este comando se usa para crear cualquier tipo nuevo de archivo en sistemas Linux.

```
touch file_name
```

Para **cambiar la hora** p fecha de un fichero hay que hacer lo sigueinte

| Comando                      | Descripcion                                |
| ---------------------------- | ------------------------------------------ |
| -t \[AñoMesDiaHorasMinutos]  | Para cmabiar la hora a ficheros o carpetas |
| -ht \[AñoMesDiaHorasMinutos] | Para cambiar la hora a enlaces simbolicos  |

#### 4. mkdir

Este comando permite a los usuarios crear directorios (carpetas). Posibilita la creación de varios directorios a la vez, así como establecer los permisos para los directorios.

```
mkdir <dirname>  
```

#### 5 .rm

**rm** elimina cada archivo especificado en la línea de comando y directorios. Ten mucho cuidado al usarlo porque no se puede deshacer y es muy difícil recuperar archivos eliminados de esta manera.

```
rm file_to_copy.txt
```

En el caso de quieras eliminar un carpeta deberas utilizar el flag -R. Esto viene de «recursivo». Indica que la orden se ejecutará también para sub-directorios y para todos los archivos que estén dentro de la carpeta.

```
rm -R
```

Para «forzar» la orden se utiliza el flag -f, evitando que la consola te pida confirmación para borrar ciertos archivos o directorios contenidos en el directorio que quieres borrar (que te la podría pedir, y te resultará muy molesto si tienes que confirmar… 50 archivos).

```
rm -Rf
```

#### 6.  cd

Con la ayuda de este comando, podemos navegar por todos nuestros directorios en nuestro sistema. Las opciones que nos permite serían:



* Cambiar del directorio actual a un nuevo directorio
* Cambiar directorio usando una ruta absoluta
* Cambiar directorio usando la ruta relativa
* Cambiar al directorio de inicio
* Cambiar al directorio anterior
* Cambiar al directorio principal
* Cambiar al directorio raíz
* Cambiar al directorio de inicio de otro usuario
* Cambiar a directorio con espacios
* Cambiar hasta múltiples subdirectorios

```
cd [OPTIONS] directory
```

#### 7. tar

Este comando se utiliza para crear y extraer archivos de almacenamiento.

```
tar [options] [archive-file] [file or directory to be archived]
```

| Flag | Descripcion                |
| ---- | -------------------------- |
| -cf  | crea un fichero comprimido |
| -xf  | descomprime un fichero     |

#### Otros comandos

| Comandos                | Descripcion                   |
| ----------------------- | ----------------------------- |
| bc                      | calculadora en consola (quit) |
| bash \[archive-file]    | ejecutar ficheros             |
| env                     | para ver el enotno            |
| cp \[Origen] \[Destino] | Copia un archivo              |

### Bibliografia

* [https://profile.es/blog/comandos-linux/](https://profile.es/blog/comandos-linux/)
* [https://borrowbits.com/2013/04/borrar-directorio-no-vacio-en-linux/](https://borrowbits.com/2013/04/borrar-directorio-no-vacio-en-linux/)
