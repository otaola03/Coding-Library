---
description: Starting with vim
---

# Vim Basics

### ¿Que es vim?

Vim es una versión mejorada del editor de texto Vi, presente en todos los sistemas UNIX. Su autor, Bram Moolenaar, presentó la primera versión en 1991, fecha desde la que ha experimentado muchas mejoras

### Los modos de Vim

La clave para aprender a manejar Vim es acostumbrarse a sus distintos modos de funcionamiento. Esta es la parte que hace a Vim especial y difícil de entender para las personas que se inician.

#### Modo Comando

Una vez abierto Vim, se inicia en modo comando. El modo comando permite realizar gran cantidad de acciones administrativas sobre el fichero, como buscar en el texto, salir, guardar, borrar líneas, etc. Se podira decir que es una consola intregada en el propio vim.

#### Modo insercion

El modo inserción nos sirve cuando queremos editar el texto del archivo, añadiendo nuevo contenido con el teclado, o borrando carácter a carácter con las correspondientes teclas (_Retroceso_/_Supr_).

Estando en modo comando, pasamos a modo inserción pulsando la tecla **(**_**i)**_. A partir de entonces el editor funcionará tal y como se esperaría en un editor de texto. Es decir, escribes cualquier cosa y se va introduciendo el texto en el archivo.

Para salir del modo inserción y volver al modo comando pulsamos la tecla escape _Esc_.

<figure><img src="https://conpilar.kryptonsolid.com/wp-content/uploads/2021/03/1615419657_155_Guia-de-5-pasos-para-comenzar-con-VIM-Editor-en.png" alt=""><figcaption></figcaption></figure>

### Guardar y cerrar

Todos estos comandos se aplican cuando vim esta en el modo consola.

* _**:w**_** ** –> Permite guardar el fichero.
* _**:q**_ –> Salir de Vim. Si el fichero ha sido modificado pero no se ha guardado, nos advertirá y no podremos salir de Vim usando este comando.
* _**:q!**_ –> Salir de Vim, descartando posibles cambios no guardados que se hayan realizado en el fichero.
* _**:x** _ –> Hace el guardado del archivo y después sale de Vim.
  * **:wq** o pulsar dos veces la tecla z (**zz**) tambien realiza la misma accion.
* **:a** --> para aplicar el comando a todas las pestañas

### Deshacer y rehacer

* _**u**_ –> Deshacer acción.
* _**Ctrl+r**_ –> Rehacer una acción.

### Moverse por el fichero

Además de usar los cursores para movernos por el archivo, podemos movernos de una manera más rápida con algunos comandos:

* _**gg**_ –> Ponerse al inicio del fichero.
* _**Mayús+g**_ –> Ir a la última línea del fichero.
* _**Num+G**_ –> Ir a una línea determinada. Por ejemplo 14G llevaría el cursor a la línea 14.
* **Num+%** -> te lleva al porcentaje del docuemnto que deseas

Para moverse en la misma lieas:

* _**$**_ –> Ir al final de la línea.
* _**0**_ –> Ir al principio de la línea.
* **w** --> Avanza un apalabra
  * **Num+w** --> Avanza Num palabras
  * **Mayus+w** --> te coloca al principio de la palabra del siguienrte espacio
* **b** --> Retrocede palabras
* **e** --> te coloca al final de la palabra
  * **Num+e** --> te coloca al final de la Num palabra a partir de la posicion del cursor
* **g+e** --> te coloca al fiual de la palabra anterior

Otros comandos basicos para desplazarse por el documento son los sigientes, aunque en algunos casos tambien se pueden utilizar las flechas del teclado.

* **H** -> Desplazarse hacia la Izquierda
* **J** -> Desplazarse hacia Abajo
* **K** -> Desplazarse hacia la Arriba
* **L** -> Desplazarse hacia la Derecha

Si tecleas un numero antes de presionar una de estas teclas el cursor se desplazar n posiciones hacia la direcion que deseas. Por ejemplo si pongo 4j el cursor se movera 4 lineas hacia abajo, a partir de su posicion actual.

### Copiar, Cortar y Pegart

* _**dd**_ –> El comando permite cortar la línea actual, donde está el cursor, para posteriormente poderla pegar en otro lado. De no ser asi, tambien se puede utilizar para borrar lineas
* _**d+num+direccion**_–> Este comando permite cortar un número de líneas o letras en la direccion que quieras. Por ejemplo, d3+(Flecha hacia abajo) cortara la lina actual y las tres de abajo. Si la lineas so se colocan de nuevo puede utilizarse tamben para borrar
* **Mayus+d** -> Borra la linea a partir de donde esta el cursor
* **yy** -> El comando permite copiar la linea actual, donde esta el cursor.
  * **Num+Mayus+y** -> Esto te copiara la linea acual y num-1 lineas mas hacia abajo a partir e la posicion del cursor.
* **p** -> Pega la linea copiada debajo de la posicion del cursor
* **Mayus+p** -> Pega la linea copiada encima de la posicion del cursor

### Eliminar y Añadir texto

* **Mayus+c** --> Elimina la linea a partir de la poscion del curosr y se pone en modo insertar
* **Mayus+a** --> Se coloca al final de la linea y se pone en modo insertar
* **o** --> Se coloca en una nueva linea creada debajo del cursor y se pone en modo insertar&#x20;
* **d + w** --> elimina solo la palabra en la que esta el cursor, pero a partir de la poscion del cursor
  * **d+Num+w** --> elimina Num palabras

### Tabs y repeticiones

* **Num+>+Direccion** --> Para tabular las lineas que quieras
* **Num+<+Direccion** --> Para destabular las lineas que quieras

### Ventanas

* **:split+Name** --> Abre en division horizontal el fichero que eligas
* **:vsplit+Name** --> Abre en division vertical el fichero que eligas

