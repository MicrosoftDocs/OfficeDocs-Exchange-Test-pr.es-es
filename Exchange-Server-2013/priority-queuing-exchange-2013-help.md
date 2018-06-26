---
title: 'Prioridad en las colas: Exchange 2013 Help'
TOCTitle: Prioridad en las colas
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 51406525
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Prioridad en las colas

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

La *cola de prioridad* es una característica de Microsoft Exchange Server 2013 que permite que la prioridad definida por el remitente de un mensaje afecte al procesamiento del mensaje por parte del servicio de transporte en el servidor de buzones.

El remitente asigna la prioridad del mensaje en Microsoft Outlook cuando crea y envía el mensaje. El remitente puede establecer cualquiera de los siguientes valores para la prioridad del mensaje en Outlook:

  - Importancia baja

  - Importancia normal

  - Importancia alta

La prioridad predeterminada para un mensaje creado en Outlook o Outlook Web App es la prioridad normal. La prioridad del mensaje se almacena en el campo de encabezado de `X-Priority` en el encabezado del mensaje.

Cada mensaje que se envía o recibe en una organización de Exchange 2013 debe categorizarse por el servicio de transporte en un servidor de buzones de correo antes de que se enrute y se entregue. El categorizador del servicio de transporte en un servidor de buzones selecciona un mensaje por vez de una cola de envío y realiza la resolución del destinatario, la resolución del enrutamiento y la conversión del contenido en el mensaje antes de colocarlo en la cola de entrega. Para obtener más información, consulte [Flujo de correo](mail-flow-exchange-2013-help.md).

Las colas de entrega se crean dinámicamente según el destino del mensaje. Para obtener más información, consulte [Colas](queues-exchange-2013-help.md).

Todos los mensajes que tienen el mismo destino se colocan en la misma cola de entrega. La cola de prioridad afecta a la transmisión de los mensajes de una cola de entrega al servidor de mensajería de destino. Cuando la cola de prioridad está habilitada, los mensajes de prioridad alta se transmiten a los destinos antes que los mensajes de prioridad normal y éstos, a su vez, se transmiten a sus destinos antes que los de prioridad baja. La entrega con prioridad de los mensajes según la prioridad de éstos puede ayudar a definir los requisitos del contrato de nivel de servicio (SLA) específico para las horas de entrega de los mensajes.

## Opciones para configurar la cola de prioridad

La compatibilidad para las colas de prioridad se controla mediante claves en el archivo de configuración de la aplicación XML `%ExchangeInstallPath%bin\EdgeTransport.exe.config`. Para obtener instrucciones sobre cómo configurar las colas de prioridad, consulte [Habilitar y configurar colas de prioridad](enable-and-configure-priority-queuing-exchange-2013-help.md).

La tabla siguiente explica todas las claves con mayor detalle.

### Claves de colas de prioridad en el archivo EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>PriorityQueuingEnabled</em></p></td>
<td><p><code>false</code></p></td>
<td><p>Esta clave habilita o deshabilita colas de prioridad en el servicio de transporte del servidor de buzones. La entrada válida para esta clave es <code>true</code> o <code>false</code>.</p>
<p>Cuando la clave es <code>false</code>, la cola de prioridad está deshabilitada y se omiten todos los límites de mensaje de la cola de prioridad que existen en el archivo EdgeTransport.exe.config.</p></td>
</tr>
<tr class="even">
<td><p><em>MaxHighPriorityMessageSize</em></p></td>
<td><p><code>250KB</code></p></td>
<td><p>Esta clave especifica el tamaño máximo permitido de un mensaje de prioridad alta. Si un mensaje de prioridad alta es mayor que el valor especificado por esta clave, el mensaje baja automáticamente de prioridad alta a normal.</p>
<p>El valor de esta clave debe ser bastante menor que el valor del parámetro <em>MaxSendMessageSize</em> en el cmdlet <strong>Set-TransportConfig</strong>. El valor predeterminado de este parámetro es <code>10 MB</code>. La diferencia en estos dos valores ayuda a garantizar tiempos de entrega coherentes y predecibles para los mensajes de prioridad alta.</p>
<p>Cuando especifique un valor, califíquelo con una de las siguientes unidades:</p>
<ul>
<li><p>KB (kilobytes)</p></li>
<li><p>MB (megabytes)</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><em>LowPriorityDelayNotificationTimeout</em></p>
<p><em>NormalPriorityDelayNotificationTimeout</em></p>
<p><em>HighPriorityDelayNotificationTimeout</em></p></td>
<td><p><strong>Baja</strong> <code>8:00:00</code> (8 horas)</p>
<p><strong>Normal</strong> <code>4:00:00</code> (4 horas)</p>
<p><strong>Alta</strong> <code>00:30:00</code> (30 minutos)</p></td>
<td><p>Estas claves especifican el intervalo de tiempo de espera para los mensajes de notificación de estado de entrega (DSN) de retraso en función de la prioridad del mensaje.</p>
<p>Después de cada error de entrega de mensaje, el servidor de transporte de genera un mensaje de DSN de retraso y lo pone en cola para entregarlo al remitente del mensaje no entregado. Este mensaje DNS de retraso solo se envía después de un intervalo de espera de notificación de retraso especificado y solo en caso de que el mensaje erróneo no se hubiera entregado durante este período. Este retraso evita enviar mensajes DSN de retraso innecesarios que podrían estar provocados por errores de transmisión de mensajes temporales.</p>
<p>Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>LowPriorityMessageExpirationTimeout</em></p>
<p><em>NormalPriorityMessageExpirationTimeout</em></p>
<p><em>HighPriorityMessageExpirationTimeout</em></p></td>
<td><p><strong>Baja</strong> <code>2.00:00:00</code> (2 días)</p>
<p><strong>Normal</strong> <code>2.00:00:00</code> (2 días)</p>
<p><strong>Alta</strong> <code>8:00:00</code> (8 horas)</p></td>
<td><p>Estas claves especifican la duración máxima de tiempo durante el cual el servicio de transporte intenta entregar un mensaje erróneo. Si no es posible entregar el mensaje antes del intervalo de tiempo de espera de expiración, se entrega al remitente un informe de no entrega (NDR) con el mensaje original o los encabezados del mensaje.</p>
<p>Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.</p></td>
</tr>
<tr class="odd">
<td><p><em>MaxPerDomainLowPriorityConnections</em></p>
<p><em>MaxPerDomainNormalPriorityConnections</em></p>
<p><em>MaxPerDomainHighPriorityConnections</em></p></td>
<td><p><strong>Baja</strong>   2</p>
<p><strong>Normal</strong>   15</p>
<p><strong>Alta</strong>   3</p></td>
<td><p>Estas claves especifican el número máximo de conexiones que el servicio de transporte puede tener abiertas a cualquier dominio remoto único. Las conexiones de salida a dominios remotos ocurren al usar las colas de entrega y los conectores de envío que existen en el servidor de buzones.</p>
<p>La suma de estas tres claves debería ser menor o igual al valor del parámetro <em>MaxPerDomainOutboundConnections</em> en el cmdlet <strong>Set-TransportService</strong>. El valor predeterminado de este parámetro es <code>20</code>.</p></td>
</tr>
</tbody>
</table>


## Cómo afectan las colas de prioridad a otros límites de mensaje en servidores de buzones

Todos los mensajes que pasan por un servidor de transporte están sujetos a una variedad de reintentos, reenvíos y límites de expiración de mensaje. Para obtener más información, consulte [Límites de tamaño de mensaje](message-size-limits-exchange-2013-help.md).

Algunos límites de mensaje disponibles en el cmdlet **Set-TransportService** tienen sus correspondientes límites de mensaje de cola de prioridad, que están disponibles en el archivo de configuración EdgeTransport.exe.config. En la tabla siguiente se describen los límites de mensaje correspondientes.

### Límites de mensaje en el cmdlet Set-TransportService que corresponden a los límites de mensaje de la cola de prioridad en el archivo EdgeTransport.exe.config

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Origen</th>
<th>Parámetro o clave</th>
<th>Valor predeterminado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code> (4 horas)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityDelayNotificationTimeout</em></p></td>
<td><p><code>4:00:00</code> (4 horas)</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MessageExpirationTimeOut</em></p></td>
<td><p><code>2.00:00:00</code> (2 días)</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe.config</p></td>
<td><p><em>NormalPriorityMessageExpirationTimeout</em></p></td>
<td><p><code>2.00:00:00</code> (2 días)</p></td>
</tr>
</tbody>
</table>


Cuando la cola de prioridad está deshabilitada, se omiten todos los límites de mensaje de la cola de prioridad que existen en el archivo de configuración EdgeTransport.exe.config. Todos los límites de mensaje del cmdlet **Set-TransportService** se aplican a todos los mensajes que viajan por el servicio de transporte en el servidor de buzones.

Cuando la cola de prioridad está habilitada, los límites de mensaje de la cola de prioridad en el archivo de configuración EdgeTransport.exe.config invalidan los límites de mensaje correspondientes en el cmdlet **Set-TransportService**. Los otros límites de mensaje del cmdlet **Set-TransportService** se aplican a los mensajes de prioridades baja, normal y alta que viajan por el servidor de transporte en el servidor de buzones.

## Configuración de usuario para la cola de prioridad

El cmdlet **Set-Mailbox** tiene el parámetro *DowngradeHighPriorityMessagesEnabled*. El valor predeterminado es `$false`. Cuando este parámetro está establecido en `$true`, cualquier mensaje de prioridad alta que se envíe desde el buzón de correo bajará automáticamente a prioridad normal.

