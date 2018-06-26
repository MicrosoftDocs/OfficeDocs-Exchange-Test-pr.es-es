---
title: 'Configuraciones de PBX e IP PBX: Exchange 2013 Help'
TOCTitle: Configuraciones de PBX e IP PBX
ms:assetid: fb086680-6e3e-477a-a5d8-e24ca30196ee
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb430797(v=EXCHG.150)
ms:contentKeyID: 54652463
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configuraciones de PBX e IP PBX

 

_**Se aplica a:**Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Cada vez es más frecuente que las organizaciones adquieran, instalen y mantengan los componentes de hardware, por ejemplo, centrales de conmutación (PBX) o IP PBX, que son necesarios para admitir sus propios sistemas de telefonía. Numerosas organizaciones compran su propio equipo de telefonía y forman a su personal para reducir los gastos asociados al mantenimiento de sus sistemas de telefonía y para poder aprovechar mejor prestaciones de telefonía que brindan.

Para que una organización pueda poseer y mantener una red de telefonía, debe comprar los componentes de hardware necesarios. También debe tener en cuenta el mantenimiento diario del equipo de telefonía y la formación necesaria para que el personal administre el sistema de telefonía. En este tema se abordan los distintos tipos de sistemas de telefonía para empresas u organizaciones, así como los componentes de hardware de telefonía que precisan. El tema también proporciona ejemplos de los distintos tipos de configuraciones de telefonía.


> [!IMPORTANT]
> Se recomienda que todos los clientes que tengan la intención de implementar la mensajería unificada de Microsoft Exchange&nbsp;2013&nbsp;soliciten ayuda a un especialista en mensajería unificada. Así, se asegurará una transición sin problemas del sistema antiguo de correo de voz. Una implementación nueva de mensajería unificada o la actualización de un sistema de correo de voz requiere conocimientos profundos de PBX, IP PBX y mensajería unificada. Para obtener más información de contacto, consulte el sitio web de <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">Microsoft PinPoint</A>.



**Contenido**

Introducción a los sistemas de telefonía

Configuraciones de PBX heredadas y tradicionales

Configuraciones de IP PBX

Identificación de la persona que llama o del receptor de la llamada

## Introducción a los sistemas de telefonía

En las redes de conmutación de circuitos, como la Red telefónica conmutada (RTC), se transmiten varias llamadas a través del mismo medio de transmisión. Con frecuencia, el medio empleado en PSTN es el cobre. No obstante, también se puede emplear cable de fibra óptica.

Una red de conmutación de circuitos consiste en una red con una conexión dedicada. Una conexión dedicada es un circuito o un canal establecido entre dos nodos para que se puedan comunicar. Cuando se establece una llamada entre dos nodos, esa conexión solo la pueden usar estos dos nodos. Cuando uno de los dos nodos termina la llamada, la conexión se cancela.

Hay varios tipos de categorías de sistemas telefónicos de empresas y organizaciones que pueden incluir una red basada en circuitos, una red basada en IP o ambas. Cada tipo de sistema telefónico tiene unas ventajas e inconvenientes que se deben sopesar al planear e implementar un sistema de telefonía.

  - **Centrex:** Centrex es un tipo de servicio telefónico que las compañías telefónicas alquilan a las empresas y organizaciones. Un sistema telefónico Centrex tradicional elimina la necesidad de que una empresa u organización compre el hardware de telefonía que se usa in situ para controlar el sistema telefónico de la organización. Los sistemas Centrex se suelen usar en oficinas pequeñas que alquilan los servicios Centrex a una compañía telefónica por línea y por mes. Algunas veces son organizaciones más grandes las que usan los sistemas de telefonía Centrex, pero en este caso se trata básicamente de organizaciones gubernamentales, públicas y privadas. Los sistemas Centrex usan a menudo líneas telefónicas analógicas para las conexiones con empresas u organizaciones. No obstante, también pueden usar circuitos T1 con un desmultiplexor in situ para admitir teléfonos analógicos y digitales o líneas RDSI.
    
    En un sistema de telefonía basado en Centrex, la oficina central de la compañía telefónica actúa como centralita. Está diseñada específicamente para satisfacer las necesidades de una organización determinada. La oficina telefónica central enruta las llamadas procedentes del interior de la compañía al número de teléfono interno o externo adecuado. Los sistemas Centrex usan la centralita de la oficina central de la compañía para enrutar las llamadas internas a una extensión. Por ejemplo, con Centrex, la centralita telefónica o la oficina central de la compañía telefónica reconoce las extensiones internas. Así, un empleado ubicado dentro de la red de telefonía de la organización puede marcar el número de otro empleado de la misma red de telefonía o plan de marcado usando un número de extensión de cuatro dígitos. Cuando se marca el número de la extensión telefónica interna, la llamada se reenvía a la oficina central de la compañía telefónica y, a continuación, se enruta de nuevo al número de extensión que inició la llamada.

Existe una variante del sistema de telefonía Centrex tradicional denominado *IP Centrex*. En un sistema telefónico IP Centrex, la llamada se envía a través de una puerta de enlace de voz sobre IP (VoIP) ubicada en la oficina central de una compañía telefónica o in situ, en un proveedor de servicios. En este tipo de sistema telefónico, la puerta de enlace VoIP transforma la llamada en paquetes de datos basados en IP que se pueden enviar por Internet o a través de una red basada en VoIP. No obstante, si la llamada se envía por Internet, suele haber otra puerta de enlace VoIP que recibe la llamada y la transforma de nuevo en una llamada tradicional de conmutación de circuitos.

Las organizaciones que disponen de un sistema telefónico Centrex in situ deben instalar, implementar y mantener una o más puertas de enlace VoIP para que la mensajería unificada funcione correctamente. Para que mensajería unificada funcione con IP Centrex, puede que se deba instalar, implementar y mantener puertas de enlace VoIP. Varios factores determinan si se necesita una puerta de enlace VoIP. Dichos factores son la clase de teléfonos que se usan en la organización (analógicos, digitales o IP), así como los protocolos que el sistema IP Centrex admite.

  - **Teléfono multilínea:** en un sistema telefónico multilínea, la oficina central de la compañía telefónica está conectada a la organización mediante líneas telefónicas analógicas o digitales estándar. Un único número de extensión telefónica está conectado a varios teléfonos; así, cuando se hace una llamada a la organización mediante este número de teléfono, todos los teléfonos asociados con esa línea o número de extensión suenan al mismo tiempo.

En los sistemas telefónicos multilínea, los usuarios individuales comparten las líneas. Por lo tanto, las personas que llaman no se encuentran con las frecuentes señales de línea ocupada cuando intentan llamar a la organización. Los sistemas telefónicos multilínea suelen usarse en oficinas pequeñas, donde el volumen de llamadas internas es grande pero el volumen de llamadas externas es pequeño.

Los sistemas telefónicos multilínea se han ido sofisticando y pueden funcionar con la mensajería unificada si se agrega una puerta de enlace VoIP. Sin embargo, algunos sistemas menos sofisticados pueden no funcionar aunque se utilice una puerta de enlace VoIP compatible.

  - **PBX:** una PBX heredada es un dispositivo de telefonía que conmuta las llamadas en una red de telefonía o de conmutación de circuitos. Una PBX heredada es una PBX que no dispone de adaptador de red y que no puede transmitir paquetes IP. Al no poder transmitir paquetes IP, algunas empresas y organizaciones han sustituido las PBX heredadas por IP PBX. Para obtener una lista de PBX admitidas por la mensajería unificada, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).
    
    La mayoría de las compañías medianas y grandes usan PBX. PBX permite a los usuarios o abonados compartir un determinado número de líneas externas para hacer llamadas telefónicas consideradas externas a la PBX. Una PBX es una solución mucho menos cara que proporcionar a cada usuario de la empresa una línea telefónica externa. A una PBX se pueden conectar teléfonos, aparatos de fax, módems y otros muchos dispositivos de comunicación.
    
    El equipo de PBX se suele instalar en la propia organización y conecta las llamadas entre los teléfonos situados en la organización y la compañía telefónica. Normalmente, hay un número limitado de líneas externas, también denominadas líneas troncales, para realizar y recibir llamadas externas a la empresa desde un origen externo, como la PSTN.
    
    Para habilitar una PBX heredada para usarla con la mensajería unificada, debe implementar una puerta de enlace VoIP admitida. Para obtener una lista de las puertas de enlace VoIP admitidas, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

  - **IP PBX:** una IP PBX es una PBX que dispone de un adaptador de red compatible con el protocolo IP. Forma parte de un equipo de conmutación telefónica que suele residir en una organización o empresa en vez de ubicarse en las instalaciones de una compañía telefónica. Existen dos tipos de IP PBX: IP PBX tradicionales e IP PBX híbridas. Las IP PBX tradicionales y las IP PBX híbridas son compatibles con el protocolo IP para el envío de conversaciones de voz en paquetes a teléfonos basados en VoIP. No obstante, las IP PBX híbridas también conectan teléfonos analógicos y digitales tradicionales.
    
    Las IP PBX suelen ser más fáciles de administrar que las PBX heredadas, ya que los administradores pueden configurar más fácilmente los servicios de IP PBX mediante un explorador de Internet u otra herramienta basada en IP. Además, no es necesario instalar cables ni paneles de conexión adicionales. En el caso de una IP PBX, para trasladar un teléfono basado en IP basta con desenchufarlo y volverlo a enchufar en otro lugar. Esto permite evitar los costosos servicios necesarios para trasladar un teléfono de un proveedor de PBX heredada. Asimismo, las empresas propietarias de una IP PBX no tienen los costos adicionales de infraestructura necesarios para mantener y administrar dos redes separadas de conmutación de circuitos y de conmutación de paquetes. Para obtener una lista de PBX admitidas para mensajería unificada, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).
    
    Volver al principio

## Configuraciones de PBX heredadas y tradicionales

En las redes de telefonía que tienen PBX heredadas o tradicionales, una PBX realiza las funciones siguientes:

  - Crea conexiones o circuitos entre los teléfonos de dos usuarios.

  - Mantiene la conexión el tiempo que los usuarios la necesiten.

  - Proporciona información para la contabilidad (por ejemplo, mide las llamadas).

Además de las tres funciones de la lista anterior, las PBX pueden proporcionar otras características de llamada, por ejemplo:

  - Operadores automáticos

  - Contabilidad de llamada

  - Recogida de llamada

  - Transferencia de llamada

  - Llamada en espera

  - Llamada en conferencia

  - Marcado interno directo (DID)

  - No molestar (DND)

Aunque existen varios fabricantes de PBX, todos se encuentran en dos categorías básicas: analógicas y digitales. Estos tipos de PBX se conocen habitualmente como PBX *heredadas* o *tradicionales*.

Los sistemas PBX suelen estar conectados a la oficina central de la compañía telefónica mediante líneas telefónicas especiales, denominadas líneas T1 y E1. Las líneas T1 y E1 tienen varios canales. Estas líneas telefónicas también se denominan *líneas troncales.* Permiten a la oficina central o a la PBX enviar varias llamadas por la misma línea para mejorar la eficacia usando un sencillo diseño de cableado. Una PBX también puede funcionar con líneas analógicas o RDSI.

La correcta configuración de la PBX permite controlar el número de canales o líneas que se desea configurar para recibir llamadas de personas externas a la organización y el número de canales o líneas dedicadas a llamadas de personas de dentro de la organización. La configuración del número de canales o líneas ayuda a evitar las señales de línea ocupada y permite configurar el número de canales o líneas dedicadas a aplicaciones como los centros de llamadas. La correcta configuración de la PBX es un método rentable para administrar los canales o las líneas de la organización, ya que reduce el número de líneas alquiladas necesarias.

Una PBX puede enrutar un número de teléfono concreto marcado a un teléfono concreto, de forma que los usuarios pueden tener su propio número individual o de extensión. Este número se denomina número de marcado interno directo (DID). Cuando se marca el número de teléfono de un usuario, la compañía telefónica envía el número de DID a la PBX usando el servicio de identificación del número marcado (DNIS). Dado que la compañía telefónica usa el DNIS para enviar el número, no es necesaria la intervención de un operador para enrutar la llamada. La PBX dispone de la información de la llamada que permite enrutarla correctamente al número marcado por la persona que llama. Para obtener una lista de PBX admitidas por mensajería unificada, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Volver al principio

## PBX analógicas y digitales

Las PBX analógicas envían la voz y la información de señalización de llamada, como los tonos de teclado del número marcado, como sonido analógico. Por tanto, el sonido no se digitaliza nunca. Para dirigir correctamente la llamada, la PBX y la oficina central de la compañía telefónica tienen que escuchar la información de señalización.


> [!NOTE]
> Los tonos de teclado se denominan, más técnicamente, tono de marcado multifrecuencia (DTMF). Cuando la persona que llama presiona una tecla del teléfono, éste produce dos tonos independientes: un tono de alta frecuencia y un tono de baja frecuencia. Cuando una persona habla por teléfono, solo se emite un tono o frecuencia. El envío de dos tonos con frecuencias diferentes al mismo tiempo reduce la posibilidad de que los tonos de señalización se interpreten como una voz humana o que una voz humana se interprete como tonos de señalización.



Las PBX digitales codifican o digitalizan el sonido analógico en un formato digital. Normalmente, las PBX digitales codifican los sonidos de voz mediante un códec de audio estándar del sector como G.711 o G.729. Después de codificar la voz digitalizada, la envían por un canal mediante conmutación de circuitos. La conmutación de circuitos establece una conexión abierta de un extremo a otro. Esto deja el canal abierto mientras dura la llamada para uso exclusivo de la persona que llama. No obstante, el método de señalización que usa la PBX depende del fabricante. Los fabricantes de PBX pueden tener un método de señalización propio para el establecimiento de llamadas.


> [!NOTE]
> Las PBX digitales admiten líneas troncales digitales y analógicas.



En organizaciones más grandes, las PBX hacen posible que los empleados situados en ubicaciones físicas separadas se pongan en contacto marcando el número de extensión de un usuario. Esto se puede hacer mediante una única PBX o puede implicar a varias PBX configuradas en red. Las PBX situadas en oficinas distintas se pueden conectar a una única red de conmutación de circuitos transparente mediante líneas T1 o E1. Cuando estas líneas conectan las PBX, se denominan frecuentemente *líneas de enlace*. Las PBX se comunican entre sí a través de las líneas de enlace mediante un protocolo de PBX a PBX, como QSIG. QSIG permite que un conjunto de PBX actúe como si fuera una única PBX.

Este tipo de entorno de PBX también puede incluir características avanzadas, como la transferencia de llamadas y la conferencia telefónica. Además de admitir características avanzadas, tener dos PBX conectadas también puede ahorrar dinero a la organización, ya que se reducen los gastos de llamadas a larga distancia entre empleados situados en lugares diferentes. La razón es que una llamada realizada entre dos empleados permanece en una línea de enlace entre las PBX y requiere que el usuario marque únicamente el número de extensión del otro usuario en lugar de realizar una llamada de larga distancia.

En un entorno de telefonía que incluye una o varias PBX analógicas o digitales, es necesario que haya una puerta de enlace VoIP entre la PBX y el servidor de acceso de cliente y el servidor de buzones de Exchange 2013 para convertir los protocolos basados en circuitos de las redes de telefonía en los protocolos basados en IP de las redes de datos. Para obtener más información acerca de las puertas de enlace VoIP, consulte los siguientes temas:

  - [Puertas de enlace IP de mensajería unificada](um-ip-gateways-exchange-2013-help.md)

  - [Conectar una puerta de enlace VoIP para comunicarse con una PBX](connect-a-voip-gateway-to-communicate-with-a-pbx-exchange-2013-help.md)

Para obtener una lista de puertas de enlace VoIP admitidas para mensajería unificada, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Volver al principio

## Configuraciones de IP PBX

Una IP PBX es una PBX que admite el protocolo IP para conectar teléfonos mediante una LAN Ethernet o de conmutación de paquetes. Envía las conversaciones de voz en paquetes IP o de datos. Una IP PBX puede tener varias interfaces. Entre ellas hay interfaces para una red de datos y otras interfaces que permiten la conexión con una red de telefonía o de conmutación de circuitos.

El desarrollo de protocolos de Internet en tiempo real ha hecho posible enviar correctamente mensajes de voz y fax por una red de datos. Entre estos protocolos de Internet en tiempo real destacan los protocolos VoIP que se usan con la mensajería unificada: protocolo de inicio de sesión (SIP) sobre protocolo de control de transmisión (TCP) para mensajes de voz. Estos protocolos han hecho posible enviar correctamente mensajes de voz y faxes por una red de datos. Se necesitan protocolos VoIP en tiempo real para enviar mensajes de voz a través de una red de datos o de conmutación de circuitos, con el fin de mantener y controlar el orden de entrega y la sincronización de los paquetes de datos. Si no se usaran estos protocolos para mantener y controlar el orden de entrega y la sincronización de los paquetes de datos, la voz de las personas se descompondría y su sonido sería incoherente o las imágenes podrían ser confusas. Para obtener una lista de PBX admitidas para mensajería unificada, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).


> [!NOTE]
> La mensajería unificada admite únicamente SIP sobre TCP.



## Configuraciones de IP PBX tradicionales

Una IP PBX tradicional o estándar contiene al menos una interfaz de red que conecta con una red de datos mediante protocolos VoIP. También puede contener interfaces de red adicionales u otras interfaces de telefonía que permiten conectar con una red de telefonía existente, como PSTN. La conexión con la red de datos permite la comunicación con otros hosts de VoIP ubicados en la red de datos mediante paquetes de datos IP. Entre estos hosts de VoIP se incluyen otras IP PBX, teléfonos basados en VoIP, puertas de enlace VoIP y el servidor de acceso de cliente y el servidor de buzones que ejecutan servicios de mensajería unificada. Una IP PBX tradicional no admite teléfonos analógicos ni digitales. Solo admite teléfonos VoIP.

Dado que la IP PBX puede conectar con una red de datos y convertir los protocolos basados en circuitos de la PSTN en protocolos VoIP de conmutación de paquetes, puede que no sea necesaria una puerta de enlace VoIP para habilitar la comunicación con el servidor de acceso de cliente y el servidor de buzones en la red de datos.

## Configuraciones de IP PBX híbridas

Las IP PBX híbridas pueden proporcionar capacidades analógicas, digitales y basadas en VoIP. Si en una IP PBX están instaladas las interfaces correctas y el software que admite varios tipos de interfaces está instalado correctamente, la IP PBX se considera una IP PBX híbrida. Una IP PBX híbrida posibilita el uso de una combinación de teléfonos analógicos, digitales y basados en IP.

Las IP PBX más modernas admiten y proporcionan los tres tipos de comunicación por voz. Una IP PBX tradicional se puede actualizar a una IP PBX híbrida mediante la instalación de las interfaces y de las correspondientes actualizaciones de software o firmware.

La combinación de teléfonos analógicos, digitales y basados en IP posibilita que los usuarios de la organización usen numerosas características nuevas y proporciona gran flexibilidad al entorno de telefonía. El uso de una IP PBX híbrida también permite una migración más gradual a un entorno de telefonía y un sistema de mensajes de voz completamente basados en VoIP en la organización.

Existen varios factores que determinan si va a ser necesaria una puerta de enlace VoIP al conectar con el servidor de acceso de cliente y el servidor de buzones. Uno de estos factores es la compatibilidad de los protocolos VoIP que usa la IP PBX o la IP PBX híbrida y la mensajería unificada. Si una puerta de enlace VoIP no es necesaria, se reduce la complejidad de la infraestructura de telefonía y el soporte necesario para mensajería unificada es más sencillo.

Volver al principio

## Identificación de la persona que llama o del receptor de la llamada

La identificación de la persona que llama o de la persona llamada es un servicio de la compañía telefónica que indica a la persona que recibe la llamada el número de teléfono y, a veces, el nombre de la persona que llama y otra información relacionada con la llamada. Esta información se envía por un cable serie a través de la señal de llamada. Cuando una PBX o una IP PBX recibe una llamada de una compañía telefónica, la llamada incluye la siguiente información de identificación:

  - El número de teléfono de la persona que llama.

  - El número de teléfono de la persona llamada.

  - Códigos de estado, como sonido sin respuesta, estado de la línea, línea ocupada y reenviar siempre las llamadas.

  - El número de línea o de puerto que se usa para la llamada.

  - En telefonía, la información de señalización se usa para intercambiar información entre extremos de una red para establecer, controlar y terminar llamadas. La mensajería unificada admite varios métodos de señalización usados por las puertas de enlace VoIP y las IP PBX. El método de señalización usado depende del tipo de dispositivo que se use y del tipo de método de señalización usado por la compañía telefónica. El factor más importante es que el dispositivo que se conecta con la compañía telefónica y con la puerta de enlace VoIP, o con la IP PBX, debe admitir al menos uno de los métodos de señalización que permiten a las personas que llaman enviar y recibir información de la persona llamada o de la persona que hace la llamada. Para obtener más información acerca de cómo configurar la señalización para una puerta de enlace VoIP compatible, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

Aunque se pueden usar otros métodos de señalización, los dos más conocidos son los siguientes:

  - **Interfaz de escritorio de mensajería simplificada (SMDI):** SMDI es un protocolo que se usa para proporcionar información de señalización, control de llamadas e identificación de llamadas desde una interfaz situada entre un sistema de telefonía y un sistema de correo de voz. Se usa para proporcionar al sistema de correo de voz la información que necesita para procesar las llamadas entrantes. Cada vez que una llamada entrante se envía mediante SMDI a través de una interfaz serie o de una interfaz RS-232, la información que se envía identifica la línea o el puerto, el tipo de llamada y los números de la persona a la que se llama o que hace la llamada. El cable SMDI conecta un dispositivo, como una PBX, con una conexión serie de la puerta de enlace VoIP. No obstante, SMDI también se usa con IP PBX. El protocolo SMDI permite un máximo de 10 dígitos por cada número que llama y cada número llamado. Es una limitación del protocolo y no se puede cambiar.

  - **Interna:** la señalización interna permite el intercambio de información de señalización, control de llamadas e identificación de llamadas desde una compañía telefónica. Esta información se envía por el mismo canal y en la misma banda (300 Hz a 3,4 kHz) que la voz y otros sonidos que se emiten durante la llamada. Por ejemplo, cuando un usuario realiza una llamada mediante marcado DTMF o de tonos de teclado y habla con la persona llamada, tanto los tonos de teclado como la conversación de voz usan el mismo canal y la misma banda. La señalización interna es menos segura, ya que las señales de control se muestran al usuario. Es un método de señalización menos usado que SMDI. La señalización interna se aplica únicamente a la señalización asociada al canal (CAS).

Volver al principio

