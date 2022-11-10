# Imagenes

Una de las formas preferidas de dibujar cosas en una ventana es utilizar imágenes. Esto se deve a que la funcion `mlx_pixel_put` es muy lenta, puesto que imprime los pixeles uno a uno. El objetivo es crear una imagen (que no es otra cosa que una colección de píxeles) y editar sus píxeles directamente. Cuando esté hecho, empujaremos esa imagen sobre la ventana y deberíamos tener nuestros gráficos correctamente renderizados sin ningún problema de parpadeo.

### Crear imagenes <a href="#creating-an-image" id="creating-an-image"></a>

El primer paso es, obviamente, decirle al minilibx que queremos crear una nueva imagen. Para ello, tenemos que llamar a `mlx_new_image`:

```c
void *    mlx_new_image ( void *mlx_ptr, int width, int height );
```

Esta funcion crea una nueva imagen en memoria y returna un puntero tipo `void *` para que poder manejar esta imagen posteriormente. La funcion sólo necesita el tamaño de la imagen a crear, utilizando los parámetros de anchura y altura, y el identificador de conexión `mlx_ptr`.

A la hora de crear imagenes lo mas recomendable es crear una estructura para guarda sus propiedades:

```c
typedef struct s_img
{
	void	*mlx_img;
	char	*addr;
	int		bpp; /* bits per pixel */
	int		line_len;
	int		endian;
}	t_img;
```

### Manejar imagenes

No ha estado tan mal, ¿verdad? Ahora tenemos una imagen, pero ¿cómo escribimos exactamente los píxeles en ella? Para ello necesitamos obtener la dirección de memoria en la que vamos a mutar los bytes en consecuencia. También necesitaremos información adicional para ayudarnos con algunos cálculos (`bpp`, `line_len` y variables miembro `endian`).

Obtenemos esta dirección con la sigueinte funcion:

```c
char	*mlx_get_data_addr(void *img_ptr, int *bits_per_pixel, int *size_line, int *endian);
```

Hablando del valor de retorno, la función `mlx_get_data_addr` devuelve la dirección real de la imagen como un simple array de píxeles. Estamos obteniendo un puntero en `char`, lo que normalmente significa que vamos a navegar en el array un byte a la vez (no un píxel a la vez, un píxel normalmente toma más de un byte como hemos visto antes).

Devuelve otros 3 parametros, que tendremos que pasarlos como direccion en el header para que nos los modifique:

* `bits_per_pixel` la cantidad de bits de información necesarios para representar el color de cada píxel (también llamado la profundidad de la imagen)
* `size_line` is the number of bytes used to store one line of the image in memory. This information is needed to move from one line to another in the image.
* `endian` indica si el color de los píxeles de la imagen debe almacenarse en pequeño (`endian == 0`), o grande (`endian == 1`). Para poder profundizar en lo que es el endian aqui tienes este [post](https://www.freecodecamp.org/news/what-is-endianness-big-endian-vs-little-endian/).

### Acceder a un pixel particular de la imagen

Necesitamos recuperar un píxel en unas coordenadas x e y, pero aquí no tenemos un array bidimensional: estamos tratando con un **array unidimensional**. Recuerda también que estamos tratando con bytes, pero un píxel ocupa más de un byte porque estamos usando el estándar de colores reales. Esta cantidad viene dada por el valor `bpp` (en bits) que hemos obtenido de `mlx_get_data_addr`.

> Para saber cuantos bytes tiene un pixel hay que dividir el bpp (bits por pixel) entre 8 (bit en un byte). **bpp / 8**

Sin embargo, no sabemos realmente cuántos bytes tiene un int, por lo que no podemos realizar un casting en el puntero de forma segura.

#### Encontrar la direccion del primer byte de un pixel

Para este ejemplo, supongamos que queremos obtener el píxel en las coordenadas (5, 10). Lo que queremos es el 5º píxel de la 10ª fila.

Las dimensiones de la ventana/imagen son `600x300`.

Para empezar, vamos a encontrar la fila correcta. La anterior llamada `mlx_get_data_addr` nos proporcionó el valor `line_len`, que es básicamente la cantidad de bytes que ocupa una fila de nuestra imagen. Es equivalente a `image_width * (bpp / 8)` (pixels \* bytes).

En nuestro caso, un `int` es cuatro bytes, por lo que es `600 * 4 = 2400`. Por lo tanto, podemos decir que la primera fila comienza en el índice `0`, la segunda en el índice `2400`, la tercera en el índice `4800`, y así sucesivamente. Así, podemos encontrar el índice de fila correcto haciendo `2400 * 10`.

Para encontrar la columna correcta, tendremos que movernos en la fila por el número de píxeles dado. En nuestro caso, queremos movernos 5 píxeles "hacia la derecha". Para ello, tenemos que multiplicar `5` por el número de bytes que ocupa realmente un píxel (aquí `4`). Así, haremos `5 * 4 = 20`.

Para que quede mas claro, a la hora de recorrer las columnas para acceder aa u pixel en especifico tenemos que hacerlo byte a byte a lo largo de nuestro array unidimensional. Por ello si queremos acceder al pixel numero 5 tendremos que recorrer 20 bytes, que son lo que ocupan 5 pixeles (5 \* 4). Teniendo en cuenta que en nuestro caso un pixel tiene 4 bytes.

Si resumimos, podemos encontrar el índice correcto con el siguiente cálculo: `índice = 2400 * 10 + 5 * 4`.

Eso es todo. Sólo tenemos que generalizar la fórmula utilizando los valores que nos ha proporcionado `mlx_get_data_addr`. La siguiente fórmula es la que utilizaremos:

```c
index = line_len * y + x * (bpp / 8)
```

Ahora que tenemos la fórmula, vamos a implementar la función `img_pix_put` que pondrá un píxel en las coordenadas (x, y) de la imagen. Actuará como reemplazo de la función `mlx_pixel_put`.

```c
void	img_pix_put(t_img *img, int x, int y, int color)
{
    char    *pixel;

    pixel = img->addr + (y * img->line_len + x * (img->bpp / 8));
    *(int *)pixel = color;
}
```

Esta funcion funciona igual que mlx\_pixel\_put con la diferencia que en vez de escribir en pantalla nos pinta el pixel en un buffer de pixels que hemos creado. Posteriormente podremos utilizar estas imagenes e imprimirlas en pantalla.

### Imprimir en pantalla una imagen

Ahora estamos realizando todas nuestras operaciones de dibujo en nuestra imagen en lugar de empujar directamente los píxeles en la pantalla. Para esto se utiliza la funcion `mlx_put_image_to_window`, a la que tan solo hay que especificarle en que posicon de la pantalla queremos colocar la imagen.

```c
int
mlx_put_image_to_window ( void *mlx_ptr, void *win_ptr, void *img_ptr, int x, int y );
```

Eliminar un a imagen de la pantalla

EE. el caso de que queremos eliminar una imagen que hayamos impreso anteriormente, tan solo tendremos que utilizar la siguiente funcion, a la que le espeficaremso al imagen que deseamos borrar.

```c
int    mlx_destroy_image ( void *mlx_ptr, void *img_ptr );
```
