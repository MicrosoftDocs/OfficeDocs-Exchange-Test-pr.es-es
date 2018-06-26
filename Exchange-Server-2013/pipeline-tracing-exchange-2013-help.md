---
title: 'Seguimiento del canal: Exchange 2013 Help'
TOCTitle: Seguimiento del canal
ms:assetid: e7780499-9a6f-48b1-aea8-df88ecd8b18a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125018(v=EXCHG.150)
ms:contentKeyID: 52062073
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Seguimiento del canal

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El seguimiento de canalización captura copias de mensajes de correo electrónico de un remitente específico mientras se mueven a través del servicio de transporte en los servidores de buzones de correo, el servicio de entrega de transporte de buzones de correo en los servidores de buzones de correo y a través de los servidores de transporte perimetral. El seguimiento de canalización captura información detallada acerca de los cambios que cada agente de transporte aplica a los mensajes en la canalización de transporte en archivos de instantáneas de mensajes. Al examinar los contenidos de los archivos de instantáneas de mensajes, puede determinar si los agentes de transporte han aplicado los cambios a los mensajes en el conducto de transporte que esperaba. Si está solucionando un problema, debería determinar qué agente de transporte presenta el error. A continuación, se puede centrar en los esfuerzos de solución de problemas en ese agente para solucionar el problema. Puede ver, a continuación, los archivos de instantáneas de mensajes de nuevo para comprobar que la solución es satisfactoria.


> [!WARNING]
> <UL>
> <LI>
> <P>El seguimiento de canalización copia todo el contenido de los mensajes de correo electrónico que se envían desde la dirección de correo del remitente. Para evitar la exposición no deseada de información confidencial, deberá establecer los permisos de seguridad adecuados en la carpeta de seguimiento de canalización.</P>
> <LI>
> <P>No habilite el seguimiento de canalización durante largos períodos de tiempo. El seguimiento de canalización crea archivos que se pueden acumular rápidamente. Compruebe siempre el espacio disponible en disco cuando esté habilitado el seguimiento de canalización.</P></LI></UL>



## Configuración del seguimiento de canalización

Antes de habilitar el seguimiento de canalización, debe especificar la dirección de correo electrónico del remitente que quiere supervisar. El seguimiento de canalización está diseñado para registrar los mensajes enviados desde una dirección de correo electrónico específica. La dirección de correo electrónico del remitente puede ser interna o externa a la organización de Exchange. De manera alternativa, puede habilitar el seguimiento de canalización de los mensajes del sistema generados por el servicio de transporte en el servidor de buzones de correo o en el servidor de transporte perimetral especificados, como respuestas automáticas, mensajes de notificación de estado de entrega (DSN), informes de diario y otros mensajes generados por el sistema. También puede modificar la ubicación de la carpeta de seguimiento de canalización.

Los parámetros que usa para configurar el seguimiento de canalización se resumen en la siguiente tabla


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parámetro</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingSenderAddress</em></p></td>
<td><p>En blanco (<code>$null</code>)</p></td>
<td><p>Especifique la dirección de correo electrónico del remitente que quiere supervisar.</p>
<p>Especifique el valor &quot;&lt;&gt;&quot; para supervisar los mensajes generados por el sistema enviados por el servicio de transporte especificado en el servidor.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingPath</em></p></td>
<td><p><strong>Servicio de transporte</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Hub\PipelineTracing</code></p>
<p><strong>Servicio de transporte de buzones de correo</strong> <code>%ExchangeInstallPath%TransportRoles\Logs\Mailbox\PipelineTracing</code></p></td>
<td><p>La ruta de acceso debe estar en el servidor local. No se admiten rutas de acceso UNC.</p>
<p>La ruta de acceso especificada contiene la carpeta <code>MessageSnapshots</code> donde se almacenan los archivos de seguimiento de canalización.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>PipelineTracingEnabled</em></p></td>
<td><p><code>$false</code></p></td>
<td><p>Solo puede habilitar el seguimiento de canalización para el servicio de transporte especificado en el servidor después de configurar la dirección del remitente que quiere supervisar.</p></td>
</tr>
</tbody>
</table>


Para obtener más información acerca de cómo habilitar el seguimiento de conductos y configurar la dirección del remitente para el seguimiento de conductos, vea [Configuración del seguimiento de canalización](configure-pipeline-tracing-exchange-2013-help.md) .

## Archivos de instantáneas de mensajes

Las instantáneas de mensaje son archivos que capturan los cambios realizados en un mensaje por agentes de transporte en el servicio de transporte o en el servicio de entrega de transporte de buzones de correo. Estos archivos se almacenan en la carpeta `MessageSnapshots` en la ruta de acceso de seguimiento de canalización correspondiente del servicio de transporte.

En la carpeta `MessageSnapshots`, Exchange crea una carpeta para cada mensaje que envía el remitente supervisado que pasa a través del servicio de transporte especificado. Cada carpeta lleva el nombre de un GUID asignado al mensaje. Si habilita el seguimiento de canalización para el servicio de transporte y el servicio de transporte de buzones de correo del mismo servidor de buzones de correo, cada servicio de transporte asigna otro GUID al mismo mensaje, de manera que el nombre de la carpeta del mensaje en la carpeta `MessageSnapshots` del servicio de transporte es diferente al nombre de la carpeta del mismo mensaje en la carpeta `MessageSnapshots` del servicio de transporte de buzones de correo. Si habilita el seguimiento de canalización en más de un servidor de Exchange, se asigna otro GUID al mismo mensaje mientras viaja a través del servicio de transporte especificado en cada servidor de Exchange.

En cada carpeta de mensajes, Exchange crea varios archivos de instantáneas de mensajes con las extensiones de archivo .eml. Estos archivos de instantáneas de mensajes abarcan el contenido del mensaje a medida que encuentra cada evento SMTP y agente de transporte.

Si un agente de transporte se encuentra registrado en un evento SMTP, Exchange crea una instantánea del mensaje antes de que el mensaje encuentre cualquier agente de transporte. Esto le ofrece una copia del mensaje antes de que el mensaje encuentre agentes de transporte que estén registrados en ese evento. A continuación, se crea una nueva instantánea de mensaje para cada agente de transporte que encuentre el mensaje, sin tener en cuanta si un agente de transporte modifica los contenidos del mensaje. No obstante, si no hay agentes registrados en un evento, Exchange no crea ninguna instantánea de mensaje para este evento.

Por ejemplo, si hay tres agentes registrados en el evento **OnEndofData** pero sólo dos de los agentes de transporte modifican un mensaje, se crean cuatro instantáneas de mensajes. La primera instantánea de mensajes captura el mensaje a medida que encuentra el evento **OnEndofData** antes de que las modificaciones realizadas por los agentes de transporte se registren en ese evento. A continuación, se crea una instantánea de mensaje para cada agente de transporte sin tener en cuenta si un agente de transporte modifica el mensaje.

Los archivos de instantáneas de mensajes que se crean se describen en la siguiente lista:

  - **Original.eml**   Este archivo incluye el contenido original no modificado del mensaje de correo electrónico antes de que encuentre cualquier evento SMTP o agente de transporte.

  - **Routingnnnn.eml**   Estos archivos incluyen el contenido del mensaje de correo electrónico cuando se encuentra con el transporte de los eventos SMTP y los agentes de transporte registrados en dichos eventos en la parte de categorización del servicio de transporte. El marcador de posición *nnnn* representa un valor entero que empieza por `0001`. El valor se incrementa para cada evento SMTP y agente de transporte registrado en dichos eventos en el orden en el que los eventos y los agentes actúan en el mensaje. El servicio de entrega de transporte de buzones de correo no genera estos archivos de instantáneas **Routing**.

  - **SmtpReceivennnn.eml**   Estos archivos incluyen el contenido de los mensajes de correo electrónico cuando se encuentran con los eventos SMTP **OnEndofData** y **OnEndOfHeaders** y los agentes de transporte registrados en dichos eventos durante la parte de recepción de SMTP del servicio de transporte o del servicio de entrega de transporte de buzones de correo. El marcador de posición *nnnn* representa un valor entero que empieza por `0001`. El valor se incrementa para cada evento SMTP y agente de transporte registrado en dichos eventos en el orden en el que los eventos y los agentes actúan en el mensaje.

Puede abrir los archivos de archivos de instantáneas de mensajes mediante el Bloc de notas o un editor de textos.

Cada archivo de instantánea de mensaje se inicia con encabezados que se añaden al contenido de los mensajes e indican el evento SMTP y el agente de transporte a los que se asocia el archivo de instantánea del mensaje. Estos encabezados empiezan con `X-CreatedBy: MessageSnapshot-Begin injected headers` y terminan con `X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers`, Estos encabezados se reemplazan en cada archivo de instantánea de mensaje por cada agente de transporte y evento SMTP subsiguiente. Aquí le mostramos un ejemplo de los encabezados que se agregan a un archivo de mensaje de correo electrónico:

    X-CreatedBy: MessageSnapshot-Begin injected headers
    X-MessageSnapshot-UTC-Time: 2013-01-23T23:20:18.138Z
    X-MessageSnapshot-Record-Id: 21474836486
    X-MessageSnapshot-Source: OnSubmittedMessageX-Sender: michelle@nwtraders.com
    X-Receiver: chris@contoso.com
    X-EndOfInjectedXHeaders: MessageSnapshot-End injected headers

Después de los encabezados de la instantánea del mensaje, el archivo incluye el contenido del mensaje, incluso todos los encabezados originales del mensaje. Si un agente de transporte modifica los contenidos del mensaje, los cambios aparecen integrados en el mensaje. A medida que se procesa el mensaje por cada agente de transporte, los cambios realizados por cada uno de ellos se aplican a los contenidos del mensaje. Si un agente de transporte no realiza cambios al contenido de un mensaje, la instantánea del mensaje creada por el agente será idéntica a la instantánea del mensaje creada por el agente de transporte anterior.

