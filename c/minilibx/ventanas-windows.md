# Ventanas (windows)

Cuando ejecutas el código,  puedes  notar que no aparece nada y que no se está renderizando nada. Bueno, esto obviamente tiene algo que ver con el hecho de que no estás creando una ventana todavía, así que vamos a intentar inicializar una pequeña ventana que permanecerá abierta para siempre. Puedes cerrarla pulsando CTRL + C en tu terminal.

### Crear y destruir una ventana

Ahora es el momento de crear nuestra primera ventana. Para ello, vamos a utilizar la función `mlx_new_window`. Aquí está el prototipo:

```c
void	*mlx_new_window(void *mlx_ptr,int size_x,int size_y,char *title);
```

La función `mlx_new_window()` crea una nueva ventana en la pantalla, utilizando los parámetros `size_x` y `size_y` para determinar su tamaño, y `title` como el texto que debe mostrarse en la barra de título de la ventana.

El parámetro `mlx_ptr` es el identificador de conexión devuelto por `mlx_init`(). `mlx_new_window()` devuelve un identificador de ventana `void *` que puede ser utilizado por otras llamadas de MiniLibX, por ello tendremos que guardar este puntero en una variable tipo `void *`.

Es recomendable definir el ancho y el alto de la ventana como constantes simbólicas (`WINDOW_WIDTH` y `WINDOW_HEIGHT`) para hacerlo más claro. Luego llamamos a `mlx_new_window`, pasándole todos los parámetros necesarios, para obtener nuestra nueva ventana.

La llamada a `mlx_destroy_window` se encarga de liberar todos los recursos que han sido asignados a la ventana cuando ya no se necesita.

```c
int    mlx_destroy_window ( void *mlx_ptr, void *win_ptr );
```

Esta funcion recibe como primer parametro el puntero que hemos conseguido al iniciar la ventana y como segundo el puntero recibido al crear la ventana.

### Limitaciones de las ventanas

Mirando la implementación de minilibx, parece que hay algunas limitaciones relacionadas con la creación de ventanas:

Por ejemplo, parece que actualmente es imposible cambiar el tamaño de una ventana: por lo tanto, sólo se nos permite tratar con las dimensiones originales de la ventana. Esto no es un problema, ya que no necesitamos esta característica para la mayoría de los 42 proyectos, pero si te preguntabas si es posible o no, aparentemente no lo es.

### Posibles errores

Las funciones de minilibx que utilizamos para inicializar y crear ventanas son propensas a errores, y no comprobamos esos posibles errores. Si por casualidad se produce un error, es probable que nuestro programa se bloquee. Afortunadamente, la solución aquí es bastante fácil. Sabemos por las páginas man de minilibx que si se produce un error en `mlx_init` o `mlx_new_window`, el puntero devuelto será `NULL`. Por lo tanto, lo único que hay que hacer aquí es comprobar el valor de retorno y adaptar el flujo de control del programa en consecuencia.

### Ejemplo

```c
#include <stdlib.h>
#include <mlx.h>

# define WINDOW_WIDTH 600
# define WINDOW_HEIGHT 300
#define MLX_ERROR 1

int main(void)
{
	void	*mlx_ptr;
	void	*win_ptr;

	mlx_ptr = mlx_init();
	if (mlx_ptr == NULL)
		return (MLX_ERROR);
	win_ptr = mlx_new_window(mlx_ptr, WINDOW_WIDTH, WINDOW_HEIGHT, "My first window!");
	if (win_ptr == NULL)
	{
		free(win_ptr);
		return (MLX_ERROR);
	}
	while (1)
		;
	mlx_destroy_window(mlx_ptr, win_ptr);
	mlx_destroy_display(mlx_ptr);
	free(mlx_ptr);
}
```

En vez de  utilizar `while (1)`, se podria utilizar **`mlx_loop()`**. Esta funcion sirve para mantener abierta la ventan y que no se cierre instantaneamente una vez se haya abierto. Si no utilizaramos esta funcion, "no seria necesaria" la funcion `mlx_destroy_display()`, puesto que la cerraria nada mas abrirse.

### Cerrar la ventana

Como habrás notado, actualmente es imposible cerrar la ventana. Y eso es simplemente porque no hemos configurado ningún evento responsable de cerrar la ventana. Si estás atascado, puedes matar el proceso usando las teclas `Ctrl-C`.

Esto es realmente malo, porque al forzar la muerte del proceso así no se ejecutará el código que está después del bucle infinito. Por lo tanto, dará lugar a fugas de memoria.

Entonces tenemos que encontrar una manera de ejecutar nuestro programa continuamente hasta que ocurra un evento particular.

El minilibx ofrece una solución a ese problema, utilizando las funciones `mlx_loop` y `mlx_*hook`.&#x20;
