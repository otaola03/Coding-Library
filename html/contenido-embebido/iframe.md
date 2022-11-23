# Iframe

Cuando tenemos una página web y queremos colocar contenido en ella, lo conveniente es utilizar formatos libres para garantizar que sean accesibles desde cualquier tipo de dispositivo.

¿Pero que ocurre si lo que quiero colocar no son formatos de video, de audio o de imagen? Por ejemplo, servicios como Youtube, Vimeo, SoundCloud, SlideShare u otros similares. Se trata de servicios que ofrecen **contenido externo para incrustar** en nuestra página, pero no nos proporcionan directamente imágenes, video o audio en formatos que reconozca el navegador, sino que nos ofrecen un enlace o contenidos que requieren un plugin externo instalado en el navegador.&#x20;

Para esto la mas comun es utilizar `<iframe>`:

```html
<iframe src="https://www.youtube.com/embed/Imeq3GeRttw" width="560" height="315">
</iframe>

<a href="http://www.bing.com/" target="marco">Abrir buscador Bing</a>
<iframe name="marco" width="100%" height="450"
  src="https://w.soundcloud.com/player/?url=https%3A//api.soundcloud.com/tracks/38289724&visual=true">
</iframe>
```

Esto codigo imprimiria en pantalla el siguiente fragmento de video:

{% embed url="https://www.youtube.com/watch?v=hAgrrW5LM6M&list=PLROIqh_5RZeB92ME1GFyeqDVOa-gL0Ybd&index=64" %}
