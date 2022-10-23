# Sistema de ficheros

En linux un sistema de ficheros no es nada mas que la forma en la que se guardan los datos dentro del sistema.&#x20;

### Orígenes del sistema de archivos Linux <a href="#mntl-sc-block_1-0-6" id="mntl-sc-block_1-0-6"></a>

Los orígenes del sistema de archivos de Linux se **encuentran en el propio origen en general del núcleo y es sistema operativo** en general: **Unix**. Por ende este tiene todas las convenciones de Unix y una estructura determinada y compatible con otros sistemas Unix. Contrario a Window o MS-DOS el sistema de archivos de cualquier sistema operativo derivado de Unix no está relacionado directamente con la estructura del hardware o sea lo que es más común, con la cantidad de discos que se le asocien a un computador.&#x20;

<figure><img src="http://mural.uv.es/oshuso/Captura_de_pantalla_2011-03-23_a_las_18.45.59.png" alt=""><figcaption></figcaption></figure>

### Organización de directorios en Linux

La organización de directorios de Linux se lleva a cabo mediante una jerarquía establecida mediante el **FHS (Filesystem Hierarchy Estándar)** en el que se definen la distribución y nombres de ficheros y directorios de Linux.

La estructura de directorios y ficheros de Linux se organiza **en forma de árbol invertido,** es decir, desde un directorio principal denominado **“/” o directorio raíz**, cuelgan absolutamente todos los demás, incluso las particiones cuando son montadas. Los principales directorios que cuelgan de raíz son:

#### Directorio /bin <a href="#mntl-sc-block_1-0-14" id="mntl-sc-block_1-0-14"></a>

La primera carpeta que nos encontramos es **/bin**, ésta **contiene los archivos binarios o compilados** de los programas básicos del [**sistema operativo**](https://lovtechnology.com/que-es-un-sistema-operativo/). Cuando usamos el término básico nos referimos a las utilidades más básicas necesarias para utilizar el sistema operativo. No deben existir directorios dentro de **/bin**, pero si contiene miles de archivos binarios. Veamos algunos ejemplos de programas básicos instalados en esta carpeta:

* Para navegar por el sistema de archivos comandos como **cd**, **cp** y **mv**.
* Comandos para el tratamiento de los permisos y administración de los archivos y carpetas como **chmod** y **chown** (cambiar propietarios de archivos).
* Comandos como **mount**, **unmount**, **kill**, **echo** básicos todos para el trabajo en estas distribuciones.

Muchos de estos programas no pueden ser desinstalados por el usuario.

#### Directorio /boot <a href="#mntl-sc-block_1-0-21" id="mntl-sc-block_1-0-21"></a>

Contiene todo lo **necesario para ejecutar el proceso de arranque** de todo el sistema. Este directorio almacena todos los datos que se utilizan antes de que el kernel ejecute los programas como modo usuario. Contiene copias del **kernel del sistema operativo**. Es extremadamente importante saber que no debemos jugar y menos borrar algún archivo contenido en esta carpeta, porque de hacerlo causaríamos una altísima probabilidad que nuestro sistema operativo no vuelva a iniciar.

#### Directorio /cdrom <a href="#mntl-sc-block_1-0-26" id="mntl-sc-block_1-0-26"></a>

Su existencia se debe a la necesidad de que existiera un directorio donde **montar las unidades CD-ROM**. Lo mismo existió en su momento un directorio al mismo nivel en el sistema de archivos llamado **/floppy** para montar nuestros **viejos amigos los llamados diskettes**. Lo que nos lleva a que es una carpeta prácticamente en desuso pues hoy comúnmente encontramos el contenido de un CD-ROM que introducimos en nuestro computador en la carpeta **/media** que veremos más adelante.

#### Directorio /dev <a href="#mntl-sc-block_1-0-30" id="mntl-sc-block_1-0-30"></a>

Como sabemos los sistemas operativos basados en Unix: **todo es un archivo**_._ Lo que se quiere decir con esto es que desde una partición de tu [**disco duro**](https://lovtechnology.com/que-es-una-unidad-de-disco-duro/) hasta el control de tu [**mouse inalámbricos**](https://lovtechnology.com/mejores-mouse-gamer/) o [**mouse por cable**](https://lovtechnology.com/los-mejores-mouse-gamer-por-cable-para-2021/), memoria RAM está en archivos en el directorio **/dev**. Es en **/dev** donde se guardan los archivos especiales y de todos los dispositivos que tiene tu computador.

Es importante saber que los dispositivos con archivos asociados en este directorio pueden ser de bloque o de carácter. De bloque llamamos a los dispositivos que almacenan datos y los de carácter a los que transfieren datos como [**las memorias eMMC**](https://lovtechnology.com/memorias-emmc/) y los [**HDD o SSD**](https://lovtechnology.com/discos-duros-internos-hdd-y-ssd/).

#### Directorio /etc <a href="#mntl-sc-block_1-0-37" id="mntl-sc-block_1-0-37"></a>

Este directorio existe para **ubicar los archivos adicionales** que se necesiten, normalmente son archivos de configuración para personalizar aplicaciones y herramientas. Es una dirección que nunca debe contener archivos binarios. Por ejemplo si instalamos un **cntlm** en nuestro computador su archivo de configuración **cntlm.conf** se encuentra en **/etc**, y el mundialmente conocido archivo **sources.list** donde definimos los repositorios de aplicaciones de nuestra distribución también se encuentra allí. De forma general podemos decir que en ese directorio hay dos grandes grupos de archivos:

* Los archivos y carpetas de configuración global, estos son independientes de los usuarios que usen el sistema.
* Y los llamados **archivos esqueleto**, utilizados con valores por defecto para la configuración del usuario del sistema. Un ejemplo de archivo de usuario es el archivo **profile** que contiene la **configuración del shell Bash**.

Es común que los archivos de configuración de una aplicación se encuentren en una carpeta con el mismo nombre dentro de **/etc** lo cual hace bastante cómodo navegar por sus carpetas y mantiene una muy buena organización.

#### Directorio /home <a href="#mntl-sc-block_1-0-44" id="mntl-sc-block_1-0-44"></a>

Este directorio viene siendo el equivalente de Linux para la carpeta Users del disco C del sistema operativo Window. O sea acá se encuentra toda la información personal de los usuarios existentes en el sistema, por cada usuario tendremos una carpeta en **/home** que coincide con su usuario.

#### Directorio /root <a href="#mntl-sc-block_1-0-44" id="mntl-sc-block_1-0-44"></a>

La carpeta **/root** hace función de la carpeta **/home** pero para el usuario administrador del sistema o el llamado usuario raíz (_root_). No se ubican los archivos del usuario administrador en **/home** para mantenerlos lejos de los usuarios normales y para tener acceso a este directorio se deben proveer las credenciales de administración.

#### Directorios /lib <a href="#mntl-sc-block_1-0-49" id="mntl-sc-block_1-0-49"></a>

En la actualidad casi todos usamos sistemas operativos sobre 64 bits, esto implica que tengas en tu raíz de sistema de archivos un grupo de carpetas llamadas **/lib**, **/lib32** y **/lib64**. En esta ubicación se **guardan las bibliotecas de los paquetes** que han sido instalados compartidos para todos los demás paquetes. Es normal encontrar muchas carpetas duplicadas.

#### Directorio /media <a href="#mntl-sc-block_1-0-52" id="mntl-sc-block_1-0-52"></a>

En este directorio **encontramos los** [**dispositivos externos**](https://lovtechnology.com/disco-duro-externo-hdd-y-ssd/) **montados** en tu computador, por ejemplo una memoria flash un CD o DVD. Hoy día con solo insertar uno de estos dispositivos se crea una nueva carpeta dentro de este directorio haciendo referencia al nuevo dispositivo montado.

#### Directorio /mnt <a href="#directorio-mnt" id="directorio-mnt"></a>

Originalmente es un directorio vacío que en sus funciones es muy parecido al directorio de **/media**. En la actualidad se usa muy poco y en la mayoría de los casos para **montar ubicaciones y discos de forma temporal**.

#### El directorio /opt <a href="#mntl-sc-block_1-0-56" id="mntl-sc-block_1-0-56"></a>

Directorio donde se **ubican las bibliotecas opcionales**. Fue concebido para ubicar en él todas las bibliotecas del software opcional que el usuario instalará en el sistema y de esta forma no afectar al resto del sistema de archivos en caso de que hubiera problemas en la instalación o desinstalación. En la actualidad el desarrollo de aplicaciones en Linux ha ido enfocado a que de cada aplicación producida esté **disponible en paquetes .deb y .rpm**, lo que implica que cada vez se use menos la instalación de bibliotecas y uso del directorio **/opt**.

#### Directorio /sbin <a href="#mntl-sc-block_1-0-60" id="mntl-sc-block_1-0-60"></a>

Aquí ubicamos archivos binarios como mismo en el directorio **/bin** con la diferencia que en **/sbin** se **ubican los archivos binarios del sistema**, de ahí su nombre (system binary). Por su importancia para el funcionamiento del sistema solo el usuario root puede ejecutarlos.

#### Directorio /usr <a href="#mntl-sc-block_1-0-64" id="mntl-sc-block_1-0-64"></a>

Este directorio contiene la mayor parte de las **aplicaciones instaladas del sistema** o sea lo que está disponible aparte de las utilidades básicas que contiene el directorio **/bin**. Entre las aplicaciones más conocidas que se instalan ahí tenemos:

* El paquete de ofimática LibreOffice
* Editor de imágenes Gimp.
* Las versiones Java de tu JRE o JDK.
* Los [**controladores de hardware**](https://lovtechnology.com/controlador-de-dispositivo/).

Tiene su propia jerarquía de carpetas con las subcarpetas llamadas **bin**, **lib** y **sbin,** que tienen la misma filosofía de funcionamiento que sus equivalentes al mismo nivel de **/usr**. Su subdirectorio **/share** contiene todos los iconos del sistema que pueden ser administrados de forma muy sencilla con una interfaz gráfica (GUI) a través de la aplicación Alacarte. El subdirectorio **/local** cumple una función similar a **/opt** y existe cierto debate de cuál de ambos debe permanecer existiendo en el sistema de archivos de Linux.

#### El directorio /var <a href="#mntl-sc-block_1-0-75" id="mntl-sc-block_1-0-75"></a>

Contiene información de los programas de forma temporal y su contenido no debería ser borrado. Encontramos archivos de logs, temporales, caché, copias de seguridad etc. Es el último de los directorios principales del sistema de archivos.

### Bibliografia

* [https://ayudalinux.com/sistema-de-ficheros-linux/](https://ayudalinux.com/sistema-de-ficheros-linux/)
* [https://bigsoftware.es/sistema-de-archivos-de-linux-que-es-y-como-funciona/](https://bigsoftware.es/sistema-de-archivos-de-linux-que-es-y-como-funciona/)
* [https://programacionfacil.org/blog/el-sistema-de-archivos-linux/](https://programacionfacil.org/blog/el-sistema-de-archivos-linux/)
