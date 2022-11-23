# Audio y video

### Audio

Al igual que vimos en el tema anterior con los videos, es posible añadir archivos de audio a nuestras páginas web para colocar música, sonidos o simplemente usar música como ambientación.

En este caso, utilizaremos la etiqueta `<audio>` que funciona exactamente igual que `<video>`, pero con relación a archivos de audio.

Un primer ejemplo muy básico para colocar un audio en nuestra página web:

```html
<audio src="audio.mp3" cotrols></audio>
```

### Video

En HTML5 se introduce la interesante posibilidad de **mostrar videos directamente** desde nuestro navegador. De hecho, si arrastramos un video a la ventana del navegador, veremos que comienza a reproducirse en él. Para poder insertar videos en nuestras páginas HTML tenemos que utilizar la etiqueta `<video>`.

Un primer ejemplo muy básico para colocar un video en nuestra página web:

```html
<video src="video.mp4" width="640" height="480" controls></video>
```

En el caso de queramos estabelcer una imagen como fondo por defecto antes de que se inicialice el video puedes utilizar el atributo `poster` y especificar la direccion de la imagen

### Atributos

La etiqueta `<audio>` tiene varios atributos a nuestra disposición:

* `src`: Audio o video a reproducir. Obligatoria si actua como etiqueta contenedora. Aqqui introduciremos al URL de nuestro audio.
* `autoplay`: Comienza a reproducirse  automáticamente. Los navegadores suelen deshabilitarlo
* `loop`: Vuelve a iniciarse cuando finaliza su reporduccion (bucle)
* `muted`: Establece el audio o video sin sonido
* `controls`: Si está presente este atributo, el navegador ofrecerá controles para permitir que el usuario controle la reproducción de audio y video, incluyendo volumen, búsqueda y pausar/reanudar reproducción.

{% hint style="info" %}
El atributo `controls` es necesario para que visualice le elemento de audio en pantalla o para poder iniciar los videos
{% endhint %}

### Bibliografia

* [https://lenguajehtml.com/html/multimedia/etiquetas-html-de-video/](https://lenguajehtml.com/html/multimedia/etiquetas-html-de-video/)
* [https://lenguajehtml.com/html/multimedia/etiquetas-html-de-audio/](https://lenguajehtml.com/html/multimedia/etiquetas-html-de-audio/)
