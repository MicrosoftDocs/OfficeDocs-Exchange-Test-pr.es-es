---
title: 'Filtros de mensajes: Exchange 2013 Help'
TOCTitle: Filtros de mensajes
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 49895767
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtros de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

El filtrado genera diferentes vistas de los mensajes en las colas. Mediante la especificación de criterios de filtro, es posible buscar los mensajes y realizar acciones en ellos. Cuando se envía un mensaje de correo electrónico a varios destinatarios, éste se puede ubicar en varias colas. Si filtra por las propiedades del mensaje, puede encontrar mensajes en todas las colas. Las siguientes situaciones son ejemplos de cómo podría utilizar el filtrado de mensajes para administrar el flujo de correo:

  - La cola de envío en un servidor de buzones de correo o un servidor de transporte perimetral que recibe correo de Internet tiene un alto volumen de mensajes que esperan en cola para entregarse. Muchos de los mensajes tienen el mismo asunto. Por tanto, existe la sospecha de que se está enviando correo no deseado a la organización. Para solucionar este problema, puede crear un filtro y ver todos los mensajes que cumplen los criterios del asunto y, si determina que los mensajes son correo no deseado, puede seleccionarlos y eliminarlos de la cola de entrega sin enviar un informe de no entrega (NDR).

  - Un usuario informa de que el flujo de correo es lento. Examina las colas y comprueba que muchos mensajes que tienen asuntos aleatorios parecen provenir de un solo dominio. Puede crear un filtro para ver todos los mensajes en cola de ese dominio y, si determina que los mensajes son correo no deseado, puede seleccionarlos y eliminarlos de las colas sin enviar un informe de no entrega (NDR).

## Propiedades de mensajes como filtros

Puede utilizar las propiedades de los mensajes para crear un filtro y encontrar los mensajes que cumplen los criterios especificados. Puede crear filtros en el Visor de cola o bien usando el parámetro *Filter* en los cmdlets de administración de mensajes. Observe que los cmdlets de administración de mensajes admiten más propiedades filtrables que el Visor de cola. En la tabla siguiente se muestran las propiedades de mensaje en las que puede basar el filtro y los valores asociados a ellas.

### Propiedades de mensaje que se deben utilizar al filtrar mensajes

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propiedad de mensaje de Visor de cola</th>
<th>Propiedad de mensaje del Shell</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Fecha de recepción</strong></p></td>
<td><p><code>DateReceived</code></p></td>
<td><p>La fecha/hora del momento en que se colocó el mensaje en la cola.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>DeferReason</code></p></td>
<td><p>Esta propiedad identifica la razón por la cual el mensaje se ha aplazado. Si el mensaje no se ha aplazado, esta propiedad tiene el valor <code>None</code>. Un mensaje aplazado se devuelve a la cola de envíos debido a los errores temporales encontrados durante la resolución del destinatario. Para obtener más información acerca de los mensajes aplazados, consulte <a href="recipient-resolution-exchange-2013-help.md">Resolución de destinatarios</a>. Los valores posibles son:</p>
<p><code>AD Transient Failure During Content Conversion</code></p>
<p><code>AD Transient Failure During Resolve</code></p>
<p><code>Agent</code></p>
<p><code>Ambiguous Recipient</code></p>
<p><code>Loop Detected</code></p>
<p><code>Marked As Retry Delivery If Rejected</code></p>
<p><code>Rerouted By Store Driver</code></p>
<p><code>Storage Transient Failure During Content Conversion</code></p>
<p><code>Transient Failure</code></p>
<p><code>Target Site Inbound Mail Disabled</code></p>
<p><code>Recipient Thread Limit Exceeded</code></p>
<p><code>Transient Attribution Failure</code></p>
<p><code>Transient Accepted Domains Load Failure</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Fecha de expiración</strong></p></td>
<td><p><code>ExpirationTime</code></p></td>
<td><p>Esta propiedad contiene la fecha/hora del momento en que el mensaje expirará y se eliminará de la cola, en el caso de no poder entregarse.</p></td>
</tr>
<tr class="even">
<td><p><strong>Dirección de origen</strong></p></td>
<td><p><code>FromAddress</code></p></td>
<td><p>Esta propiedad contiene la dirección SMTP del remitente.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Esta propiedad es la identidad del mensaje en forma de <em>&lt;Servidor&gt;\&lt;Cola&gt;\&lt;MessageInteger&gt;</em>. Para obtener más información, consulte la sección &quot;Identidad de mensaje&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Id. de mensaje de Internet</strong></p></td>
<td><p><code>InternetMessageId</code></p></td>
<td><p>Esta propiedad contiene el valor del campo del encabezado <code>Message-ID:</code> que está situado en el encabezado del mensaje. El valor se expresa como una dirección de correo electrónico que contiene un GUID y el FQDN del servidor de envío SMTP. Por ejemplo:</p>
<p><code>&lt;67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p><strong>Último error</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Esta propiedad contiene el texto del último error registrado para un mensaje. Por ejemplo, <code>A matching connector cannot be found to route the external recipient</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>MessageLatency</code></p></td>
<td><p>Esta propiedad contiene la cantidad de tiempo transcurrida entre el momento en que el mensaje entró por primer vez en la cola de envíos y el momento en que el mensaje se colocó en cola. El valor usa la sintaxis <em>hh:mm:ss.ff</em>, donde <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo, y <em>ff</em> = fracciones de segundo.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Nombre de origen del mensaje</strong></p></td>
<td><p><code>MessageSourceName</code></p></td>
<td><p>Esta propiedad contiene una cadena de texto que indica el nombre del componente de transporte que envió el mensaje a la cola. Por ejemplo, si el mensaje procedió de un conector de recepción, el valor sería: <code>SMTP:</code><em>&lt;ConnectorName&gt;</em>. Si el mensaje es una notificación de estado de entrega (DSN), el valor es <code>DSN</code>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>Priority</code></p></td>
<td><p>Esta propiedad contiene la prioridad del mensaje que el usuario asignó en Outlook o Outlook Web App. Los valores posibles son <code>Low</code>, <code>Normal</code> y <code>High</code>. Para obtener más información, consulte <a href="priority-queuing-exchange-2013-help.md">Prioridad en las colas</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Id. de cola</strong></p></td>
<td><p><code>Queue</code></p></td>
<td><p>Esta propiedad es la identidad de la cola que almacena el mensaje. La identidad de la cola usa la sintaxis <em>&lt;Servidor&gt;\&lt;Cola&gt;</em>. Para obtener más información, consulte la sección &quot;Identidad de cola&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>RetryCount</code></p></td>
<td><p>Esta propiedad identifica el número de veces que se ha intentado realizar la entrega del mensaje a su destino, ya sea automática o manualmente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SCL</strong></p></td>
<td><p><code>SCL</code></p></td>
<td><p>El valor de la propiedad del nivel de confianza de correo no deseado (SCL) especifica el SCL del mensaje. Las entradas SCL válidas son números enteros del 0 al 9. Un valor de propiedad SCL vacío indica que el agente de filtrado de contenido no ha procesado el mensaje.</p>
<p>Esta propiedad contiene el valor de nivel de confianza de correo electrónico no deseado (SCL) del mensaje. Las entradas válidas de SCL son números enteros del 0 al 9 y -1. Para obtener más información, consulte <a href="spam-confidence-level-threshold-exchange-2013-help.md">Umbral de nivel de confianza de correo no deseado</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tamaño (KB)</strong></p></td>
<td><p><code>Size</code></p></td>
<td><p>Esta propiedad indica el tamaño del mensaje.</p></td>
</tr>
<tr class="odd">
<td><p><strong>IP de origen</strong></p></td>
<td><p><code>SourceIP</code></p></td>
<td><p>Esta propiedad contiene la dirección IP del servidor que envió el mensaje al servidor Exchange que almacena el mensaje en la cola. La dirección podría ser la dirección IP de un servidor SMTP remoto o la dirección UP de un servidor Exchange local.</p></td>
</tr>
<tr class="even">
<td><p><strong>Estado</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Esta propiedad indica el estado actual del mensaje. Un mensaje puede tener uno de los siguientes estados:</p>
<p><code>Active</code></p>
<p><code>Locked</code></p>
<p><code>None</code></p>
<p><code>Pending Remove</code></p>
<p><code>Pending Suspend</code></p>
<p><code>Ready</code></p>
<p><code>Retry</code></p>
<p><code>Suspended</code></p>
<p>Para obtener más información, consulte la sección &quot;Propiedades de mensaje&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Asunto</strong></p></td>
<td><p><code>Subject</code></p></td>
<td><p>Esta propiedad indica el asunto del mensaje que se encontró en el campo del encabezado <code>Subject:</code> en el encabezado del mensaje.</p></td>
</tr>
</tbody>
</table>

