# MiniLibX

La minilibx es una pequeña librería en C para el renderizado de gráficos, utilizada principalmente por estudiantes de 42. Como su nombre indica, esta biblioteca está construida sobre la API del sistema X Window, para proporcionar una interfaz de programación mucho más sencilla y adecuada para los principiantes. De hecho, no se necesita ningún conocimiento de X para renderizar gráficos correctamente usando este tipo de librería.

### Instalacion

Debido a que MiniLibX requiere Cocoa de MacOSX (AppKit) y OpenGL (ya no utiliza X11) necesitamos enlazarlos de forma adecuada. Esto puede causar un proceso de compilación complicado. Un proceso de compilación básico tiene el siguiente aspecto.

Para los archivos de objetos, podrías añadir la siguiente regla a tu makefile, asumiendo que tienes el código fuente de mlx en un directorio llamado mlx en la raíz de tu proyecto:

```makefile
%.o: %.c
	$(CC) -Wall -Wextra -Werror -Imlx -c $< -o $@
```

Para enlazar con la API interna de macOS necesaria:

```makefile
$(NAME): $(OBJ)
	$(CC) $(OBJ) -Lmlx -lmlx -framework OpenGL -framework AppKit -o $(NAME)
```

En caso de error prueva a compilar con `clang main.c -lX11 -lXext -lmlx`.

Una vez instalado correctamente el minilibx y enlazado con el MAkefile, tendras que añadir a tu main la siguiente libreria proporcionada por minilibx:

```c
#include <mlx.h>
```

### Inicializacion

Cuando se utiliza el minilibx, es necesario inicializar un montón de cosas antes de poder empezar a renderizar las cosas. La biblioteca incluye una única función que hace precisamente este trabajo: `mlx_init`. Bajo el capó, esta función crea una estructura que contiene todas las cosas que el minilibx necesitará para hacer sus cosas.

```c
void	*mlx_init();
```

Esta es una función muy simple, pero hay algo interesante aquí. Lo que la función mlx\_init realmente devuelve es un puntero void que tendremos que guarda para su posterior utilizacion.

En realidad, el minilibx devuelve la dirección de un elemento `t_xvar`, que es la gran estructura que contiene todas las cosas útiles de las que hablaba antes. Los desarrolladores de minilibx decidieron ocultarnos el tipo, para que no podamos acceder fácilmente a los miembros de la estructura. Eso es porque se supone que no debemos hacerlo. La cabecera "pública" de minilibx `mlx.h` no tiene ninguna declaración de tipo adicional. Todo eso se hace en el interior de la biblioteca. Eso se llama encapsulación (aunque esto es más una palabra de programación de objetos orientada).

### Destruir y liberar los recursos

Una vez que hayamos terminado con nuestro programa, querremos liberar todos los recursos asignados para él. En este punto, puede simplemente llamar a la función `free` y pasarle su `mlx_ptr`. Sin embargo, si ejecutamos un programa detector de errores de memoria como `valgrind`, veremos que hay algunas fugas. Eso es porque la pantalla no ha sido cerrada. ¿Pero qué es la pantalla?

Una de las cosas más importantes que `mlx_init` inicializa es la pantalla. En programación X, la pantalla se refiere básicamente al identificador de conexión utilizado para comunicarse con el servidor X. No vamos a profundizar en los detalles aquí, pero ten en cuenta que esta es otra gran estructura gestionada bajo el capó para ti. Lo que es importante saber, sin embargo, es que esta pantalla necesita ser cerrada en algún momento. El minilibx ahora tiene una función muy básica para permitirte hacer eso sin usar la API de Xlib.

Esa es la función **`mlx_destroy_display`**. Necesitamos llamarla antes de la función `free` porque necesitamos acceder a la `mlx_ptr` para recuperar la variable display. Ahora, ya no deberíamos tener ninguna fuga.

### Ejemplo simple

```c
#include <stdlib.h>
#include <mlx.h>

int main(void)
{
	void	*mlx_ptr;

	mlx_ptr = mlx_init();
	mlx_destroy_display(mlx_ptr);
	free(mlx_ptr);
}
```

### Bibliografia

* [Documentacion oficial](https://qst0.github.io/ft\_libgfx/man\_mlx.html)
* [https://harm-smits.github.io/42docs/libs/minilibx](https://harm-smits.github.io/42docs/libs/minilibx)
* [https://aurelienbrabant.fr/blog/getting-started-with-the-minilibx](https://aurelienbrabant.fr/blog/getting-started-with-the-minilibx)
