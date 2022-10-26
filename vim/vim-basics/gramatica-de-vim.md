# Gramatica de Vim

### Sustantivos (Movimientos)

Hablemos de los movimientos como sustantivos. Los movimientos son utilizados para movernos por el texto en Vim. También hay sustantivos de Vim. En la lista a continuación veremos algunos ejemplos de movimientos:

```
h    Izquierda
j    Abajo
k    Arriba
l    Derecha
w    Mover el cursor hacia adelante al principio de la palabra siguiente
}    Saltar al siguiente párrafo
$    Ir al final de la línea
```

Imagina que estás en algún lugar dentro de un paréntesis, como por ejemplo `(hola Vim)` y necesitas **eliminar la frase entera dentro del paréntesis**. Vim tiene una manera de capturar esta estructura con los objetos de texto. Hay dos tipos de objetos de texto:

```
i + objeto    Dentro del objeto de texto
a + objeto    Fuera del objeto de texto
```

Echemos un vistazo a un ejemplo diferente. Supongamos que tenemos esta función de Javascript y tu cursor está en la letra "H" de la palabra "Hello":

* Para eliminar por completo el texto "Hello Vim": `di(`.
* Para eliminar el contenido de la función (rodeado por `{}`): `di{`
* Para eliminar la palabra "Hello": `diw`

### Verbos (Operadores)

De acuerdo a lo que podemos leer en la ayuda de Vim mediante el comando `:h operator`, Vim tiene 16 operadores. Sin embargo, en mi experiencia, con aprender estos 3 es suficiente para el 80% de las necesidades a la hora de editar mis textos:

```
y    Copiar un texto (*yank* en Vim sería la acción de copiar, de ahí la letra `y`)
d    Eliminar un texto y guardarlo en el registro (*delete* en Vim sería la acción de eliminar, de ahí la letra `d`)
c    Eliminar un texto, guardarlo en el registro y comenzar en el modo de insertar
```

Por cierto, después de que copies un texto, lo puedes **pegar** con `p` (después de la posición del cursor) o con `P` (antes de la posición del cursor).

