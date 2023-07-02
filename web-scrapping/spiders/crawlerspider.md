# CrawlerSpider

CrawlerSpider es una clase de araña especializada en el framework Scrapy que facilita la creación de arañas de rastreo web avanzadas. Esta clase está diseñada específicamente para la extracción estructurada de datos de sitios web mediante el seguimiento de enlaces y la navegación automática por las páginas.

Para crear un `CrawSpider` escribe el siguiente comando:

```bash
scrapy genspider -t crawl [name] [url]
```

### **Características de CrawlerSpider**

1. **Reglas de rastreo configurables:** CrawlerSpider permite definir reglas de rastreo configurables que especifican cómo se deben seguir los enlaces y cuáles son las páginas objetivo para la extracción de datos.
2. **Extracción estructurada:** Permite realizar la extracción estructurada de datos utilizando selectores XPath o CSS para identificar y capturar elementos específicos de las páginas web.
3. **Recursividad automática:** CrawlerSpider se encarga automáticamente de seguir los enlaces dentro de las páginas objetivo definidas, lo que permite el rastreo en profundidad de un sitio web.
4. **Configuración centralizada:** Proporciona una forma conveniente de centralizar la configuración de rastreo, lo que facilita la gestión y mantenimiento de múltiples arañas.

```python
import scrapy
from scrapy.linkextractors import LinkExtractor
from scrapy.spiders import CrawlSpider, Rule

class MySpider(CrawlSpider):
    name = 'my_spider'
    allowed_domains = ['example.com']
    start_urls = ['http://www.example.com']

    rules = (
        Rule(LinkExtractor(allow=r'category\.php'), callback='parse_category', follow=True),
    )

    def parse_category(self, response):
        # Lógica de extracción de datos
```

### Reglas

Las reglas de CrawlerSpider en Scrapy son una característica clave que permite definir cómo se deben seguir los enlaces y cuáles son las páginas objetivo para la extracción de datos durante el proceso de rastreo web.&#x20;

Estas reglas proporcionan flexibilidad y control sobre el comportamiento de la araña, permitiendo una extracción estructurada y eficiente de información de múltiples páginas web.

```python
rules = (
    Rule(LinkExtractor(allow=r'category\.php'), callback='parse_category', follow=True),
)
```

Puedes crear todas las reglas que desees y estas sen van cumpliendo una a una, es decir una vez se scrapeen todos los enlaces encontrados mediante una regla, se ejecutara la siguiente regla.

**Estructura de las reglas**

Las reglas en CrawlerSpider están compuestas por tres elementos principales:

1. **LinkExtractor:** Es una clase de Scrapy que define los criterios para seleccionar los enlaces que la araña debe seguir. Se pueden configurar varios parámetros, como expresiones regulares para el patrón de URL, restricciones de dominio, reglas para excluir o incluir enlaces, entre otros.
2. **Callback:** Es el método de la araña que se ejecutará cuando se siga un enlace que cumple con los criterios definidos en el LinkExtractor. En este método, se realiza la extracción de datos de la página objetivo.
3. **Follow (opcional):** Indica si la araña debe seguir los enlaces encontrados en las páginas objetivo. Si se establece en True, la araña continuará el proceso de rastreo siguiendo los enlaces de manera recursiva. Si se establece en False, la araña solo extraerá datos de las páginas objetivo sin seguir enlaces adicionales.

> La funcion del `callback` nunca puede llamarse solo `parse`

**Principales parámetros de LinkExtractor**

`LinkExtractor` extrae todos los enlaces del documentos HTML que cumplan las reglas especificadas mediante una de las siguientes opciones:

1. **`allow`:** Este parámetro permite filtrar los enlaces que se deben seguir en función de una expresión regular que coincida con la URL. Por ejemplo, `allow=r'category\.php'` permitiría seguir enlaces que contengan "category.php" en la URL.
2. **`deny`:** Permite excluir enlaces basados en una expresión regular. Los enlaces que coincidan con esta expresión no serán seguidos.
3. **`allow_domains`:** Se utiliza para filtrar los enlaces por dominio. Solo se seguirán los enlaces cuyo dominio esté incluido en la lista `allow_domains`.
4. **`deny_domains`:** Permite excluir enlaces por dominio. Los enlaces cuyo dominio esté en la lista `deny_domains` no serán seguidos.
5. **`restrict_xpaths`:** Este parámetro acepta una lista de selectores XPath. Solo se seguirán los enlaces que estén dentro de los elementos seleccionados por estos selectores.
6. **`restrict_css`:** Permite especificar un selector CSS para restringir la búsqueda de enlaces dentro de un subconjunto de elementos HTML en lugar de buscar en toda la página.

### User-Agent

Al igual que con las spiders con las CrawlerSpiders tambien se puede cambiar el User-Agent de las mismas [maneras](./#user-agent), pero el header de las peticiones se camba de una manera distinta devio a que estas spider funcionan con reglas.

Con las CrawlerSpider tambien tenemos que reescribir la funcion `start_request`, pero sin el argumento `callback`:

```python
user_agent = 'user-agent propio'

def start_requests(self):
    yield scrapy.Request(url='url de inicio', headers={
        'User-Agent': self.user_agent
    })
```

Esto cambiara el user agent a la primera peticion, pero si queremos cambair el User-Agent de cada regal lo tenemos que hacer mediante una funcion externa que llamaremos a traves de cada regla:

```python
rules = (
        Rule(LinkExtractor(allow=r'category\.php'), callback='parse_category', 
        follow=True, process_request='set_user_agent'),
)
    
def set_user_agent(self, request, spider):
    request.headers['User-Agent'] = self.user_agent
    return request
```

{% hint style="info" %}
Si etas usando una version de `scrapy 2.0` o mayor es necesario que la funcion `set_user_Agent` tenga el argumento `spider`.
{% endhint %}
