# Loops (bucles)

Ahora que por fin entiendes lo básico de la librería MiniLibX, empezaremos dibujando una pequeña animación en la ventana. Para ello utilizaremos dos nuevas funciones, `mlx_loop` y `mlx_loop_hook`.

Los bucles son una característica de MiniLibX en la que continuará llamando a su evento registrado en mlx\_loop\_hook para renderizar nuevos fotogramas, los cuales, obviamente, deberás pasar a la ventana tú mismo.

Bien, el `mlx_loop_hook` es un hook que se dispara cuando no hay ningún evento procesado. Es especialmente útil para dibujar cosas continuamente en la pantalla Eso está directamente relacionado con la forma en que se implementa el `mlx_loop`. Puedes mirar la [implementación](https://aurelienbrabant.fr/blog/managing-events-with-the-minilibx) si tienes esa curiosidad.

### Bucles <a href="#mlx_loop_hook" id="mlx_loop_hook"></a>

Para iniciar un bucle, llamamos a la función `mlx_loop` con la instancia mlx como único parámetro, echa un vistazo:

```c
#include <mlx.h>

int	main(void)
{
	void	*mlx;

	mlx = mlx_init();
	mlx_loop(mlx);
}
```

Esto no hará nada, por supuesto, ya que no tenemos registrado ningún hook de bucle, por lo que no podremos escribir nada en nuestro marco.

Para ello, tendrás que crear una nueva ventana y utilizar las mutaciones que describimos en el capítulo de Introducción. Una versión de ejemplo podría tener el siguiente aspecto:

```c
#include <mlx.h>

int	render_next_frame(void *YourStruct);

int	main(void)
{
	void	*mlx;

	mlx = mlx_init();
	mlx_loop_hook(mlx, render_next_frame, YourStruct);
	mlx_loop(mlx);
}
```

Ahora para cada fotograma que requiera, llamará a la función `render_next_frame` con el parámetro `YourStruct`. Esto persistirá a través de múltiples llamadas si se trata de un puntero. Es decir mientras no ocurra ningun evento la funcion `render_next_frame` ira creando y cerrando nuevas ventanas mostrando asi efectos visuales.
