---
title: 'Filtros de cola: Exchange 2013 Help'
TOCTitle: Filtros de cola
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 49896034
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Filtros de cola

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El filtrado genera distintas vistas de las colas. Las propiedades de las colas se utilizan como opciones de filtro. Mediante la especificación de criterios de filtro, es posible localizar las colas con rapidez y realizar acciones en ellas. Las siguientes situaciones son ejemplos de cómo podría utilizar el filtrado de colas para administrar el flujo de correo:

  - Recibe un mensaje de Microsoft System Center Operations Manager que indica que la longitud de una cola ha superado el umbral establecido. Desea investigar si hay algún problema de flujo de correo en todo el servidor.
    
    Puede crear un filtro para ver todas las colas que tienen un contador de mensajes que supera lo que se considera normal. Si se detecta un problema de flujo de correo, puede seleccionar todas las colas de los resultados del filtro y suspenderlas mientras continúa con la investigación.

  - Suspende varias colas para investigar la causa de los problemas de flujo de correo. Determina que el problema se debió a una mala configuración de un conector y lo soluciona.
    
    Puede crear un filtro para ver todas las colas que tienen el estado Suspended y, seguidamente, seleccionar todas las colas de los resultados del filtro para reanudarlas.

## Propiedades de las colas que se deben utilizar cuando se filtran colas

Las propiedades de las colas se pueden utilizar para crear un filtro y buscar aquellas colas que cumplen criterios especificados. Puede crear filtros en el Visor de cola o usando el parámetro *Filter* en los cmdlets de administración de colas. Tenga en cuenta que los cmdlets de administración de colas son compatibles con más propiedades de filtrado que el Visor de cola. La tabla siguiente muestra las propiedades de las colas por las que se puede establecer el filtro y los valores válidos de dichas propiedades.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Propiedad de cola del Visor de cola</th>
<th>Propiedad de cola del Shell</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>DeferredMessageCount</code></p></td>
<td><p>Esta propiedad identifica el número de mensajes devueltos a la cola de envío debido a los errores transitorios que se encontraron durante la resolución de destinatarios. Para obtener más información acerca de los mensajes aplazados, consulte <a href="recipient-resolution-exchange-2013-help.md">Resolución de destinatarios</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Tipo de entrega</strong></p></td>
<td><p><code>DeliveryType</code></p></td>
<td><p>Los valores válidos de <strong>DeliveryType</strong> se explican en la sección &quot;NextHopSolutionKey&quot; del tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Identity</code></p></td>
<td><p>Esta propiedad es la identidad de la cola con el formato <em>&lt;Servidor&gt;\&lt;Cola&gt;</em>. Para obtener más información consulte la sección &quot;Identidad de colas&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>IncomingRate</code></p></td>
<td><p>Esta propiedad es un número calculado que indica la velocidad de entrada de los mensajes en la cola. Para obtener más información, consulte la sección &quot;IncomingRate, OutgoingRate y velocidad&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Último error</strong></p></td>
<td><p><code>LastError</code></p></td>
<td><p>Esta propiedad indica la cadena de texto del último error que se registró en la cola.</p></td>
</tr>
<tr class="even">
<td><p><strong>Hora del último reintento</strong></p></td>
<td><p><code>LastRetryTime</code></p></td>
<td><p>Esta propiedad indica la fecha y la hora del último intento de conexión de una cola con el estado de <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>LockedMessageCount</code></p></td>
<td><p>Esta propiedad se reserva para el uso interno de Microsoft y no se usa en las organizaciones de Exchange 2013 locales.</p></td>
</tr>
<tr class="even">
<td><p><strong>Número de mensajes</strong></p></td>
<td><p><code>MessageCount</code></p></td>
<td><p>Esta propiedad indica el número de mensajes de la cola.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>NextHopCategory</code></p></td>
<td><p>Esta propiedad designa el siguiente salto de la cola como <code>Internal</code> o <code>External</code> y se basa en el valor de la propiedad <strong>DeliveryType</strong> de la cola. Para obtener más información, consulte la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>NextHopConnector</code></p></td>
<td><p>Esta propiedad es el GUID del siguiente salto y se basa en el valor de la propiedad <strong>DeliveryType</strong> de la cola. Para obtener más información, consulte la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Dominio del salto siguiente</strong></p></td>
<td><p><code>NextHopDomain</code></p></td>
<td><p>Esta propiedad es el nombre del siguiente salto y se basa en el valor de la propiedad <strong>DeliveryType</strong> de la cola. Para obtener más información, consulte la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Hora del siguiente reintento</strong></p></td>
<td><p><code>NextRetryTime</code></p></td>
<td><p>Esta propiedad indica la fecha y la hora del siguiente intento de conexión de una cola con el estado de <code>Retry</code>.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>OutgoingRate</code></p></td>
<td><p>Esta propiedad es un número calculado que indica la velocidad de salida de los mensajes en la cola. Para obtener más información, consulte la sección &quot;IncomingRate, OutgoingRate y velocidad&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>RiskLevel</code></p></td>
<td><p>Esta propiedad se reserva para el uso interno de Microsoft y no se usa en las organizaciones de Exchange 2013 locales.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Estado</strong></p></td>
<td><p><code>Status</code></p></td>
<td><p>Esta propiedad indica el estado actual de la cola. Una cola puede tener uno de los siguientes valores de estado: Activo, Conectando, Ninguno, Suspendido, Preparado o Reintentar. Para obtener más información, consulte la sección &quot;Estado de la cola&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="even">
<td><p>n/d</p></td>
<td><p><code>TlsDomain</code></p></td>
<td><p>Esta propiedad contiene el FQDN del dominio de destino si el destino está configurado para Seguridad de dominio.</p></td>
</tr>
<tr class="odd">
<td><p>n/d</p></td>
<td><p><code>Velocity</code></p></td>
<td><p>Esta propiedad contiene un número calculado que indica la efectividad de la purga de la cola. Para obtener más información, consulte la sección &quot;IncomingRate, OutgoingRate y velocidad&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
</tbody>
</table>

