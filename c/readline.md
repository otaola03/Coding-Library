# Readline

### Compilacion

Para poder utilizar la función readline() en un programa de C, es necesario tener instalada la biblioteca GNU Readline o editline en el sistema. Estas bibliotecas proporcionan la funcionalidad de readline() y otras funciones adicionales.

Para incluir la biblioteca en el código, es necesario incluir la cabecera `#include <readline/readline.h>` o `#include <editline/readline.h>` dependiendo de la biblioteca que se tenga instalada, en el archivo fuente donde se quiere usar readline().

Para compilar el programa, es necesario indicar al compilador que se desea vincular con la biblioteca de readline. Esto se puede hacer utilizando la opción -lreadline o -leditline dependiendo de la biblioteca que se tenga instalada. Por ejemplo, si se está usando GCC, el comando para compilar el programa sería algo similar a esto:

```bash
gcc -o programa programa.c -leditline
```

#### Instalar readline

Por otro lado para poder utilizar otras fucniones como `rl_clear_history()` o `rl_replace_line()` es necesariao tener instalada la libreria readline. Para ello tan solo tenemos que instalarla con brew, `brew install readline`, y depues añadir su cabezera a nuestro fichero. `#include<readline/readline.h>`.

Ademas es necesariao hacer referencia a dicha libreria a la hora de compilar:

```bash
gcc programa.c  -lreadline -L /Users/$(USER)/.brew/opt/readline/lib -I /Users/$(USER)/.brew/opt/readline/include
```

### Readline

La función readline() es una función de biblioteca que permite a los programas de C leer líneas de entrada del usuario de una manera conveniente.

```c
char * readline(const char * prompt)
```

La función toma un solo argumento, que es una cadena de caracteres que se utiliza como un prompt para indicar al usuario que debe ingresar información. La función devuelve un puntero a una cadena de caracteres que contiene la línea de entrada del usuario.

La forma en que la función readline() funciona es mediante la lectura de caracteres desde el flujo de entrada estándar (stdin) hasta que se encuentra un carácter de nueva línea ('\n') o se alcanza el final de archivo (EOF). Cada carácter leído se agrega a un buffer temporal, hasta que se alcanza el carácter de nueva línea o el final del archivo.

Una vez que se ha leído una línea completa, la función readline() asigna memoria dinámica para almacenar una copia de la línea de entrada. Esta memoria se debe liberar manualmente después de usarla con la función free() para evitar fugas de memoria.

Aquí tienes un ejemplo de cómo usar la función readline() en un programa de C:

```c
#include <stdio.h>
#include <stdlib.h>
#include <readline/readline.h>

int main() {
    char *line;

    // Mostrar el prompt al usuario y leer la línea de entrada
    line = readline("Ingresa una línea de texto: ");

    // Imprimir la línea de entrada
    printf("La línea ingresada es: %s\n", line);

    // Liberar la memoria asignada para la línea de entrada
    free(line);

    return 0;
}
```

En este ejemplo, se incluyen las cabeceras necesarias para usar la función r`eadline()`, que en este caso es r`eadline/readline.h`. La función `readline()` se llama con un prompt "Ingresa una línea de texto: " y el resultado se almacena en una variable char\* llamada "line". El contenido de la linea se imprime con printf y luego se libera la memoria con free.

### Historial

El historial en readline() es una funcionalidad que permite al usuario recuperar líneas de entrada previamente ingresadas usando las flechas arriba y abajo. Esto es útil cuando el usuario desea volver a ingresar una línea de comando que ya ha utilizado previamente, o si desea verificar una línea de comando anterior.

Cada vez que se utiliza la función `readline()` para leer una línea de entrada del usuario, esa línea se agrega automáticamente al historial. El usuario puede navegar por el historial de líneas utilizando las flechas arriba y abajo. Cada vez que se presiona la flecha arriba, readline() mostrará la línea anterior en el historial, y cada vez que se presiona la flecha abajo, readline() mostrará la línea siguiente en el historial.

Además, el usuario también puede buscar en el historial de líneas ingresadas mediante el uso de comandos como ctrl + R, esto le permitirá buscar una línea específica en el historial.

La capacidad de guardar el historial de líneas es configurable, el usuario puede limitar la cantidad de líneas que se guardan en el historial o deshabilitarlo completamente. También se puede cambiar la ubicación donde se guarda el historial, ya sea en un archivo o en memoria.

Es importante tener en cuenta que esta funcionalidad solo estará disponible si se tiene una biblioteca como GNU Readline o editline instalada y se incluye en el código.

### add\_history()

`add_history()` es una función proporcionada por la biblioteca GNU Readline que permite agregar una línea al historial.

```c
void add_history(const char *line);
```

La función `add_history()` tiene un solo argumento, que es un puntero a una cadena de caracteres que representa la línea que se desea agregar al historial. Este argumento es obligatorio, si no se proporciona una cadena de caracteres la función no agregará nada al historial.

* `line` es un puntero a una cadena de caracteres, es la línea que se desea agregar al historial.

La función `add_history()` se utiliza para agregar una línea al historial, esta línea se agrega al final del historial y se convierte en la línea actual. Esto es útil cuando el usuario desea agregar una línea al historial después de haber utilizado `readline()` o cuando se quieren agregar líneas de forma programática al historial. Es importante tener en cuenta que esta función no afecta al archivo de historial, si se tiene un archivo de historial configurado sigue existiendo.

{% hint style="info" %}
La función `read_history()` y `write_history()` permiten trabajar con el archivo de historial, permitiendo cargarlo o guardarlo en disco, respectivamente.
{% endhint %}

Aquí te dejo un ejemplo de cómo utilizar el historial de líneas utilizando `readline()` y `add_history()` en un programa:

```c
#include <stdio.h>
#include <stdlib.h>
#include <readline/readline.h>

int main() {
    char *line;
    int i;
    for(i = 0; i < 5; i++) {
        line = readline("Ingresa una línea de texto: ");
        add_history(line);
    }
    while(1) {
        line = readline("Ingresa una línea de texto (o presiona ctrl + c para salir): ");
        if(line != NULL) {
            printf("La línea ingresada es: %s\n", line);
        } else {
            break;
        }
    }
    return 0;
}
```

### rl\_clear\_history

`rl_clear_history()` es una función proporcionada por la biblioteca GNU Readline que permite limpiar todas las líneas almacenadas en el historial. Esta función no requiere ningún parámetro y no devuelve ningún valor.

La funcionalidad de esta función es eliminar todas las líneas almacenadas en el historial. Una vez que se llama a esta función, el historial quedará vacío y no habrá líneas disponibles para recuperar con las flechas arriba y abajo. Es importante tener en cuenta que esta función no afecta al archivo de historial, si se tiene un archivo de historial configurado sigue existiendo.

Aquí te dejo un ejemplo de cómo utilizar esta función en un programa:

```c
#include <stdio.h>
#include <stdlib.h>
#include <readline/readline.h>

int main() {
    char *line;
    int i;
    for(i = 0; i<10; i++) {
        line = readline("Ingresa una línea de texto: ");
        add_history(line);
    }
    printf("Historial antes de limpiar: %d\n", history_length);
    rl_clear_history();
    printf("Historial despues de limpiar: %d\n", history_length);
    return 0;
}
```

En este ejemplo se agrega 10 líneas al historial, luego se llama a la función `rl_clear_history()` y se imprime el tamaño del historial antes y después de limpiarlo. El resultado seria "Historial antes de limpiar: 10" y "Historial despues de limpiar: 0"

### rl\_on\_new\_line

`rl_on_new_line()` es una función proporcionada por la biblioteca de lectura GNU que se utiliza para indicar al sistema que se ha movido a una nueva línea vacía. Esto es útil para actualizar el estado interno del sistema de lectura de línea de comandos, ya que permite realizar tareas como la actualización del historial de comandos, la limpieza de la pantalla, la actualización de la posición del cursor, entre otras.

La firma de la función es:

```c
void rl_on_new_line(void);
```

La función no recibe argumentos.

Un ejemplo de uso de `rl_on_new_line()` podría ser el siguiente:

```c
#include <stdio.h>
#include <readline/readline.h>

int main(void) {
    while (1) {
        char *input = readline("Enter a command: ");
        printf("You entered: %s\n", input);
        rl_on_new_line();
    }
    return 0;
}
```

En este ejemplo, la función `rl_on_new_line()` se llama después de que el usuario ingresa un comando y se imprime en pantalla. Esto indica al sistema que se ha movido a una nueva línea vacía y permite que el sistema actualice su estado interno para el próximo comando del usuario. Sin embargo, es importante tener en cuenta que esta función no ejecuta ninguna acción específica, sólo indica al sistema que se ha movido a una nueva línea vacía.

Si en el ejemplo anterior no se utiliza la función `rl_on_new_line()`, el sistema de lectura de línea de comandos no sería capaz de actualizar su estado interno correctamente. Esto podría tener varias consecuencias, dependiendo de las funcionalidades que se estén utilizando. Algunas posibles consecuencias incluyen:

* El historial de comandos podría no actualizarse correctamente, lo que podría dificultar el acceso a comandos previamente ingresados.
* La posición del cursor podría no actualizarse correctamente, lo que podría causar problemas al ingresar nuevos comandos.
* La pantalla podría no limpiarse correctamente, lo que podría causar problemas de visualización al ingresar nuevos comandos.

En general, la falta de llamada a la función `rl_on_new_line()` puede causar problemas en la funcionalidad del sistema de lectura de línea de comandos y afectar al uso de la aplicación. Es importante tener en cuenta que esta función es necesaria para actualizar el estado interno del sistema de lectura de línea de comandos, y su omisión puede causar problemas en el funcionamiento de la aplicación.

### rl\_replace\_line

La función `rl_replace_line()` es una función de la biblioteca de lectura de línea de comandos de GNU (readline) que se utiliza para reemplazar el contenido actual de la línea de comandos con una nueva cadena de texto. Esta función se utiliza para actualizar la línea de comandos con nueva información, por ejemplo, cuando se desea mostrar información adicional al usuario mientras se ingresa un comando.

La cabecera de esta función es la siguiente:

```c
void rl_replace_line (const char *string, int clear_undo)
```

Los argumentos de esta función son:

* `string`: Es un puntero a una cadena de caracteres que contiene el nuevo texto que se desea utilizar para reemplazar la línea actual.
* `clear_undo`: es un valor booleano que indica si se debe limpiar el historial de deshacer al reemplazar la línea de comandos.

La función `rl_replace_line()` funciona reemplazando el contenido actual de la línea de comandos con la cadena de texto especificada en el argumento `string`. Si se especifica `1` en el argumento `clear_undo`, el historial de deshacer se limpia automáticamente al reemplazar la línea de comandos. Si se especifica `0`, el historial de deshacer no se limpia.

Aquí te dejo un ejemplo de código que utiliza solo la función rl\_replace\_line:

```c
#include <stdio.h>
#include <readline/readline.h>

int main() {
    char *input;
    input = readline("Enter a line of text: ");
    printf("You entered: %s\n", input);
    rl_replace_line("This is the new line", 0);
    rl_redisplay();
    input = readline("Enter another line of text: ");
    printf("You entered: %s\n", input);
    return 0;
}
```

En este ejemplo, primero se solicita al usuario que ingrese una línea de texto a través de la función readline(). Luego, se imprime el valor introducido y se reemplaza la línea actual con el texto "This is the new line" utilizando la función rl\_replace\_line. Se llama a rl\_redisplay() para actualizar la pantalla y se vuelve a solicitar al usuario que ingrese otra línea de texto. En este caso, no se utiliza la variable rl\_line\_buffer, pero se esta usando rl\_replace\_line para reemplazar el texto en la línea actual y rl\_redisplay para actualizar el prompt.

El output del ejemplo anterior sería algo similar a esto:

```bash
Enter a line of text: Hello World!
You entered: Hello World!
This is the new line
Enter another line of text: 
You entered: 
```

La función rl\_replace\_line reemplaza el contenido actual de la línea de entrada en readline con el texto especificado en el primer argumento. El segundo argumento indica si se mueve el cursor al principio de la línea después del reemplazo.

En el ejemplo que te di, después de llamar a rl\_replace\_line con el texto "This is the new line", la próxima vez que se llame a readline() el buffer de entrada tendrá ese texto en lugar del que fue ingresado previamente. Por eso se muestra en la siguiente llamada a readline(). Esto se puede apreciar en el sigueinte ejemplo:

```c
#include <stdio.h>
#include <readline/readline.h>

int main() {
    char *input = "";
    char *new_line = "This is the new line content";

    // get initial input
    input = readline("Enter some text: ");
    printf("Original input: %s\n", input);

    // replace the current line with new content
    rl_replace_line(new_line, 0);
    printf("New input: %s\n", rl_line_buffer);

    return 0;
}
```

En este ejemplo, primero se solicita al usuario que ingrese una línea de texto a través de la función readline(). Luego, se imprime el valor introducido y se reemplaza la línea actual con el texto "This is the new line" utilizando la función rl\_replace\_line. Se llama a rl\_redisplay() para actualizar la pantalla y se vuelve a solicitar al usuario que ingrese otra línea de texto. En este caso, no se utiliza la variable rl\_line\_buffer, pero se esta usando rl\_replace\_line para reemplazar el texto en la línea actual y rl\_redisplay para actualizar el prompt.

rl\_line\_buffer es una variable global proporcionada por el encabezado readline/readline.h. No es necesario inicializarla ya que ya está inicializada por defecto al momento de incluir el encabezado. Puede ser utilizada en cualquier parte de tu programa después de incluir el encabezado readline/readline.h. Esta variable almacena el contenido actual de la línea de comando y se actualiza automáticamente cada vez que se llama a una función de readline, como rl\_replace\_line.

{% hint style="info" %}
`rl_line_buffer` guarda el último valor introducido a través de una función de readline, como `readline()` o `rl_replace_line()`.
{% endhint %}

#### Buffer de entarda

En el contexto de la biblioteca readline, el buffer de entrada es una variable que contiene la línea de texto que el usuario ha ingresado. Cada vez que se llama a la función readline(), el usuario ingresa una línea de texto y esta línea se almacena en el buffer de entrada. La función readline() devuelve un puntero al buffer de entrada, por lo que se puede acceder al contenido de la línea ingresada mediante este puntero.

La función rl\_replace\_line(), permite modificar el contenido del buffer de entrada, permitiendo al programador reemplazar el contenido anterior con uno nuevo. Una vez llamada esta funcion, se debe llamar a rl\_redisplay() para que el nuevo contenido sea mostrado en pantalla.&#x20;

### rl\_redisplay

La función rl\_redisplay() es una función de la biblioteca readline que se utiliza para actualizar la línea de entrada mostrada en la pantalla. Esta función no tiene argumentos y no devuelve ningún valor.

La función rl\_redisplay() se utiliza después de haber realizado cambios en la línea de entrada mediante otras funciones de la biblioteca readline, como rl\_replace\_line(). Sin llamar a esta función, los cambios realizados en la línea de entrada no se mostrarían en pantalla.

Esta función no tiene argumentos y no tiene un valor de retorno. La cabecera de la función es la siguiente

```c
void rl_redisplay (void);
```

En cuanto a un ejemplo de uso, si tienes el siguiente código:

```c
#include <stdio.h>
#include <readline/readline.h>

int main() {
    char *input;
    input = readline("Enter a line of text: ");
    printf("You entered: %s\n", input);
    rl_replace_line("This is the new line", 0);
    rl_redisplay();
    input = readline("Enter another line of text: ");
    printf("You entered: %s\n", input);
    return 0;
}
```

El output sería:

```bash
Enter a line of text: AAAA
You entered: AAAA
This is the new line
Enter another line of text: SSS
You entered: SSS
```

En este ejemplo, se utiliza la función rl\_replace\_line para reemplazar el contenido de la línea actual con el texto "This is the new line". Luego se llama a rl\_redisplay() para actualizar la línea en la terminal. En la siguiente llamada a readline(), se mostrará el nuevo contenido de la línea en lugar del valor anterior. Si no se llama a rl\_redisplay() después de usar rl\_replace\_line(), el nuevo contenido de la línea no se mostrará en la terminal.

Si no utilizas la función rl\_redisplay, entonces la línea actual de texto no se actualizará en la interfaz de línea de comandos. Es decir, el texto que reemplazaste con la función rl\_replace\_line no se mostrará en pantalla, y el usuario seguiría viendo el texto anterior. Sin la llamada a rl\_redisplay, la función rl\_replace\_line solo actualiza el buffer interno de readline, pero no actualiza lo que se ve en la pantalla.

