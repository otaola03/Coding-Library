# Spiders

Una spider en Scrapy es un objeto Python que define cómo navegar por un sitio web y cómo extraer los datos de interés. Las spiders son responsables de realizar solicitudes HTTP a las páginas web, analizar las respuestas y extraer los datos estructurados utilizando selectores o patrones específicos. En resumen, una spider es la entidad encargada de la lógica de extracción en Scrapy.

### Creación de una spider básica

En Scrapy, `scrapy.Spider` es una clase fundamental que proporciona la base para crear spiders personalizadas. Para crear un spider basica tienes que usar el siguiente comando

```bash
scrapy genspider [spiderName] [start_urls]
```

Esto generara el codigo de una spider con el nombre y start\_url proporcionados:

```python
import scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'
    allowed_domains = ['example.com']
    start_urls = ['https://www.example.com']

    def parse(self, response):
        # Lógica para extraer datos aquí
        pass
```

Como puedes ver se crean tes varables por defecto al crear la spider:

* `name = 'my_spider'`: Esta variable se utiliza para asignar un nombre único a la spider. El nombre se utiliza para identificar la spider en el proyecto de Scrapy y al ejecutar el comando de inicio de la spider. Es importante elegir un nombre descriptivo y único para evitar conflictos con otras spiders en el proyecto.
* `allowed_domains = ['example.com']`: Esta variable se utiliza para especificar los dominios permitidos para realizar el crawling. En este caso, se configura como `example.com`, lo que significa que la spider solo seguirá enlaces que pertenezcan a este dominio. Esto ayuda a evitar que la spider siga enlaces a otros sitios web y se mantenga dentro del dominio objetivo.
* `start_urls = ['https://www.example.com']`: Esta variable se utiliza para especificar las URL de inicio para la extracción de datos. La spider comenzará la extracción de datos visitando estas URL de inicio. Puedes proporcionar una o varias URL de inicio según tus necesidades. Si lo haces ejecutara la funcion `parse` en cada una de ellas de manera secuencial.

En resumen, estas variables se utilizan de la siguiente manera:

* `name` asigna un nombre único a la spider.
* `allowed_domains` especifica los dominios permitidos para el crawling.
* `start_urls` define las URL de inicio para la extracción de datos.

Estas variables son parte de la configuración básica de una spider en Scrapy y se utilizan para personalizar el comportamiento y el alcance de la extracción de datos.

### Yield

En Scrapy, el uso de `yield` en las spiders es una técnica poderosa y fundamental para el procesamiento y almacenamiento de datos durante el web scraping. En lugar de devolver los resultados directamente desde los métodos de extracción de datos, se utilizan generadores con `yield` para enviar los elementos extraídos a través del flujo de ejecución de Scrapy.

**Ejemplo de uso de `yield` en una Spider de Scrapy**

```python
import scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['https://www.example.com']

    def parse(self, response):
        # Lógica para extraer datos aquí
        for elemento in response.xpath('//div[@class="item"]'):
            titulo = elemento.xpath('h2/text()').get()
            descripcion = elemento.xpath('p/text()').get()
            
            yield {
                'titulo': titulo,
                'descripcion': descripcion
            }
```

En este ejemplo, el método `parse` de la spider `MySpider` utiliza `yield` para devolver un diccionario que contiene los datos extraídos de cada elemento encontrado en la página. En lugar de devolver una lista de diccionarios, se utiliza `yield` para enviar cada diccionario a medida que se procesa.

**Ventajas del uso de `yield`**

El uso de `yield` en las spiders de Scrapy ofrece varias ventajas:

1. **Eficiencia**: Al utilizar `yield`, los datos se devuelven de forma incremental a medida que se procesan, lo que evita la necesidad de cargar todos los elementos en la memoria al mismo tiempo. Esto mejora la eficiencia, especialmente cuando se trabaja con grandes volúmenes de datos.
2. **Escalabilidad**: La técnica de `yield` permite manejar grandes volúmenes de datos sin comprometer el rendimiento. Scrapy se encarga de manejar el flujo de ejecución y el almacenamiento de los elementos devueltos, lo que facilita el desarrollo de crawlers escalables.
3. **Flexibilidad**: Al utilizar `yield`, se pueden aplicar transformaciones o filtros a los datos antes de enviarlos. Esto permite realizar modificaciones o ajustes específicos en los elementos extraídos antes de continuar con el procesamiento.

En resumen, el uso de `yield` en las spiders de Scrapy permite generar resultados de extracción de datos de forma incremental, mejorando la eficiencia y el manejo de grandes volúmenes de información. Esta técnica proporciona ventajas en términos de eficiencia, escalabilidad y flexibilidad, facilitando el desarrollo de crawlers robustos y eficientes.

### Opcion `-o` en Scrapy

La opción `-o` en Scrapy se utiliza para guardar la salida de la araña directamente en un archivo específico, sin necesidad de crear un pipeline personalizado. Puedes usar esta opción al ejecutar la araña desde la línea de comandos.

Aquí tienes un ejemplo de cómo usar la opción `-o` para guardar la salida en un archivo CSV:

```bash
scrapy crawl my_spider -o output.csv
```

En este caso, `my_spider` es el nombre de tu araña y `output.csv` es el nombre del archivo en el que se guardará la salida.

Scrapy también admite otros formatos de archivo, como JSON y XML. Puedes especificar el formato deseado utilizando la extensión de archivo correspondiente. Por ejemplo:

```bash
scrapy crawl my_spider -o output.json
scrapy crawl my_spider -o output.xml
```

Esto guardará la salida en archivos JSON y XML, respectivamente.

Recuerda que al usar la opción `-o`, Scrapy utilizará un formato predeterminado para la salida según la extensión del archivo especificado. Sin embargo, si necesitas un formato personalizado o realizar operaciones adicionales antes de guardar la salida, puedes considerar la opción de utilizar `pipelines` personalizados, como se mencionó anteriormente.

### Seguir enlaces con `follow()`

Una de las características poderosas de Scrapy es su capacidad para seguir enlaces automáticamente durante el proceso de web scraping. Esto permite extraer datos de múltiples páginas de un sitio web de manera eficiente y completa.

El método `follow()` es una forma sencilla de indicar a Scrapy que siga un enlace en una página y continúe extrayendo datos de la página enlazada. Aquí tienes un ejemplo:

```python
import scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['https://www.example.com']

    def parse(self, response):
        link = response.xpath("//a/@href").get #Obtner ruta relativa
        yield response.follow(url=link)
```

**Argumentos de `follow()`**

Esta es la sintaxis del metodo `follow()`:

```python
response.follow(url, callback=None, method='GET', headers=None, body=None, cookies=None, meta=None, encoding='utf-8', priority=0, dont_filter=False)
```

A continuación, se explica cada uno de los argumentos de la función:

* `url` (obligatorio): La URL del enlace que se va a seguir. Puede ser una URL absoluta o una URL relativa.
* `callback` (opcional): El nombre de la función de devolución de llamada (callback) que se utilizará para procesar la respuesta de la página enlazada. Si no se proporciona, se utilizará el método `parse()` de la spider actual.
* `method` (opcional): El método HTTP utilizado para realizar la solicitud. Los valores comunes son "GET" y "POST". Por defecto, se utiliza "GET".
* `headers` (opcional): Un diccionario con los encabezados HTTP adicionales que se deben enviar con la solicitud.
* `body` (opcional): El cuerpo de la solicitud, que se utiliza cuando se realiza una solicitud POST.
* `cookies` (opcional): Un diccionario con las cookies que se deben enviar con la solicitud.
* `meta` (opcional): Un diccionario que contiene metadatos adicionales que se pasan a la función de devolución de llamada.
* `encoding` (opcional): La codificación utilizada para decodificar la respuesta. Por defecto, se utiliza UTF-8.
* `priority` (opcional): La prioridad de la solicitud. Las solicitudes con una prioridad más alta se procesarán antes. Por defecto, es 0.
* `dont_filter` (opcional): Un booleano que indica si se debe aplicar el filtro de duplicados a esta solicitud. Por defecto, es False.

#### Scrapear enlaces seguidos

Una vez que has seguido un enlace utilizando `response.follow()` en Scrapy, puedes realizar el scraping de la página enlazada utilizando la función de devolución de llamada (callback) correspondiente. Aquí tienes un ejemplo de cómo hacerlo:

```python
pythonCopy codeimport scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['https://www.example.com']

    def parse(self, response):
        # Lógica para extraer datos de la página inicial aquí
        
        # Seguir enlaces a otras páginas
        for enlace in response.css('a::attr(href)').getall():
            yield response.follow(enlace, callback=self.parse_detalles)

    def parse_detalles(self, response):
        # Lógica para extraer datos de la página enlazada aquí
        titulo = response.css('h1::text').get()
        contenido = response.css('p::text').get()

        yield {
            'Título': titulo,
            'Contenido': contenido
        }
```

En este ejemplo, después de seguir un enlace utilizando `response.follow(enlace, callback=self.parse_detalles)`, el motor de Scrapy llamará al método `parse_detalles()` para procesar la respuesta de la página enlazada. Dentro de esta función de devolución de llamada, puedes usar selectores CSS o XPath para extraer la información deseada de la página enlazada.

En el ejemplo, se extraen el título (`<h1>`) y el contenido (`<p>`) de la página enlazada, y se almacenan en un diccionario que se devuelve usando la instrucción `yield`. Puedes realizar otras operaciones en la función de devolución de llamada según tus necesidades.

#### Mandar informacion entre dos metodos de parseo

Para pasar información entre dos métodos de parseo en Scrapy, puedes utilizar el atributo `meta` de la solicitud (`Request`) para almacenar y transmitir los datos necesarios. El atributo `meta` es un diccionario que puede contener cualquier información adicional que desees pasar entre las solicitudes y las funciones de devolución de llamada.

Aquí tienes un ejemplo de cómo pasar información utilizando el atributo `meta`:

```python
import scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['https://www.example.com']

    def parse(self, response):
        # Lógica para extraer datos aquí
        
        # Pasar información a otra función de devolución de llamada
        datos = {
            'id': 123,
            'nombre': 'Ejemplo'
        }
        yield scrapy.Request(url='https://www.example.com/detalles', callback=self.parse_detalles, meta={'datos': datos})

    def parse_detalles(self, response):
        # Acceder a los datos pasados desde la función de devolución de llamada anterior
        datos = response.meta.get('datos')
        datos = response.request.meta['datos']

        # Utilizar los datos en la lógica de extracción de detalles aquí
        id = datos.get('id')
        nombre = datos.get('nombre')

        # Puedes realizar otras operaciones o guardar los datos extraídos en un archivo, base de datos, etc.

        yield {
            'ID': id,
            'Nombre': nombre
        }
```

En este ejemplo, se utiliza el atributo `meta` para pasar información de la función `parse()` a la función `parse_detalles()`. Se crea un diccionario llamado `datos` que contiene la información necesaria. Luego, al realizar la solicitud utilizando `scrapy.Request()`, se pasa el diccionario `datos` como valor del argumento `meta`.

En la función `parse_detalles()`, se accede a los datos pasados utilizando `response.meta.get('datos')`. Luego, puedes utilizar esos datos en la lógica de extracción de detalles o cualquier otra operación que necesites realizar.

### Seguir enlaces con `scrapy.Request`

Además del método `follow()`, Scrapy también proporciona la clase `scrapy.Request` para realizar solicitudes HTTP personalizadas. Esto es útil cuando se necesita controlar más aspectos de la solicitud, como los encabezados, los parámetros de URL o el método HTTP utilizado. Aquí tienes un ejemplo:

> Tanto `follow` como `Requests` reciben los mismos argumentos

```python
import scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['https://www.example.com']

    def parse(self, response):
        link = response.xpath("//a/@href").get #Obtner ruta relativa
        absolute_url = f'https://www.example.com{link}'
        absolute_url = response.urljoin(link)
        
        yield scrapy.Request(url=absolute_url)
```

### User-Agent

El User-Agent es una cadena de texto que se envía en las solicitudes HTTP para identificar el software o la aplicación que realiza la solicitud. Cambiar el User-Agent puede ayudar a simular un comportamiento de navegación legítimo y evitar bloqueos o restricciones impuestas por los sitios web.

Hay varias maneras paracambairlo:

#### `USER_AGENT`

El User-Agent se establece una vez en el momento de iniciar la araña y se mantiene constante durante toda la ejecución de la araña, a menos que se cambie manualmente. Al cambiar la variable `USER_AGENT` en el archivo `settings.py`, estarás modificando el User-Agent utilizado por defecto en todas las solicitudes realizadas por tus arañas en Scrapy.

```python
USER_AGENT = 'user-agent propio'
```

#### `DEFAULT_REQUEST_HEADERS`

Al agregar un User-Agent personalizado al atributo `DEFAULT_REQUEST_HEADERS` en el archivo `settings.py`, estarás estableciendo un User-Agent predeterminado para todas las solicitudes, pero permitiendo que se sobrescriba en cada solicitud individual.

Si una solicitud no tiene un encabezado `User-Agent` definido, se utilizará el User-Agent predeterminado especificado en `DEFAULT_REQUEST_HEADERS`.

Si una solicitud específica tiene su propio encabezado `User-Agent` definido, ese valor se utilizará en lugar del User-Agent predeterminado. Esto proporciona flexibilidad para cambiar el User-Agent en solicitudes individuales según sea necesario.

```python
DEFAULT_REQUEST_HEADERS = {
    'User-Agent': 'user-agent propio'
}
```

#### Cambiar el header de las peticiones

Para esto tenemos que reescribir el metodo `start_requests` y editar su `header` para añadirle nuestro `User-Agent` personalizado. Esta funcion es la funcion principal de nuestra araña, la que la inicializa. Por eso el el callback se llama al metodo `parse`.

```python
def start_requests(self):
    yield scrapy.Request(url='url de inicio', callback=self.parse, headers={
        'User-Agent': 'user-agent propio'
    })
```

Este cambio es aplicable a cualqueir request que hagamos para acceder a cualqueir pagina web, es decir no solo a la pagina de inicio. Es mas en este solo al llamar la pagina de inicio el `header` estara cambiado, en todoas las demas peticiones estar puesto el predefinido.

{% hint style="info" %}
El `User-Agent` solo se puede cambiar al hacer peticiones con `scrapy.Request`, no se puede con `response.follow`
{% endhint %}
