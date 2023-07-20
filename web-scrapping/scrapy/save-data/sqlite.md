# SQLite

SQLite es un motor de base de datos relacional que permite almacenar, consultar y manipular datos estructurados. Se utiliza ampliamente en aplicaciones que requieren una base de datos local y no necesitan una infraestructura de servidor compleja. Por ejemplo, se puede emplear en aplicaciones móviles, aplicaciones de escritorio y pequeñas aplicaciones web.

### Ventajas y Desventajas de SQLite

#### **Ventajas**

1. **Ligereza**: SQLite no requiere una instalación de servidor adicional y se ejecuta dentro del propio proceso de la aplicación, lo que implica un bajo consumo de recursos.
2. **Portabilidad**: Al ser una base de datos de archivo único, es fácil moverla y transportarla entre sistemas operativos y dispositivos.
3. **Rendimiento**: La arquitectura sin servidor de SQLite lo convierte en una opción eficiente para operaciones de acceso a datos rápidas y locales.
4. **Simplicidad**: La sintaxis SQL de SQLite es fácil de entender y su modelo de datos es simple de manejar.

#### **Desventajas**

1. **Capacidad Limitada**: SQLite es ideal para aplicaciones con cantidades moderadas de datos. Para proyectos con grandes volúmenes de datos y operaciones concurrentes, otras bases de datos como MySQL o PostgreSQL pueden ser más adecuadas.
2. **Acceso Concurrente Limitado**: SQLite no es óptimo para aplicaciones con múltiples usuarios que requieran acceso simultáneo y concurrencia en escritura intensiva.
3. **Escalabilidad**: Si se espera un crecimiento significativo en el volumen de datos, puede ser más complicado escalar SQLite que otras bases de datos orientadas a servidores.

### **Cuándo Usar y No Usar SQLite**

#### **Cuándo Usar SQLite:**

1. **Aplicaciones de Pequeña Escala**: SQLite es ideal para aplicaciones con volúmenes moderados de datos y poca concurrencia, como aplicaciones móviles, pequeñas aplicaciones web o prototipos.
2. **Aplicaciones Sin Servidor**: SQLite es una excelente opción para aplicaciones sin una infraestructura de servidor, ya que su ligereza y capacidad de almacenar la base de datos en un único archivo la hacen fácil de distribuir y utilizar en diferentes entornos.
3. **Proyectos Individuales o de Desarrollo**: En el desarrollo de proyectos individuales o de prueba, donde la simplicidad y facilidad de integración son esenciales, SQLite ofrece una solución rápida y eficiente.

#### **Cuándo No Usar SQLite:**

1. **Aplicaciones Escalables**: Si se espera un crecimiento significativo en la cantidad de datos o se requiere acceso concurrente a gran escala, otras bases de datos más robustas como MySQL o PostgreSQL son más apropiadas para garantizar un rendimiento óptimo.
2. **Aplicaciones con Altas Demandas de Escritura Concurrente**: Si la aplicación necesita un alto rendimiento en escritura y acceso concurrente para múltiples usuarios, es mejor considerar bases de datos diseñadas específicamente para esta situación.

### Como guarda la informacion?

SQLite viene con Python, por lo que no necesita instalar nada para usarlo en tus proyectos Scrapy. Tan solo, instalar e importar `sqlite3` a nuestro archivo `pipelines.py`.

#### Abiri o crea la base de datos

Dentro del método **`open_spider`**, configuraremos el pipeline para hacer lo siguiente cada vez que una spider active el pipeline:

* Intenta conectarse a la base de datos `demo.db`,  si no existe la crea.
* Cree un cursor que usaremos para ejecutar comandos SQL en la base de datos.
* Cree una nueva tabla de `quotes` con las columnas `text`, `tags` y `author`, si aún no existe una en la base de datos.

```python
# pipelines.py

import sqlite3

class SqliteDemoPipeline:

    def open_spider(self, spider):

        ## Create/Connect to database
        self.connection = sqlite3.connect('demo.db')

        ## Create cursor, used to execute commands
        self.cur = self.con.cursor()
        
        ## Create quotes table if none exists
        self.cur.execute("""
        CREATE TABLE IF NOT EXISTS quotes(
            text TEXT,
            tags TEXT,
            author TEXT
        )
        """)
        self.connection.commit()
        
    def close_spider(self, spider):
        self.client.close()
```

#### Guardar los datos

A continuación, vamos a utilizar el evento `process_item` dentro de nuestro pipeline  para almacenar los datos que recopilamos en nuestra base de datos SQLite.

El `process_item` se activará cada vez que nuestra spider extraiga un elemento, por lo que debemos configurar el método `process_item` para insertar los datos de los elementos en la base de datos.

```python
# pipelines.py

import sqlite3

class SqliteDemoPipeline:

    def __init__(self):
        # Crear o abrir la base de datos
        # ...

    def process_item(self, item, spider):

        ## Define insert statement
        self.cur.execute("""
            INSERT INTO quotes (text, tags, author) VALUES (?, ?, ?)
        """,
        (
            item['text'],
            str(item['tags']),
            item['author']
        ))

        ## Execute insert of data into database
        self.connection.commit()
        return item
```

En el caso de que queira evitar elementos repetido en tu base de datos puede usar el sigueinte metodo `process_item`:

```python
    def process_item(self, item, spider):

        ## Check to see if text is already in database 
        self.cur.execute("select * from quotes where text = ?", (item['text'],))
        result = self.cur.fetchone()

        ## If it is in DB, create log message
        if result:
            spider.logger.warn("Item already in database: %s" % item['text'])
        
        ## If text isn't in the DB, insert data
        else:

            ## Define insert statement
            self.cur.execute("""
                INSERT INTO quotes (text, tags, author) VALUES (?, ?, ?)
            """,
            (
                item['text'],
                str(item['tags']),
                item['author']
            ))

            ## Execute insert of data into database
            self.con.commit()
        
        return item
```
