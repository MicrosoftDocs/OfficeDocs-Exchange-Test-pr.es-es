---
title: 'Conectar la UM para su sistema telefónico: Exchange 2013 Help'
TOCTitle: Conectar la mensajería unificada para su sistema telefónico
ms:assetid: 92c3e029-f732-4d6d-b147-2b3006d5f088
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673544(v=EXCHG.150)
ms:contentKeyID: 50556861
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conectar la mensajería unificada para su sistema telefónico

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-30_

La mensajería unificada combina la mensajería de voz y la mensajería del correo electrónico en un buzón de correo al que se puede tener acceso desde muchos dispositivos diferentes. Los usuarios pueden escuchar los mensajes de correo de voz desde su Bandeja de entrada del correo electrónico o desde cualquier teléfono si utilizan Outlook Voice Access.

Al implementar mensajería unificada en una organización de Microsoft Exchange, debe instalar, implementar y configurar una única o varias puertas de enlace de voz sobre IP (VoIP) para conectar a las centrales de conmutación (PBXs) en su red de telefonía o instalar, implementar y configurar PBX con protocolo de inicio de sesión (SIP) habilitado o IP PBX. Si actualiza su sistema de correo de voz actual, deberá implementar los dispositivos que se conectan a su red de telefonía, instalar sus servidores de acceso de cliente de Exchange y de buzones de correo y crear los componentes de mensajería unificada necesarios que le permitan conectar su red de telefonía con su red de datos. Esto permite que las llamadas entrantes de la red de telefonía se conecten a sus puertas de enlace VoIP, IP PBX o PBX con SIP habilitado, y que estos dispositivos se conecten a su organización de Exchange.

Si instala, implementa y configura Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server, no usará puertas de enlace VoIP, IP PBX, ni PBX con SIP habilitado para conectar directamente con la mensajería unificada de Exchange. En su lugar, un Lync Mediation Server y una puerta de enlace VoIP o una puerta de enlace VoIP avanzada que tenga la funcionalidad de un Mediation Server y una puerta de enlace VoIP le permitirán conectar a la mensajería unificada de Exchange. Los usuarios de mensajería unificada con Enterprise Voice habilitado pueden recuperar, escuchar y responder a los mensajes de voz y realizar llamadas salientes. También tienen acceso a otras características relacionadas con Lync incluyendo la presencia y la mensajería instantánea usando Office Communicator o un cliente Lync.

La siguiente información le ayudará a establecer e implementar la mensajería unificada y habilitar las características de correo de voz para los usuarios de una organización:

  - [Conectar una puerta de enlace VoIP, IP PBX o un controlador de borde de sesión a mensajería unificada](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)   Más información acerca de cómo conectar puertas de enlace VoIP o IP PBX con la mensajería unificada.

  - [Asesor de telefonía para Exchange 2013](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephony-advisor-for-exchange-2013)   Más información acerca de las puertas de enlace de VoIP compatibles, IP PBX y PBX.

  - [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways)  Más información acerca de cómo establecer sus puertas de enlace de VoIP, IP PBX y PBX.

