---
title: 'Conectores externos: Exchange 2013 Help'
TOCTitle: Conectores externos
ms:assetid: 21c6a7a9-f4d2-4359-9ac9-930701b63a4e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996779(v=EXCHG.150)
ms:contentKeyID: 49895513
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Conectores externos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-09-25_

Un conector externo entrega mensajes a un servidor o a un sistema externo que no usa SMTP como mecanismo de transporte principal. Un ejemplo de esto puede ser un servidor de la puerta de enlace de fax. Un conector externo usa un directorio de destino local o compartido para enviar mensajes salientes, mediante una transferencia de archivos, al sistema externo. Los conectores externos se pueden crear en el servicio de transportes del servidor de buzones de correo de Microsoft Exchange Server 2013.

Los servidores de puerta de enlace externos pueden enviar mensajes en una organización de Exchange 2013 usando los directorios de recogida o de reproducción que existan en el servicio de transporte de un servidor de buzones de correo. Los archivos de mensajes de correo electrónico con un formato correcto que copia en cada directorio se envían para ser entregados a un buzón de correo de Exchange.


> [!TIP]
> En la mayoría de los casos en que debe entregar mensajes salientes a un sistema que no es SMTP, recomendamos los conectores de agente de entrega porque permiten la administración de colas de mensajes. Además, los mensajes no tienen que escribirse en el sistema de archivos, entre otros beneficios. El tema <A href="delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md">Agentes de entrega y conectores de agentes de entrega</A> proporciona más detalles.



## Más información

[Crear un conector externo para entregar los mensajes a una puerta de enlace no SMTP fax](create-a-foreign-connector-to-deliver-messages-to-a-non-smtp-fax-gateway-exchange-2013-help.md)

[Agentes de entrega y conectores de agentes de entrega](delivery-agents-and-delivery-agent-connectors-exchange-2013-help.md)

[New-ForeignConnector](https://technet.microsoft.com/es-es/library/aa996310\(v=exchg.150\))

[Set-ForeignConnector](https://technet.microsoft.com/es-es/library/bb123789\(v=exchg.150\))

