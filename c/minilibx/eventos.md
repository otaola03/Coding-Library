# Eventos

Los eventos son la base para escribir aplicaciones interactivas en MiniLibX. Todos los hooks en MiniLibX no son más que una función que se llama cada vez que se dispara un evento. Dominar todos estos eventos no será necesario, sin embargo, repasaremos rápidamente cada uno de los eventos de X11.

Tanto X-Window como MacOSX son sistemas gráficos bidireccionales. Por un lado, el programa envía órdenes a la pantalla para mostrar píxeles, imágenes, etc. Por otro lado, puede obtener información del teclado y del ratón asociada a la pantalla. Para ello, el programa recibe "eventos" del teclado o del ratón.

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption></figcaption></figure>

### **Interfaz X11**

X11 es la biblioteca que se utiliza junto a MiniLibX. Por lo tanto, no es un secreto que esta cabecera es muy útil para encontrar todos los eventos correspondientes de MiniLibX. Para poder utilizar estos eventos y mascaras es necesaria la siguiente libreria:&#x20;

```c
#include <X11/X.h>
```

{% hint style="info" %}
En MacOS - Cocoa (AppKit) y OpenGL - versión, minilibx tiene soporte parcial de eventos X11 y no soporta la máscara X11 (el argumento x\_mask de mlx\_hook es inútil, manténgalo en 0).
{% endhint %}

#### Eventos del X1

Hay una serie de eventos que se pueden describir.

<table><thead><tr><th>Key</th><th width="162">Event</th><th width="74"></th><th>Key</th><th width="191">Event</th><th width="72"></th><th>Key</th><th>Event</th></tr></thead><tbody><tr><td><code>02</code></td><td>KeyPress</td><td> </td><td><code>14</code></td><td>NoExpose</td><td> </td><td><code>26</code></td><td>CirculateNotify</td></tr><tr><td><code>03</code></td><td>KeyRelease</td><td> </td><td><code>15</code></td><td>VisibilityNotify</td><td> </td><td><code>27</code></td><td>CirculateRequest</td></tr><tr><td><code>04</code></td><td>ButtonPress</td><td> </td><td><code>16</code></td><td>CreateNotify</td><td> </td><td><code>28</code></td><td>PropertyNotify</td></tr><tr><td><code>05</code></td><td>ButtonRelease</td><td> </td><td><code>17</code></td><td>DestroyNotify</td><td> </td><td><code>29</code></td><td>SelectionClear</td></tr><tr><td><code>06</code></td><td>MotionNotify</td><td> </td><td><code>18</code></td><td>UnmapNotify</td><td> </td><td><code>30</code></td><td>SelectionRequest</td></tr><tr><td><code>07</code></td><td>EnterNotify</td><td> </td><td><code>19</code></td><td>MapNotify</td><td> </td><td><code>31</code></td><td>SelectionNotify</td></tr><tr><td><code>08</code></td><td>LeaveNotify</td><td> </td><td><code>20</code></td><td>MapRequest</td><td> </td><td><code>32</code></td><td>ColormapNotify</td></tr><tr><td><code>09</code></td><td>FocusIn</td><td> </td><td><code>21</code></td><td>ReparentNotify</td><td> </td><td><code>33</code></td><td>ClientMessage</td></tr><tr><td><code>10</code></td><td>FocusOut</td><td> </td><td><code>22</code></td><td>ConfigureNotify</td><td> </td><td><code>34</code></td><td>MappingNotify</td></tr><tr><td><code>11</code></td><td>KeymapNotify</td><td> </td><td><code>23</code></td><td>ConfigureRequest</td><td> </td><td><code>35</code></td><td>GenericEvent</td></tr><tr><td><code>12</code></td><td>Expose</td><td> </td><td><code>24</code></td><td>GravityNotify</td><td> </td><td><code>36</code></td><td>LASTEvent</td></tr><tr><td><code>13</code></td><td>GraphicsExpose</td><td> </td><td><code>25</code></td><td>ResizeRequest</td><td> </td><td> </td><td> </td></tr></tbody></table>

#### Mascaras X11

Cada evento X11, también tiene una máscara correspondiente. De este modo, puedes registrar sólo una tecla cuando se dispara, o todas las teclas si dejas tu máscara por defecto. Las máscaras de teclas, por lo tanto, le permiten poner en una lista blanca o negra los eventos de sus suscripciones a eventos. Se permiten las siguientes máscaras:



<table><thead><tr><th width="137">Mask</th><th width="213">Description</th><th width="40">    </th><th width="123">Mask</th><th width="247">Description</th></tr></thead><tbody><tr><td><code>0L</code></td><td>NoEventMask</td><td> </td><td><code>(1L&#x3C;&#x3C;12)</code></td><td>Button5MotionMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;0)</code></td><td>KeyPressMask</td><td> </td><td><code>(1L&#x3C;&#x3C;13)</code></td><td>ButtonMotionMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;1)</code></td><td>KeyReleaseMask</td><td> </td><td><code>(1L&#x3C;&#x3C;14)</code></td><td>KeymapStateMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;2)</code></td><td>ButtonPressMask</td><td> </td><td><code>(1L&#x3C;&#x3C;15)</code></td><td>ExposureMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;3)</code></td><td>ButtonReleaseMask</td><td> </td><td><code>(1L&#x3C;&#x3C;16)</code></td><td>VisibilityChangeMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;4)</code></td><td>EnterWindowMask</td><td> </td><td><code>(1L&#x3C;&#x3C;17)</code></td><td>StructureNotifyMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;5)</code></td><td>LeaveWindowMask</td><td> </td><td><code>(1L&#x3C;&#x3C;18)</code></td><td>ResizeRedirectMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;6)</code></td><td>PointerMotionMask</td><td> </td><td><code>(1L&#x3C;&#x3C;19)</code></td><td>SubstructureNotifyMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;7)</code></td><td>PointerMotionHintMask</td><td> </td><td><code>(1L&#x3C;&#x3C;20)</code></td><td>SubstructureRedirectMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;8)</code></td><td>Button1MotionMask</td><td> </td><td><code>(1L&#x3C;&#x3C;21)</code></td><td>FocusChangeMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;9)</code></td><td>Button2MotionMask</td><td> </td><td><code>(1L&#x3C;&#x3C;22)</code></td><td>PropertyChangeMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;10)</code></td><td>Button3MotionMask</td><td> </td><td><code>(1L&#x3C;&#x3C;23)</code></td><td>ColormapChangeMask</td></tr><tr><td><code>(1L&#x3C;&#x3C;11)</code></td><td>Button4MotionMask</td><td> </td><td><code>(1L&#x3C;&#x3C;24)</code></td><td>OwnerGrabButtonMask</td></tr></tbody></table>

### AppleScript key codes

Todo accion realizada a traves del teclado o el mouse tiene  un numero de referencia, de esta manera mediante los eventos que nos facilita MiniLibX podremos saber en todo momento que informacion no esta enviando el usuario de nuestro programa. Para asi si lo deseasmos estabelcerle a ciertas acciones una funcion o accion corespondiente.

La key codes del teclado de mac son las [siguientes](https://eastmanreference.com/complete-list-of-applescript-key-codes):

<figure><img src="../../.gitbook/assets/Screen Shot 2022-11-11 at 8.12.36 PM.png" alt=""><figcaption></figcaption></figure>

### Tipos de eventos

Para que podamos registrar eventos, el minilibx nos proporciona un conjunto de funciones llamadas hooks que podremos utilizar para registrar eventos antes de que se llame a `mlx_loop`. Esta funcion deja el programa en un bucle infinito, para asi poder recibir los datos de entrada a traves del teclado y asi ejecutar las funciones correspodientes.

```c
int    mlx_loop ( void *mlx_ptr );
```

#### mlx\_hook <a href="#mlx_hook" id="mlx_hook"></a>

El estar a la escucha de eventos es una de las herramientas más potentes que proporciona MiniLibX. Permite registrarse a cualquiera de los eventos mencionados con la llamada de una simple función de registro de eventos.

Para ello, llamamos a la función mlx\_hook.

```c
void mlx_hook(mlx_win_list_t *win_ptr, int x_event, int x_mask, int (*f)(), void *param)
```

> Alguna versión de mlbx no implementa x\_mask y sea cual sea el valor no habrá máscara.

#### Prototipo de las funciones de evento

Las funciones de evento tienen un prototipo diferente dependiendo del evento de enganche.



<table><thead><tr><th>Hooking event</th><th width="78">code</th><th width="432">Prototype</th></tr></thead><tbody><tr><td>ON_KEYDOWN</td><td>2</td><td><code>int (*f)(int keycode, void *param)</code></td></tr><tr><td>ON_KEYUP*</td><td>3</td><td><code>int (*f)(int keycode, void *param)</code></td></tr><tr><td>ON_MOUSEDOWN*</td><td>4</td><td><code>int (*f)(int button, int x, int y, void *param)</code></td></tr><tr><td>ON_MOUSEUP</td><td>5</td><td><code>int (*f)(int button, int x, int y, void *param)</code></td></tr><tr><td>ON_MOUSEMOVE</td><td>6</td><td><code>int (*f)(int x, int y, void *param)</code></td></tr><tr><td>ON_EXPOSE*</td><td>12</td><td><code>int (*f)(void *param)</code></td></tr><tr><td>ON_DESTROY</td><td>17</td><td><code>int (*f)(void *param)</code></td></tr></tbody></table>

El prototipo hacer referencia al prototipo de la funcion que le pasamos como parametro ( int \*f() ) a mlx\_hook o a cualquiera de sus alias.

#### Alias para registro de eventos

Para facilitar el trabajo Minilibx tiene algunas funciones que realizan el mismo trabajo que `mlx_hook` con ciertos parametros:

* `mlx_expose_hook` Una parte de la ventana debe ser redibujada (esto se llama un evento de "exposición", y es su programa manejarlo). Evento (`12`).
* `mlx_key_hook` Una tecla es presionada. Evento (`3`).
* `mlx_mouse_hook` Se pulsa el botón del ratón. Evento (`4`)

```c
int	mlx_mouse_hook (void *win_ptr, int (*funct_ptr)(), void *param);
int	mlx_key_hook (void *win_ptr, int (*funct_ptr)(), void *param);
int	mlx_expose_hook (void *win_ptr, int (*funct_ptr)(), void *param);
```

#### mlx\_key\_hook

`mlx_key_hook` registra cada tecla que pulsemos y enviara como parametros a la funcion que le hayamos especifciado `*funct_ptr)()` el numero correspondiente de cada tecla. Para poder acceder a este valor lo haremos mediante el argumento `keycode` de la fucnion `*fuct_ptr()`.

> mlx\__key\_hook se acciona al **soltar** la tecla pulsada, mientras este pulsada no se activara el evento._

Este es uno entre los dos argumentos que tendremos que declarar a la funcion que utilicemos para pasar como parametro a `mlx_key_hook`. El otro es `void *param` que sirve para pasar como parametro la estrcutura que hayameos creado para guardar las vairables de mlx. Este parametro luego habra que castearlo.

```c
int    funct_ptr(int keycode, void *param);
```

#### mlx\_mouse\_hook

Con respecto a los eventos de raton cada accion qque podenmos ralizar con el raton tambien tiene un numero asginado:

Keycode del ratón para MacOS:

* Left click: 1
* Right click: 2
* Middle click: 3
* Scroll up: 4
* Scroll down : 5

<figure><img src="../../.gitbook/assets/image (2) (2).png" alt=""><figcaption></figcaption></figure>

### Ejemplo

```c
#include <mlx.h>
#include <stdio.h>

typedef struct	s_vars {
	void	*mlx;
	void	*win;
}				t_vars;

int	key_hook(int keycode, t_vars *vars)
{
	printf("The key pressed is: %d\n", keycode);
	return (0);
}

int	main(void)
{
	t_vars	vars;

	vars.mlx = mlx_init();
	vars.win = mlx_new_window(vars.mlx, 640, 480, "Hello world!");
	mlx_key_hook(vars.win, key_hook, &vars);
	mlx_loop(vars.mlx);
}
```

Esta funcion escribira en pantalla el keycode de cada teclas pulsada por el usuario en el a traves del teclado.
