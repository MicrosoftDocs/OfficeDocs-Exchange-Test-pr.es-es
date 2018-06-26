---
title: 'Diseño de mensajería unificada: Exchange 2013 Help'
TOCTitle: Diseño de mensajería unificada
ms:assetid: 942788b1-b19d-40b3-a52e-2e1fef8df3f9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ674306(v=EXCHG.150)
ms:contentKeyID: 49895789
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Diseño de mensajería unificada

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Al diseñar la implementación de la mensajería unificada (MU), existen muchos factores que debe tener en cuenta para poder implementarla correctamente. Es preciso que conozca los distintos elementos de la mensajería unificada, así como cada componente y característica, para poder diseñar adecuadamente su infraestructura e implementación. La asignación de tiempo para planear y resolver estos problemas ayudará a impedir que surjan problemas al implementar la mensajería unificada en la organización.

Puede implementar la mensajería unificada en una organización nueva de Exchange o bien actualizarla a partir de una solución de correo de voz heredada o de terceros. Si está actualizándola, deberá decidir si desea convertir los dispositivos que aceptan protocolos basados en circuitos de telefonía a una red de datos a través de IP o si desea implementar una solución Enterprise Voice, como Microsoft Lync Server. Este es solamente el primer paso para entender e implementar la mensajería unificada en su organización.

## Diseñar el sistema de correo de voz

La mensajería unificada proporciona mensajes de voz, fax y mensajes de correo electrónico en un almacén al que se puede tener acceso desde un teléfono, el equipo de un usuario o un dispositivo móvil. Los usuarios pueden tener acceso a los mensajes de voz, al correo, a la información de calendario y a los contactos personales ubicados en su buzón de Exchange desde clientes de correo electrónico, como por ejemplo Outlook y Outlook Web App.

Los servidores de acceso de cliente que ejecutan el servicio de enrutador de llamadas de mensajería unificada y los servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange están diseñados para proporcionar características de correo de voz para los usuarios de su organización.

Los servidores de buzones de correo se basan en los servidores de acceso de cliente para reenviar el tráfico SIP de las llamadas entrantes y, a continuación, establecen una conexión con una puerta de enlace VoIP, IP PBX o Session Border Controller (SBC) y aceptan el tráfico de medios RTP/SRTP. Todos los mensajes de correo de voz y fax se envían desde el servicio de mensajería unificada de Microsoft Exchange a un servidor de buzones para que se entreguen al buzón del usuario. Para que un usuario utilice las características de correo de voz con la mensajería unificada, debe tener un buzón de Exchange.

## Diseño de la implementación de la mensajería unificada

Por lo general, cuanto más simple sea la topología de mensajería unificada, mas fácil será implementarla y mantenerla. Instale el menor número posible de servidores de acceso de cliente y de buzones y cree el menor número de componentes de MU como sean necesario (como planes de marcado de MU, operadores automáticos y directivas de buzones de MU) para cubrir los objetivos empresariales y organizativos que necesite. Las grandes empresas con complejos entornos de red y de telefonía, múltiples unidades de negocio u otras características complejas requieren una planificación mayor que las organizaciones más pequeñas con necesidades de mensajería unificada relativamente sencillas.

Las siguientes son algunas de las áreas que debería tener en cuenta a la hora de diseñar la mensajería unificada en la organización:

  - **Requisitos organizativos**   Evalúe las necesidades de su compañía, la utilidad de implementar un sistema de correo de voz, su red física y topología empresarial, así como los requisitos de seguridad de la organización.

  - **Requisitos de telefonía**   Revise su telefonía existente, la red de circuitos conmutados y el sistema de correo de voz.

  - **Requisitos de red**   Analice la topología de su red, su diseño actual de red IP de paquetes combinados, incluidos los puntos de conectividad LAN y WAN, así como también los dispositivos.

  - **Active Directory (servicio de directorios)**   Observe la implementación y el diseño actuales, y piense sobre cómo integrará la MU.

  - **Modelo de implementación**   Decida si desea tener una implementación de MU híbrida, en línea o local.

  - **Requisitos de Exchange** Determine lo siguiente:
    
      - cuántos usuarios utilizarán el correo de voz,
    
      - y qué características de MU y servicios desea implementar (como llamadas concurrentes, acceso interno y externo a usuarios, fax entrantes, previsualización de correo de voz, etc.).
    
      - El número de servidores de acceso de cliente y buzones que necesitará implementar.
    
      - Los requisitos de almacenamiento y las cuotas para los usuarios de correo de voz.
    
      - El mejor diseño de alta disponibilidad y resistencia del sitio. Esto incluye requisitos del sistema de MU, proporcionando una alta disponibilidad y una implementación de MU escalable, así como requisitos de hardware del sistema para garantizar su rendimiento.

  - **Integración con componentes y dispositivos de telefonía**   Decida si desea usar el equipo de telefonía tradicional o Microsoft Lync Server. Considere la posibilidad de añadir puertas de enlace VoIP, equipos de telefonía y servidores de acceso de cliente y buzones, y si desea habilitar Enterprise Voice en la organización.

## Conectar la red de telefonía

La mensajería unificada requiere que integre su implementación de Exchange Server con su sistema de telefonía existente o bien con Microsoft Lync Server. Debe realizar un análisis exhaustivo de la infraestructura de telefonía existente de la que dispone y Microsoft Lync Server. A continuación, deberá seguir los pasos de diseño correctos para poder implementar y administrar el correo de voz de MU correctamente.

**Puertas de enlace VoIP** Elegir la puerta de enlace VoIP correcta y aspectos como la IP PBX, PBX con SIP habilitada o SBC es solo el primer paso para integrar su red de telefonía a la MU. Debe configurar estos dispositivos para que funcionen con la MU, implementar los servidores requeridos de acceso de cliente y buzones, y crear y configurar todos los componentes de MU necesarios. Estos componentes le permitirán realizar la conexión desde la red de protocolo basado en circuitos a su red de datos IP y así proporcionar el correo de voz a sus usuarios.

**Microsoft Lync Server**   La mensajería unificada puede utilizar Microsoft Lync Server para combinar la mensajería de voz, la mensajería instantánea, la presencia mejorada, la conferencia de audio y video, y el correo electrónico en una experiencia de comunicación integrada y familiar. La integración de mensajería unificada y Microsoft Lync Server tiene las siguientes ventajas:

  - Mejora de la presencia de los avisos en una serie de aplicaciones que mantienen informados a los usuarios sobre la disponibilidad de los contactos.

  - Integración de mensajería instantánea, mensajes de voz, conferencias, correo electrónico y otros métodos de comunicación que permiten a los usuarios elegir el método más adecuado para la tarea. Los usuarios pueden alternar entre los métodos según necesiten.

  - Disponibilidad de alternativas para la comunicación desde cualquier punto en el que haya disponible una conexión a Internet.

  - Un cliente inteligente (Microsoft Lync) para telefonía, mensajería instantánea y conferencias.

  - Continuidad de la experiencia del usuario en varios dispositivos.

Para obtener más información acerca de Microsoft Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).


> [!NOTE]
> Diseñar e implementar la mensajería unificada puede plantear algunos retos. En función de la experiencia técnica que tenga con Exchange y con los sistemas de correo de voz, es probable que requiera la asistencia de un especialista en mensajería unificada. Estos especialistas de MU de Exchange le ayudarán a garantizar una transición sencilla desde el sistema de correo de voz heredado o de terceros a una mensajería unificada de Exchange. Se necesitan amplios conocimientos sobre puertas de enlace VoIP, PBX y de mensajería unificada para realizar una nueva implementación o actualizar un sistema de correo de voz heredado. Para obtener más información acerca de cómo contactar con un especialista en mensajería unificada, consulte <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">Microsoft Exchange Server 2013 Unified Messaging (UM) Specialists</A> .



## Pasos para la implementación

Existen muchas opciones de implementación disponibles para mensajería unificada. Cada opción tiene varios pasos en común que se requieren para crear un sistema escalable y de alta disponibilidad. Estos pasos son los siguientes:

1.  Implemente y configure los componentes de telefonía o Microsoft Lync Server con la mensajería unificada.

2.  Compruebe que haya instalado correctamente los servidores Acceso de cliente y de buzones necesarios para la mensajería unificada.

3.  Cree y configure los componentes requeridos de mensajería unificada, incluidos los planes de marcado de mensajería unificada, las puertas de enlace IP de mensajería unificada, los grupos de extensiones de mensajería unificada y las directivas de buzones de mensajería unificada.

4.  Realice las tareas posteriores a la implementación, incluida la obtención de certificados para TLS mutua, la creación de operadores automáticos de mensajería unificada y la configuración del servicio de fax.

Para obtener información acerca de la implementación de mensajería unificada, consulte [Implementar mensajería unificada de Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Si está integrando su entorno de mensajería unificada en Microsoft Lync Server, hay que añadir más consideraciones en la planificación. Para obtener información más detallada, consulte [Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

