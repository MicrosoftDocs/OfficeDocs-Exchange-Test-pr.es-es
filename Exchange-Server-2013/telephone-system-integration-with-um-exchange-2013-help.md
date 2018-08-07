---
title: 'Integración del sistema telefónico con UM: Exchange 2013 Help'
TOCTitle: Integración del sistema telefónico con mensajería unificada
ms:assetid: b8790117-b040-4c84-9d34-005c75088e76
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673558(v=EXCHG.150)
ms:contentKeyID: 50556872
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Integración del sistema telefónico con mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Para implementar correctamente la mensajería unificada (UM), se deben conocer y comprender los conceptos y los componentes básicos de telefonía. Después de conocer los conceptos básicos sobre telefonía, puede integrar la mensajería unificada en una organización de Exchange. Los conceptos y componentes básicos incluyen:

  - Redes de conmutación de circuitos y de conmutación de paquetes

  - Central de conmutación (PBX)

  - IP PBX

  - Protocolo de voz sobre Internet (VoIP)

  - Puertas de enlace VoIP

En un entorno local, híbrido o de Office 365, la conexión y la configuración de los componentes de telefonía necesarios representa el paso más complejo e importante para implementar la mensajería unificada correctamente, ya sea con o sin Lync Server Enterprise Voice. Debe conectar y configurar puertas de enlace VoIP, puertas de enlace VoIP avanzadas, PBX, IP PBX y controladores de borde de sesión (SBC) para una red de telefonía convencional y conectarse a una red de telefonía si va a usar Microsoft Lync Server y la mensajería unificada.

La planificación y la ejecución de una nueva implementación de mensajería unificada o la actualización de un sistema de correo de voz heredado puede presentar ciertos desafíos para las organizaciones. Se requiere un gran conocimiento sobre puertas de enlace VoIP, PBX, IP PBX, Microsoft Lync Server y mensajería unificada. En función de la experiencia técnica que tenga con Exchange y con los sistemas de correo de voz, es probable que requiera la asistencia de un especialista en mensajería unificada. Estos especialistas de MU de Exchange le ayudarán a garantizar una transición sencilla desde el sistema de correo de voz heredado o de terceros a una mensajería unificada de Exchange. Para obtener más información acerca de cómo contactar con un especialista en mensajería unificada, consulte [Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists](http://go.microsoft.com/fwlink/p/?linkid=262708) .

## Integrar la red de telefonía

La mensajería unificada requiere que integre su implementación de Exchange Server con su red de telefonía existente o bien integrar la mensajería unificada con Microsoft Lync Server en la organización. Para implementar y administrar correctamente el correo de voz de mensajería unificada, realice un análisis exhaustivo de la infraestructura de telefonía existente o de la implementación de Microsoft Lync Server Enterprise Voice y siga los pasos de planificación necesarios.

## Puertas de enlace VoIP

Al implementar la mensajería unificada en una organización de Exchange, debe instalar, implementar o configurar una o más puertas de enlace VoIP para conectar las PBX a la red de telefonía, o bien instalar, implementar y configurar PBX habilitadas con el Protocolo de inicio de sesión (SIP) o IP PBX.

Una puerta de enlace VoIP es un dispositivo de hardware de terceros que conecta una PBX heredada a una LAN. La puerta de enlace VoIP permite al sistema PBX comunicarse con los servidores Exchange de su organización.

La mensajería unificada depende de la capacidad de la puerta de enlace VoIP para traducir o convertir la multiplexación por división de tiempo (TDM) o los protocolos basados en conmutación de circuitos, como ISDN o QSIG, desde una PBX a los protocolos basados en IP o VoIP como SIP, el protocolo de transporte en tiempo real (RTP) o T.38 para el transporte de facsímil en tiempo real. La puerta de enlace VoIP forma parte integral de la funcionalidad y la operación de la mensajería unificada. La puerta de enlace VoIP también puede conectar con sistemas PBX que usen VoIP en lugar de protocolos de conmutación de circuitos de red de telefonía conmutada (PSTN).

Elegir la puerta de enlace VoIP correcta y aspectos como la IP PBX, PBX con SIP habilitada o SBC es solo el primer paso para integrar su red de telefonía en la mensajería unificada. Debe configurar dichos dispositivos para que funcionen con la mensajería unificada. En implementaciones locales e híbridas, debería implementar los servidores de acceso de cliente y de buzones de correo y crear y configurar todos los componentes necesarios de mensajería unificada. Para Office 365 con correo de voz hospedado, no es necesario que instale ni configure ningún servidor. Los componentes le permitirán realizar la conexión desde la red de telefonía de conmutación de circuitos hasta su red de datos IP y habilitar así el correo de voz para los usuarios de la organización. Para obtener más detalles y ver los dispositivos de telefonía compatibles, consulte los siguientes recursos:

  - [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md)

  - [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Notas de configuración de los controladores de borde de sesión admitidos](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

## Microsoft Lync Server

La mensajería unificada puede utilizar Microsoft Lync Server para combinar la mensajería de voz, la mensajería instantánea, la presencia mejorada, la conferencia de audio y vídeo y el correo electrónico en una experiencia de comunicación integrada y familiar. Al ofrecer las características de Enterprise Voice a los usuarios de la organización mediante la integración de la mensajería unificada y Microsoft Lync Server, podrá beneficiarse de las siguientes ventajas:

  - Mejora de la presencia de los avisos en una serie de aplicaciones que mantienen informados a los usuarios sobre la disponibilidad de los contactos.

  - Integración de mensajería instantánea, mensajes de voz, conferencias, correo electrónico y otros modos de comunicación que permiten a los usuarios elegir el modo más adecuado para la tarea. Además, los usuarios pueden alternar entre los modos según necesiten.

  - Disponibilidad de alternativas para la comunicación desde cualquier punto en el que haya disponible una conexión a Internet.

  - Un cliente inteligente (Microsoft Lync) para telefonía, mensajería instantánea y conferencias.

  - Continuidad de la experiencia del usuario en varios dispositivos.

El componente de enrutamiento de mensajería unificada de Exchange administra el enrutamiento de correo de voz entre Lync Server y los servidores Exchange para integrar Lync Server con las características de mensajería unificada. El componente de enrutamiento de mensajería unificada de Exchange que se incluye en Lync Server también se encarga de enrutar el correo de voz en la red RTC cuando los servidores Exchange no están disponibles. Si implementó Enterprise Voice en varias sucursales, y dichos sitios no tienen un vínculo WAN resistente a un sitio central, la aplicación de sucursal con funciones de supervivencia que implemente en la sucursal proporcionará correo de voz a los usuarios de la sucursal si se produce un error en el vínculo WAN. Cuando el vínculo WAN no está disponible, la aplicación de sucursal con funciones de supervivencia hace lo siguiente:

  - Vuelve a enrutar las llamadas sin responder a través de la red RTC a un servidor Exchange del sitio central.

  - Permite que los usuarios recuperen mensajes de voz a través de la PSTN.

  - Pone las notificaciones de llamada perdida en cola y, a continuación, las carga al servidor Exchange cuando se restablece el vínculo WAN.

Para obtener más información acerca de Microsoft Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).


> [!WARNING]
> Al integrar la mensajería unificada y Lync Server, en una implementación local o híbrida, las notificaciones de llamadas perdidas no estarán disponibles para los usuarios que tengan un buzón en un servidor de buzones de correo Exchange&nbsp;2007 o Exchange&nbsp;2010. Las notificaciones de llamadas perdidas se generan cuando un usuario se desconecta antes de que la llamada se envíe a un servidor de buzones.


