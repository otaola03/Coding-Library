# Splash

Splash es una herramienta de renderizado de páginas web para web scraping de sitios dinámicos que utilizan JavaScript. Permite obtener el contenido completo de las páginas renderizadas, lo que facilita la extracción de datos de aplicaciones web modernas. Proporciona funciones para interactuar con elementos dinámicos y obtener datos precisos.

Para poder utilizar splash necesitas tener instalado docker y para utilizarlo en el vanegador tienes que ejecutar el siguiente comando:

```bash
sudo docker run -it -p 8050:8050 scrapinghub/splash

# Busca en el navegador
http://127.0.0.1:8050
```

Splash funciona con el lenguje Lua y al igual que en C los scripts requeiren de una funcion main con su return al final. Para ejecutar las distintas acciones es recomendable utilizar la funcion `assert`, ya que esta comprueba si la funcion en su interior ha sido ejecutada correctamente y de no ser asi devuelve un error.

```lua
funcion main(splash, args)
    url = args.url
    assert(splash:go(url))
    assert(splash:wait(1))
    return
    {
        image = splash:png(),
        html = splash:html()
    }
end
```

### Buscar elementos

Cuando se trabaja con Splash, una de las tareas fundamentales es la búsqueda y extracción de elementos específicos en el HTML renderizado de una página web. Splash proporciona diversas opciones y comandos para llevar a cabo esta tarea.

#### Selección de elementos por etiqueta

Puedes utilizar el comando `splash:select` para seleccionar elementos basados en su etiqueta. Por ejemplo, para seleccionar todos los elementos `div` en la página, puedes utilizar el siguiente código:

```lua
local divs = splash:select_all('div')
for _, div in ipairs(divs) do
    -- Realizar acciones con los elementos seleccionados
end
```

#### Selección de elementos por clase o ID

Si deseas buscar elementos por su clase o ID, puedes utilizar los selectores de CSS en conjunto con el comando `splash:select`. Por ejemplo, para seleccionar un elemento con una clase específica, puedes hacer lo siguiente:

```lua
local element = splash:select('.mi-clase')
```

Si en cambio deseas seleccionar un elemento por su ID, puedes utilizar:

```lua
local element = splash:select('#mi-id')
```

#### Extracción de atributos y texto de elementos

Una vez que hayas seleccionado un elemento, puedes extraer atributos específicos o el texto contenido en él. Por ejemplo, para obtener el valor del atributo `href` de un enlace (`<a>`), puedes utilizar:

```lua
local link = splash:select('a')
local href = link.node.attributes.href

local href = link:get_attribute('href')
```

Si deseas obtener el texto contenido dentro de un elemento, puedes utilizar la propiedad `node.text`. Por ejemplo:

```lua
local paragraph = splash:select('p')
local text = paragraph.node.text
```

#### Búsqueda de elementos anidados

Splash también te permite buscar elementos anidados dentro de un elemento seleccionado previamente. Puedes utilizar el comando `:select` en conjunto con el selector CSS correspondiente. Por ejemplo, para seleccionar todos los elementos `<li>` dentro de una lista `<ul>`, puedes hacer lo siguiente:

```lua
luaCopy codelocal ul = splash:select('ul')
local lis = ul:select_all('li')
```

Recuerda adaptar los selectores CSS según la estructura y los elementos específicos que deseas buscar en la página.

## Acciones con Splash

Splash es una herramienta poderosa para interactuar con páginas web dinámicas y realizar diversas acciones automatizadas. A continuación, exploraremos las diferentes acciones que se pueden realizar con Splash y cómo utilizarlas en el contexto del web scraping.

#### Centrar elementos

El método `focus` se utiliza para establecer el foco en un elemento HTML, como un campo de entrada de texto o un botón. Esto permite que el elemento esté listo para recibir eventos de teclado o interacciones del usuario.

```lua
local input = assert(splash:select('.my-input'))
input:focus()
```

En este ejemplo, `input:focus()` establece el foco en un elemento con la clase CSS `.my-input`. Después de eso, el elemento está listo para recibir eventos de teclado o interacciones del usuario.

#### Escribir texto en campos de formulario

Una de las formas de escribir texto en campos de formulario utilizando Splash es a través del método `splash:send_text`. Sin embargo, también es posible utilizar el método `element:send_text` para interactuar directamente con un elemento específico. Por ejemplo:

```lua
local input = splash:select('.search-input')
input:send_text('texto de búsqueda')

splash:send_text('.search-input', 'texto de búsqueda')
```

En este caso, se selecciona el elemento de entrada con la clase `.search-input` utilizando `splash:select` y luego se utiliza `send_text` en ese elemento para escribir el texto de búsqueda especificado.

#### Hacer clic en elementos

El método `splash:mouse_click` que mencionamos anteriormente se puede utilizar para simular clics en elementos. Sin embargo, también es posible utilizar el método `element:click` para hacer clic en un elemento específico. Por ejemplo:

```lua
local button = splash:select('.btn-submit')
button:click()

splash:mouse_click('.btn-submit')
```

Aquí, se selecciona el botón con la clase `.btn-submit` utilizando `splash:select` y se utiliza `click` en ese elemento para simular el clic.

#### Presionar teclas

Además de la opción de usar `splash:send_keys` para enviar eventos de teclado, también es posible utilizar el método `element:send_keys` para presionar teclas en un elemento específico. Por ejemplo:

```lua
local input = splash:select('.search-input')
input:send_keys('<Enter>')
```

En este caso, se selecciona el campo de entrada con la clase `.search-input` utilizando `splash:select` y se utiliza `send_keys` en ese elemento para simular la pulsación de la tecla Enter.

#### Esperar a elementos

En ocasiones, es necesario esperar a que aparezcan ciertos elementos en la página antes de realizar acciones adicionales. Puedes utilizar el comando `splash:wait` para esperar a que un elemento específico esté presente en la página. Por ejemplo:

```lua
local input = splash:select('.search-input')
splash:wait(input)

splash:wait('.elemento-esperado')
```

Este comando espera hasta que aparezca un elemento con la clase `.elemento-esperado`. Tambien se puede utilizar este metodo para esperar un timepo especifico. Por ejemplo 5 segundos:

```lua
splash:wait(5)
```

#### Capturar capturas de pantalla

Splash te permite capturar capturas de pantalla de la página renderizada. Puedes usar el comando `splash:png` para obtener una imagen PNG de la página. Por ejemplo:

```lua
local screenshot = splash:png()
```

Este comando captura una captura de pantalla de la página actual y la guarda en la variable `screenshot`.

#### Modo incognito

El atributo `splash.private_mode_enabled` en Splash habilita el modo de navegación privada, que protege la privacidad al eliminar cookies, ignorar cachés y no almacenar el historial de navegación.

```lua
splash.private_mode_enabled = true
```

### User-Agent

Cuando utilizas Splash, tienes varios métodos disponibles para cambiar el User-Agent en tus solicitudes. Los métodos más comunes son los siguientes:

**set\_user\_agent**

El método `set_user_agent` te permite establecer un User-Agent personalizado en el objeto `splash`. Puedes utilizarlo dentro del script Lua para cambiar el User-Agent de todas las solicitudes siguientes. Aquí tienes un ejemplo:

```lua
function main(splash, args)
    splash:set_user_agent("Mi User-Agent Personalizado")

    -- Resto del código...
end
```

Al llamar a `set_user_agent`, especificas el User-Agent que deseas utilizar en tus solicitudes posteriores.

**set\_custom\_headers**

El método `set_custom_headers` te permite establecer encabezados personalizados en el objeto `splash`. Esto incluye la posibilidad de cambiar el User-Agent. Puedes utilizarlo dentro del script Lua para configurar los encabezados de las solicitudes. Aquí tienes un ejemplo:

```lua
function main(splash, args)
    headers = {
        ["User-Agent"] = "Mi User-Agent Personalizado"
    }
    splash:set_custom_headers(headers)

    -- Resto del código...
end
```

Al llamar a `set_custom_headers`, proporcionas un diccionario de encabezados personalizados. Puedes incluir el User-Agent y otros encabezados según tus necesidades.

**on\_request**

El método `on_request` te permite manipular cada solicitud individualmente y modificar sus encabezados, incluido el User-Agent. Puedes utilizarlo para personalizar el User-Agent en solicitudes específicas. Aquí tienes un ejemplo:

```lua
function main(splash, args)
    splash:on_request(function(request)
        if string.find(request.url, "example.com") then
            request:set_header("User-Agent", "Mi User-Agent Personalizado")
        end
        return request
    end)

    -- Resto del código...
end
```

Al utilizar `on_request`, puedes verificar la URL de cada solicitud y establecer el User-Agent de manera selectiva en base a tus criterios.

**Diferencias entre los métodos**

* `set_user_agent` y `set_custom_headers` son métodos generales para establecer el User-Agent en todas las solicitudes o en todas las solicitudes con encabezados personalizados. Son útiles cuando deseas aplicar el mismo User-Agent a todas las solicitudes.
* `on_request` te permite modificar las solicitudes individualmente y personalizar el User-Agent según criterios específicos. Es útil cuando deseas tener un control más granular sobre el User-Agent en diferentes solicitudes.

En resumen, los métodos `set_user_agent` y `set_custom_headers` son adecuados para establecer un User-Agent global, mientras que `on_request` te brinda la flexibilidad de personalizar el User-Agent en solicitudes individuales. Puedes elegir el método que mejor se adapte a tus necesidades y escenarios de uso en particular.

### **scrapy-splash**

Scrapy-Splash es una extensión de Scrapy que permite el scrapeo de contenido dinámico al interactuar con Splash, un renderizador web basado en navegador. Simplifica el proceso de renderizado de páginas web con JavaScript, lo que facilita el scrapeo de sitios que dependen de interacciones dinámicas.

{% embed url="https://scrapeops.io/python-scrapy-playbook/scrapy-splash/" %}

#### Orden de funcionamiento

Aquí está el orden de ejecución nuevamente:

1. Scrapy envía una solicitud a Splash.
2. El script Lua en Splash se ejecuta.
3. Dentro del script Lua, se realizan las acciones, como hacer clic en botones o escribir texto.
4. Splash procesa y renderiza la página web, teniendo en cuenta las acciones realizadas en el script Lua.
5. Splash devuelve el HTML renderizado junto con otros datos como respuesta a Scrapy.
6. Scrapy recibe la respuesta de Splash y continúa con el procesamiento de la respuesta en su propia lógica de scrapeo.

En resumen, las acciones que realices con scrapy-splash se ejecutan dentro del script Lua en Splash, entre el envío de la solicitud desde Scrapy y la devolución de la respuesta a Scrapy. Esto permite interactuar con la página web antes de extraer los datos deseados.

#### Integrar Scrapy-splash

Para utilizar Scrapy Splash en nuestro proyecto, primero necesitamos instalar el descargador scrapy-splash:

```bash
pip install scrapy-splash
```

Luego, debemos agregar la configuración requerida de Splash en el archivo settings.py de nuestro proyecto Scrapy:

```python
# settings.py

# Splash Server Endpoint
SPLASH_URL = 'http://localhost:8050'


# Enable Splash downloader middleware and change HttpCompressionMiddleware priority
DOWNLOADER_MIDDLEWARES = {
    'scrapy_splash.SplashCookiesMiddleware': 723,
    'scrapy_splash.SplashMiddleware': 725,
    'scrapy.downloadermiddlewares.httpcompression.HttpCompressionMiddleware': 810,
}

# Enable Splash Deduplicate Args Filter
SPIDER_MIDDLEWARES = {
    'scrapy_splash.SplashDeduplicateArgsMiddleware': 100,
}

# Define the Splash DupeFilter
DUPEFILTER_CLASS = 'scrapy_splash.SplashAwareDupeFilter'
```

#### Usar splash desde scrapy

Como vamos a utilizar splash para hacer el request a la pagina web, es necesario reeescribir el emtodo `start_requests` y en vez de usar el metodo `scrapy.Request` tenemos que usar un metodo propio de la libreria `splash-request` que se llama `SplashRequest`:

```python
import scrapy
from quotes_js_scraper.items import QuoteItem
from scrapy_splash import SplashRequest 

lua_script = """
function main(splash, args)
    assert(splash:go(args.url))

  while not splash:select('div.quote') do
    splash:wait(0.1)
    print('waiting...')
  end
  return {html=splash:html()}
end
"""

class QuotesSpider(scrapy.Spider):
    name = 'quotes'

    def start_requests(self):
        url = 'https://quotes.toscrape.com/scroll'
        yield SplashRequest(
            url, 
            callback=self.parse, 
            endpoint='execute', 
            args={'lua_source': lua_script}
            )

    def parse(self, response):
        print(response.body)
```
