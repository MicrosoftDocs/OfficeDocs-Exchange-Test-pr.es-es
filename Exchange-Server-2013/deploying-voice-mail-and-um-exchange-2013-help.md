---
title: 'Implementación del correo de voz y mensajería unificada: Exchange 2013 Help'
TOCTitle: Implementación del correo de voz y mensajería unificada
ms:assetid: 3df61b62-a1e4-41fb-969c-319189ae4e42
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673519(v=EXCHG.150)
ms:contentKeyID: 49895591
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Implementación del correo de voz y mensajería unificada

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

La mensajería unificada (MU) de Exchange le permite proporcionar servicios de correo de voz a usuarios en su organización. Cuando implemente la mensajería unificada, debe integrar su implementación de Exchange Server con el sistema de telefonía existente para su organización o con Microsoft Lync Server. Una implementación correcta requiere un análisis cuidadoso de la infraestructura telefónica existente y la realización de los pasos de planificación adecuados para implementar y administrar el correo de voz en la mensajería unificada. Si integra Exchange con Lync Server, también debe familiarizarse con el producto.

Cuando implementa la Mensajería unificada, tiene varias opciones, según el hardware de telefonía de su organización. Si está conectando la MU a su red telefónica, es posible que tenga una de las siguientes configuraciones en su organización:

  - Una o varias puertas de enlace VoIP con uno o varios sistemas PBX

  - Uno o varios IP PBX

  - Uno o varios sistemas PBX habilitados para SIP

  - Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server 2010 o 2013


> [!WARNING]
> Cuando implemente la MU de Exchange en un entorno híbrido o alojado, debe implementar controladores de borde de sesión (SBC). Los SBC no permiten a la MU conectarse a una red telefónica o proporcionar tono de marcado a una organización. Sin embargo, sí conectan sus implementaciones de MU locales a un centro de datos con el protocolo IP mediante una WAN pública o privada.



**Hardware de telefonía** Elegir la puerta de enlace VoIP, IP PBX o SBC correctos es solo el primer paso para integrar su red de telefonía a la MU. Debe configurar dichos dispositivos para trabajar con mensajería unificada, implementar los servidores de acceso de clientes y de buzones de correo y crear y configurar todos los componentes de mensajería unificada necesarios. Estos componentes le permiten conectar su red de protocolo basada en circuitos con su red de datos IP y habilitar el correo de voz para los usuarios de su organización. Para obtener información más detallada, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md).

**Microsoft Lync Server**    La mensajería unificada puede utilizar Microsoft Lync Server para combinar la mensajería de voz, la mensajería instantánea, la presencia mejorada, la conferencia de audio y video y el correo electrónico en una experiencia de comunicación integrada y familiar. La integración de mensajería unificada y Lync Server tiene las siguientes ventajas:

  - Mejora de la presencia de los avisos en una serie de aplicaciones que mantienen informados a los usuarios sobre la disponibilidad de los contactos.

  - Integración de mensajería instantánea, mensajes de voz, conferencias, correo electrónico y otros métodos de comunicación para permitir a los usuarios elegir el método más adecuado para la tarea. Los usuarios pueden alternar entre los métodos según necesiten.

  - Disponibilidad de alternativas para la comunicación desde cualquier punto en el que haya disponible una conexión a Internet.

  - Un cliente inteligente (Microsoft Lync) para telefonía, mensajería instantánea y conferencias.

  - Continuidad de la experiencia del usuario en varios dispositivos.

Para obtener más información acerca de Lync Server, consulte [Microsoft Lync Server](https://go.microsoft.com/fwlink/p/?linkid=265752).

## Pasos para la implementación

Existen muchas opciones de implementación disponibles para mensajería unificada. Cada opción tiene varios pasos en común que se requieren para crear un sistema escalable y de alta disponibilidad. Estos pasos son los siguientes:

1.  Implemente y configure los componentes de telefonía o Microsoft Lync Server con la mensajería unificada.

2.  Compruebe que haya instalado correctamente los servidores Acceso de cliente y de buzones necesarios para la mensajería unificada.
    

    > [!WARNING]
    > Debe implementar al menos un servidor de buzones de Exchange 2013 en su organización antes de configurar las puertas de enlace VoIP o las centrales de conmutación (PBX) de IP para enviar protocolos de inicio de sesión (SIP) de UM y tráfico RTP a los servidores de acceso de cliente de Exchange 2013.



3.  Cree y configure los componentes de mensajería unificada, incluidos los planes de marcado de mensajería unificada, las puertas de enlace IP de mensajería unificada, los grupos de extensiones de mensajería unificada y las directivas de buzón de mensajería unificada.

4.  Realice las tareas posteriores a la implementación, incluida la implementación de certificados para TLS mutua, la creación de operadores automáticos de mensajería unificada y la configuración del características de clientes.

Para obtener más información acerca de cómo implementar la mensajería unificada, consulte [Implementar mensajería unificada de Exchange 2013](deploy-exchange-2013-um-exchange-2013-help.md).

Si está integrando su entorno de mensajería unificada en Microsoft Lync Server, hay que añadir más consideraciones en la planificación. Para obtener información más detallada, consulte [Resumen de implementación de Mensajería unificada de Exchange 2013 y Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md).

