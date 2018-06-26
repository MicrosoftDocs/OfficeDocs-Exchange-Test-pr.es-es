---
title: 'Agentes de transporte: Exchange 2013 Help'
TOCTitle: Agentes de transporte
ms:assetid: e7389d63-3172-40d5-bf53-0d7cd7e78340
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125012(v=EXCHG.150)
ms:contentKeyID: 48268814
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agentes de transporte

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Los agentes de transporte permiten instalar software personalizado creado por Microsoft, por otros proveedores o por una organización en un servidor Exchange. A continuación, el software procesa los mensajes de correo electrónico que pasan por la canalización de transporte. En Microsoft Exchange Server 2013, la canalización de transporte consta de los siguientes procesos:

  - Servicio de transporte front-end en servidores de acceso de cliente

  - Servicio de transporte en servidores de buzones de correo

  - Servicio de transporte de buzones en servidores de buzones de correo

  - Servicio de transporte en servidores de transporte perimetral

Para obtener más información sobre la canalización de transporte, vea [Flujo de correo](mail-flow-exchange-2013-help.md).

Al igual que en la versión anterior de Exchange, el transporte de Exchange 2013 proporciona extensibilidad mediante el SDK de agentes de transporte de Microsoft Exchange Server 2013. La versión de Exchange 2013 del SDK se basa en la versión 4.0 de Microsoft.NET Framework y les permite a terceros implementar las siguientes clases predefinidas:

  - **SmtpReceiveAgent**

  - **RoutingAgent**

  - **DeliveryAgent**

Cuando se comprueba la compatibilidad con las bibliotecas del SDK, los ensamblados resultantes se registran en Exchange 2013, que carga los agentes e invoca a sus controladores de eventos durante etapas específicas del procesamiento de mensajes o sesiones SMTP. Estas etapas o eventos forman parte de las definiciones de agentes. La información del registro de agentes se almacena en un archivo de configuración XML.

La siguiente lista explica los requisitos para usar agentes de transporte en Exchange 2013.

  - El servicio de transporte en servidores de buzones de correo y servidores de transporte perimetral admite por completo todas las clases predefinidas en el SDK y, por lo tanto, todos los agentes de transporte de terceros escritos para los roles de servidor de transporte perimetral y transporte de concentradores en Microsoft Exchange Server 2010 deben funcionar con el servicio de transporte de Exchange 2013.

  - El servicio de transporte front-end solo admite la clase **SmtpReceiveAgent** en el SDK y los agentes de terceros no pueden operar con el evento SMTP **OnEndOfData**.

  - El servicio de transporte de buzones no admite el SDK en ningún caso, por lo que puede usar cualquier agente de terceros en este servicio.

La compatibilidad con agentes de transporte anteriores basados en versiones de .NET Framework previas a la versión 4.0 no está habilitada de manera predeterminada, pero se puede habilitar. Para obtener instrucciones, vea [Habilitar la compatibilidad para agentes de transporte heredados](enable-support-for-legacy-transport-agents-exchange-2013-help.md).

**Contenido**

Actualizaciones para la administración de agentes de transporte

Agentes de transporte y eventos SMTP

Prioridad de los agentes de transporte

Agentes de transporte integrados

Solución de problemas de los agentes de transporte

## Actualizaciones para la administración de agentes de transporte

Debido a las actualizaciones realizadas en la canalización de transporte de Exchange 2013, los cmdlets de los agentes de transporte deben distinguir entre el servicio de transporte y el servicio de transporte front-end, especialmente si los servidores de acceso de cliente y de buzones de correo están instalados en el mismo equipo. Para obtener más información, vea [Administrar agentes de transporte](manage-transport-agents-exchange-2013-help.md).

Los cmdlets de administración del agente de transporte manipulan un archivo de configuración ubicado en `%ExchangeInstallPath%TransportRoles\Shared`. Para el servicio de transporte en servidores de buzones de correo y servidores de transporte perimetral, el archivo es `agents.config`. Para el servicio de transporte front-end en servidores de acceso de cliente, el archivo es `fetagents.config`. Ambos archivos utilizan el mismo formato que en Exchange 2010. Para obtener más información sobre la administración de los agentes de transporte, vea [Administrar agentes de transporte](manage-transport-agents-exchange-2013-help.md).

Volver al principio

## Agentes de transporte y eventos SMTP

Los agentes de transporte utilizan eventos SMTP. Estos eventos se desencadenan a medida que los mensajes se desplazan por el canal de transporte. Los eventos SMTP dan a los agentes de transporte acceso a los mensajes en puntos específicos durante la conversación SMTP y durante el enrutamiento de los mensajes por la organización.

Observe que hay eventos de recepción SMTP nuevos en Exchange 2013. La recepción de SMTP existe en el servicio de transporte perimetral en los servidores de acceso de cliente, el servicio de transporte en servidores de buzones de correo y servidores de transporte perimetral y el servicio de entrega de transporte de buzones en los servidores de buzones de correo. El categorizador existe solo en el servicio de transporte en servidores de buzones de correo y servidores de transporte perimetral. Para más información sobre los servicios de transporte y el categorizador, vea [Enrutamiento de correo](mail-routing-exchange-2013-help.md).

La tabla siguiente incluye los eventos SMTP que proporcionan acceso a los mensajes en la canalización de transporte.

### Eventos de recepción SMTP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Secuencia</th>
<th>Evento SMTP</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong></p></td>
<td><p>La conexión inicial desencadena este evento desde un host SMTP remoto.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnHeloCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>HELO</code>.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnEhloCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>EHLO</code>.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnStartTlsCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>STARTTLS</code>.</p></td>
</tr>
<tr class="odd">
<td><p>5</p></td>
<td><p><strong>OnAuthCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>AUTH</code>.</p></td>
</tr>
<tr class="even">
<td><p>6</p></td>
<td><p><strong>OnProcessAuthentication</strong></p></td>
<td><p>Este evento se desencadena cuando se procesa la autenticación con el host SMTP remoto.</p></td>
</tr>
<tr class="odd">
<td><p>7</p></td>
<td><p><strong>OnEndOfAuthentication</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto ha completado la autenticación.</p></td>
</tr>
<tr class="even">
<td><p>8</p></td>
<td><p><strong>OnXSessionParamsCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>XSESSIONPARAMS</code>.</p></td>
</tr>
<tr class="odd">
<td><p>9</p></td>
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>MAIL FROM</code>.</p></td>
</tr>
<tr class="even">
<td><p>10</p></td>
<td><p><strong>OnRcptToCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>RCPT TO</code>.</p></td>
</tr>
<tr class="odd">
<td><p>11</p></td>
<td><p><strong>OnDataCommand</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite el comando <code>DATA</code> (texto) o <code>BDAT</code> (datos binarios).</p></td>
</tr>
<tr class="even">
<td><p>12</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto ha completado el envío de encabezados de mensajes de correo electrónico. Esto se indica con una línea en blanco (<code>&lt;CRLF&gt;</code>) que separa los encabezados de mensajes y los cuerpos de mensajes.</p></td>
</tr>
<tr class="odd">
<td><p>13</p></td>
<td><p><strong>OnProxyInboundMessage</strong></p></td>
<td><p>Este evento se desencadena cuando el servicio de transporte front-end retransmite o envía por <em>proxy</em> una sesión SMTP entrante en un servidor de acceso de cliente al servicio de transporte de un servidor de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p>14</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP remoto emite un comando de fin de datos. En el caso de las sesiones de texto que inicia el comando <code>DATA</code>, el indicador de fin de datos es <code>&lt;CRLF&gt;.&lt;CRLF&gt;</code>. En el caso de las sesiones binarias que inicia el comando <code>BDAT</code>, el indicador de fin de datos es <code>BDAT LAST</code>.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnHelpCommand</strong></p></td>
<td><p>Este evento se desencadena si el host SMTP remoto emite el comando <code>HELP</code>.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnNoopCommand</strong></p></td>
<td><p>Este evento se desencadena si el host SMTP remoto emite el comando <code>NOOP</code>.</p></td>
</tr>
<tr class="odd">
<td><p>**</p></td>
<td><p><strong>OnReject</strong></p></td>
<td><p>Este evento se desencadena si el host SMTP de recepción emite un código de notificación de estado de entrega (DSN) temporal o permanente al host SMTP emisor.</p></td>
</tr>
<tr class="even">
<td><p>**</p></td>
<td><p><strong>OnRsetCommand</strong></p></td>
<td><p>Este evento se desencadena si el host SMTP de envío emite el comando <code>RSET</code>.</p></td>
</tr>
<tr class="odd">
<td><p>15</p></td>
<td><p><strong>OnDisconnectEvent</strong></p></td>
<td><p>Este evento se desencadena cuando el host SMTP de envío o de recepción se desconecta de la conversación SMTP. Por lo general, esto sucede cuando el host SMTP remoto emite el comando <code>QUIT</code>.</p></td>
</tr>
</tbody>
</table>


\*\* Estos eventos pueden producirse en cualquier momento después de **OnConnectEvent** pero antes de **OnDisconnectEvent**.

### Eventos de categorizador

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Secuencia</th>
<th>Evento de categorizador</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>1</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
<td><p>Este evento se desencadena cuando un mensaje llega en la cola de envío en el servicio de transporte en el servidor de buzones de correo de recepción o el servidor de transporte perimetral.</p></td>
</tr>
<tr class="even">
<td><p>2</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
<td><p>Este evento se desencadena una vez que se han resuelto todos los destinatarios pero antes de que se determine el siguiente salto para cada uno de ellos. El evento de enrutamiento <strong>OnResolvedMessage</strong> permite que los eventos de enrutamiento posteriores invaliden el comportamiento de enrutamiento predeterminado mediante la utilización del método por destinatario <strong>SetRoutingOverride</strong>.</p></td>
</tr>
<tr class="odd">
<td><p>3</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
<td><p>Este evento se desencadena una vez que los mensajes se han categorizado, las listas de distribución se han expandido y se han resuelto los destinatarios.</p></td>
</tr>
<tr class="even">
<td><p>4</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
<td><p>Este evento se desencadena cuando el categorizador finaliza el procesamiento del mensaje.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Prioridad de los agentes de transporte

Hay dos factores que determinan el orden en el que actúan los agentes de transporte en los mensajes en la canalización de transporte:

1.  El evento SMTP en el que se registra el agente de transporte y cuando el evento SMTP encuentra mensajes.

2.  El valor de prioridad que se asigna al agente de transporte si hay varios agentes registrados en el mismo evento SMTP. La prioridad más alta es 1. Un valor entero más alto indica una prioridad de agente más baja.

Por ejemplo, supongamos que configuró los siguientes agentes de transporte:

  - El agente de transporte A con una prioridad de 1 y el agente de transporte C con una prioridad de 2 están registrados en el evento SMTP **OnEndOfHeaders**.

  - El agente de transporte B con una prioridad de 4 está registrado en el evento SMTP **OnMailCommand**.

El agente de transporte B se aplica primero a los mensajes porque el evento **OnMailCommand** encuentra mensajes antes del evento **OnEndOfHeaders**. Cuando los mensajes alcanzan el evento **OnEndOfHeaders**, el agente de transporte A se aplica antes del agente de transporte C porque el agente de transporte A tiene mayor prioridad (valor entero más bajo) que el agente de transporte C.

## Agentes de transporte integrados

Exchange 2013 incluye muchos agentes de transporte integrados que proporcionan características como la función contra correo no deseado, reglas de transporte y registro en diario. La mayoría de los agentes de transporte integrados en los servidores de buzones de correo y los servidores de acceso de cliente de Exchange 2013 son invisibles y los cmdlets de administración de agentes de transporte no pueden administrarlos. Prácticamente todos los agentes de transporte integrados que son visibles y se pueden administrar están en el servicio de transporte en los servidores de buzones de correo y en los servidores de transporte perimetral.

Los agentes de transporte integrados más interesantes de los servidores de buzones de correo se describen en la tabla siguiente. Tenga en cuenta que esta tabla no incluye muchos de los agentes de transporte invisibles que no se pueden administrar.

### Agentes de transporte integrados interesantes en servidores de buzones de correo

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del agente</th>
<th>¿Fácil de administrar?</th>
<th>Priority</th>
<th>Eventos del categorizador o SMTP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente de regla de transporte</p></td>
<td><p>Sí</p></td>
<td><p>1</p></td>
<td><p><strong>OnResolvedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de malware</p></td>
<td><p>Sí</p></td>
<td><p>2</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de enrutamiento de mensajes de texto</p></td>
<td><p>Sí</p></td>
<td><p>3</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de entrega de mensajes de texto</p></td>
<td><p>Sí</p></td>
<td><p>4</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p>Agente de registro en diario</p></td>
<td><p>No</p></td>
<td><p>No configurable</p></td>
<td><p><strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de descifrado de informes de diario</p></td>
<td><p>No</p></td>
<td><p>No configurable</p></td>
<td><p><strong>OnCategorizedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de descifrado de RMS</p></td>
<td><p>No</p></td>
<td><p>No configurable</p></td>
<td><p><strong>OnSubmittedMessage</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de cifrado de RMS</p></td>
<td><p>No</p></td>
<td><p>No configurable</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de descifrado de protocolo RMS</p></td>
<td><p>No</p></td>
<td><p>No configurable</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
</tbody>
</table>


En los servidores de transporte perimetral, la mayoría de los agentes de transporte integrados son visibles y se pueden administrar mediante cmdlets de administración de agentes de transporte u otros cmdlets específicos para las funciones.

Los agentes de transporte integrados más interesantes de los servidores de transporte perimetral se describen en la tabla siguiente. Tenga en cuenta que esta tabla no incluye los agentes de transporte invisibles ni los que no se pueden administrar.

### Agentes de transporte integrados interesantes en servidores de transporte perimetral

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del agente</th>
<th>¿Fácil de administrar?</th>
<th>Priority</th>
<th>Eventos del categorizador o SMTP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Agente de filtro de conexión</p></td>
<td><p>Sí</p></td>
<td><p>1</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnMailCommand</strong>, <strong>OnRcptComand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de reescritura de direcciones entrantes</p></td>
<td><p>Sí</p></td>
<td><p>2</p></td>
<td><p><strong>OnRcptCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de regla perimetral</p></td>
<td><p>Sí</p></td>
<td><p>3</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de filtro de contenido*</p></td>
<td><p>Sí</p></td>
<td><p>4</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de identificador de remitente*</p></td>
<td><p>Sí</p></td>
<td><p>5</p></td>
<td><p><strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de filtro de remitentes*</p></td>
<td><p>Sí</p></td>
<td><p>6</p></td>
<td><p><strong>OnMailCommand</strong>, <strong>OnEndOfHeaders</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de filtro de destinatarios</p></td>
<td><p>Sí</p></td>
<td><p>7</p></td>
<td><p><strong>OnRcptCommand</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de análisis de protocolo*</p></td>
<td><p>Sí</p></td>
<td><p>8</p></td>
<td><p><strong>OnConnectEvent</strong>, <strong>OnEndOfHeaders</strong>, <strong>OnEndOfData</strong>, <strong>OnReject</strong>, <strong>OnRsetCommand</strong>, <strong>OnDisconnectEvent</strong></p></td>
</tr>
<tr class="odd">
<td><p>Agente de filtro de datos adjuntos</p></td>
<td><p>Sí</p></td>
<td><p>9</p></td>
<td><p><strong>OnEndOfData</strong></p></td>
</tr>
<tr class="even">
<td><p>Agente de reescritura de direcciones salientes</p></td>
<td><p>Sí</p></td>
<td><p>10</p></td>
<td><p><strong>OnSubmittedMessage</strong>, <strong>OnRoutedMessage</strong></p></td>
</tr>
</tbody>
</table>


\* También puede instalar y configurar estos agentes contra correo no deseado en los servidores de buzones de correo. Para más información, vea [Habilitar la funcionalidad contra correo electrónico no deseado en un servidor Buzón de correo](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).

Volver al principio

## Solución de problemas de los agentes de transporte

Como ayuda para solucionar problemas con los agentes de transporte, puede usar las siguientes funciones:

  - **Get-TransportPipeline**   Este cmdlet muestra los eventos SMTP y los agentes de transporte correspondientes que encuentran mensajes en el servidor Exchange. Para más información, vea [Ver agentes de transporte en la canalización de transporte](view-transport-agents-in-the-transport-pipeline-exchange-2013-help.md).

  - **Seguimiento de canalización**   El seguimiento de canalización permite crear una instantánea exacta de un mensaje antes y después de que encuentre los agentes de transporte. Esto le permite encontrar un agente de transporte que está provocando resultados inesperados. Para más información, vea [Seguimiento del canal](pipeline-tracing-exchange-2013-help.md).

Volver al principio

