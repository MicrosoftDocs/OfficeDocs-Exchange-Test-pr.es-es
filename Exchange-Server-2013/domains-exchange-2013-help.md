---
title: 'Dominios: Exchange 2013 Help'
TOCTitle: Dominios
ms:assetid: 11748c2d-2e32-43a4-b77d-e0c17db6200b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673041(v=EXCHG.150)
ms:contentKeyID: 49895478
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dominios

 

_**Se aplica a:** Exchange Server 2013, Office 365_

_**Última modificación del tema:** 2012-10-11_

Los dominios representan los espacios de nombres SMTP para los cuales se configuran los directorios de correo electrónico y los buzones de correo. Al configurar los dominios que interactúan con su organización de Microsoft Exchange Server 2013, puede configurar cómo procesa el envío de correo electrónico a y desde varios dominios Exchange.

## Dominios aceptados

Un dominio aceptado es cualquier espacio de nombres para el cual su organización de Exchange envía o recibe mensajes de correo electrónico. Los dominios aceptados incluyen aquellos para los que la organización de Exchange está autorizada, además de los dominios de retransmisión interna y externa. Una organización de Exchange está autorizada cuando administra la entrega de correo de los destinatarios en el dominio aceptado. Los dominios aceptados también incluyen dominios para los que la organización de Exchange recibe correo y lo retransmite a un servidor de correo electrónico que está fuera de la organización.

Para obtener más información acerca de los dominios aceptados, consulte [Dominios aceptados](accepted-domains-exchange-2013-help.md).

## Dominios remotos

En Exchange 2013, puede crear entradas de dominio remoto para definir la configuración de transferencia de mensajes entre la organización de Exchange y los dominios fuera de su organización. Cuando se crea una entrada de dominio remoto, se controlan los tipos de mensajes que se envían a ese dominio. También es posible aplicar directivas de formato de mensajes y juegos de caracteres aceptables para los mensajes que se envíen desde usuarios de la organización hasta el dominio remoto.

La configuración para dominios remotos son valores de configuración globales para la organización de Exchange. La configuración del dominio remoto se aplica a los mensajes durante la categorización. Cuando se produce la resolución de destinatarios, el dominio del destinatario se compara con los dominios remotos configurados. Si una configuración de dominio remoto bloquea el envío de un tipo de mensaje específico a los destinatarios de ese dominio, el mensaje se elimina. Si especifica un formato de mensaje en particular para el dominio remoto, los encabezados y el contenido de los mensajes se modifican. La configuración se aplica a todos los mensajes procesados por la organización de Exchange.

Para obtener más información acerca de los dominios remotos, vea [Dominios remotos](remote-domains-exchange-2013-help.md).

