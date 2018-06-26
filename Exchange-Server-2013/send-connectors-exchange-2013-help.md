---
title: 'Conectores de envío: Exchange 2013 Help'
TOCTitle: Conectores de envío
ms:assetid: 6aa19a12-c7b2-4eac-a8dc-9a4d26919ac5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998662(v=EXCHG.150)
ms:contentKeyID: 49895684
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectores de envío

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-15_

En Microsoft Exchange Server 2013, los conectores de envío controlan el flujo de mensajes salientes al servidor de recepción y están configurados en servidores de buzones que ejecutan el servicio de transporte. En general, los conectores de envío se configuran para enviar mensajes de correo electrónico saliente a un host inteligente, o directamente a su destinatario, a través de DNS.

Los servidores de buzones de Exchange 2013 que ejecutan el servicio de transporte requieren conectores de envío para entregar los mensajes al próximo salto de camino a su destino. Los conectores de envío que se crean en servidores de buzones se almacenan en Active Directory y están disponibles para todos los servidores de buzones que ejecuten el servicio de transporte en la organización.


> [!IMPORTANT]
> Al implementar Exchange&nbsp;2013, no se puede producir un flujo de correo saliente hasta que se configure un conector de envío para enrutar el correo saliente a Internet. Para obtener más información, consulte <A href="create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md">Crear un conector de envío para correo electrónico enviado a Internet</A>.



## Selección del tipo de conector de envío

Generalmente, los conectores de envío se crean en la sección **Flujo de correo** del Centro de administración de Exchange (EAC). Al crear un conector de envío nuevo, debe elegir el **Tipo** adecuado para su entorno de conexión. El tipo determina los conjuntos de permisos predeterminados que se asignan al conector y otorga estos permisos a las entidades de seguridad de confianza. Las entidades de seguridad incluyen usuarios, equipos y grupos de seguridad.

Para ver los procedimientos que explican la selección de un **Tipo** específico, consulte [Crear un conector de envío para enrutar el correo saliente a través de un Host inteligente](create-a-send-connector-to-route-outbound-email-through-a-smart-host-exchange-2013-help.md) y [Crear un conector de envío para enviar correo electrónico a un colaborador con Seguridad de la capa de transporte (TLS) aplicada](create-a-send-connector-to-send-email-to-a-partner-with-transport-layer-security-tls-applied-exchange-2013-help.md).

Si prefiere utilizar el Shell de administración de Exchange en lugar del EAC, cree un conector de envío y especifique un tipo mediante el cmdlet [New-SendConnector](https://technet.microsoft.com/es-es/library/aa998936\(v=exchg.150\)).

## Nuevas características de conectores de envío en Exchange 2013

Los conectores de envío funcionan ahora de manera distinta debido a la relación entre el servicio de transporte frontend en los servidores de acceso de clientes y el servicio de transporte en los servidores de buzones de Exchange 2013. En primer lugar, puede establecer un conector de envío en el servicio de transporte de un servidor de buzones para enrutar el correo saliente a través de un servidor de transporte frontend en el sitio local de Active Directory mediante el parámetro *FrontEndProxyEnabled* del cmdlet [Set-SendConnector](https://technet.microsoft.com/es-es/library/aa998294\(v=exchg.150\)). De este modo, se consolida el modo en que el correo electrónico se enruta desde el servicio de transporte. En [Enrutamiento de correo](mail-routing-exchange-2013-help.md) se ofrece más información acerca de los servicios de transporte, el comportamiento de enrutamiento y los destinos en Exchange 2013. En [Flujo de correo](mail-flow-exchange-2013-help.md) se presenta una descripción general de la canalización del transporte y de las descripciones de los servicios de transporte.

El parámetro *IsCoexistenceConnector* se ha quedado obsoleto. En la mayoría de los casos, cuando desee configurar un entorno híbrido, en el que parte de los buzones están hospedados de forma local y parte en la nube, se recomienda utilizar el asistente de configuración híbrida.

*LinkedReceiveConnector* se ha quedado obsoleto. Este parámetro se usaba para crear conectores que pudieran enrutar mensajes, por ejemplo, a un servicio contra correo electrónico no deseado de terceros. Ahora, en la mayoría de los casos, el correo se enruta al servicio contra correo electrónico no deseado mediante el registro MX, por lo que el comportamiento vinculado a un conector ya no es necesario.

El tamaño máximo de mensaje predeterminado, especificado por el parámetro *MaxMessageSize*, se ha incrementado de 10 MB a 25 MB. En [Set-SendConnector](https://technet.microsoft.com/es-es/library/aa998294\(v=exchg.150\)) se ofrece más información sobre cómo establecer parámetros en un conector de envío.

Se ha agregado *TlsCertificateName*. Se utiliza para autenticar el certificado local que se va a usar para las conexiones salientes y minimizar el riesgo de certificados fraudulentos.

