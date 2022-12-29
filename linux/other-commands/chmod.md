---
description: Editar permisos
---

# Chmod

### ¿Que es chmod?

El comando chmod **se usa para cambiar los permisos de archivos o directorios**. En Linux y otros sistemas operativos como Unix, hay un conjunto de reglas para cada archivo que define quién puede acceder a ese archivo, y cómo se puede acceder a él. Estas reglas se llaman permisos de archivo o modos de archivo .

### Syntaxis de Chmod

En general, los comandos chmod toman la forma:

```
chmod [OPTION] MODE FILE
```

Al comando _chmod_ le sigue el elemento opcional _**options**_, que permite definir opciones avanzadas. El elemento _mode_ representa el modo que se aplicará a _**file**_, que podrá ser un archivo o un directorio. El _**mode**_ indica si una clase de usuario debe recibir permisos de acceso o si los permisos con los que cuenta se han de retirar.

### Los modos de chmod

De acuerdo con el sistema de archivos Unix, en un servidor Linux, cada archivo, como también los directorios, cuenta con permisos de acceso propios, que se regulan siempre en base a tres clases de usuarios:

|           |                                                                                                                                                                                                                       |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| User (u)  | Por lo general, cualquier usuario que crea un archivo en un sistema Unix se define automáticamente como _user_ de ese archivo                                                                                         |
| Group (g) | La clase _grupo_ aúna en el servidor a varias cuentas de usuario. En sistemas de archivos tipo Unix, cada cuenta se subordina a un grupo principal de forma automática, pero también puede pertenecer a otros grupos. |
| Other (o) | La clase de usuario _other_ abarca a todos los usuarios que no son propietarios de archivos ni miembros de un grupo con derechos de acceso.                                                                           |

Para hacer referencia a todas las clases se utiliza la letra **a (all)**.

### Tipos de permisos

Linux utiliza una simbologia que asigna a cada tipo de permisos y usaurios una letrayt. En la sigueintre tabla podras observar las simoblogia para los distintos tipos de permisos:

| Permisos | Descripcion                      |
| -------- | -------------------------------- |
| r        | Permiso de lectura (_read_)      |
| w        | Permiso de escritura (_write_)   |
| x        | Permiso de ejecución (_execute_) |

### Visualizacion de permisos

Una manera rápida y fácil de enumerar los permisos de un archivo es con la opción de listado largo ( -l ) del comando ls. Por ejemplo, para ver los permisos de archivo.txt , puedo usar el comando:

```
ls -l archivo.txt
```

Utilizando unicamnete el comando **ls -l** se listaran todos tu archivos y directorios y sus respectivos permisos. Para mas informacion hacerca accede al aprtado de [ls](ls.md#como-listar-archivos-y-directorios-con-informacion-detallada).

### Agregar y quitar permisos con letras

Si la definición de los derechos se hace por el modo simbólico, para vincular las clases de usuario con sus respectivos permisos se utilizan los siguientes **operadores:**

| Operadores | Descripcion                                                                                                                         |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------- |
| **+**      | Con el operador “+” se asignan más derechos de archivo a una clase de usuario. Solo se sobrescriben los derechos afectados.         |
| -          | El operador “-“retira derechos de acceso a una clase de usuario.                                                                    |
| =          | Si los permisos de archivo de una clase de usuario se han de renovar, sin importar qué derechos tuvo antes, se usa el operador “=”. |

Si por ejemplo queremos que nuestro usuario tenga permisos de ejecion en el fichero archivo.txt tendremos que ejecutar el siguiente comando:

```
chmod u+x archivo.txt
```

Con el metodo simbolico simepre que queiras agregar o quitar permisos a alguna de las clases tendras que hacerle referencia en el comando . Por ejemplo, si ahora queremos quitar los permisos de escritura al usuario y al gurpo tednriamos que ejecutar el siguiente comando:

```
chmod ug-w
```

### Agregar y quitar permisos con el metodo octal

Aunque la notación simbólica es una de las más utilizadas, su uso frecuente puede hacerla inmanejable. Por esta razón, muchos administradores recurren a la notación octal a la hora de atribuir derechos. Se trata de un número de tres cifras en el que cada posición representa una clase de usuario del servidor. La notación octal sigue siempre el mismo orden:

| Posición de la cifra de la clase de usuario | Significado                                               |
| ------------------------------------------- | --------------------------------------------------------- |
| 1                                           | Corresponde a la clase de usuario “propietario” (_user_). |
| 2                                           | Corresponde a la clase de usuario “grupo” (_group_).      |
| 3                                           | Corresponde a la clase de usuario “otros” (_other_).      |

El metodo octal se basa en realizar combinaciones de sumas entre los 4 sigueintes numeros, para asi dar permisos a las distintas clases.&#x20;

| Valor para derechos de acceso | Significado  |
| ----------------------------- | ------------ |
| 4                             | Leer         |
| 2                             | Escrir       |
| 1                             | Ejecutar     |
| 0                             | Sin permisos |

Para que quede mas claro, si aprecias el sgueinte conando podras apreciar que el usario tiene permisos de lecutara(4) y escritura(2), (4+2), el grupo solo tiene permisos lectura(4) y los otros usuarios no tienen ningun permisos(0)

```
chmod 640 archivo.txt
```

### Opciones y Flags de chmod

| Flags               | Descripcion                                                                                                                      |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------- |
| -R, -recursive      | El cambio de los derechos de acceso se aplica a todos los archivos y subdirectorios dentro de una carpeta.                       |
| -v, verbose         | Después del comando se emite un diagnóstico de todos los archivos procesados.                                                    |
| -c, changes         | Después del comando se muestra un diagnóstico para todos los archivos que se han modificado.                                     |
| -f, silent, -quiet: | Se silencian los mensajes de error.                                                                                              |
| -no-preserve-root:  | Se usa para definir que no trate ‘ / ‘ (el directorio raíz ) de ninguna manera especial, que es la configuración predeterminada. |
| -preserve-root      | Se usa para indicar que no opere recursivamente en ‘ / ‘.                                                                        |
| -reference = RFILE  | Indica que debe establecer los permisos para que coincidan con los del archivo RFILE, ignorando cualquier MODO especificado.     |

### Bibliografia

* [https://www.ionos.es/digitalguide/servidores/know-how/asignacion-de-permisos-de-acceso-con-chmod/](https://www.ionos.es/digitalguide/servidores/know-how/asignacion-de-permisos-de-acceso-con-chmod/)
* [https://ayudalinux.com/comando-chmod-que-es-como-usarlo/](https://ayudalinux.com/comando-chmod-que-es-como-usarlo/)
