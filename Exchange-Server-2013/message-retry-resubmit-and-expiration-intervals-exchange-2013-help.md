---
title: 'Intervalos de reintento, reenvío y expiración de mensajes: Exchange 2013 Help'
TOCTitle: Intervalos de reintento, reenvío y expiración de mensajes
ms:assetid: 03020e6f-4c01-4c6e-ae47-fd74d4c4f96a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ891103(v=EXCHG.150)
ms:contentKeyID: 51406469
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Intervalos de reintento, reenvío y expiración de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

En Microsoft Exchange Server 2013, los mensajes que no se puedan entregar correctamente están sujetos a varias fechas límite de reintento, reenvío y expiración en función del origen y el destino del mensaje. *Reintentar* es un nuevo intento de conexión con el destino. *Reenvío* es el acto de devolver los mensajes a la cola de envío para que los vuelva a procesar el categorizador. El mensaje *expira* después de que todos los intentos de entrega hayan sido erróneos durante un período de tiempo especificado. Cuando un mensaje expira, se avisa al remitente del error de entrega. A continuación, se elimina el mensaje de la cola.

En los tres casos (reintento, reenvío y expiración) se puede intervenir manualmente antes de que se apliquen las acciones automáticas a los mensajes.

Para instrucciones sobre cómo configurar estos intervalos, vea [Configurar los intervalos de reintento, reenvío y expiración de mensajes](configure-message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).

## Opciones de configuración para el reintento de mensajes

Cuando un servidor de transporte no puede conectarse al siguiente salto, la cola pasa al estado de reintento. Se sigue intentando conectar hasta que la cola expira o se establece la conexión.

## Opciones de configuración para el reintento automático de mensajes

En la tabla siguiente se describen las opciones de configuración que están disponibles para los intervalos de reintento de mensajes.

### Opciones de configuración que están disponibles para los intervalos de reintento de mensajes

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del parámetro o clave</th>
<th>Valor predeterminado</th>
<th>Dónde configurarlo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueGlitchRetryCount</em></p></td>
<td><p>4</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Esta clave especifica el número de reintentos de conexión que se hacen inmediatamente después de que en el servidor de transporte se observen problemas al conectar con el servidor de destino. Estos problemas de conexión son provocados normalmente por breves interrupciones en la red.</p>
<p>La entrada válida para esta clave es un entero de 0 a 15.</p>
<p>Normalmente no hace falta modificar esta clave a no ser que la red no sea confiable y sigan produciéndose interrupciones accidentales de la conexión.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueGlitchRetryInterval</em></p></td>
<td><p><code>00:01:00</code> o 1 minuto</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Esta clave controla el intervalo de conexión entre cada intento de conexión que especifica la clave <em>QueueGlitchRetryCount</em>.</p>
<p>Normalmente no hace falta modificar este parámetro a no ser que la red no sea confiable y sigan produciéndose interrupciones accidentales de la conexión.</p></td>
</tr>
<tr class="odd">
<td><p><em>TransientFailureRetryCount</em></p></td>
<td><p>6</p></td>
<td><p>Cmdlet <strong>Set-TransportService</strong> o propiedades del servidor del Centro de administración de Exchange (EAC)</p></td>
<td><p>Este parámetro especifica el número de intentos de conexión que se hacen después de que hayan fallado los reintentos de conexión que están controlados por las claves <em>QueueGlitchRetryCount</em> y <em>QueueGlitchRetryInterval</em>. Los problemas de conexión que consumen las claves <em>QueueGlitchRetryCount</em> y <em>QueueGlitchRetryInterval</em> pueden estar provocados por reinicios del servidor o errores de búsquedas de DNS en memoria caché.</p>
<p>El valor válido para este parámetro es un entero del 0 al 15. Si define este parámetro en 0, el siguiente intento de conexión lo controlará el parámetro <em>OutboundConnectionFailureRetryInterval</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>TransientFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Servicio de transporte en los servidores de buzones de correo: <code>00:05:00</code> o 5 minutos</p></li>
<li><p>Servidores de transporte perimetral: <code>00:01:00</code> o 10 minutos</p></li>
</ul></td>
<td><p>Cmdlet <strong>Set-TransportService</strong> o propiedades de servidor en el EAC</p></td>
<td><p>Este parámetro controla el intervalo de conexión entre cada intento de conexión que especifica el parámetro <em>TransientFailureRetryCount</em>.</p>
<p>Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.</p></td>
</tr>
<tr class="odd">
<td><p><em>OutboundConnectionFailureRetryInterval</em></p></td>
<td><ul>
<li><p>Servicio de transporte en los servidores de buzones de correo: <code>00:10:00</code> o 10 minutos</p></li>
<li><p>Servidores de transporte perimetral: <code>00:30:00</code> o 30 minutos</p></li>
</ul></td>
<td><p>Cmdlet <strong>Set-TransportService</strong> o propiedades de servidor en el EAC</p></td>
<td><p>Este parámetro especifica el intervalo de reintento para los intentos de conexión de salida que hayan fallado anteriormente. Los intentos de conexión fallidos anteriores están controlados por los parámetros <em>TransientFailureRetryCount</em> y <em>TransientFailureRetryInterval</em>.</p>
<p>Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>MessageRetryInterval</em></p></td>
<td><p><code>00:15:00</code> o 15 minutos</p></td>
<td><p>Cmdlet <strong>Set-TransportService</strong></p></td>
<td><p>Este parámetro especifica el intervalo de reintento para cada mensaje que tiene un estado de reintento. Recomendamos que no modifique el valor predeterminado a no ser que el Servicio de soporte técnico y atención al cliente de Microsoft le aconseje hacerlo.</p></td>
</tr>
<tr class="odd">
<td><p><em>MailboxDeliveryQueueRetryInterval</em></p></td>
<td><p><code>00:05:00</code> o 5 minutos</p></td>
<td><p>EdgeTransport.exe.config</p></td>
<td><p>Esta clave especifica la frecuencia con que las colas intentan conectarse al servicio de entrega de transporte de buzones para una base de datos de buzones de correo de destino a la que no se puede conectar correctamente.</p>
<p>Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.</p>
<p>El valor válido para esta clave es de 00:00:01 a 1.00:00:00.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Opciones de configuración para el reintento manual de mensajes

Cuando una cola de entrega está en estado de Reintentar, puede forzar manualmente un intento de conexión inmediato con el Visor de cola del cuadro de herramientas de Exchange o con el cmdlet **Retry-Queue** del Shell. Este reintento de conexión manual invalida el siguiente tiempo de reintento programado. Si no se logra establecer la conexión, se restablece el temporizador de intervalos de reintento. La cola debe estar en estado de reintento para que esta acción tenga efecto.

Para más información, vea la sección "Reintentar colas" en [Administración de colas](manage-queues-exchange-2013-help.md).

Volver al principio

## Opciones de configuración de los mensajes de DSN con retraso

Después de cada error de entrega de mensaje, el servidor de transporte perimetral o el servicio de transporte del servidor de buzones de correo genera una notificación de estado de entrega (DSN) con retraso y lo pone en cola para entregarlo al remitente del mensaje que no se puede entregar. Este mensaje de DSN de retraso solo se envía después de un intervalo de tiempo de expiración de notificación de retraso especificado y solo en caso de que el mensaje erróneo no se hubiera entregado durante este período. De forma predeterminada, el intervalo de tiempo de expiración de notificación de retraso es de 4 horas. Este retraso evita enviar mensajes DSN de retraso innecesarios que podrían estar provocados por errores de transmisión de mensajes temporales. El envío de mensajes de notificación de DSN se puede habilitar o deshabilitar de forma selectiva para los mensajes que se generan dentro o fuera de la organización de Exchange.

En la tabla siguiente se describen las opciones de configuración que están disponibles para los mensajes de DSN de retraso.

### Opciones de configuración que están disponibles para los mensajes de DSN de retraso

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del parámetro</th>
<th>Valor predeterminado</th>
<th>Ubicación</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>DelayNotificationTimeOut</em></p></td>
<td><p><code>4:00:00</code>4 horas</p></td>
<td><p><strong>Set-TransportService</strong> o propiedades de servidor en el EAC</p></td>
<td><p>Este parámetro especifica cuánto tiempo espera el servidor antes de enviar un mensaje de DSN al remitente. El valor de este parámetro siempre debe ser mayor que el valor del parámetro <em>TransientFailureRetryCount</em> multiplicado por el valor del parámetro <em>TransientFailureRetryInterval</em>.</p>
<p>Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>ExternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Este parámetro especifica si los mensajes de DSN con retraso se pueden enviar a los remitentes de mensajes de fuera de la organización de Exchange.</p>
<p>La entrada válida para este parámetro es <code>$true</code> o <code>$false</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>InternalDelayDSNEnabled</em></p></td>
<td><p><code>$true</code></p></td>
<td><p><strong>Set-TransportConfig</strong></p></td>
<td><p>Este parámetro especifica si los mensajes de DSN con retraso se pueden enviar a los remitentes de mensajes de dentro de la organización de Exchange.</p>
<p>La entrada válida para este parámetro es <code>$true</code> o <code>$false</code>.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> En los servidores de transporte de concentradores de Exchange 2007, todos los parámetros <EM>ExternalDSN*</EM> y <EM>InternalDSN*</EM> están disponibles en el cmdlet <STRONG>Set-TransportServer</STRONG> (y no en el cmdlet <STRONG>Set-TransportConfig</STRONG>). Si tiene algún servidor de transporte de concentradores de Exchange 2007 en la organización, deberá realizar los cambios en estos valores usando el cmdlet <STRONG>Set-TransportServer</STRONG> en cada uno de los servidores de transporte de concentradores de Exchange 2007.



Volver al principio

## Opciones de configuración para el reenvío de mensajes

El reenvío de mensajes devuelve los mensajes no entregados a la cola de envío para que el categorizador los vuelva a procesar.

## Reenvío automático de mensajes

Los mensajes no entregados se reenvían automáticamente si la cola de entrega se encuentra en el estado de reintento y no ha podido entregar con éxito ningún mensaje durante un determinado periodo de tiempo. Este período de tiempo está controlado por la clave *MaxIdleTimeBeforeResubmit* del archivo de configuración de la aplicación EdgeTransport.exe.config. Solo los mensajes de las colas de entrega son candidatos para el reenvío automático.

Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.

El valor predeterminado es `12:00:00` o 12 horas.

## Reenvío manual de mensajes

Se pueden reenviar manualmente los mensajes que tengan el siguiente estado en el servicio de transporte de un servidor de buzones de correo o de un servidor de transporte perimetral:

  - Colas de entrega con estado "Reintentar". Los mensajes de las colas no deben estar en estado suspendido.

  - Los mensajes que están en la cola inaccesible y no se encuentran en el estado suspendido.

  - Los mensajes que están en la cola de mensajes dudosos.

Para más información la cola de mensajes dudosos y de la cola inaccesible, vea "Acerca de la cola de mensajes dudosos y la cola inaccesible" en el tema [Colas](queues-exchange-2013-help.md).

Si quiere reenviar manualmente mensajes situados en las colas de entrega o en la cola de entrega inaccesible sin esperar a que transcurra el período de tiempo especificado por el parámetro *MaxIdleTimeBeforeResubmit*, debe usar el cmdlet **Retry-Queue** con el parámetro *Resubmit*. Para reenviar manualmente los mensajes situados en la cola de mensajes dudosos, se puede utilizar el Visor de Cola o el cmdlet **Resume-Message** para reanudar el mensaje. Para más información, vea la sección "Reenviar mensajes en colas" en [Administración de colas](manage-queues-exchange-2013-help.md).

Otra forma de reenviar manualmente mensajes es suspender los mensajes, exportarlos a archivos de texto con la extensión .eml y luego copiar los archivos .eml en el directorio de reproducción de cualquier servidor de buzones de correo o de transporte perimetral. Este método de reenvío funciona para mensajes ubicados en las colas de entrega o en la cola inaccesible. Los mensajes situados en la cola de mensajes dudosos ya se encuentran en estado suspendido. Los mensajes que se hallan en la cola de envío no se pueden suspender ni exportar.


> [!NOTE]
> Cuando se exportan mensajes desde una cola, no se eliminan de ella. Una vez que haya exportado los mensajes y los haya reenviado satisfactoriamente mediante el directorio de reproducción, deberá quitar los mensajes suspendidos para evitar que se entreguen por duplicado.



Para obtener más información, vea [Exportar mensajes de las colas](export-messages-from-queues-exchange-2013-help.md).

Volver al principio

## Opciones de configuración para la expiración de mensajes

El *intervalo de tiempo de espera de expiración del mensaje* especifica el período de tiempo máximo durante el cual un servidor de transporte perimetral o el servicio de transporte de un servidor de buzones de correo intenta entregar un mensaje que no se ha podido entregar antes. Si no se consigue entregar el mensaje antes de que transcurra el intervalo de tiempo de espera de expiración, se entrega al remitente un NDR con el mensaje original o los encabezados del mensaje.

## Expiración automática de mensajes

El intervalo de espera de expiración de mensajes está controlado por el parámetro *MessageExpirationTimeOut* del cmdlet **Set-TransportService** o de las propiedades de servidor del EAC.

Para especificar un valor, especifíquelo como un intervalo de tiempo: dd.hh:mm:ss en el que d = días, h = horas, m = minutos y s = segundos.

El valor predeterminado es `2.00:00:00` o 2 días. El intervalo de entrada válido para este parámetro es de `00:00:05` a `90.00:00:00`.

## Expiración manual de mensajes

Aunque no se puede forzar manualmente la expiración de los mensajes, sí se pueden eliminar manualmente los mensajes de cualquier cola, a excepción de la cola de envío, sin o con un NDR.

Para más información, vea la sección "Eliminar mensajes en colas" en [Administrar mensajes en colas](manage-messages-in-queues-exchange-2013-help.md).

Volver al principio

