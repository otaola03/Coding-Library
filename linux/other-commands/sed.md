---
description: Buscar, buscar y reemplazar, insertar o eliminar
---

# Sed

El comando SED en UNIX es sinónimo de editor de flujo y puede realizar muchas funciones en archivos como buscar, encontrar y reemplazar, insertar o eliminar. Aunque el uso más común del comando SED en UNIX es para sustitución o para buscar y reemplazar. Al usar SED, puede editar archivos incluso sin abrirlo, que es una forma mucho más rápida de encontrar y reemplazar algo en el archivo, que primero abrir ese archivo en VI Editor y luego cambiarlo.

### Sintaxis

El comando SED funciona con **órdenes** y se aplica a los archivos. Tanto el propio comando como las órdenes pueden ampliarse mediante parámetros.

```
sed [parámetro(s)] 'orden(es)' [archivo(s)]
```

Puedes introducir las órdenes de manera directa dentro del comando SED o hacer que sean **leídas de un archivo**. En este último caso, debes introducir la ruta del archivo en lugar de la orden.

### Parámetros

Para el comando SED, los parámetros son especialmente importantes ya que solo a través de ellos queda claro cómo debe interpretarse el comando que viene a continuación. Existen los siguientes parámetros:

| Flags | Descripcion                                                                |
| ----- | -------------------------------------------------------------------------- |
| -e    | Hace que utilicen uno o varios scripts SED                                 |
| -f    | Hace que el script se extraiga de un archivo                               |
| -n    | Los resultados no se deben emitir                                          |
| -i    | Crea un archivo temporal que posteriormente sustituye al archivo de origen |
| -u    | No se utiliza ningún buffer de datos                                       |
| -s    | El comando acepta expresiones regulares ampliadas                          |
| -r    | El comando acepta expresiones regulares ampliadas                          |

Los parámetros -e y -f son los más importantes. Indican si las **ordenes están directamente en el comando** (entonces es un script SED) o si el comando debe dirigirse a un archivo adicional para conseguir esas órdenes. A menudo se puede prescindir de escribir el parámetro -e, ya que es el parámetro por defecto. Sin embargo, en cuanto incluyas más de una orden en el comando al mismo tiempo, es obligatorio poner el parámetro -e.

Muy importante, y probablemente indispensable para tu trabajo, es el parámetro -n. Si no introduces el parámetro -n en el comando, todas y cada una de las líneas del archivo de texto que lea el comando se mostrarán en el terminal, lo cual no es muy útil, especialmente con grandes bases de datos. Si introduces este parámetro en el comando, en el terminal **solo se mostrarán las líneas que se vean afectadas por el comando**.

### Órdenes

Con una orden, se le indica al comando qué debe hacer con el archivo fuente, teniendo en cuenta los parámetros especificados



###

### Bibliografia

* [https://www.hostinger.es/tutoriales/el-comando-sed-de-linux-usos-y-ejemplos/](https://www.hostinger.es/tutoriales/el-comando-sed-de-linux-usos-y-ejemplos/)
* [https://www.ochobitshacenunbyte.com/2019/05/28/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/](https://www.ochobitshacenunbyte.com/2019/05/28/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/)
* [https://geekland.eu/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/](https://geekland.eu/uso-del-comando-sed-en-linux-y-unix-con-ejemplos/)
* [https://www.ionos.es/digitalguide/servidores/configuracion/comando-sed-de-linux/](https://www.ionos.es/digitalguide/servidores/configuracion/comando-sed-de-linux/)
