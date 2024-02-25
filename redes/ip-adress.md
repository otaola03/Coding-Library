---
description: Internet Protocol Adress
---

# IP Adress



Una dirección IP (Internet Protocol) es un número único que identifica a un dispositivo en una red. Las direcciones IP son necesarias para que los dispositivos puedan comunicarse entre sí en una red y para que se puedan enviar y recibir datos.

Las direcciones IP se componen de cuatro números separados por puntos. Cada número puede variar entre 0 y 255, lo que significa que existen más de cuatro mil millones de posibles combinaciones de direcciones IP.

{% embed url="https://www.youtube.com/watch?v=8npT9AALbrI" %}

Para entender cómo funcionan las direcciones IP, podemos utilizar una metáfora utilizando la dirección de una casa para enviar correo. Imagina que quieres enviar una carta a tu amigo que vive en otra ciudad. Para asegurarte de que la carta llegue a su destino, debes incluir la dirección completa de la casa de tu amigo en el sobre de la carta.

De manera similar, cuando envías datos a través de una red, debes incluir la dirección IP completa del dispositivo de destino para asegurarte de que los datos lleguen a su destino correctamente. Si la dirección IP está incompleta o es incorrecta, los datos pueden perderse o ser enviados al dispositivo equivocado. Por lo tanto, es importante asegurarse de que la

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

### Tipos de direcciones IP

#### Dirección IP Estática

Una dirección IP estática es una dirección IP permanente que se asigna a un dispositivo y nunca cambia. Esta dirección se utiliza principalmente para servidores web, correo electrónico, DNS, cámaras de seguridad, y otros dispositivos que necesitan ser accesibles desde cualquier lugar en todo momento. Una dirección IP estática es proporcionada por el proveedor de Internet y puede ser pública o privada.

Las ventajas de utilizar una dirección IP estática son que es fácilmente identificable y accesible, lo que la hace ideal para servicios que necesitan estar en línea y accesibles de manera constante. Sin embargo, una desventaja de utilizar una dirección IP estática es que puede ser menos segura debido a que es fácilmente identificable.

#### Dirección IP Dinámica

Una dirección IP dinámica es una dirección IP temporal que se asigna a un dispositivo cuando se conecta a Internet. La dirección IP dinámica es proporcionada por el proveedor de servicios de Internet (ISP) y cambia periódicamente. Es utilizado por la mayoría de los usuarios de Internet en hogares y oficinas y es más rentable para los proveedores de servicios de Internet.

Las ventajas de utilizar una dirección IP dinámica son que es más rentable y seguro debido a que es difícil de identificar y cambia periódicamente. Sin embargo, una desventaja de utilizar una dirección IP dinámica es que puede ser menos accesible debido a que cambia periódicamente.

#### Dirección IP Privada

Una dirección IP privada se aplica al dispositivo principal que las personas usan para conectar su red de internet empresarial o doméstica con su proveedor de servicios de internet (ISP). En la mayoría de los casos, este será el enrutador. Todos los dispositivos que se conectan a un enrutador se comunican con otras direcciones IP utilizando la dirección IP del enrutador.

Conocer una dirección IP externa es crucial para que las personas puedan abrir puertos utilizados para juegos en línea, servidores de correo electrónico y web, transmisión de medios y crear conexiones remotas.

Las ventajas de utilizar una dirección IP privada son que es más segura debido a que no es accesible desde Internet y que es fácilmente accesible desde cualquier dispositivo conectado a la misma red. Sin embargo, una desventaja de utilizar una dirección IP privada es que no es accesible desde fuera de la red privada.

#### Dirección IP Pública

Una dirección IP pública, o dirección IP externa, se aplica al dispositivo principal que las personas usan para conectar su red de internet empresarial o doméstica con su proveedor de servicios de internet (ISP). En la mayoría de los casos, este será el enrutador. Todos los dispositivos que se conectan a un enrutador se comunican con otras direcciones IP utilizando la dirección IP del enrutador.

Conocer una dirección IP externa es crucial para que las personas puedan abrir puertos utilizados para juegos en línea, servidores de correo electrónico y web, transmisión de medios y crear conexiones remotas.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### IPv4 e IPv6

IPv4 e IPv6 son dos versiones del protocolo de Internet que se utilizan para identificar dispositivos en una red. Mientras que IPv4 es la versión más antigua y ampliamente utilizada, IPv6 fue desarrollado para superar las limitaciones de IPv4 en términos de dirección IP y seguridad.

#### Título H3: IPv4

IPv4 es la cuarta versión del protocolo de Internet y se ha utilizado ampliamente desde su introducción en 1983. Las direcciones IPv4 consisten en cuatro octetos (32 bits) y se representan en formato decimal separado por puntos, como por ejemplo: 192.168.0.1.

Sin embargo, la cantidad limitada de direcciones IPv4 ha llevado a la creación de redes privadas y el uso de la traducción de direcciones de red (NAT) para permitir que varios dispositivos compartan una dirección IP pública.

<figure><img src="../.gitbook/assets/image (2) (3).png" alt=""><figcaption></figcaption></figure>

#### Título H3: IPv6

IPv6 es la sexta versión del protocolo de Internet y se desarrolló para superar las limitaciones de dirección de IPv4 y mejorar la seguridad en línea. Las direcciones IPv6 consisten en ocho grupos de cuatro dígitos hexadecimales (128 bits) y se representan en formato hexadecimal separado por dos puntos, como por ejemplo: 2001:0db8:85a3:0000:0000:8a2e:0370:7334.

IPv6 ofrece un espacio de direccionamiento mucho más grande que IPv4, lo que significa que hay suficientes direcciones para permitir que cada dispositivo tenga una dirección IP pública única. Además, IPv6 también incluye características de seguridad mejoradas, como la autenticación y el cifrado de paquetes.

A medida que la cantidad de dispositivos en línea sigue creciendo, IPv6 se está convirtiendo en una opción cada vez más atractiva para la conectividad de Internet.

### Net ID y Host ID

El direccionamiento IP se divide en dos partes principales: Net ID y Host ID. El Net ID se utiliza para identificar una red en particular, mientras que el Host ID se utiliza para identificar un dispositivo específico en esa red.

#### Net ID

El Net ID (Identificador de Red) es la porción de una dirección IP que se utiliza para identificar una red en particular. En una dirección IP de claseful (Clase A, B, o C), el Net ID se encuentra en la primera, primera y primera y segunda octetos respectivamente.

Por ejemplo, en una dirección IP de clase C de 192.168.0.1, el Net ID es 192.168.0. En una dirección IP de clase B de 172.16.0.1, el Net ID es 172.16.

En el subneteo, se utiliza el Net ID para identificar una subred en particular dentro de una red más grande.

#### Host ID

El Host ID (Identificador de Host) es la porción de una dirección IP que se utiliza para identificar un dispositivo específico en una red. En una dirección IP de claseful, el Host ID se encuentra en los últimos octetos.

Por ejemplo, en una dirección IP de clase C de 192.168.0.1, el Host ID es 1. En una dirección IP de clase B de 172.16.0.1, el Host ID es 0.1.

El Host ID se utiliza para enrutar paquetes a dispositivos específicos en una red, identificando de manera única cada dispositivo dentro de una red específica.

### Clases de direcciones IP

Existen cinco clases de direcciones IP, cada una con diferentes rangos de direcciones y diferentes propósitos de uso:

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

#### Clase A

Las direcciones de clase A son aquellas en las que el primer octeto (los primeros 8 bits) se utiliza para identificar la red y los tres octetos restantes se utilizan para identificar los hosts. El primer bit siempre es 0, lo que significa que el rango de direcciones va desde 0.0.0.0 hasta 127.255.255.255.

Las direcciones de clase A se utilizan para grandes redes, ya que permiten un gran número de hosts. Sin embargo, debido a la cantidad limitada de redes disponibles, la mayoría de las direcciones de clase A se han agotado.

#### Clase B

Las direcciones de clase B son aquellas en las que los dos primeros octetos se utilizan para identificar la red y los dos octetos restantes se utilizan para identificar los hosts. El primer bit del primer octeto siempre es 1 y el segundo bit siempre es 0, lo que significa que el rango de direcciones va desde 128.0.0.0 hasta 191.255.255.255.

Las direcciones de clase B se utilizan para redes medianas y grandes, ya que permiten un número moderado de hosts y un número suficiente de redes.

#### Clase C

Las direcciones de clase C son aquellas en las que los tres primeros octetos se utilizan para identificar la red y el último octeto se utiliza para identificar los hosts. El primer bit del primer octeto siempre es 1, el segundo bit siempre es 1 y el tercer bit siempre es 0, lo que significa que el rango de direcciones va desde 192.0.0.0 hasta 223.255.255.255.

Las direcciones de clase C se utilizan para redes pequeñas, ya que permiten un número limitado de hosts pero un gran número de redes.

<figure><img src="../.gitbook/assets/Screen Shot 2023-03-10 at 6.47.46 PM.png" alt=""><figcaption></figcaption></figure>

#### Clase D

Las direcciones de clase D se utilizan para identificar grupos multicast. El primer octeto comienza siempre con los tres primeros bits en 1 y el cuarto bit en 0, lo que significa que el rango de direcciones va desde 224.0.0.0 hasta 239.255.255.255.

Las direcciones de clase D se utilizan para transmitir datos a múltiples hosts en una sola transmisión.

#### Clase E

Las direcciones de clase E se utilizan para fines experimentales y reservados para uso futuro. El primer octeto comienza siempre con los cuatro primeros bits en 1, lo que significa que el rango de direcciones va desde 240.0.0.0 hasta 255.255.255.255.

Las direcciones de clase E no se utilizan actualmente en Internet y se mantienen reservadas para un uso futuro.
