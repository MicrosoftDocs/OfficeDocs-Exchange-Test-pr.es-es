---
title: 'Limitación de mensajes: Exchange 2013 Help'
TOCTitle: Limitación de mensajes
ms:assetid: fba87902-2a79-42ac-b394-46a9016f667e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232205(v=EXCHG.150)
ms:contentKeyID: 49896030
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Limitación de mensajes

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

La *limitación de mensajes* se refiere a un grupo de límites que se establecen respecto del número de mensajes y conexiones que pueden ser procesados por un equipo de Microsoft Exchange Server 2013. Estos límites evitan el agotamiento accidental o intencionado de los recursos del sistema en el servidor de Exchange.

**Contenido**

Message throttling scope

Message cost and mail flow throttling

Message throttling on servers

Message throttling on Send connectors

Message throttling on Receive connectors

Message throttling policies

## Ámbito de limitación de mensajes

La limitación de mensajes incluye una variedad de límites para las velocidades de procesamiento de mensajes, las velocidades de conexión de SMTP y los valores de tiempo de espera de sesiones de SMTP. Estos límites trabajan juntos para evitar la saturación de un servidor de Exchange causada por la aceptación y la entrega de mensajes. Aunque es posible que haya una gran cantidad de mensajes y conexiones pendientes esperando el procesamiento, los límites de mensajes permiten que el servidor de Exchange procese los mensajes y las conexiones en orden.

Además de la limitación de mensajes, también puede establecer límites de tamaño para los componentes individuales de los mensajes, como el número de destinatarios, el tamaño del encabezado del mensaje o el tamaño de los datos adjuntos individuales. Para obtener más información acerca de los límites de tamaño de los mensajes, consulte [Límites de tamaño de mensaje](message-size-limits-exchange-2013-help.md).

Otra característica que ayuda a evitar la saturación de los recursos del sistema de un servidor de transporte de Exchange es la *contrapresión*. La contrapresión es una característica de supervisión de los recursos del sistema en el servicio de transporte en servidores de buzones de correo y servidores de transporte perimetral. Cuando un recurso del sistema supervisado, como el uso del disco duro o el uso de memoria, supera el umbral especificado, el servidor reduce la velocidad con la que acepta conexiones y mensajes nuevos, y se concentra en entregar mensajes existentes. Cuando el uso de los recursos supervisados del sistema vuelve a los niveles normales, el servidor aumenta gradualmente la velocidad con la que acepta conexiones y mensajes nuevos, y luego establece un nivel normal.

Volver al principio

## Limitación del flujo de correo y costo de los mensajes

Para ofrecer un rendimiento más coherente de los mensajes y una latencia de entrega de mensajes predecible, Exchange 2013 establece un costo acumulado para los mensajes. Esta característica de calidad de servicio (QoS) se agregó a Microsoft Exchange Server 2010 SP1. Este costo se basa en los siguientes criterios:

  - Tamaño del mensaje

  - Número de destinatarios

  - Frecuencia de transmisión

Los servidores de transporte de Exchange 2013 realizan un seguimiento del costo de entrega promedio de los mensajes que envían los usuarios individuales. Al usar los costos de los mensajes, Exchange 2013 proporciona un grupo de valores de configuración que pueden controlar el efecto que un usuario o una conexión tienen en una organización de Exchange. Este grupo de configuración se conoce como *directiva de limitación*. Cuando un usuario envía repetidamente mensajes costosos, como mensajes con datos adjuntos de gran tamaño o mensajes que se envían a muchos destinatarios, los servidores de transporte basados en Exchange 2013 utilizan una directiva de limitación para asignar una prioridad más baja a los mensajes de costo alto del usuario y entregar los mensajes con un costo más bajo. Este nuevo comportamiento aporta un aspecto de \&quot;calidad de servicio\&quot; a la funcionalidad de la limitación de mensajes en Exchange 2013.


> [!NOTE]
> La limitación de mensajes no afecta a la prioridad de los mensajes desde la perspectiva de un usuario. Los mensajes aún conservan la prioridad original establecida por el usuario. Por ejemplo, los mensajes conservan una configuración de Importante o Urgente, y así sucesivamente.



Para respaldar esta nueva funcionalidad, Exchange 2013 usa los mecanismos siguientes:

  - **Agente de priorización interno** Este agente se desencadena en el evento **OnResolvedMessage** y asigna una prioridad menor a los mensajes de un mismo remitente que tengan un alto coste acumulado. Este costo se mide durante un minuto y afecta a los mensajes que tienen más de 500 destinatarios o cuyo tamaño supera 1 megabyte (MB).

  - **Colas de prioridad por cuotas para el tipo de cola MapiDelivery**   Con este mecanismo, Exchange entrega los mensajes de una cola de prioridad normal con más frecuencia que los mensajes de una cola de prioridad baja. De forma predeterminada, la relación de mensajes de normal a baja es de 20:1. Sin embargo, los mensajes nuevos con una cola de prioridad más baja no se entregan antes que los elementos nuevos de una cola con una prioridad más alta. Por ejemplo, considere la siguiente situación:
    
    1.  Se entregan veinte mensajes de prioridad normal. De forma predeterminada, el siguiente mensaje entregado es un mensaje con una prioridad más baja.
    
    2.  El servidor de transporte recibe dos nuevos mensajes: Un mensaje proveniente de una cola con una prioridad más alta y un mensaje de una cola con una más baja.
    
    En este escenario, se entrega primero el mensaje de la cola con la prioridad más alta. A continuación, se entrega el mensaje de la cola con la prioridad menor.

  - **Limitar conexiones simultáneas según el estado de la base de datos de mensajería**   Este mecanismo supervisa el estado de la base de datos de mensajería (MDB) de Exchange y limita las conexiones simultáneas con servidores de transporte de Exchange según un valor asignado de medida de estado. La API del monitor de estado de recursos supervisa la MDB en el servicio de transporte del servidor de buzones de correo y la MDB recibe un valor de estado de -1 a 100. Este valor se basa en las estadísticas de rendimiento de RPC que se incluyen con cada respuesta de RPC desde el proceso Store.exe en el servicio de transporte de buzones de correo. El marco Mantenimiento de recursos utiliza el contador de rendimiento de la relación **Solicitudes/segundo** y el contador de rendimiento de **Latencia RPC promedio** para calcular un valor de mantenimiento para la base de datos. Para ayudar a mantener una experiencia de usuario interactiva y coherente, Exchange reduce el número de conexiones simultáneas a medida que el valor de estado disminuye. Están disponibles los intervalos de valores de mantenimiento siguientes:
    
      - **-1:** este valor indica que se desconoce el estado de mantenimiento de la MDB. Este valor se asigna cuando se inicia la base de datos. En este escenario, la base de datos se considera correcta.
    
      - **0:** este valor se asigna cuando la base de datos se encuentra en un estado incorrecto. En este estado, no se debe establecer contacto con la base de datos.
    
      - **De 1 a 99:** estos valores representan un estado de mantenimiento razonable. Un valor inferior representa una base de datos menos correcta.
    
      - **100:** este valor representa una base de datos correcta.

El servicio de limitación de peticiones de Microsoft Exchange proporciona el marco para la limitación del flujo de correo. El servicio de limitación de peticiones de Exchange realiza un seguimiento de la configuración de limitación del flujo de correo para un usuario específico y almacena en caché la información sobre la limitación. La configuración de la limitación del flujo de correo también se conoce como *presupuesto*. Al reiniciar el servicio de limitación de peticiones de Exchange, también se restablecen los presupuestos de limitación del flujo de correo.

Puede usar los cmdlets de la directiva de limitación que están disponibles en Exchange 2013 para configurar las opciones de presupuesto individuales para una directiva de limitación. Un presupuesto es la cantidad de acceso que puede tener un usuario o una aplicación para una configuración específica. Un presupuesto representa el número de conexiones que puede tener un usuario o la cantidad de actividad que puede permitirse un usuario para cada minuto. Por ejemplo, un presupuesto puede configurarse para establecer la cantidad de tiempo durante el cual un usuario puede usar una característica específica en Exchange, como ActiveSync, Outlook Web App o los servicios Web Exchange. Este umbral se almacena en una directiva de limitación y define el presupuesto.

La configuración del tiempo para un presupuesto se establece con un porcentaje de un minuto. Por lo tanto, un umbral de 100 por ciento representa 60 segundos. Por ejemplo, suponga que quiere especificar la configuración de una directiva de Outlook Web App que limite la cantidad de tiempo durante la cual un usuario puede ejecutar un código de Outlook Web App en un servidor de acceso de cliente y la cantidad de tiempo que un usuario puede comunicarse con el servidor de acceso de cliente a 600 milisegundos durante un minuto. Para lograrlo, necesita establecer el valor a 1 por ciento de un minuto (600 milisegundos) para los dos parámetros siguientes:

  - **OWAPercentTimeInCAS:** 1

  - **OWAPercentTimeInMailboxRPC:** 1

Un usuario que tenga aplicada esta directiva tiene un presupuesto de OWAPercentTimeInCAS de 600 milisegundos y de OWAPercentageTimeInMailboxRPC de 600 milisegundos. En este escenario, cuando el usuario inicia sesión en Outlook Web App, puede ejecutar el código de acceso de cliente durante 600 milisegundos como máximo. Pasado este tiempo, se considera que la conexión sobrepasa el presupuesto y el servidor de Exchange no permite ninguna acción posterior de Outlook Web App hasta un minuto después de alcanzar el límite de presupuesto. Pasado un minuto, el usuario puede ejecutar un código de acceso de cliente de Outlook Web App durante otros 600 milisegundos.

Volver al principio

## Limitación de mensajes en servidores

Puede establecer las opciones de aceleración de mensajes en las siguientes ubicaciones:

  - En el servicio de transporte

  - En un conector de envío

  - En un conector de recepción

Con el Shell de administración de Exchange, puede configurar todas las opciones de limitación de mensajes que están disponibles en el servicio de transporte en servidores de buzones de correo, en el servicio de transporte de buzones de correo en servidores de buzones de correo o en el servicio de transporte front-end en servidores de acceso de cliente. También puede establecer algunas de las mismas opciones mediante la configuración de las propiedades del servidor de transporte en el Centro de administración de Exchange (EAC).

En la siguiente tabla, se muestran las opciones de limitación de mensajes disponibles en servidores de transporte.

### Opciones de limitación de mensajes en servidores de transporte

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origen</th>
<th>Parámetro</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxDeliveries</em></p></td>
<td><p>20</p></td>
<td><p>Este parámetro especifica el número máximo de subprocesos de entrega que el servicio de transporte puede tener abiertos al mismo tiempo para entregar mensajes a buzones de correo. El rango de entrada válido para este parámetro es de 1 a 256. Le recomendamos que no modifique el valor predeterminado a menos que el Servicio de soporte y atención al cliente de Microsoft le aconseje hacerlo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p>
<p><strong>Set-MailboxTransportService</strong></p></td>
<td><p><em>MaxConcurrentMailboxSubmissions</em></p></td>
<td><p>20</p></td>
<td><p>Este parámetro especifica el número máximo de subprocesos de envío que el servicio de transporte puede tener abiertos al mismo tiempo para enviar mensajes desde buzones de correo. El intervalo de entrada válido para este parámetro es de 1 a 256.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>MaxConnectionRatePerMinute</em></p></td>
<td><p>1200</p></td>
<td><p>Este parámetro especifica la frecuencia máxima permitida de apertura de conexiones con el servicio de transporte. Si se intentan establecer muchas conexiones con el servicio de transporte al mismo tiempo, el parámetro <em>MaxConnectionRatePerMinute</em> limita la tasa de apertura de conexiones de forma que los recursos del servidor no se vean desbordados.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong> o</p>
<p>Propiedades del servidor de transporte</p></td>
<td><p><em>MaxOutboundConnections</em></p></td>
<td><p>1000</p></td>
<td><p>Este parámetro especifica el número máximo de conexiones de salida que se pueden abrir a la vez. Si escribe un valor <code>unlimited</code>, no se impone ningún límite en el número de conexiones de salida. El valor de este parámetro debe ser mayor o igual que el valor del parámetro <em>MaxPerDomainOutboundConnections</em>.</p>
<p>Este valor también se puede configurar mediante el EAC en <strong>Servidores</strong> &gt; <strong>Servidores</strong> &gt; <strong>Propiedades</strong> &gt; <strong>Límites de transporte</strong> &gt; <strong>Restricciones de conexión de salida</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-TransportService</strong> o</p>
<p>Propiedades del servidor de transporte</p></td>
<td><p><em>MaxPerDomainOutboundConnections</em></p></td>
<td><p>20</p></td>
<td><p>Este parámetro especifica el número máximo de conexiones simultáneas en un único dominio. Si escribe un valor <code>unlimited</code>, no se impone ningún límite en el número de conexiones de salida por dominio. El valor de este parámetro debe ser mayor o igual que el valor del parámetro <em>MaxOutboundConnections</em>.</p>
<p>Este valor también se puede configurar mediante el EAC en <strong>Servidores</strong> &gt; <strong>Servidores</strong> &gt; <strong>Propiedades</strong> &gt; <strong>Límites de transporte</strong> &gt; <strong>Restricciones de conexión de salida</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-TransportService</strong></p></td>
<td><p><em>PickupDirectoryMaxMessagesPerMinute</em></p></td>
<td><p>100</p></td>
<td><p>Este parámetro especifica el número máximo de mensajes que el directorio de recogida y el directorio de reproducción procesarán por minuto. Cada directorio puede procesar independientemente los archivos de mensajes con la velocidad especificada por este parámetro.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Limitación de mensajes en conectores de envío

En la siguiente tabla, se muestra la opción de limitación de mensajes disponible en conectores de envío. Debe usar el Shell de administración de Exchange para configurar esta opción.

### Opción de limitación de mensajes disponible en conectores de envío

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origen</th>
<th>Parámetro</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-SendConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>10 minutos</p></td>
<td><p>Este parámetro especifica el tiempo máximo que puede permanecer inactiva una conexión SMTP con un servidor de mensajería de destino antes de que se cierre la conexión.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Limitación de mensajes en conectores de recepción

En la siguiente tabla, se muestran las opciones de limitación de mensajes disponibles en conectores de recepción que están configurados en el servicio de transporte en un servidor de buzones de correo o en un servidor de transporte perimetral. Debe usar el Shell de administración de Exchange para configurar estas opciones.

### Opciones de limitación de mensajes disponibles en conectores de recepción

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Origen</th>
<th>Parámetro</th>
<th>Valor predeterminado</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionInactivityTimeOut</em></p></td>
<td><p>5 minutos en el servicio de transporte en los servidores Buzón de correo</p>
<p>5 minutos en el servicio the transporte front-end en los servidores de Acceso de clientes.</p>
<p>1 minuto en los servidores Transporte perimetral.</p></td>
<td><p>Este parámetro especifica el tiempo máximo que puede permanecer inactiva una conexión SMTP abierta con un servidor de mensajería de origen antes de que se cierre la conexión. El valor de este parámetro debe ser menor que el valor especificado por el parámetro <em>ConnectionTimeout</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>ConnectionTimeOut</em></p></td>
<td><p>10 minutos en el servicio de transporte en los servidores Buzón de correo</p>
<p>10 minutos en el servicio the transporte front-end en los servidores de Acceso de clientes.</p>
<p>5 minutos en los servidores Transporte perimetral.</p></td>
<td><p>Este parámetro especifica el tiempo máximo que puede permanecer abierta una conexión SMTP con un servidor de mensajería de origen, incluso aunque el servidor de mensajería de origen esté transmitiendo datos. El valor de este parámetro debe ser mayor que el valor especificado por el parámetro <em>ConnectionInactivityTimeout</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnection</em></p></td>
<td><p>5000</p></td>
<td><p>Este parámetro especifica el número máximo de conexiones SMTP entrantes que permite este conector de recepción al mismo tiempo.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPercentagePerSource</em></p></td>
<td><p>100% en el conector de recepción predeterminado en el servicio de transporte en un servidor de buzones de correo</p>
<p>2% en los otros conectores de recepción en el servicio de transporte en servidores de buzones de correo y en el servicio de transporte front-end en servidores de acceso de cliente.</p></td>
<td><p>Este parámetro especifica el número máximo de conexiones SMTP que permite un conector de recepción al mismo tiempo desde un único servidor de mensajería de origen. El valor se expresa como el porcentaje de conexiones restantes disponibles en un conector de recepción. El número máximo de conexiones que permite el conector de recepción se define con el parámetro <em>MaxInboundConnection</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxInboundConnectionPerSource</em></p></td>
<td><p>unlimited en el conector de recepción predeterminado en el servicio de transporte en un servidor de buzones de correo</p>
<p>20 en los otros conectores de recepción en el servicio de transporte en los servidores de buzones de correo y en el servicio de transporte front-end en los servidores de acceso de cliente.</p></td>
<td><p>Este parámetro especifica el número máximo de conexiones SMTP que permite un conector de recepción al mismo tiempo desde un único servidor de mensajería de origen.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>MaxProtocolErrors</em></p></td>
<td><p>5</p></td>
<td><p>Este parámetro especifica el número máximo de errores de protocolo SMTP que un conector de recepción permite antes de cerrar la conexión con el servidor de mensajería de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Set-ReceiveConnector</strong></p></td>
<td><p><em>TarpitInterval</em></p></td>
<td><p>5 segundos</p></td>
<td><p>Este parámetro especifica el retraso que se usa en el <em>retraso del tráfico de red (tarpitting)</em>. El bloqueo del correo electrónico masivo es la práctica de retrasar artificialmente las respuestas de SMTP para ciertos patrones de comunicación de SMTP que indican ataques de robo de directorio u otros mensajes no deseados. Un <em>ataque de robo de directorio</em> es un intento de recopilar direcciones de correo electrónico válidas de una organización concreta para utilizarlas como destino para correo electrónico comercial no solicitado.</p>
<p>El retraso especificado por el parámetro <em>TarpitInterval</em> sólo se aplica a conexiones anónimas.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Directivas de limitación de mensajes

En Exchange 2013, cada buzón de correo tiene una configuración de *ThrottlingPolicy*. De forma predeterminada, el valor de está configuración está en blanco (`$null`). Puede usar el parámetro *ThrottlingPolicy* en el cmdlet **Set-Mailbox** para configurar una directiva de limitación para un buzón de correo.

Existe una directiva de limitación predeterminada para ofrecer una configuración de presupuesto predeterminada para usuarios que se conecten a Exchange. Para configurar opciones de prepuesto personalizadas para uno o más usuarios, cree una nueva directiva de limitación. A continuación, aplique la directiva al grupo o usuario apropiado.


> [!IMPORTANT]
> Le recomendamos que no modifique la directiva de limitación predeterminada.



En el Shell de administración de Exchange, puede configurar todas las opciones de limitación de mensajes disponibles en los servidores de buzones de correo. Los cmdlets siguientes están disponibles para administrar las directivas de limitación:

  - **Get-ThrottlingPolicy**

  - **Remove-ThrottlingPolicy**

  - **New-ThrottlingPolicy**

  - **Set-ThrottlingPolicy**

Puede usar los cmdlets **New-ThrottlingPolicy** y **Set-ThrottlingPolicy** para configurar la cantidad de actividad que puede realizar un usuario en Exchange durante un período o una conexión específicos. Estos valores constituyen el presupuesto del usuario. Puede establecer directivas de limitación para controlar el acceso a las siguientes características de Exchange:

  - Exchange ActiveSync

  - Servicios web de Exchange

  - Outlook Web App

  - Mensajería unificada

  - IMAP4

  - POP3

  - Conexiones de cliente de Outlook (conexiones MAPI o RPC)

  - Configuración de flujo de correo

  - Comandos de PowerShell

  - Usos de la CPU

Volver al principio

