# Selenium

Selenium es una herramienta de automatización de pruebas y scrapeo web que permite controlar y manipular navegadores web de forma programática. Permite simular interacciones humanas en una página web, automatizar pruebas funcionales, extraer datos y realizar tareas repetitivas en aplicaciones web, todo a través de su API fácil de usar y soporte para varios navegadores.

Su instalacion es muy sencilla tansolo tienes que instalarlo con `pip insatall` y despues instalar el Driver que desees utilzar. Aqui tienes una guia

{% embed url="https://selenium-python.readthedocs.io/installation.html" %}

### Webdriver

El webdriver de Selenium es una herramienta popular y potente para la automatización de pruebas y el scrapeo web. Permite controlar un navegador web real o un navegador en modo headless para interactuar con páginas web, realizar acciones y extraer datos de manera programática.

Para poder utilizarlo una vez lo hayamos instalado, tan solo tenemos que instanciarlo en nuestro script:

```python
from selenium import webdriver

driver = webdriver.Chrome(executable_path="./chromedriver.exe")
driver.get("https://duckduckgo.com")
driver.close()
```

Con este codido establecemos que vamos a utilizar el driver de google chrome que esta en el directorio actual y mediante ese driver abriremos en el navegador la pagina `duckduckgo.com`. Una vez abierto lo cerraremos con `driver.close()`. Esto es necesario si no se llenara la memoria.

Sin embargo hay una manera mas eficiente inicializar el webdriver sin tener que especifcar la ruta del driver:

```python
from selenium import webdriver
from shutil import wich

chrome_path = which("chromedriver")
driver = webdriver.Chrome(executable_path="chrome_path)
driver.get("https://duckduckgo.com")
driver.close()
```

En ete ejemplo estamos utilizando la funcion `which` de la libreria `shutil` para bsucar el drive de crome ya que esta funcion sirve para buscar la ruta de un archivo ejecutable en el sistema operativo.

#### Headless

La opción `headless` en Selenium se utiliza para ejecutar el navegador en modo sin interfaz gráfica. Es una buena práctica usar esta opción en la automatización de pruebas y otras tareas donde no se requiere ver el navegador. Proporciona beneficios como mayor eficiencia, rendimiento y escalabilidad al eliminar la necesidad de mostrar la interfaz gráfica.

Para implemntarlo tan solohay que hacer lo siguiente:

```python
from selenium import webdriver
from selenium.webdriver.chrome.options import Options

# Configuración de opciones de Chrome
options = Options()
options.headless = True

# Creación de una instancia del webdriver de Chrome con opciones
driver = webdriver.Chrome(options=options)
```

### **Búsqueda de elementos**

En Selenium, la búsqueda y manipulación de elementos en una página web es una parte fundamental de la automatización de pruebas y el scrapeo web. En este artículo, exploraremos las distintas maneras de buscar elementos con Selenium y cómo utilizar los métodos adecuados para acceder y manipularlos.

#### **Búsqueda por ID**

La búsqueda por ID es una forma común y eficiente de localizar elementos en una página web. Utiliza el método `find_element_by_id` para buscar un elemento específico por su ID único. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_id('my-element-id')
```

#### **Búsqueda por nombre de etiqueta**

Otra manera de buscar elementos es por el nombre de etiqueta HTML. Utiliza el método `find_element_by_tag_name` para buscar un elemento por su nombre de etiqueta. Por ejemplo:

```python
element = driver.find_element_by_tag_name('a')
```

#### **Búsqueda por clase**

Puedes buscar elementos por su clase utilizando el método `find_element_by_class_name`. Este método devuelve el primer elemento que coincide con la clase especificada. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_class_name('my-class')
```

#### **Búsqueda por selector CSS**

Selenium también permite buscar elementos utilizando selectores CSS. Utiliza el método `find_element_by_css_selector` para buscar elementos que coincidan con un selector CSS específico. Por ejemplo:

```python
element = driver.find_element_by_css_selector('.my-class > .child-element')
```

{% hint style="info" %}
Mientras que la búsqueda por clase se limita a buscar elementos por su clase CSS exacta, los selectores CSS permiten especificar condiciones adicionales y jerarquías más complejas para encontrar elementos específicos
{% endhint %}

#### **Búsqueda por XPath**

XPath es otra forma poderosa de buscar elementos en una página web. Utiliza el método `find_element_by_xpath` para buscar elementos que coincidan con una expresión XPath específica. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_xpath('//div[@class="my-class"]')
```

### **Acciones sobre elementos**

En Selenium, la interacción con elementos de una página web es fundamental para realizar tareas automatizadas y pruebas funcionales. En este artículo, exploraremos las distintas acciones que se pueden realizar sobre un elemento utilizando Selenium, como enviar texto, hacer clic, obtener atributos y más.

#### **Enviar texto a un elemento**

Enviar texto a un elemento es una acción común en la automatización de pruebas y el scrapeo web. Utiliza el método `send_keys` para ingresar texto en un campo de entrada. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_id('my-element-id')
element.send_keys('Texto de ejemplo')
```

En este caso, el método `send_keys` se utiliza para ingresar el texto "Texto de ejemplo" en el elemento identificado por su ID único.

#### **Hacer clic en un elemento**

Hacer clic en un elemento es una acción común para interactuar con enlaces, botones u otros elementos interactivos. Utiliza el método `click` para simular un clic en un elemento. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_css_selector('.my-button')
element.click()
```

En este ejemplo, el método `click` se utiliza para hacer clic en el elemento con la clase CSS "my-button".

#### **Obtener atributos de un elemento**

Puedes obtener atributos específicos de un elemento utilizando el método `get_attribute`. Esto es útil para extraer información relevante de elementos, como URLs de imágenes o valores de atributos personalizados. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_tag_name('img')
image_src = element.get_attribute('src')
```

En este caso, se utiliza el método `get_attribute` para obtener el valor del atributo "src" del elemento de imagen.

#### **Obtener texto de un elemento**

Para obtener el texto visible de un elemento, puedes utilizar el atributo `text` o el método `get_text`. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_css_selector('.my-element')
text = element.text
```

En este ejemplo, se utiliza el atributo `text` para obtener el texto visible del elemento con la clase CSS "my-element".

#### **Esperar a que un elemento esté visible**

A veces, es necesario esperar a que un elemento esté visible antes de interactuar con él. Utiliza el método `WebDriverWait` junto con las condiciones de espera predefinidas, como `visibility_of_element_located`, para esperar a que un elemento esté visible. Por ejemplo:

```python
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC

# Esperar hasta que el elemento esté visible
wait = WebDriverWait(driver, 10)
element = wait.until(EC.visibility_of_element_located((By.ID, 'my-element-id')))
```

En este ejemplo, se utiliza `WebDriverWait` junto con la condición `visibility_of_element_located` para esperar hasta que el elemento con el ID "my-element-id" esté visible.

#### **Limpiar un campo de entrada**

Si deseas borrar el contenido de un campo de entrada antes de enviar nuevo texto, puedes utilizar el método `clear`. Aquí tienes un ejemplo:

```python
element = driver.find_element_by_id('my-input-field')
element.clear()
```

En este caso, el método `clear` se utiliza para borrar el contenido del campo de entrada identificado por su ID único.

#### **Realizar acciones de teclado**

Selenium también permite simular acciones de teclado, como pulsar teclas especiales o realizar combinaciones de teclas. Puedes utilizar la clase `Keys` para enviar teclas específicas. Aquí tienes un ejemplo:

```python
from selenium.webdriver.common.keys import Keys

# Enviar teclas especiales
element.send_keys(Keys.ENTER)

# Combinación de teclas
element.send_keys(Keys.CONTROL + 'a')
```

En este ejemplo, se envía la tecla "Enter" al elemento y se realiza la combinación de teclas "Control + a" para seleccionar todo el texto en un campo de entrada.

### scrapy-selenium

Scrapy-Selenium es una extensión de Scrapy que combina Selenium y Scrapy para el scrapeo de sitios web dinámicos. Permite interactuar con JavaScript y extraer datos de manera eficiente. Con Scrapy-Selenium, obtienes lo mejor de ambos mundos: la potencia de Selenium y las capacidades avanzadas de scrapeo de Scrapy. Es ideal para scrapear sitios web complejos.

{% embed url="https://scrapeops.io/python-scrapy-playbook/scrapy-selenium/" %}

#### Integrar selenium en scrapy

Para empezar necesitas instalar la libreria `scrapy-splash` con el siguiente comando:

```bash
pip install scrapy-selenium
```

A continuación, para integrar scrapy-selenium en el proyecto hay que actualiar el archivo settings.py con la siguiente configuración si usa un controlador de Chrome:

```python
## settings.py

# for Chrome driver 
from shutil import which
  
SELENIUM_DRIVER_NAME = 'chrome'
SELENIUM_DRIVER_EXECUTABLE_PATH = which('chromedriver')
SELENIUM_DRIVER_ARGUMENTS=['--headless']  
  
DOWNLOADER_MIDDLEWARES = {
     'scrapy_selenium.SeleniumMiddleware': 800
     }
```

O estas configuraciones si usa un controlador FireFox:

```python
## settings.py

# For Firefox driver 
from shutil import which
  
SELENIUM_DRIVER_NAME = 'firefox'
SELENIUM_DRIVER_EXECUTABLE_PATH = which('geckodriver')
SELENIUM_DRIVER_ARGUMENTS=['--headless']  
  
DOWNLOADER_MIDDLEWARES = {
     'scrapy_selenium.SeleniumMiddleware': 800
     }
```

#### Usar selenium desde scrapy

Para implementar código de Selenium en un spider de Scrapy utilizando `scrapy-selenium`, puedes utilizar el objeto `self.browser` o  `response.meta['driver']` proporcionado por la extensión. Aquí tienes un ejemplo:

```python
import scrapy
from scrapy_selenium import SeleniumRequest

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['http://example.com']

    def start_requests(self):
        for url in self.start_urls:
            yield SeleniumRequest(
                url=url,
                wait_time=3,
                screenshot=True,
                callback=self.parse
            )

    def parse(self, response):
        driver = response.meta['driver']
        driver = self.browser

        # Ejemplo de uso de Selenium
        search_input = driver.find_element_by_xpath("//h1")
        text = search_input.text
```

Una vez hays realizado todas las acciones que dees con selenium puede qe el codigo fuente hay cambaido. De ser asi ahora las acciones de scrappy no podremos realizarlas sobre `request` si no sobre un nuevo codigo fuente proprocionado por selenium. Esto se hace de la sigueinte manera:

```python
import scrapy
from scrapy_selenium import SeleniumRequest
from scrapy.slector import Selector

class MySpider(scrapy.Spider):
    name = 'my_spider'
    start_urls = ['http://example.com']

    def start_requests(self):
        #yield SeleniumRequest

    def parse(self, response):
    driver = response.meta['driver']
        # Acciones con selenium
        # ...
        
        html = driver.page_source
        response_obj = Selector(text=html)
        
        link = response_obj.xpath("//h1")
```
