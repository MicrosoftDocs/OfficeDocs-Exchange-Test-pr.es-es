---
title: 'Conceptos y componentes de telefonía: Exchange 2013 Help'
TOCTitle: Conceptos y componentes de telefonía
ms:assetid: ce70bf6a-db85-411b-8b93-2987703963a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124606(v=EXCHG.150)
ms:contentKeyID: 54652450
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conceptos y componentes de telefonía

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-25_

Si va a planear e implementar mensajería unificada (UM) de Microsoft Exchange 2013 en la red, debe comprender el funcionamiento de la mensajería unificada y las redes de telefonía. En este tema se proporciona información general sobre los conceptos y componentes de infraestructura telefónica que le ayudarán a planear e implementar servidores que ejecutan la mensajería unificada de Exchange 2013.

**Contenido**

Información general

Conceptos y componentes

Redes de conmutación de circuitos

Redes de conmutación de paquetes

PBX

IP PBX

PBX habilitadas para SIP

VoIP

Puertas de enlace VoIP

## Información general

En versiones de Microsoft Exchange anteriores a Exchange Server 2007, la principal responsabilidad del administrador de Exchange era administrar mensajes de correo electrónico y, en ocasiones, administrar una infraestructura de red. Las versiones anteriores de Exchange no contaban con prestaciones de mensajería unificada. Los administradores de Exchange Server, versión 5.5, Exchange 2000 Server y Exchange Server 2003 se centraban en el entorno de Exchange y la infraestructura de red y dependían en gran medida de los consultores de telefonía para administrar su entorno e infraestructura telefónica.

## Conceptos y componentes

Para implementar correctamente la mensajería unificada en Exchange 2013, se deben conocer y comprender los conceptos y los componentes básicos de telefonía. Una vez que haya adquirido y asimilado los conocimientos de los aspectos básicos de telefonía, podrá integrar correctamente la mensajería unificada de Exchange 2013 en una organización de Exchange 2013. Los conceptos y componentes básicos incluyen:

  - Redes de conmutación de circuitos y de conmutación de paquetes

  - Central de conmutación (PBX)

  - IP PBX

  - Protocolo de voz sobre Internet (VoIP)

  - Puertas de enlace VoIP

## Redes de conmutación de circuitos

En las redes de conmutación de circuitos, como es la Red telefónica publica conmutada (PSTN), se transmiten varias llamadas a través del mismo medio de transmisión. Con frecuencia, el medio empleado en PSTN es el cobre. No obstante, también se puede emplear cable de fibra óptica.

Una red de conmutación de circuitos es una red en la que existe una conexión dedicada. Una conexión dedicada es un circuito o un canal establecido entre dos nodos para que se puedan comunicar. Cuando se establece una llamada entre dos nodos, esa conexión sólo la pueden usar estos dos nodos. Cuando uno de los dos nodos termina la llamada, la conexión se cancela.


> [!NOTE]
> PSTN es una agrupación de las redes telefónicas públicas de conmutación de circuitos del mundo. Esta agrupación se asemeja a Internet en que éste es una agrupación de las redes públicas de conmutación de paquetes basadas en IP del mundo.



Hay dos tipos básicos de redes de conmutación de circuitos: analógicas y digitales. Las analógicas fueron diseñadas para la transmisión de voz. Durante muchos años, la PSTN era solo analógica, pero hoy en día, las redes basadas en circuitos, como la PSTN, han pasado de ser analógicas a digitales. Para que la señal analógica de transmisión de voz sea compatible con una red digital, se debe codificar la señal de transmisión analógica o convertirla a formato digital antes de entrar en una WAN de telefonía. En el extremo de recepción de la conexión, la señal digital se debe descodificar o volver a convertir en formato de señal analógica.

Las redes de conmutación de circuitos tienen ventajas y desventajas. Las desventajas son las siguientes. Las redes de conmutación de circuitos pueden ser relativamente ineficaces, ya que se puede desperdiciar ancho de banda. Éste no es el caso cuando se usa VoIP en una red de conmutación de paquetes. VoIP comparte el ancho de banda disponible con todas las otras aplicaciones de red y hace un uso más eficaz del mismo. Otra desventaja de las redes de conmutación de circuitos es que se debe prever el número máximo de llamadas de teléfono que se necesitará en períodos de uso intenso y pagar por el uso del circuito o de los circuitos que admitan el número máximo de llamadas.

La conmutación de circuitos tiene una gran ventaja con respecto a las redes de conmutación de paquetes. Cuando se usa un circuito en una red de conmutación de circuitos, se tiene el circuito completo durante todo el tiempo que se esté usando, sin la competencia de otros usuarios. Este no es el caso de las redes de conmutación de paquetes.


> [!NOTE]
> La Jerarquía digital sincrónica (SDH) se ha convertido en el principal protocolo de transmisión de la mayoría de las redes PSTN. SDH se transmite a través de redes de fibra óptica.



Información general

## Redes de conmutación de paquetes

La conmutación de paquetes es un técnica que divide un mensaje de datos en unidades más pequeñas llamadas paquetes. Éstos se envían a su destino siguiendo la mejor ruta disponible, y se reensamblan en el extremo de recepción.

En las redes de conmutación de paquetes, como es Internet, los paquetes se enrutan a su destino por la ruta más oportuna, pero no todos los paquetes que viajan entre dos hosts siguen la misma ruta, ni siquiera los que pertenecen a un mismo mensaje. Esto prácticamente garantiza que los paquetes llegarán en diferentes momentos y desordenados. En una red de conmutación de paquetes, los paquetes (mensajes o fragmentos de mensajes) se enrutan individualmente entre los nodos en vínculos de datos que pueden estar compartidos por otros nodos. En la conmutación de paquetes, a diferencia de la conmutación de circuitos, las diferentes conexiones con nodos de la red comparten el ancho de banda disponible.


> [!NOTE]
> En la conmutación de circuitos, todos los paquetes llegan al receptor en orden y por un solo camino.



Las redes de conmutación de paquetes tienen su razón de ser para permitir la comunicación de datos mediante Internet en todo el mundo. Una red de datos pública o una red de conmutación de paquetes es el equivalente de datos de la PSTN.

También se pueden encontrar redes de conmutación de paquetes en entornos de redes LAN o WAN. Un entorno WAN de conmutación de paquetes depende de circuitos telefónicos, pero éstos están organizados de tal forma que mantienen una conexión permanente con su punto final. En un entorno LAN de conmutación de paquetes, como una red Ethernet, la transmisión de los paquetes de datos depende de la conmutación de los paquetes, los enrutadores y los cables de la LAN. En una LAN, la conmutación establece una conexión entre dos segmentos sólo durante el tiempo suficiente para enviar el paquete. Los paquetes entrantes se guardan en un área de memoria temporal o un búfer de la memoria. En una LAN basada en Ethernet, un marco de Ethernet contiene la carga o la porción de datos del paquete y un encabezado especial que incluye la información de dirección de control de acceso de medios (MAC) del origen y el destino del paquete. Cuando los paquetes llegan a su destino, un ensamblador de paquetes los vuelve a ordenar. El ensamblador de paquetes es necesario por las diferentes rutas que pueden seguir los paquetes.

Las redes de conmutación de paquetes han hecho posible que exista Internet y, al mismo tiempo, ha hecho que las redes de datos, especialmente las redes IP basadas en LAN, estén más disponibles de forma más generalizada.

Información general

## PBX

Una PBX heredada es un dispositivo de telefonía que actúa como conmutador de llamadas en una red telefónica o de conmutación de circuitos.


> [!NOTE]
> Una PBX heredada es una PBX que no puede pasar paquetes IP. En muchas empresas, las PBX heredadas se han reemplazado por IP PBX.



PBX es un dispositivo de telefonía que usan la mayoría de las medianas y grandes empresas. PBX permite a los usuarios o abonados compartir un determinado número de líneas externas para hacer llamadas telefónicas consideradas externas a la PBX. Una PBX es una solución mucho menos cara que proporcionar a cada usuario de la empresa una línea telefónica externa. A una PBX se pueden conectar teléfonos, aparatos de fax, módems y otros dispositivos de comunicación.

El equipamiento de PBX normalmente se instala en la propia empresa y conecta las llamadas entre los teléfonos situados e instalados en la empresa. Normalmente, hay un número limitado de líneas externas, también denominadas líneas troncales, para realizar y recibir llamadas externas a la empresa desde un origen externo, como la PSTN.

Las llamadas internas de la empresa realizadas a números de teléfono externos mediante una PBX se realizan marcando el 9 o el 0 seguido del número externo en algunos sistemas. Para completar la llamada se selecciona automáticamente una línea troncal saliente. Al contrario, las llamadas realizadas entre usuarios dentro de la empresa normalmente no necesitan el marcado de ningún número especial ni el uso de una línea externa troncal. Esto se debe a que la PBX enruta o conmuta las llamadas internas entre teléfonos que están conectados físicamente a la PBX.

En las grandes y medianas empresas, pueden darse las configuraciones de PBX siguientes:

  - Una sola PBX para toda la empresa.

  - Una agrupación de dos o más PBX que no están en red ni conectadas unas a otras.

  - Una agrupación de dos o más PBX que están conectadas unas a otras o están en red.


> [!NOTE]
> Un plan de marcado de mensajería unificada de Exchange&nbsp;2013 puede abarcar más de una PBX o IP&nbsp;PBX.



Información general

## IP PBX

Una IP PBX es una central de conmutación compatible con el protocolo IP para conectar teléfonos mediante el uso de una LAN Ethernet o de conmutación de paquetes y que envía sus conversaciones de voz en paquetes IP. Una IP PBX híbrida es compatible con el protocolo IP para enviar conversaciones de voz en paquetes, pero también conecta teléfonos analógicos y digitales de conmutación de circuitos multiplexión por división de tiempos (TDM). Una IP PBX es un equipamiento de conmutación de teléfono que reside en una empresa privada en lugar de una empresa telefónica.

Las IP PBX son frecuentemente más fáciles de administrar que las PBX heredadas, ya que los administradores pueden configurar fácilmente sus servicios de IP PBX mediante un explorador de Internet u otra utilidad basada en IP. Además, no es necesario instalar cables ni paneles de conexión adicionales Con una IP PBX, trasladar un teléfono basado en IP es tan fácil como desenchufarlo y volverlo a enchufar en otro lugar, en lugar de los costosos servicios necesarios para trasladar un teléfono de un proveedor de PBX heredadas. Asimismo, las empresas propietarias de una IP PBX no tienen los costos adicionales de infraestructura necesarios para mantener y administrar dos redes separadas de conmutación de circuitos y de conmutación de paquetes.

## PBX habilitadas para SIP

Una PBX habilitada para SIP es un dispositivo de telefonía que actúa como un conmutador de red para conmutar llamadas en una red telefónica o de conmutación de circuitos. Sin embargo, la diferencia entre una PBX habilitada para SIP y una PBX tradicional estriba en que la primera se puede conectar a Internet y usar el protocolo SIP para realizar llamadas por Internet.

Las PBX habilitadas para SIP hacen uso de un formato para llamadas que incluye una URI de SIP con un número E.164 global y el parámetro "user=phone". Por ejemplo: sip:+14255551234@contoso.com;user=phone

El número E164 empieza por un signo más ("+") y carece de un parámetro de contexto telefónico o separadores. Las PBX habilitadas para SIP admiten tanto TCP como UDP (este último, todavía de amplio uso en sistemas heredados). Las PBX habilitadas para SIP también admiten Seguridad de la capa de transporte mutua (TLS mutua) y consultas DNS.

## VoIP

El Protocolo de voz sobre Internet (VoIP) es una tecnología que contiene hardware y software que permite el uso de una red basada en IP como el medio de transmisión de las llamadas telefónicas. En VoIP, los datos de voz se envían en paquetes mediante IP en lugar de las transmisiones de circuitos tradicionales o las líneas de conmutación de circuitos de la PSTN. Una puerta de enlace VoIP que se conecta a la red IP utiliza protocolos VoIP para enviar paquetes de voz entre servidores de buzones y de acceso de cliente de Exchange 2013 y un sistema PBX.

## Puertas de enlace VoIP

Una puerta de enlace VoIP es un producto o dispositivo de hardware de terceros que conecta una PBX heredada a una LAN. La puerta de enlace VoIP posibilita que el sistema PBX se comunique con los servidores de buzones y de acceso de cliente de Exchange 2013 en los que se ejecutan los servicios de mensajería unificada y de enrutador de llamada de mensajería unificada de Microsoft Exchange.


> [!NOTE]
> La puerta de enlace VoIP también puede conectar sistemas PBX que usan VoIP en lugar de protocolos de conmutación de circuitos RTC.



La mensajería unificada de Exchange 2013 depende de la capacidad de la puerta de enlace VoIP para traducir o convertir TDM o protocolos de telefonía basados en conmutación de circuitos, como ISDN o QSIG, desde una central de conmutación (PBX) a protocolos basados en VoIP o IP, como el protocolo de sesión iniciada (SIP), el protocolo de transporte en tiempo real (RTP) o T.38 para el transporte de facsímil en tiempo real. La puerta de enlace VoIP es parte integral del funcionamiento de la mensajería unificada.


> [!IMPORTANT]
> Una vez instalada la puerta de enlace VoIP, IP&nbsp;PBX o PBX habilitada para SIP, deberá crear una puerta de enlace IP de mensajería unificada que represente el dispositivo físico. Una vez creada la puerta de enlace IP de mensajería unificada, los servidores de buzones y de acceso de cliente asociados a la puerta de enlace IP de mensajería unificada envían una solicitud SIP OPTIONS a la puerta de enlace VoIP, IP&nbsp;PBX o PBX habilitada para SIP para asegurarse de que el dispositivo responde. Si la puerta de enlace VoIP no responde a la solicitud SIP OPTIONS procedente del servidor de buzones, este registrará un evento con el identificador&nbsp;1088 en el que se deja constancia del error de la solicitud. Para solucionar este problema, procure que la puerta de enlace VoIP, IP&nbsp;PBX o PBX habilitada para SIP está disponible y en línea y, asimismo, que la configuración de mensajería unificada es correcta en el servidor tanto de buzones como de acceso de cliente.



Para obtener más información acerca de la configuración de PBX e IP PBX, consulte [Configuraciones de PBX e IP PBX](pbx-and-ip-pbx-configurations-exchange-2013-help.md).

Información general

## Más información

[Protocolos, puertos y servicios de mensajería unificada (UM)](um-protocols-ports-and-services-exchange-2013-help.md)

[Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

