# CSV y JSON

Una vez creado el spider que extraerá datos de un sitio web hay guardar la informacion en algún lugar. Una de las formas más fáciles de guardar datos de raspado es en un archivo CSV o JSON.

### Scrapy Feed Exporters

La necesidad de guardar los datos scrapeados en un archivo es un requisito muy común para los desarrolladores, por lo que para facilitarnos la tarea, los desarrolladores de Scrapy han implementado los Exportadores de Alimentación.

Los Feed Exporters son una caja de herramientas lista para usar que nos permite guardar/exportar fácilmente nuestros datos scrapeados en los siguientes formatos:

* Formato JSON y JSON lines
* Formato CSV
* Formato XML
* Formato pickle de Python

Y guardarlos en:

* La máquina local donde se está ejecutando Scrapy
* Una máquina remota utilizando FTP (protocolo de transferencia de archivos)
* Almacenamiento en Amazon S3
* Almacenamiento en Google Cloud Storage
* Salida estándar

En esta guía, aprenderas sobre las diferentes formas en las que puedes guardar archivos JSON desde Scrapy.

### A traves de la linea de comandos

Para guardar en un archivo CSV, agrega la bandera `-o` al comando `scrapy crawl` junto con la ruta del archivo donde deseas guardar los datos. Tambien es posible usar la opcion `-O`.

<table><thead><tr><th width="199">Flag</th><th>Description</th></tr></thead><tbody><tr><td><code>-o</code></td><td>Añadir informacion aun fichero existente</td></tr><tr><td><code>-O</code></td><td>Reescriber un el fichero existente</td></tr></tbody></table>

Puedes establecer una ruta relativa de la siguiente manera:

```bash
scrapy crawl bookspider -o bookspider_data.csv
```

O si no puedes indicar la ruta absoluta:

```bash
scrapy crawl bookspider -o file:///path/to/my/project/bookspider_data.csv
```

### Guardar la informacion con Feeds Settings

A menudo, la opción más limpia es decirle a Scrapy que guarde los datos en un CSV a través de la configuración FEEDS.

Paa ello, en el archivo `settings.py`, podemos establecer la opción `FEED` para definir el formato y la ubicación de salida de los datos scrapeados. A continuación, un ejemplo:

```python
# settings.py

FEEDS = {
    'data.csv': {'format': 'csv'}
}
```

Tambien es posible especificar el formato de salida para cada spider. PAra ello tan solo hay que añadir la propiedad `custom_setting` a la spider:

```python
custom_settings = {
        'FEEDS': { 'data.csv': { 'format': 'csv',}}
}
```

#### Dynamic File Paths/Names <a href="#1-setting-dynamic-file-pathsnames" id="1-setting-dynamic-file-pathsnames"></a>

Establecer una ruta de archivo estática está bien para el desarrollo o proyectos muy pequeños, sin embargo, cuando esté en producción, es probable que no desee que todos sus datos se guarden en un archivo grande. Entonces, para resolver esto, Scrapy le permite crear rutas / nombres de archivos dinámicos usando variables de araña.

Por ejemplo, aquí indique crear un CSV para los datos en la carpeta de datos, seguido de la subcarpeta con el nombre de las spiders y un nombre de archivo que incluya el nombre de la spider y la fecha en que se extrajo.

```python
# settings.py 

FEEDS = {
    'data/%(name)s/%(name)s_%(time)s.csv': {
        'format': 'csv',
        }
}
```

La ruta generada se vería así:

```
"data/bookspider/bookspider_2022-05-18T07-47-03.csv"
```

#### Configuraciones extra

La funcionalidad **Feeds** tiene otras configuraciones que puede configurar pasando pares clave/valor al diccionario `FEEDS` que defina.

<table><thead><tr><th width="217"></th><th></th></tr></thead><tbody><tr><td><code>encoding</code></td><td>La codificación que se utilizará para el feed. Si no se configura o se establece en Ninguno (predeterminado), usa UTF-8 para todo, excepto para la salida JSON, que usa codificación numérica segura (secuencias \uXXXX) por razones históricas.</td></tr><tr><td><code>fields</code></td><td>Una lista de campos para exportar, que le permite guardar solo ciertos campos de sus artículos.</td></tr><tr><td><code>item_classes</code></td><td>Una lista de clases de elementos para exportar. Si no está definido o está vacío, se exportan todos los elementos.</td></tr><tr><td><code>item_filter</code></td><td>Una clase de filtro para filtrar elementos para exportar. <code>ItemFilter</code> se utiliza por defecto.</td></tr><tr><td><code>indent</code></td><td>Cantidad de espacios usados ​​para tabular la salida en cada nivel.</td></tr><tr><td><code>store_empty</code></td><td>Si exportar feeds vacíos (es decir, feeds sin artículos).</td></tr><tr><td><code>uri_params</code></td><td>Una cadena con la ruta de importación de una función para establecer los parámetros que se aplicarán con el formato de cadena estilo printf al URI del feed.</td></tr><tr><td><code>postprocessing</code></td><td>Lista de complementos a utilizar para el posprocesamiento.</td></tr><tr><td><code>batch_item_count</code></td><td>Si se le asigna un número entero superior a 0, Scrapy genera varios archivos de salida que almacenan hasta el número especificado de elementos en cada archivo de salida.</td></tr></tbody></table>

Por ejemplo:

```python
# settings.py 

FEEDS = {
    'data/%(name)s/%(name)s_%(time)s.csv': {
        'format': 'csv',
        'encoding': 'utf8',
        'store_empty': False,
        'item_classes': [MyItemClass1, 'myproject.items.MyItemClass2'],
        'fields': None,
        'indent': 4,
        'item_export_kwargs': {
           'export_empty_fields': True,
        },
        }
}
```

#### Saving Data To Multiple CSV File Batches <a href="#saving-data-to-multiple-csv-file-batches" id="saving-data-to-multiple-csv-file-batches"></a>

Dependiendo de su trabajo, es posible que desee almacenar los datos extraídos en numerosos lotes de archivos en lugar de en un archivo CSV grande para que sea más manejable. Scrapy hace que sea muy fácil hacer esto con la clave `batch_item_count` que puede configurar en la configuración de **FEEDS**.

Simplemente configure agregar la clave `batch_item_count` a la configuración de su Feed y configure la cantidad de elementos que desea en cada archivo. Esto iniciará un nuevo archivo CSV cuando alcance este límite.

{% hint style="info" %}
**Nota**: También deberá agregar al menos uno de los siguientes marcadores de posición en el URI del feed para indicar cómo se generan los diferentes nombres de archivos de salida:
{% endhint %}

| Placehold       | Description                                          |
| --------------- | ---------------------------------------------------- |
| %(batch\_time)s | Inserta una marca de tiempo cuando se crea el lote   |
| %(batch\_id)d   | Inserta un número de secuencia basado en 1 del lote. |

Por ejemplo, esta configuración de Feed dividirá los datos en numerosos lotes de igual tamaño (excepto el último lote):

```python
# settings.py 

FEEDS = {
    'data/%(name)s/%(name)s_batch_%(batch_id)d.csv': {
        'format': 'csv',
        'batch_item_count': 10,
        }
}
```

Este seria el resultado:

```bash
"data/bookspider/bookspider_batch_1.csv"
"data/bookspider/bookspider_batch_2.csv"
"data/bookspider/bookspider_batch_3.csv"
"data/bookspider/bookspider_batch_4.csv"
"data/bookspider/bookspider_batch_5.csv"
"data/bookspider/bookspider_batch_6.csv"
```
