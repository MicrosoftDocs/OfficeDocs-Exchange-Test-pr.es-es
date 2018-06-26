---
title: 'Dominios remotos: Exchange 2013 Help'
TOCTitle: Dominios remotos
ms:assetid: 10fb7d62-4d78-40a3-82db-d62bcd27ba42
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996309(v=EXCHG.150)
ms:contentKeyID: 49895475
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Dominios remotos

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Puede crear entradas de dominio remoto para definir las opciones de transferencia de mensajes entre la organización de Microsoft Exchange Server 2013 y los dominios fuera de la organización de Exchange. Cuando se crea una entrada de dominio remoto, se controlan los tipos de mensajes que se envían a ese dominio. También es posible aplicar directivas de formato de mensajes y juegos de caracteres aceptables para los mensajes que se envíen desde usuarios de la organización hasta el dominio remoto. La configuración para dominios remotos son valores de configuración globales para la organización de Exchange.

Las configuraciones del dominio remoto se aplican a los mensajes durante la categorización en los servidores de transporte y de buzones de correo. Cuando se produce la resolución de destinatarios, el dominio del destinatario se compara con los dominios remotos configurados. Si una configuración de dominio remoto bloquea el envío de un tipo de mensaje específico a los destinatarios de ese dominio, el mensaje se elimina. Si especifica un formato de mensaje en particular para el dominio remoto, los encabezados y el contenido de los mensajes se modifican. La configuración se aplica a todos los mensajes procesados por la organización de Exchange.


> [!NOTE]
> Si establece valores de configuración de mensajes por usuario, la configuración por usuario reemplaza la configuración de la organización.



De forma predeterminada, hay una única entrada de dominio remoto. El espacio de la dirección de dominio está configurado como un asterisco (\*). Esto representa todos los dominios remotos. Si no crea entradas de dominio remoto adicionales, se aplica la misma configuración a todos los mensajes que se envían a todos los destinatarios de todos los dominios remotos.

Cuando configure dominios remotos, puede impedir que se envíen ciertos tipos de mensajes a ese dominio. Estos tipos de mensaje incluyen los mensajes de fuera de la oficina, mensajes de respuesta automática, informes de no entrega (NDR) y notificaciones de reenvío de reunión. Si tiene un entorno con varios bosques, quizá desee permitir el envío de esos tipos de mensajes a esos dominios. Sin embargo, si ha identificado un dominio desde el que se origine correo electrónico no deseado, quizá desee bloquear el envío de esos tipos de mensajes a esos dominios remotos.

**Contenido**

Formato del mensaje

Configuración de respuestas automáticas

Control de la información de NDR

## Formato del mensaje

Puede especificar el formato de mensaje y el juego de caracteres a usar para los mensajes de correo electrónico que se envían a dominios remotos. Estas configuraciones pueden ser útiles para garantizar que el correo electrónico enviado por remitentes del dominio propio al dominio remoto sea compatible con el sistema de correo electrónico receptor. Por ejemplo, si sabe que el sistema de mensajería del dominio remoto es Exchange, puede especificar que siempre se use el formato de texto enriquecido (RTF) de Exchange. Para obtener más información, consulte [Conversión de contenido](content-conversion-exchange-2013-help.md).

## Configuración de respuestas automáticas

En Exchange 2013, los usuarios pueden establecer respuestas automáticas distintas para los destinatarios internos que para los externos. Además, los tipos de respuestas automáticas disponibles para cada organización dependen de la versión de Microsoft Outlook que se use.

En Exchange 2013, hay dos tipos de respuestas automáticas:

  - **Externas**   Admitidas por Exchange 2013 y Exchange 2010. Éstas solo se pueden establecer mediante Outlook 2010 o Office Outlook 2007, o también mediante Microsoft Office Outlook Web App.

  - **Internas**   Admitidas por Exchange 2013 y Exchange 2010. Éstas solo se pueden establecer mediante Outlook 2010 o Outlook 2007, o también mediante Outlook Web App.

La tabla que aparece a continuación describe diversas combinaciones de cliente y servidor, y los tipos de respuestas automáticas que se pueden usar en cada escenario.

**Compatibilidad de clientes y servidores para respuestas automáticas**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Versión de cliente</th>
<th>Versión de Exchange</th>
<th>Respuestas automáticas admitidas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2010 o Outlook 2007</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>Internas, externas</p></td>
</tr>
<tr class="even">
<td><p>Outlook Web App</p></td>
<td><p>Exchange 2013Exchange 2010Exchange 2007</p></td>
<td><p>Internas, externas</p></td>
</tr>
</tbody>
</table>


## Control de la información de NDR

Como se mencionó al inicio de este tema, puede evitar que los NDR se envíen a un dominio remoto. Al bloquear los NDR que se envían a un dominio remoto, puede evitar que la información contenida en el mensaje de NDR deje la organización y, de ese modo, se limita el conocimiento que puede obtener un usuario malintencionado acerca de su organización. Sin embargo, esto también evita que remitentes legítimos reciban NDR, lo que provoca confusión y pérdida de productividad.

Exchange 2013 le proporciona un control granular de los contenidos de un NDR destinado para un dominio remoto. Con Exchange 2013, puede permitir NDRs en un dominio remoto y, a la vez, quitar toda información de diagnóstico. De esta forma, puede evitar que la información acerca de la implementación de Exchange deje su organización y, al mismo tiempo, proporcionar notificaciones de NDR a remitentes externos.

Esta característica se controla con el parámetro nuevo *NDRDiagnosticInfoEnabled* en el cmdlet **Set-RemoteDomain**. Debido a que esta configuración se puede configurar para todos los dominios remotos, puede tener configuraciones distintas basadas en sus necesidades. Por ejemplo, puede elegir quitar la información de diagnóstico de NDR para el dominio remoto predeterminado y permitir la información de diagnóstico de NDR completa para los dominios remotos que representan sus socios.

Para obtener más información acerca de esta configuración nueva, consulte [Set-RemoteDomain](https://technet.microsoft.com/es-es/library/aa997857\(v=exchg.150\)).

