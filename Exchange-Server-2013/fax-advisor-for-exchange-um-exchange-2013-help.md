---
title: 'Asesor de fax para la mensajería unificada de Exchange: Exchange 2013 Help'
TOCTitle: Asesor de fax para la mensajería unificada de Exchange
ms:assetid: 928a466d-cc0c-4160-bd4c-f0fc76b038d4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee364747(v=EXCHG.150)
ms:contentKeyID: 52061908
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Asesor de fax para la mensajería unificada de Exchange

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

La Mensajería unificada de Microsoft se basa en las soluciones certificadas de asociados de fax para obtener funcionalidades de fax mejoradas, como fax saliente o enrutamiento de fax. La configuración predeterminada no permite que los usuarios reciban mensajes de fax entrantes para entregarlos a un usuario habilitado para mensajería unificada. Los servidores Exchange envían las solicitudes de fax a una solución de socio de fax certificado. El servidor de socios de fax recibe los datos del fax y, a continuación, los envía al buzón de correo del destinatario en un mensaje de correo electrónico con el fax incluido como archivo .tif adjunto. Para obtener información detallada, consulte [Permitir que los usuarios de correo de voz reciban faxes](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md).


> [!IMPORTANT]
> Recomendamos a todos los clientes que planean implementar la mensajería unificada que consigan la ayuda de un especialista en la materia. Un especialista en mensajería unificada ayudará a garantizar que exista una transición correcta del sistema de correo de voz heredado a la mensajería unificada. Se necesitan amplios conocimientos de PBX y de mensajería unificada para realizar una nueva implementación o actualizar un sistema de correo de voz heredado. Para obtener más información acerca de cómo contactar con un especialista en mensajería unificada, consulte las páginas sobre <A href="http://go.microsoft.com/fwlink/p/?linkid=262708">especialistas en mensajería unificada de Microsoft Exchange Server 2013</A> o <A href="https://go.microsoft.com/fwlink/p/?linkid=261951">mensajería unificada de Microsoft Pinpoint</A>.



## Programa de socios de fax de mensajería unificada de Exchange

Para convertirse en un socio de fax certificado para interactuar con la UM de Exchange, el socio debe implementar los requisitos incluidos en la especificación de interoperabilidad de socios de fax y la solución de fax debe estar certificada por un proveedor de certificación independiente. Para obtener más información acerca de la certificación de un producto de fax para trabajar con la mensajería unificada de Exchange, envíe una solicitud a los [socios de fax para mensajería unificada](mailto:fax-part@microsoft.com).

## Soluciones de socios de fax certificados como interoperables con la mensajería unificada

Si ya ha implementado la Mensajería unificada de Exchange y está buscando un socio de fax que pueda habilitar faxes entrantes en su organización, consulte el artículo sobre [Microsoft Pinpoint para socios de fax](https://go.microsoft.com/fwlink/p/?linkid=190238). Estos proveedores de software están certificados para interaccionar con Exchange Server e incluyen soluciones de software certificadas para mensajería unificada.

## Compatibilidad con puertas de enlace de medios, VoIP e IP PBX

La configuración correcta de las puertas de enlace VoIP de la organización es una tarea de difícil implementación que se debe realizar para implementar correctamente la mensajería unificada de Exchange con los faxes entrantes. Para ayudar a responder preguntas y obtener la información más reciente sobre la configuración de puertas de enlace VoIP, consulte [Asesor de telefonía para Exchange 2013](telephony-advisor-for-exchange-2013-exchange-2013-help.md). [Notas para la configuración de puertas de enlace de VoIP, IP PBX y PBX compatibles](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md) proporciona información y archivos de configuración de la puerta de enlace VoIP que debe tener para configurar correctamente las puertas de enlace VoIP, las IP PBX y las SBC de su organización para que funcionen con la mensajería unificada de Exchange.

La prueba de interoperabilidad de la mensajería unificada de Exchange con puertas de enlace VoIP ahora está integrada con el programa de comunicaciones unificadas e interoperabilidad abierta de Microsoft. Para obtener más información, consulte el [Programa de Comunicaciones Unificadas e Interoperabilidad Abierta de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=140722).

El programa de certificación del [Programa de comunicaciones unificadas e interoperabilidad abierta de Microsoft](http://go.microsoft.com/fwlink/p/?linkid=140722) para puertas de enlace VoIP e IP PBX garantiza que los clientes tengan una experiencia de instalación y compatibilidad sin problemas cuando utilizan puertas de enlace e IP-PBX de telefonía cualificada con software de comunicaciones unificadas de Microsoft.


> [!IMPORTANT]
> El envío y la recepción de faxes mediante T.38 o G.711 no se admite en entornos en los que la mensajería unificada y Communications Server 2007 R2 o Microsoft Lync Server están integrados.



## Implementación y configuración de fax

La mensajería unificada reenvía las llamadas de fax entrantes a una solución de socios de fax dedicado que, luego, relaciona la llamada de fax con el remitente del fax y lo recibe en nombre del usuario habilitado para mensajería unificada. Sin embargo, para permitir que los usuarios habilitados para mensajería unificada reciban mensajes de fax en sus buzones de correo, primero debe configurar el servidor del socio de fax y, luego, configurar los planes de marcado de UM, las directivas de buzón de correo de UM y habilitar a los usuarios habilitados para UM para que reciban faxes. Para obtener información detallada, consulte [Configuración de faxes entrantes](setting-up-incoming-faxing-exchange-2013-help.md).

