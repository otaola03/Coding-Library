---
description: .png y .xmp
---

# Leer imagenes

Las imágenes son una herramienta muy importante en MiniLibX para aprovechar todo su potencial. Estas funciones le permitirán leer archivos directamente en un objeto de imagen. Esto es muy útil para texturas o sprites, por supuesto.

### Leer imagenes

Para leer de un archivo a un objeto de imagen, se necesita el formato XMP o PNG. Para leer podemos llamar a las funciones `mlx_xpm_file_to_image` y `mlx_png_file_to_image` en consecuencia. Ambas funciones aceptan exactamente los mismos parámetros y su uso es idéntico.

```c
void	*mlx_xpm_file_to_image(void *mlx_ptr, char *filename, int *width, int *height);
void	*mlx_png_file_to_image(void *mlx_ptr, char *filename, int *width, int *height);
```

{% hint style="warning" %}
`mlx_png_file_to_image tiene fugas de memoria`
{% endhint %}

Ahora, vamos a leer de una imagen:

```c
#include <mlx.h>

int	main(void)
{
	void	*mlx;
	void	*img;
	char	*relative_path = "./test.xpm";
	int		img_width;
	int		img_height;

	mlx = mlx_init();
	img = mlx_xpm_file_to_image(mlx, relative_path, &img_width, &img_height);
}
```

Si la variable `img` es igual a `NULL`, significa que la lectura de la imagen ha fallado. También establecerá el `img_width` y el `img_height` en consecuencia, lo cual es ideal cuando se leen sprites.

Esto funciona igual que con las imagenes que creamos con `mlx_new_image`, es decir que posteriormente una vez leida la imagen podemos imprimirla en pantalla. Esto es muy util para imprimir texturas extraidas de internet.
