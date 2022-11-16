---
description: Buscar archivos
---

# Find

Para encontrar un archivo en Linux, puedes utilizar el comando Linux find. Esto inicia una búsqueda recursiva en una jerarquía de directorios siguiendo ciertos criterios. El comando find de Linux es una herramienta precisa para encontrar archivos y directorios y es compatible con casi todas las distribuciones de Linux.

### La sintaxis básica <a href="#h-la-sintaxis-b-sica" id="h-la-sintaxis-b-sica"></a>

El comando **find** es el comando que más se utiliza para encontrar y filtrar archivos en Linux. El diseño básico de este comando es el siguiente:

```bash
find <startingdirectory> <options> <search term>
```

Comienza con la palabra clave **find**, que alerta a Linux de que lo que sigue se refiere a la búsqueda de un archivo y va seguido de tres parametros:

* **\<startingdirectory>** es el punto de origen de donde deseas iniciar la búsqueda. uede ser reemplazado con varios argumento, incluyendo:
  * **/ (slash)** – busca en todo el sistema.
  * **. (punto)** – busca en la carpeta en la que estás trabajando actualmente (directorio actual).
  * **\~ (tilde)** – para buscar desde tu directorio home.
* **\<options>** se usa para tu archivo. Este podría ser el nombre, tipo, fecha de creación del archivo, etc. Se especifica mediante parametros de busqueda. (lel tipo que bas a buscar)
* **\<searchterm>** es donde se especificará el término de búsqueda relevante. (El nombre del tipo que bas a buscar)

### Parametros de busqueda

Un parámetro de búsqueda consiste en un guion que va seguido inmediatamente por el nombre del parámetro. Después un espacio y el valor del parámetro. A continuación, te presentamos un resumen de los parámetros de búsqueda más utilizados:

| Parametro de busqueda  | Descripcion                     |
| ---------------------- | ------------------------------- |
| -name, -iname          | Filtrar por nombre de archivo   |
| -type                  | Filtrar por tipo de archivo     |
| -size, -empty          | Filtrar por tamaño de archivo   |
| -ctime, -mtime, -atime | Filtrar por marca de tiempo     |
| -user, -group          | Filtrar por propietario y grupo |
| -perm                  | Filtrar por derechos de archivo |

**También se pueden combinar varios parámetros de búsqueda.** Aquí se asume implícitamente una operación lógica AND. Esto puede escribirse explícitamente. Además, se puede utilizar un enlace OR o negar una condición:

| Parametro de busqueda | Descripcion                                                                     |
| --------------------- | ------------------------------------------------------------------------------- |
| -and                  | Los resultados de la búsqueda deben cumplir ambas condiciones                   |
| -or                   | Los resultados de la búsqueda deben cumplir al menos una de las dos condiciones |
| -not                  | Negar la condición posterior                                                    |

### Búsqueda por nombre <a href="#h-b-squeda-por-nombre" id="h-b-squeda-por-nombre"></a>

Por supuesto, el método más común y obvio para buscar un archivo es usar su nombre. Para ejecutar una consulta de búsqueda simple usando el nombre del archivo, usa el comando **find** de la siguiente manera:

```bash
find . -name my-file
```

Si deseas buscar un determinado archivo por nombre y **eliminarlo**, usa el argumento **-delete** después del nombre del archivo:

```bash
find . -name my-file -delete
```

### Búsqueda por tipo <a href="#h-b-squeda-por-tipo" id="h-b-squeda-por-tipo"></a>

Linux permite a los usuarios listar toda la información basada en sus tipos. Hay varios filtros que puedes usar:

| Parametro de busqueda | Descripcion                |
| --------------------- | -------------------------- |
| d                     | directorio o carpeta       |
| f                     | archivo normal             |
| l                     | enlace simbólico           |
| c                     | dispositivos de caracteres |
| b                     | dispositivos de bloque     |

Un ejemplo simple del uso del tipo de archivo para la búsqueda se puede ver a continuación:

```bash
find / -type d
```

Esto mostrará una lista de todos los directorios presentes en tu sistema de archivos, al haber comenzado la búsqueda desde nuestro directorio raíz con el símbolo de barra inclinada /.

### Búsqueda por fecha <a href="#h-b-squeda-por-fecha" id="h-b-squeda-por-fecha"></a>

Si quieres buscar archivos en función de su fecha de acceso y las registros de fecha de modificación, Linux te ofrece las herramientas para hacerlo. Hay 3 registros de tiempo de los cuales Linux realiza seguimiento en los archivos:

| Parametro de busqueda | Descripcion                       |
| --------------------- | --------------------------------- |
| -ctime, -cmin         | Filtrar por fecha de creación     |
| -mtime, -mmin         | Filtrar por fecha de modificación |
| -atime, -amin         | Filtrar por fecha de acceso       |





### Bibliografia

* [https://www.hostinger.es/tutoriales/como-usar-comando-find-locate-en-linux/](https://www.hostinger.es/tutoriales/como-usar-comando-find-locate-en-linux/)
* [https://www.ionos.es/digitalguide/servidores/configuracion/comando-linux-find/](https://www.ionos.es/digitalguide/servidores/configuracion/comando-linux-find/)
