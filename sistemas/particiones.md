# Particiones

### Que es una particion?

Una particion es dividir el disco duro en lo que son unidades logicas o volumnes. A estas hay que darles un formato denominado sistema de archvios, que tine que ser acorde al sistema operativo uqe se le planea instalar a esa particion o al tipo de archvios que se le van a meter

Una partición es una parte lógica de un volumen de almacenamiento físico. Puede estar formateado o no. Asimismo, puede o no tener un sistema de archivos. En cambio, es sólo una parte del disco con un tamaño asignado que se establece en la creación. Para cambiar el tamaño de una partición, tiene que formatear el disco y reescribir su tabla de particiones, posiblemente perdiendo todos los datos que tiene en dicha partición.

Cada disoco duro se considera unidad fisica, pero los sitemas operativos no trabajn con unidades fisicas, si no con unidades logicas.

### Tipos de particiones

Solo existen tres tipos de particiones, que son las siguiente:

* **Particion primaria** --> La particion primaria es aquella en la que podemos instalar un sistema operativo.
* **Particion extendida** --> Una vez alcanzas el limite de particiones primarias, se utiliza para instlar mas particiones en el sistema
* **Particiones logicas** --> Son particiones dentor de otras particiones. Estas estan dentro de lass particiones extendidas

> Un disco duro solo puede tener 4 particiones primarias

### Volumenes

#### Que es un volumen

Un volumen es, básicamente, **un contenedor de almacenamiento en un sistema de archivos** particular que su computadora puede usar y reconocer. Los principales tipos de volúmenes de almacenamiento son los discos duros, las unidades de estado sólido, los DVD y los CD. Aparte de los volúmenes físicos, también hay volúmenes lógicos.

Una de las principales características de un volumen de almacenamiento es que puede contener varias particiones. Un volumen tiene un sistema de archivos y un nombre junto con su tamaño. Por ejemplo, todos los iconos de disco que ves en el escritorio de un Mac son volúmenes. Además, al conectar la unidad flash USB, ésta se tratará como un volumen.

En términos de flexibilidad, los volúmenes tienen el borde sobre las particiones. Puede contratarlos y ampliarlos para que se ajusten a sus necesidades. Al igual que con las particiones, puede crear varios volúmenes en un solo disco. Si lo hace, su sistema operativo realizará un seguimiento de los volúmenes que pertenecen a cada unidad.

#### Tipos de volumenes

* **Volumen simple** --> abarcar una o varias regiones del mismo disco duro
* **Volumen distribuido** --> cuando se ocupa espacio de mas de un disco duro (fisico)
* **Volumen seccionado** --> Es parecido al volumen distribuido, pero a diferencia de este,  el volumne seccionado, distribuye la informacion de manera equirtativa. Es decir si hago una particion de 5 gb en dos disco a cada disco lo asignara 2.5 gb
* **Volumen reflejado** --> Es como una copia de segurid. Es decir que guardar la misma informacion que en otro disco.
* **Volumen RAID5** --> Similar el volumen distribuido, guarda informacion em mas de un disco duro, pero a diferencia de este en el RAID5 sis se pierde la informaciond e algunos de lso discos, esta se podra recuperar

### Diferencia entre Particiones y Volumenes

En resumen, una partición siempre se crea en un único disco físico, mientras que un volumen puede abarcar varios discos y tener muchas particiones. Mientras que las particiones sólo tienen números, los volúmenes tienen nombres. Por último, las particiones son más adecuadas para dispositivos individuales, mientras que los volúmenes (especialmente los volúmenes lógicos) son más flexibles y adecuados para redes.

A menudo, un volumen montado se llama partición, aunque no son idénticos. Una «partición» se refiere a una o más áreas físicas de almacenamiento en una sola unidad. Una vez que la partición se ha montado, se le puede llamar un volumen. Puede pensar en volúmenes como el etiquetado, «escaparates» accesibles al «cuarto trastero» funcional de las particiones y los dispositivos

### Tipos de discos

Existen dos tipos de discos:

* **Disco basico** --> Un disco basico es cuando se utilizan particiones primarias, logicas y extendidas, es decir, particiones en un solo disco duro.
* **Disco dinamico** --> Un disco dinamico es cuando se hace interactuar a dos o mas diuscos duros entre si, ya sea con una particion reflejada, RAID5...

### Puntos de montaje

Un **punto de montaje** es el directorio o el archivo en el que se hacen accesibles un nuevo sistema de archivos, un directorio o un archivo. Para montar un sistema de archivos o un directorio, el **punto de montaje** debe ser un directorio; y para montar un archivo, el **punto de montaje** debe ser un archivo. (/boot, /home, /usr, /var ...)

### Bibliografia

* [https://tecnonautas.net/conoce-la-diferencia-entre-un-volumen-de-contenedor-y-una-particion/](https://tecnonautas.net/conoce-la-diferencia-entre-un-volumen-de-contenedor-y-una-particion/) --> Volumenes y particiones
* [https://help.gnome.org/users/gnome-help/stable/disk-partitions.html.es](https://help.gnome.org/users/gnome-help/stable/disk-partitions.html.es) --> Volumenes y particiones
* [https://mundo-geek.com/volumen-vs-particion-cual-es-la-diferencia/](https://mundo-geek.com/volumen-vs-particion-cual-es-la-diferencia/) --> Volumenes y particiones
