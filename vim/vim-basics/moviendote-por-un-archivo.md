# Moviendote por un archivo

### Navegación por palabras

```
w     Mueve el cursor hacia adelante al comienzo de la siguiente palabra
W     Mueve el cursor hacia adelante al comienzo de la siguiente PALABRA
e     Mueve el cursor hacia adelante una palabra hasta el final de la siguiente palabra
E     Mueve el cursor hacia adelante una palabra hasta el final de la siguiente PALABRA
b     Mueve el cursor hacia atrás al principio de la palabra previa
B     Mueve el cursor hacia atrás al principio de la PALABRA previa
ge    Mueve el cursor hacia atrás al final de la palabra previa
gE    Mueve el cursor hacia atrás al final de la PALABRA previa
```

Entonces, ¿cuáles son las similitudes y diferencias entre una palabra y una PALABRA? Tanto una palabra como una PALABRA están separadas por espacios en blanco. Una palabra es una secuencia de caracteres que contienen _únicamente_ este grupo de caracteres `a-zA-Z0-9_`. Una PALABRA es una secuencia que incluyen todos los caracteres excepto el espacio en blanco (cuando me refiero a espacio en blanco, esto incluye tanto un espacio, una separación por tabulador o un fin de línea) Para aprender más, echa un vistazo a la ayuda en Vim sobre este tema con estos comandos: `:h word` o `:h WORD`.

### Navegación de línea actual

```
0     Ir al primer caracter de la línea actual
^     Ir al primer caracter que no es un espacio en blanco en la línea actual
g_    Ir al último caracter que no es un espacio en blanco en la línea actual
$     Ir al último caracter de la línea actual
n|    Ir a la columna n en la línea actual
```

También puedes realizar una búsqueda en la línea actual con `f` y `t`. Ambas opciones buscan hacia adelante en la línea actual, la diferencia entre `f` y `t` es que `f` situa el cursor en el mismo lugar de la primera letra de la primera coincidencia encontrada y `t` te lleva _hasta justo_ antes de la primera letra de la primera coincidencia encontrada. Así que si quieres realizar una búsqueda y que el cursor se sitúe sobre la letra "h", utiliza `fh`.

```
f    Busca hacia adelante una coincidencia en la línea actual
F    Busca hacia atrás una coincidencia en la línea acual
t    Busca hacia adelante una coincidencia en la línea actual, posicionando el cursor antes de la coincidencia
T    Busca hacia atrás una coincidencia en la línea actual, posicionando el cursor antes de la coincidencia
;    Repite la última búsqueda en la línea actual en la misma dirección
,    Repite la última búsqueda en la línea actual en dirección contraria
```

### Navegación por número de línea

```
gg    Va a la primera línea
G     Va a la última línea
nG    Va a la línea n
n%    Va al n% del archivo
```

### Navegación por búsqueda

```
/    Busca hacia adelante una coincidencia
?    Busca hacia atrás una coincidencia
n    Repite la última búsqueda (en la misma dirección que la búsqueda previa)
N    Repite la última búsqueda (en la dirección opuesta que la búsqueda previa)
```

Puedes habilitar el resaltado del texto buscado mediante el ajuste `:set hlsearch`. Para inhabilitar ese resaltado, puedes ejecutar `:nohlsearch.` Como utilizo esa funcionalidad de quitar el resaltado de manera frecuente, he creado un mapeado de esa funcionalidad. Para ello he añadido la siguiente línea en el archivo .vimrc:

```
nnoremap <esc><esc> :noh<return><esc>
```

### Marcando la posición

uedes utilizar marcas para guardar la posición actual del cursor y poder volver a esa posición más tarde. Es como un marcador para la edición de texto. Puedes establecer un marcador con `mx`, donde `x` puede ser cualquier letra del alfabeto `a-zA-Z`. Existen dos maneras de volver a la marca establecida: de manera exacta (línea y columna) mediante \`\`\`x\`\` y a la línea con `'x`.

```
// Some codema    Marca una posición, estableciendo la marca "a" en la posición actual del cursor
`a    Salta a la línea y columna donde se encuentra "a"
'a    Salta a la línea donde se encuentra "a"
```

Existe una diferencia entre establecer marcas con letras minúsculas (a-z) y mayúsculas (A-Z). Las marcas con letras minúsculas, son **marcas locales** y las marcas con letras mayúsculas son **marcas globales** (a veces conocidas como marcas de archivo).

Para ver todas las marcas establecidas puedes hacerlo mediante `:marks`. Puedes comprobar que en la lista de marcas hay más marcas que las de `a-zA-Z`. Algunas de ellas son:

```
''    Salta hacia atrás a la última línea donde se encontraba el cursor en el *buffer* actual antes de saltar
``    Salta hacia atrás a la última posición en el *buffer* actual a la última posición en el *buffer* actual antes de saltar
`[    Salta al comienzo del texto previamente cambiado / pegado
`]    Salta al final del texto previamente cambiado / pegado
`<    Salta al comienzo de la última selección visual
`>    Salta al final de la última selección visual
`0    Salta hacia atrás al último archivo editado cuando salió de Vim
```
