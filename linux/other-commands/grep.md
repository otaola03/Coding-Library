---
description: Buscar texto en archvios
---

# Grep

Grep (por sus siglas en inglés Globally Search For Regular Expression and Print out) **es una herramienta de líneas de comando usada para buscar cadenas de texto** y encontrar coincidencias dentro de este. También puede ser utilizada para encontrar una palabra o combinación de palabras dentro de un fichero.

### Sintaxis

A continuacion esta la sintaxis de este comando de una manera simplificada:

```
grep '<texto-buscado>' <archivo/archivos>
```

Tenga en cuenta que las comillas simples o dobles son requeridas alrededor del texto si es más de una palabra.

Tú puedes además usar el comodín (\*) para seleccionar todos los archivos en un directorio.

El resultado de esto son las ocurrencias del patrón (por la línea en la que se encuentra) en los archivos. Si no existe una coincidencia, no se imprimirá ninguna salida en la terminal.

En el **manual** aparece de esta manera la sintaxis de grep:

```
grep [OPTION...] PATTERNS [FILE...]
```

* **grep**: la instrucción de comando
* **\[opciones]**: modificadores del comando
* **pattern**: el patrón que queremos encontrar con la búsqueda
* **\[ARCHIVO]**: el archivo en el que estás realizando la búsqueda

### Flags

Antes que nada explicaremos las opciones disponibles:

| Flags  | Descripcion                                                                                                   |
| ------ | ------------------------------------------------------------------------------------------------------------- |
| -i     | no diferenciará entre mayúsculas y minúsculas.                                                                |
| –w     | fuerza que sólo encuentre palabras concretas y no con una coincidencia parcial                                |
| -v     | selecciona las líneas que no coinciden                                                                        |
| -n     | muestra el número de la línea con las palabras de solicitadas                                                 |
| -h     | Si no queremos ver los nombres del archivo en la salida de datos usaremos la opción -h (de «hide»; esconder): |
| -r     | busca directorios recursivamente.                                                                             |
| -R     | como -r pero sigue todos los enlaces simbólicos.                                                              |
| -l     | muestra sólo nombres de archivos que tengan coincidencia de lo que buscas                                     |
| -c     | imprime el numero de lineas que tienen coincidencia, no la cantidad de coicidencias                           |
| -o     | imprime solo la coincidencia, no la frase entera                                                              |
| -color | muestra los patrones coincidentes en colores                                                                  |

### Buscar dos o mas palabras a la vez

Grep sirve para buscar una apalabra en un _archvio_, pero si lo que queremos es buscar dos palabras diferentes usaremos el comando _egrep._

```
egrep -w bosques|plantas /ruta/del/archivo
```

### **`-A` (--after-context) y `-B` (--before-context) - imprimir las líneas después y antes (respectivamente) del patrón coincidente**

```
grep grep grep.txt -A 1 -B 1
```

Resultado:

```
Hello, how are you
I am grep
Nice to meet you
```

Esta coincidencia de patrón se encuentra en la línea 2. `-A 1` significa una línea después de la línea que coincide y `-B 1` significa una línea antes de la línea que coincide.

Además existe `-C` (--context) opción el cual es igual a `-A` + `-B`.  El valor pasado a -C se usaría para -A y -B.

### Expresiones regulares para patrones <a href="#expresiones-regulares-para-patrones" id="expresiones-regulares-para-patrones"></a>

`grep` también permite especificar patrones con expresiones regulares básicas. Dos de ellas son:

#### **1. `^pattern` - Inicio de línea**

Este patrón significa que `grep` solo coincide con cadenas cuyas líneas empiecen con la cadena especificada después `^`. Ejemplo:

```
grep ^I grep.txt -n
```

Resultado:

```
2: I
```

#### **2. `pattern$` - fin de la línea**

```bash
grep you$ grep.txt
```

Resultado:

```bash
1: Hello, how are you
3: Nice to meet you
```

### Bibliografia

* [https://www.hostinger.es/tutoriales/comando-grep-linux](https://www.hostinger.es/tutoriales/comando-grep-linux)
* [https://ubunlog.com/comando-grep/](https://ubunlog.com/comando-grep/)
* [https://www.freecodecamp.org/espanol/news/grep-command-tutorial-how-to-search-for-a-file-in-linux-and-unix-with-recursive-find/](https://www.freecodecamp.org/espanol/news/grep-command-tutorial-how-to-search-for-a-file-in-linux-and-unix-with-recursive-find/)
* [https://keepcoding.io/blog/que-es-el-comando-grep-y-como-usarlo-en-linux/#Busqueda\_de\_palabras\_completas](https://keepcoding.io/blog/que-es-el-comando-grep-y-como-usarlo-en-linux/#Busqueda\_de\_palabras\_completas)
