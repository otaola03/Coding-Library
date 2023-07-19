# Process data

La organización de la información con Scrapy es clave en el proceso de web scraping. Scrapy ofrece la opción ideal de utilizar el atributo `items` para estructurar y almacenar los datos extraídos en lugar de utilizar diccionarios. Esto permite una gestión más eficiente de los datos y facilita su posterior uso, análisis y almacenamiento.

### Items

Los "Items" de Scrapy son simplemente una estructura de datos predefinida que almacena tus datos. El uso de "Items" de Scrapy tiene varias ventajas:

* Una forma más estructurada de almacenar datos.
* Facilita el uso de `Item Pipelines` y `Item Loaders` de Scrapy.
* Permite configurar pruebas unitarias con extensiones de Scrapy como `Spidermon`.

#### **Definiendo el modelo de datos con el atributo `items`**

Cuando trabajamos con Scrapy, el atributo "items" juega un papel fundamental para organizar los datos extraídos de las páginas web. Al definir un modelo de datos utilizando este atributo, podemos estructurar la información en campos específicos y asegurarnos de que siga un formato coherente.

Esto se logra creando una nueva clase hija de la clase `scrapy.Item` en el fichero `items.py` cread por defecto por scrapy:

```python
import scrapy

class ProductItem(scrapy.Item):
    title = scrapy.Field()
    price = scrapy.Field()
    description = scrapy.Field()
```

En este ejemplo, hemos creado un modelo de datos llamado `ProductItem` utilizando el atributo `items`. Hemos definido tres campos: `title`, `price` y `description`. Cada campo representa una propiedad de los productos que deseamos extraer.

#### **Almacenando datos en el atributo `items` durante el scrapeo**

Una vez que hemos definido el modelo de datos, podemos utilizar el atributo "items" para almacenar los datos extraídos en cada instancia del modelo. Esto nos permite estructurar y organizar la información de manera consistente.

```python
pythonCopy codeimport scrapy

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['http://example.com']

    def parse(self, response):
        item = ProductItem()
        item['title'] = response.css('.product-title::text').get()
        item['price'] = response.css('.product-price::text').get()
        item['description'] = response.css('.product-description::text').get()
        yield item
```

En este ejemplo, hemos definido una araña llamada `MySpider`. Dentro del método `parse`, creamos una instancia de `ProductItem` y asignamos los valores extraídos de la página a los campos correspondientes. Luego, utilizamos `yield` para enviar el item al pipeline de Scrapy y almacenarlo.

### Item Loader

Cuando se trabaja con Scrapy, el uso de Item Loader proporciona una forma estructurada y eficiente de cargar datos en los ítems de la araña. Los Item Loaders facilitan la limpieza, transformación y validación de los datos extraídos antes de almacenarlos en los campos del ítem.

#### Configuración de un Item Loader

Para utilizar un Item Loader, primero se debe crear una subclase de `ItemLoader` e indicar el ítem al que se asociará. Esto normalmente se hace en un fichero aparte en la raiz del proyecto. A continuación, se pueden definir los campos del ítem y configurar los procesadores de entrada y salida para cada campo según sea necesario.

```python
from scrapy.loader import ItemLoader
from myproject.items import ProductItem

class ProductLoader(ItemLoader):
    default_item_class = ProductItem #Opcional
    
    name_in = MapCompose(str.strip)
    price_out = MapCompose(lambda x: x.split("£")[-1])
```

Los procesadores para campos específicos se definen utilizando los sufijos `_in` y `_out` para los procesadores de entrada y salida, respectivamente. En nuestro ejemplo, estamos declarando procesadores de entrada para los campos de precio (`price`) y URL (`url`).

* **Nombre**: el procesador de entrada `MapCompose(str.strip)` que elimina los espacios en blanco alrededor del nombre.
* **Precio**: El procesador de entrada para el precio dividirá cualquier valor pasado a él en el signo `£` y utilizará el segundo valor.

{% hint style="info" %}
**`MapCompose`** es un procesador de datos proporcionado por Scrapy que se utiliza para aplicar una o varias funciones a los valores extraídos de un campo antes de asignarlos al ítem.
{% endhint %}

#### Uso del Item Loader

A continuación se muestra un ejemplo de cómo se puede utilizar un Item Loader en una araña de Scrapy:

```python
from scrapy import Spider
from myproject.items import ProductItem
from myproject.loaders import ProductLoader

class MySpider(Spider):
    name = 'myspider'
    start_urls = ['http://example.com']

    def parse(self, response):
        loader = ProductLoader(item=ProductItem(), response=response)
        loader.add_xpath('name', '//h1/text()')
        loader.add_css('price', '.product-price::text')

        product_item = loader.load_item()
        yield product_item
```

En este ejemplo, se crea una instancia del Item Loader `ProductLoader` y se utilizan los métodos `add_xpath` y `add_css` para extraer y cargar los datos en los campos correspondientes del ítem. El ítem final se obtiene llamando al método `load_item()` y se devuelve utilizando `yield`.

### Pipelines

En Scrapy, los Pipelines son componentes que nos permiten procesar y almacenar los datos extraídos por nuestras arañas de manera estructurada. Los Pipelines son ideales para realizar tareas como limpiar y validar los datos, eliminar duplicados, almacenarlos en una base de datos u otros sistemas de almacenamiento, generar informes, etc.

#### Declaración y activación de los Pipelines

Para utilizar los Pipelines en Scrapy, debemos definirlos en el archivo `pipelines.py` de nuestro proyecto. Cada Pipeline es una clase que implementa una serie de métodos especiales, como `open_spider`, `close_spider`, `process_item`, y más. Luego, debemos configurar el orden de ejecución de los Pipelines y activarlos en el archivo `settings.py`.

Por ejemplo si creamos el siguiente pipeline:

```python
import csv

class MyPipeline:
    def open_spider(self, spider):
        self.file = open('data.csv', 'w', newline='')
        self.writer = csv.writer(self.file)
        self.writer.writerow(['title', 'price'])

    def process_item(self, item, spider):
        self.writer.writerow([item['title'], item['price']])
        return item

    def close_spider(self, spider):
        self.file.close()
```

Para poder activarlo hay que indicarlo en el archivo `setting.py` de la siguiente manera:

```python
ITEM_PIPELINES = {
    'myproject.pipelines.MyPipeline': 300,
    # Otros Pipelines...
}
```

En el ejemplo anterior, `'myproject.pipelines.MyPipeline'` es el nombre de tu Pipeline y `300` es la prioridad de ejecución. Puedes ajustar la prioridad según el orden en el que deseas que se ejecuten los Pipelines. Los valores más bajos tienen prioridad más alta.

#### Método `open_spider`

Este método se llama al inicio de la araña y se utiliza para realizar tareas de inicialización, como abrir archivos o conexiones a bases de datos.

```python
class MyPipeline:
    def open_spider(self, spider):
        # Inicialización de recursos
```

#### Método `close_spider`

Este método se llama al finalizar la araña y se utiliza para cerrar cualquier recurso abierto, como archivos o conexiones a bases de datos.

```python
class MyPipeline:
    def close_spider(self, spider):
        # Cierre de recursos
```

#### Método `process_item`

Este método se llama para cada ítem extraído por la araña y se utiliza para realizar el procesamiento principal de los datos. Aquí podemos aplicar transformaciones, limpiar los valores, validar la estructura y guardar los datos en la salida deseada.

```python
class MyPipeline:
    def process_item(self, item, spider):
        # Procesamiento de datos
        return item
```

#### Método `from_crawler`

Este método de clase se utiliza para obtener parámetros de configuración del objeto `Crawler`. Es útil para inicializar variables o recursos basados en la configuración de la araña. Es decir sirve para obtener valores del fichero `setting.py`.

```python
class MyPipeline:
    @classmethod
    def from_crawler(cls, crawler):
        carwler.setting.get("VARIABLE_NAME")
        # Obtener configuración de la araña
        return cls()
```
