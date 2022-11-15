---
description: Buscar, buscar y reemplazar, insertar o eliminar
---

# Sed

El comando SED en UNIX es sinónimo de editor de flujo y puede realizar muchas funciones en archivos como buscar, encontrar y reemplazar, insertar o eliminar. Aunque el uso más común del comando SED en UNIX es para sustitución o para buscar y reemplazar. Al usar SED, puede editar archivos incluso sin abrirlo, que es una forma mucho más rápida de encontrar y reemplazar algo en el archivo, que primero abrir ese archivo en VI Editor y luego cambiarlo.

### Sintaxis

El comando SED funciona con **órdenes** y se aplica a los archivos. Tanto el propio comando como las órdenes pueden ampliarse mediante parámetros.

```
sed [parámetro(s)] 'orden(es)' [archivo(s)]
```

Puedes introducir las órdenes de manera directa dentro del comando SED o hacer que sean **leídas de un archivo**. En este último caso, debes introducir la ruta del archivo en lugar de la orden.

### Parámetros

Para el comando SED, los parámetros son especialmente importantes ya que solo a través de ellos queda claro cómo debe interpretarse el comando que viene a continuación. Existen los siguientes parámetros:

| Flags | Descripcion                                                                                            |
| ----- | ------------------------------------------------------------------------------------------------------ |
| -e    | Hace que utilicen uno o varios scripts SED                                                             |
| -f    | Hace que el script se extraiga de un archivo                                                           |
| -n    | Los resultados no se deben emitir                                                                      |
| -i    | Crea un archivo temporal que posteriormente sustituye al archivo de origen. Remplaza el archivo origen |
| -u    | No se utiliza ningún buffer de datos                                                                   |
| -s    | El comando acepta expresiones regulares ampliadas                                                      |
| -r    | El comando acepta expresiones regulares ampliadas                                                      |

Los parámetros -e y -f son los más importantes. Indican si las **ordenes están directamente en el comando** (entonces es un script SED) o si el comando debe dirigirse a un archivo adicional para conseguir esas órdenes. A menudo se puede prescindir de escribir el parámetro -e, ya que es el parámetro por defecto. Sin embargo, en cuanto incluyas más de una orden en el comando al mismo tiempo, es obligatorio poner el parámetro -e.

Muy importante, y probablemente indispensable para tu trabajo, es el parámetro -n. Si no introduces el parámetro -n en el comando, todas y cada una de las líneas del archivo de texto que lea el comando se mostrarán en el terminal, lo cual no es muy útil, especialmente con grandes bases de datos. Si introduces este parámetro en el comando, en el terminal **solo se mostrarán las líneas que se vean afectadas por el comando**.

### Órdenes

Con una orden, se le indica al comando qué debe hacer con el archivo fuente, teniendo en cuenta los parámetros especificados

| Ordenes | Descripcion                                                               |
| ------- | ------------------------------------------------------------------------- |
| a       | append: añade a las líneas seleccionadas una o más líneas más             |
| c       | change: reemplaza las líneas seleccionadas por un nuevo contenido         |
| d       | delete: borra las líneas seleccionadas                                    |
| g       | get: copia el contenido del hold space al pattern space                   |
| G       | GetNewline: añade el contenido del hold space al pattern space            |
| h       | hold: copia el contenido del pattern space al hold space                  |
| H       | HoldNewLine: añade el contenido del pattern space al hold space           |
| i       | insert: inserta una o más líneas antes de las líneas seleccionadas        |
| l       | listing: muestra todos los caracteres no imprimibles                      |
| n       | next: cambia a la siguiente orden de la línea siguiente del comando       |
| p       | print: muestra las líneas seleccionadas                                   |
| q       | quit: finaliza el comando SED de Linux                                    |
| r       | read: lee las líneas seleccionadas de un archivo                          |
| s       | substitute: reemplaza una determinada cadena de caracteres por otra       |
| x       | xchange: intercambia el pattern space y el hold space entre sí            |
| y       | yank: sustituye un determinado carácter por otro                          |
| w       | write: escribe líneas en el archivo de texto                              |
| !       | Negation: aplica el comando a las líneas que no coinciden con la entrada. |

Las órdenes también se pueden complementar con parámetros:

| Parametro | Descripcion                                            |
| --------- | ------------------------------------------------------ |
| =         | Indica el número de línea de las líneas seleccionadas. |
| p         | Muestra las líneas modificadas.                        |
| q         | Aplica la orden a todo el archivo.                     |

A la hora de especificar varias ordenes, para separarlas se utilizan los limitadores. La mas comun es utilizar el "foward slash" ( / ), auque se puede utilizar cualquier delimitador, ya sea un punto, espacios, giones...  El delimitador se tomara en cuneta como el primer delimitador despues de la pirmera orden.

```bash
sed 's/pinaple/olives/' toppings.txt
```

Sin embargo, a la hora de filtar directorios puede haber alguna que otra complicacion, ya que estos son una seri de palabras sguidas  con slash entre medio. Por ello **en algunos casos es recomendable utilizar otros delimitadores**.

```bash
sed 's./etc..' paths.txt    //Elimina la palabra path de todas las liuineas
```

### Buscar y remplazar cadenas de texto con sed

El uso más habitual de Sed es buscar y reemplazar cadenas de texto. A continuación verán una serie de ejemplos que les ayudarán a dominar Sed.

#### Buscar una cadena de texto que contenga una letra o un patrón y reemplazarla por otra

Y queremos reemplazar todas las `o` mínusculas a `O` mayúsculas deberemos usar una sintaxis del siguiente tipo:

```bash
sed 's/texto_a_buscar/texto_a_reemplazar/g' fichero_a_reemplazar
```

Para reemplazar todas las apariciones de un patrón en un texto: El indicador «**/g**» (reemplazo global) especifica el comando sed para reemplazar todas las apariciones de la cadena en la línea.

Esto cambios si no los guardamos en otro fichero mediante una redireccion, no se guardar, po lo que si queremso aplicar los cambios al fichero y sobrescribirlo, hay que utilizar la flag "-i":

```bash
sed -i 's/texto_a_buscar/texto_a_reemplazar/g' fichero_a_reemplazar
```

#### Restringir las líneas en que SED realizará sustituciones de texto

En el casos de que querasmo aplicar nuestros cambios a solo unas cunatsa coincidencias, habra que especificarlos medainte un patron. Este patrosn puede ser por ejemplo alguna palabra que tengan en comun las lineas en las que queremso realizar la substitucion.

```bash
sed '/definir_patrón_a_buscar/s/texto_a_buscar_en_línea_que_aparece_patrón/texto_a_reemplazar_en_línea_que_aparece_patrón/g'
```

Por ejemplo, si queremos sustituir la "o" minuscula pro la "O" mayuscual, solo en las lineas quecontengan "LibreOffice" de nuestro texto, tendremos que realizar el sigueinte comando:

```bash
sed -i '/LibreOffice/s/O/o/g' sedexamplesnew
```

#### Reemplazar un texto por otro texto en las líneas que nosotros queramos con sed

Si queremso aplicar nuestra sustitucion a unas solas lineas en concreto, tambein lo podemso especificar:

```
sed -i '3,4 s/nueva/vieja/g' sedexamples
```

Este comando aplciara lso cambios a en las lineas 3 y 4, pero si hubiermaos pueste `1,4` hubiera aplicado el cambio a a las lineas 1, 2, 3 y 4.

#### Sustituciones múltiples en un solo comando (opción -e)

Si ahora pretendemos encadenar múltiples sustituciones usando únicamente un solo comando tendremos que usar la opción `sed -e`. Para sustituir todas las cadenas de texto de `usr` a `u` y de `bin` a `b` lo haremos del siguiente modo:

```bash
sed -e 's/usr/u/g' -e 's/bin/b/g'
```

#### Encontrar una línea que empiece por una determinada palabra y cambiar el contenido de toda la línea

Si queremos reemplazar todas las líneas que empiezan por `hola` en el texto y remplazar la linea entera por el texto `adios` haremos uso del siguiente comando:

```bash
sed -i 's/^hola .*$/adios/' text.txt
```

> **Nota**: La magia del último comando la realiza la expresión regular `^que .*$`. La parte `^que` hace referencia a todas las líneas que empiezan por la cadena de caracteres `que`. El punto `.` hace referencia a cualquier letra que aparezca las veces que aparezca `*` hasta el final de la línea`$`.

#### Cambiar todas las mayúsculas a minúsculas y viceversa

Si queremos cambiar un texto de mayúsculas a minúsculas también deberemos usar las expresiones regulares. En este caso la expresión regular que necesitamos definir es la siguiente:

`[a-z]`: Expresión regular que hace referencia a todas las letras entre la `a` y la `z`. PAra la trasnformacion se utilizara el siguiente comando:

```bash
sed -i 's/[a-z]/\U&/g' tetx.txt
sed -i 's/[A-Z]/\L&/g' text.txt
```

> **Nota**: `\U&` hace referencia a mayúsculas (Upper case). Por lo tanto el comando aplicado transforma a mayúsculas cualquier letra de la `a` a la `z` que haya en el documento. En cambio `\L&` hace referencia a las letras minusculas (Lower case).





### Bibliografia

* [https://www.hostinger.es/tutoriales/el-comando-sed-de-linux-usos-y-ejemplos/](https://www.hostinger.es/tutoriales/el-comando-sed-de-linux-usos-y-ejemplos/)
* [https://www.ochobitshacenunbyte.com/2019/05/28/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/](https://www.ochobitshacenunbyte.com/2019/05/28/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/)
* [https://geekland.eu/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/](https://geekland.eu/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/)
* [https://www.ionos.es/digitalguide/servidores/configuracion/comando-sed-de-linux/](https://www.ionos.es/digitalguide/servidores/configuracion/comando-sed-de-linux/)
