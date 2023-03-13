# Subnet Mask

La subnet mask, también conocida como máscara de subred, es un valor numérico que se utiliza en redes informáticas para definir cuál es la porción de la dirección IP que corresponde a la red y cuál es la porción que corresponde al host. En otras palabras, la subnet mask indica qué bits de la dirección IP identifican a la red y cuáles identifican a los dispositivos dentro de ella.

La subnet mask es un elemento fundamental de la arquitectura de redes, ya que permite segmentar grandes redes en subredes más pequeñas, lo que a su vez permite optimizar el rendimiento y la seguridad de la red.

[1.200 × 1.301](https://www.google.com/url?sa=i\&url=https%3A%2F%2Fnordvpn.com%2Fblog%2Fwhat-is-a-subnet-mask%2F\&psig=AOvVaw1ysNaeRxtfvWYxPQVvh-A\_\&ust=1678619437992000\&source=images\&cd=vfe\&ved=0CA0QjRxqFwoTCODDw-3e0\_0CFQAAAAAdAAAAABAD)

<figure><img src="https://nordvpn.com/wp-content/uploads/2020/11/subnet-infographic.jpg" alt=""><figcaption></figcaption></figure>

## ¿Cómo se representa la subnet mask?

La subnet mask se representa como una serie de cuatro números separados por puntos, cada uno de los cuales puede tener un **valor entre 0 y 255**. Por ejemplo, una subnet mask típica es 255.255.255.0. Este valor indica que los primeros tres octetos de la dirección IP corresponden a la red y el último octeto corresponde al host.

#### ¿Por que 255?

La razón por la que el número máximo utilizado en la máscara de subred es 255 se debe a que en IPv4, una dirección IP está formada por 32 bits divididos en cuatro octetos de 8 bits cada uno. En la máscara de subred, se indica qué bits pertenecen al Net ID y cuáles al Host ID. Cada octeto puede tener un valor máximo de 255 porque se trata de la combinación máxima de 8 bits que pueden tener los valores de 0 y 1.

Para entenderlo mejor, podemos ver la tabla de conversión de binario a decimal:

| 128 | 64 | 32 | 16 | 8  | 4  | 2  | 1  |
| --- | -- | -- | -- | -- | -- | -- | -- |
| 2⁷  | 2⁶ | 2⁵ | 2⁴ | 2³ | 2² | 2¹ | 2⁰ |
| 1   | 1  | 1  | 1  | 1  | 1  | 1  | 1  |

En esta tabla, cada número decimal (de 1 a 128) se corresponde con una posición en el octeto de 8 bits. Cada posición puede tener un valor de 0 o 1, lo que permite la combinación de hasta 255 en un solo octeto.

La máscara de subred es simplemente una forma de indicar cuántos de estos bits en la dirección IP se utilizan para el Net ID y cuántos se utilizan para el Host ID. Por ejemplo, una máscara de subred de 255.255.255.0 indica que los primeros tres octetos de la dirección IP se utilizan para el Net ID y el último octeto se utiliza para el Host ID.

## ¿Cómo se calcula la subnet mask?

La subnet mask se calcula a partir del número de bits que se utilizan para identificar la red en la dirección IP. Por ejemplo, en una dirección IP típica de la forma 192.168.1.100, los primeros tres octetos identifican la red y el último octeto identifica al host. Como cada octeto está formado por 8 bits, en este caso la subnet mask será 255.255.255.0, ya que los primeros 24 bits corresponden a la red y los últimos 8 bits corresponden al host.

## ¿Qué relación hay entre la subnet mask y la dirección IP?

La subnet mask y la dirección IP están estrechamente relacionadas, ya que juntas determinan la estructura de la red y la ubicación de los dispositivos dentro de ella. En una dirección IP típica de la forma 192.168.1.100, por ejemplo, la subnet mask indica que los primeros tres octetos corresponden a la red y el último octeto corresponde al host. Si la subnet mask fuese distinta, la estructura de la red y la ubicación de los dispositivos sería diferente.

### CDIR Value

El CIDR value, o valor CIDR, es una notación utilizada para representar una dirección IP y su máscara de subred correspondiente. Esta notación utiliza una barra (/) seguida de un número que indica la cantidad de bits en la máscara de subred. Por ejemplo, una dirección IP con un CIDR value de 24 tendría una máscara de subred de 255.255.255.0, lo que significa que los primeros 24 bits de la dirección IP corresponden al Identificador de Red (Net ID) y los últimos 8 bits corresponden al Identificador de Host (Host ID).

El uso del CIDR value es común en la configuración de redes, ya que permite una asignación más flexible y precisa de direcciones IP y subredes en comparación con el método de enrutamiento de claseful anterior.

### Como extraer informacion a partir de una Subnet Mask

Como hemos visto en el post sobre [IP Adress](ip-adress.md#clases-de-direcciones-ip) existen distintas clases de IPs y estas se clasifican en base a las Subnet Mask. Las mas comunes son la clase A, B, C y D, ya que bloquean el primero, segundo, tercero, y cuarto octeto respectivamente. Teniendo en cuenta esto la porcediemiento a seguir paa sacar todoa la informacion sobre una Subnet Mask es el siguiente:

#### Observar cuantos bits estan bloqueados

Para saber el numero de bits bloqueados en una Subnet Mask tenemos dos opcion, una mirar el CDIR Value, que nos dira directamente el numero de bits bloqueados y la segunda, seria respresentar nuestra Subnet Mask una tabla de conversion. Por ejemplo la tabla para la subnet mask 255.255.255.128 o el CDIR Value 25 seria la siguiente:

<figure><img src="../.gitbook/assets/imagen (1).png" alt=""><figcaption></figcaption></figure>

Como odeis observar al tener 255 el los primero 3 octetos, esto stres ya estan bloqueado y en el cuarto octeto al tener 128 y esto al ser igual que 2⁷, tan solo tendriamos bloqueado el pirmer bit del ultimo octeto.

#### Observar cuantas networks se pueden crear

Para encontrar el número de redes en una subred, se utiliza la fórmula `2^n`, donde "n" es el número de bits de host prestados en la subred.

$$
nº NETs = 2^n
$$



Los bits prestados son los bits "sobrantes" de la mascara, es decir seguimos con la mascara de clase C anterior `255.255.255.128` los bits sobrantes son los del cuarto octeto, ya que como solo hay un uno en el cuarto octeto no llegan a completar el octeto entero.

<figure><img src="../.gitbook/assets/Screen Shot 2023-03-11 at 5.18.35 PM.png" alt=""><figcaption></figcaption></figure>

En este caso el numero de Networks posibles a crear seria `2^1 = 2`

#### Observar cuantas IP Adressess se pueden crear

Para encontrar el número de direcciones IP disponibles en cada red, primero debes determinar cuántos bits se han reservado para los hosts en la máscara de subred.

$$
nºIPs = 2^n-2
$$

Luego, utiliza la fórmula 2^n, donde n es el número de bits reservados para los hosts, para determinar el número de direcciones IP disponibles en cada red. Sin emabrgo a este resultado hay que restarle 2, ya que la primera dirección IP es la **dirección de red** y la última dirección IP es la **dirección de broadcast**, lo que significa que no se pueden usar para asignar a dispositivos.

<figure><img src="../.gitbook/assets/Screen Shot 2023-03-11 at 5.24.05 PM.png" alt=""><figcaption></figcaption></figure>

Haciendo referencia a la mascara anterior del ultimo octeto tendriamos 7 de 8 bits para el host por lo que el numero de IPs seria `2^7 = 128`. Sin embargo, como la la primera es la direccion de red y la utlima la direccion del broadcast, en vez de tener `128` IPs disponibles tendriamos `126`.
