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

* `bits_per_pixel` se llenará con el número de bits necesarios para representar el color de un píxel (también llamado la profundidad de la imagen)
* `size_line` is the number of bytes used to store one line of the image in memory. This information is needed to move from one line to another in the image.
* `endian` indica si el color de los píxeles de la imagen debe almacenarse en pequeño (`endian == 0`), o grande (`endian == 1`).



