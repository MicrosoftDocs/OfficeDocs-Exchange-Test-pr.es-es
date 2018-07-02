---
title: 'Colas: Exchange 2013 Help'
TOCTitle: Colas
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 51406567
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Colas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Una *cola* es una ubicación temporal para alojar mensajes que esperan para entrar en la próxima etapa de procesamiento o entrega a un destino. Cada cola representa un conjunto lógico de mensajes que procesa el servidor de Exchange en un orden específico. En Microsoft Exchange Server 2013, las colas retienen mensajes antes y después de la entrega, y durante ella. Hay colas en servidores de buzones de correo y en servidores de transporte perimetral. En este tema, los servidores de buzones de correo y los servidores de transporte perimetral se denominan *servidores de transporte*.

Como en versiones anteriores de Exchange, Exchange 2013 usa una sola base de datos del motor de almacenamiento extensible (ESE) para el almacenamiento de las colas.

Puede administrar colas y los mensajes de las colas con el Shell de administración de Exchange y el Visor de cola en el cuadro de herramientas de Exchange. Puede usar estas interfaces para ver el estado y contenidos de las colas y las propiedades detalladas de los mensajes. También puede usar estas interfaces para llevar a cabo acciones que modifican las colas o los mensajes en las colas.

**Contenido**

  - Tipos de colas

  - Archivos de base de datos de colas

  - Propiedades de la cola
    
      - NextHopSolutionKey
    
      - IncomingRate, OutgoingRate y Velocity
    
      - Estado de la cola
    
      - Otras propiedades de la cola

  - Propiedades del mensaje
    
      - Estado del mensaje
    
      - Otras propiedades del mensaje

  - Administración de colas y mensajes en las colas

## Tipos de colas

En Exchange 2013 se utilizan los siguientes tipos de cola:

  - **Colas persistentes**   Las *colas persistentes* son colas que existen en todos los servidores de transporte en cada organización de Exchange. Como en las versiones anteriores de Exchange, hay tres colas persistentes en Exchange 2013:
    
      - **Cola de envío**   La cola de envío que usa el categorizador para juntar todos los mensajes que tienen que ser resueltos, enrutados y procesados por los agentes de transporte en el servidor de transporte. Todos los mensajes recibidos por el servidor de transporte entran a formar parte del procesamiento en la cola de Envío. En los servidores de buzones de correo, los mensajes se envían a través de un conector de recepción, los directorios de recogida o de reproducción o el servicio de entrega de transporte de buzones. En los servidores de transporte perimetral, los mensajes se envían normalmente a través de un conector de recepción, pero los directorios de recogida o reproducción también están disponibles.
        
        El categorizador recupera mensajes de esta cola y, entre otras cosas, determina la ubicación del destinatario y la ruta a esa ubicación. Tras la categorización, el mensaje se mueve a una cola de entrega o a una cola Inalcanzable. Cada servidor de transporte tiene una sola cola de envío. Los mensajes que se encuentran en la cola de envío no pueden estar en otras colas al mismo tiempo. Para más información sobre el categorizador y el canal de transporte, vea [Flujo de correo](mail-flow-exchange-2013-help.md).
    
      - **Cola inaccesible**   La cola inaccesible contiene mensajes que no se pueden enrutar a sus destinos. Normalmente, un destino inalcanzable es provocado por los cambios de configuración que han modificado la ruta de enrutamiento para la entrega. Sin tener en cuanta el destino, todos los mensajes con destinatarios inalcanzables residen en esta cola. Cada servidor de transporte tiene una sola cola inaccesible.
        
        Los mensajes de la cola inaccesible se reenvían automáticamente cuando se detecta un cambio de enrutamiento. Así que, después de que la condición o el error de configuración que hizo que los mensajes entraran en la cola inaccesible se repare, no es necesario realizar ninguna acción adicional para quitar los mensajes de la cola inaccesible para su entrega.
        
        La cola inaccesible normalmente está vacía. Si la cola inaccesible no contiene mensajes, no aparece en el Visor de cola ni en los resultados de **Get-Queue**.
    
      - **Cola de mensajes dudosos**   La cola de mensajes dudosos es una cola especial que se usa para aislar mensajes que se determinan como dañinos para el sistema de Exchange 2013 tras un error del servicio o del servidor de transporte. Los mensajes pueden ser realmente perjudiciales en cuanto al contenido y al formato. También pueden ser el resultado de un agente escrito incorrectamente que ha provocado un error en el servidor de Exchange cuando procesaba mensajes supuestamente incorrectos.
        
        La cola de mensajes dudosos normalmente está vacía. Si la cola de mensajes dudosos no contiene mensajes, no aparece en el Visor de cola ni en los resultados de **Get-Queue**. Los mensajes de la cola de mensajes dudosos no se reanudan nunca automáticamente ni expiran. Los mensajes permanecerán en la cola de mensajes dudosos hasta que un administrador los reanude manualmente o los quite.

  - **Colas de entrega**   Las colas de entrega retienen los mensajes antes de que se entreguen a un destino local o remoto mediante SMTP. Todos los mensajes se transmiten entre los servidores de Exchange mediante el uso de SMTP. Los destinos no SMTP también usan colas de entrega si el conector de agente de entrega da servicio al destino. . Cada cola de entrega contiene mensajes que se enrutan al mismo destino. Es prácticamente inevitable que existan varias colas de entrega en un servidor de transporte. Las colas de entrega se crean dinámicamente cuando se necesitan y se eliminan automáticamente cuando la cola está vacía o ha pasado el tiempo de expiración. El tiempo de expiración de cola lo controla el parámetro *QueueMaxIdleTime* en el cmdlet **Set-TransportService**. El valor predeterminado es de tres minutos.

  - **Colas duplicadas**   Las colas duplicadas retienen las copias redundantes de un mensaje mientras el mensaje está en tránsito. Para obtener más información, vea [Redundancia de instantánea](shadow-redundancy-exchange-2013-help.md).

  - **Red de seguridad**   La red de seguridad conserva copias de los mensajes que el servidor de transporte ha entregado correctamente. Aunque las herramientas de administración de colas no pueden obtener acceso a esta red, la red de seguridad es una cola más en la base de datos de colas. Para obtener más información, vea [Red de seguridad](safety-net-exchange-2013-help.md).

Volver al principio

## Archivos de base de datos de colas

Todas las diferentes colas se almacenan en una única base de datos ESE. De manera predeterminada, esta base de datos de colas se encuentra en un servidor de transporte en `%ExchangeInstallPath%TransportRoles\data\Queue`.

Como cualquier base de datos ESE, la base de datos de colas utiliza archivos de registro para aceptar, realizar un seguimiento y mantener datos. Para mejorar el rendimiento, todas las transacciones de mensajes se escriben primero en archivos de registro y en la memoria y, a continuación, en el archivo de base de datos. El archivo de punto de control realiza un seguimiento de las entradas del registro de transacciones que se hayan confirmado en la base de datos. Durante un cierre normal del servicio de transporte de Microsoft Exchange, los cambios no confirmados de la base de datos que se encuentran en los registros de transacciones están confirmados siempre en la base de datos.

Se utiliza un registro circular para la base de datos de colas. Esto significa que no se conserva el historial de transacciones confirmadas que se encuentran en los registros de transacciones. Todos los registros de transacciones anteriores al control actual se eliminarán de manera inmediata y automática. Por lo tanto, los registros de transacciones no pueden reproducirse para recuperar bases de datos de colas a partir de una copia de seguridad.

Exchange 2013 usa *tablas de generación* para almacenar y limpiar los mensajes en la base de datos de colas. En vez de procesar y eliminar registros de mensajes individuales desde una tabla grande, la base de datos de colas almacena mensajes en tablas basadas en tiempo y solo elimina la tabla entera después de que todos los mensajes de la tabla se hayan procesado correctamente. Por ejemplo, todos los mensajes en cola de la 1:00 p. m. a las 2:00 p. m., independientemente de la cola o el destino, se almacenan en la tabla `1p-2p_msgs`. A las 2:00 p. m., los nuevos mensajes se almacenan en la tabla `2p-3p_msgs`. A las 4:00 p. m, se crea una nueva tabla denominada `4p-5p_msgs` y toda la tabla `1p-2p_msgs` se elimina, pero solo si todos los mensajes de dicha tabla se procesaron correctamente. Este enfoque de eliminar tablas de mensajes enteras en vez de mensajes individuales ayuda a mejorar el rendimiento de E/S de la unidad que almacena la base de datos de colas.

La tabla siguiente enumera los archivos que constituyen la base de datos de colas.

### Archivos que constituyen la base de datos de colas

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Archivo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mail.que</p></td>
<td><p>Este archivo de bases de datos de colas almacena todos los mensajes en cola.</p></td>
</tr>
<tr class="even">
<td><p>Tmp.edb</p></td>
<td><p>Este archivo de base de datos temporal se utiliza para comprobar el esquema de una base de datos de colas durante el inicio.</p></td>
</tr>
<tr class="odd">
<td><p>Trn*.log</p></td>
<td><p>Este registro de transacciones registra todos los cambios realizados en la base de datos de colas. Los cambios en la base de datos de colas se escriben primero en el registro de transacciones y se confirman después en la base de datos. Trn.log es el archivo de registro de transacciones activo. Trntmp.log es el siguiente archivo de registro de transacciones suministrado y que se crea por adelantado. Si el archivo de registro de transacciones Trn.log existente alcanza su tamaño máximo, Trn.log cambia su nombre por el de Trn<em>nnnn</em>.log, donde <em>nnnn</em> es un número de secuencia. Entonces, Trntmp.log cambia su nombre por el de Trn.log y se convierte en el archivo de registro de transacciones activo.</p></td>
</tr>
<tr class="even">
<td><p>Trn.chk</p></td>
<td><p>Este archivo de punto de control realiza un seguimiento de las entradas del registro de transacciones que se hayan confirmado en la base de datos. Este archivo está siempre en la misma ubicación que el archivo mail.que.</p></td>
</tr>
<tr class="odd">
<td><p>Trnres00001.jrs</p>
<p>Trnres00002.jrs</p></td>
<td><p>Estos archivos de registro de transacciones de reserva actúan como marcadores. Sólo se utilizan cuando el disco duro que contiene el registro de transacciones se queda sin espacio para detener correctamente la base de datos de colas.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Opciones para configurar la base de datos de colas

Puede configurar la base de datos de colas al agregar o modificar claves en el archivo de configuración de la aplicación XML `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. Este archivo está asociado con el servicio de transporte de Microsoft Exchange. Los cambios que realice en el archivo EdgeTransport.exe.config se aplicarán cuando reinicie el servicio de transporte de Microsoft Exchange.

La sección `<appSettings>` del archivo EdgeTransport.exe.config es donde puede agregar nuevas claves o modificar las claves existentes. Si una clave concreta no existe, puede agregarla manualmente para cambiar su valor.

Las claves de la base de datos de colas que están disponibles en el archivo EdgeTransport.exe.config se describen en la tabla siguiente.

### Claves de la base de datos de colas de mensajes que están disponibles en el archivo EdgeTransport.exe.config

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
<td><p><em>QueueDatabaseBatchSize</em></p></td>
<td><p>40</p></td>
<td><p>Esta clave especifica el número de operaciones de E/S de base de datos que pueden agruparse antes de su ejecución. De manera predeterminada, esta clave no existe en el archivo EdgeTransport.exe.config.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseBatchTimeout</em></p></td>
<td><p>100</p></td>
<td><p>Esta clave especifica el tiempo máximo en milisegundos que la base de datos esperará para que las múltiples operaciones de E/S de bases de datos se agrupen para poder ejecutarlas. Las operaciones de E/S de bases de datos se ejecutan sin esperar ninguna más si se cumplen las condiciones siguientes:</p>
<ul>
<li><p>No se ha alcanzado el número de operaciones de E/S de bases de datos que especifica la clave <em>QueueDatabaseBatchSize</em>.</p></li>
<li><p>Ha transcurrido el tiempo especificado por la clave <em>QueueDatabaseBatchTimeout</em>.</p></li>
</ul>
<p>De manera predeterminada, esta clave no existe en el archivo EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxConnections</em></p></td>
<td><p>4</p></td>
<td><p>Esta clave especifica el número de conexiones de bases de datos ESE que se pueden abrir.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingBufferSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>Esta clave especifica la memoria que se usa para almacenar los registros de transacciones en la memoria caché antes de que se escriban en el archivo de registro de transacciones.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseLoggingFileSize</em></p></td>
<td><p>5 MB</p></td>
<td><p>Esta clave especifica el tamaño máximo de un archivo de registro de transacciones. Cuando se alcanza el tamaño máximo del archivo de registro, se abre uno nuevo.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Esta clave especifica el directorio predeterminado para los archivos de registro de bases de datos de colas. Para obtener instrucciones acerca de cómo cambiar la ubicación de la base de datos de colas, vea <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Cambio de la ubicación de la base de datos de colas</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseMaxBackgroundCleanupTasks</em></p></td>
<td><p>32</p></td>
<td><p>Esta clave especifica el número máximo de elementos de trabajo de limpieza en segundo plano que pueden colocarse en cualquier momento en la cola para el conjunto de subprocesos del motor de base de datos.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragEnabled</em></p></td>
<td><p>True</p></td>
<td><p>La clave habilita o deshabilita una desfragmentación en línea programada de la base de datos de colas de correo. De manera predeterminada, esta clave no existe en el archivo EdgeTransport.exe.config.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabaseOnlineDefragSchedule</em></p></td>
<td><p><code>1:00:00</code> o 1:00 a. m.</p></td>
<td><p>Esta clave especifica la hora del día en formato de 24 horas en que se inicia la desfragmentación en línea de la base de datos de colas de correo. Para especificar un valor, hágalo en formato de hora: <em>hh:mm:ss</em>, donde <em>h</em> = horas, <em>m</em> = minutos y<em>s</em> = segundos.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseOnlineDefragTimeToRun</em></p></td>
<td><p><code>3:00:00</code> o 3 horas</p></td>
<td><p>Esta clave especifica el tiempo que se permite ejecutar la tarea de desfragmentación en línea. Incluso si la tarea de desfragmentación no termina a la hora especificada, la base de datos de colas se deja en un estado coherente. Para especificar un valor, especifíquelo como un intervalo de tiempo: <em>hh:mm:ss</em>, donde <em>h</em> = horas, <em>m</em> = minutos y<em>s</em> = segundos.</p></td>
</tr>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p><code>%ExchangeInstallPath%TransportRoles\data\Queue</code></p></td>
<td><p>Esta clave especifica el directorio predeterminado para los archivos de bases de datos de colas. Para obtener instrucciones acerca de cómo cambiar la ubicación de la base de datos de colas, vea <a href="change-the-location-of-the-queue-database-exchange-2013-help.md">Cambio de la ubicación de la base de datos de colas</a>.</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.



Volver al principio

## Propiedades de la cola

Una cola tiene más propiedades que describen el motivo y el estado de la cola. Algunas propiedades de la cola se aplican a la cola cuando se crea y no cambian. Otras propiedades contienen el tamaño del estado, la hora y otros indicadores que se actualizan frecuentemente.

Volver al principio

## NextHopSolutionKey

El componente de enrutamiento del categorizador en el servicio de transporte de Microsoft Exchange selecciona el destino de un mensaje, y dicho destino se usa para crear la cola de entrega. El destino está marcado en cada destinatario como el atributo **NextHopSolutionKey**. Todos los valores únicos del atributo **NextHopSolutionKey** corresponden a una cola de entrega por separado.

El atributo **NextHopSolutionKey** contiene los siguientes campos:

  - **DeliveryType**   El valor de este campo representa los resultados de la categorización del mensaje, y cómo el servicio de transporte tiene intención de transmitir el mensaje al siguiente salto, que podría ser el destino final del mensaje o un salto intermedio en el camino. El servicio de transporte usa una lista predefinida de valores para **DeliveryType** en función del destino de enrutamiento o del grupo de entrega de destino.

  - **NextHopDomain**   Este campo usa valores específicos basados en el valor del campo **DeliveryType**. Para las colas de entrega, el valor de este campo es efectivamente el nombre de la cola. El valor de **NextHopDomain** no siempre es un nombre de dominio. Por ejemplo, el valor podría ser el nombre del sitio de Active Directory de destino o el grupo de disponibilidad de base de datos (DAG). Piense en este campo como el siguiente nombre de salto, donde el valor es el nombre del destino de enrutamiento o el grupo de entrega de destino.

  - **NextHopConnector**   Este campo usa valores específicos basados en el valor del campo **DeliveryType**. El valor siempre se expresa como un GUID. Si este campo no se usa, el valor es un GUID con todos ceros. El valor de **NextHopConnector** no siempre es el GUID de un conector. Por ejemplo, el valor podría ser el GUID del sitio de Active Directory de destino o el DAG. Piense en este campo como el siguiente GUID de salto, donde el valor es el GUID del destino de enrutamiento o el grupo de entrega de destino.

Exchange 2013 también agrega la propiedad **NextHopCategory** a la cola en función del valor de **DeliveryType**. El valor de **NextHopCategory** es `External` o `Internal`. El valor `External` indica que el siguiente salto de la cola está fuera de la organización de Exchange. El valor `Internal` indica que el siguiente salto de la cola está dentro de la organización de Exchange. Tenga en cuenta que es posible que un mensaje para un destinatario externo necesite uno o más saltos internos antes de que los mensajes se entreguen externamente.

Los valores de **DeliveryType**, **NextHopCategory**, **NextHopDomain** y **NextHopConnector** se describen en la siguiente tabla.


<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de entrega en el Visor de cola</th>
<th>DeliveryType en el Shell</th>
<th>Descripción</th>
<th>NextHopCategory</th>
<th>NextHopDomain</th>
<th>NextHopConnector</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Agente de entrega</strong></p></td>
<td><p><strong>DeliveryAgent</strong></p></td>
<td><p>La cola almacena mensajes para entregarlos a los destinatarios en un espacio de dirección no SMTP. Los mensajes se entregan mediante un conector de agente de entrega que se configura en el servidor local.</p></td>
<td><p>External</p></td>
<td><p>Este valor es el espacio de dirección de destino que se configura en el conector de agente de entrega.</p></td>
<td><p>Este valor es el GUID del conector de agente de entrega. Por ejemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p><strong>DnsConnectorDelivery</strong></p></td>
<td><p>La cola almacena mensajes para entregarlos a destinatarios en un espacio de dirección SMTP. Los mensajes se entregan mediante un conector de envío que se configura en el servidor local. El conector de envío está configurado para usar el enrutamiento de DNS.</p></td>
<td><p>Externo</p></td>
<td><p>Este valor es el espacio de dirección de destino que se configura en el conector de envío. Por ejemplo, <code>contoso.com</code>.</p></td>
<td><p>Este valor es el GUID del conector de envío. Por ejemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p><strong>NonSmtpGatewayDelivery</strong></p></td>
<td><p>La cola almacena mensajes para entregarlos a los destinatarios en un espacio de dirección no SMTP. Los mensajes se entregan mediante un conector externo que se configura en el servidor local.</p></td>
<td><p>Externo</p></td>
<td><p>Este valor es el espacio de dirección de destino que se configura en el conector externo.</p></td>
<td><p>Este valor es el GUID del conector externo. Por ejemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p><strong>SmartHostConnectorDelivery</strong></p></td>
<td><p>La cola almacena mensajes para entregarlos a destinatarios en un espacio de dirección SMTP. Los mensajes se entregan mediante un conector de envío que se configura en el servidor local. El conector de envío está configurado para usar el enrutamiento de host inteligente.</p></td>
<td><p>Externo</p></td>
<td><p>Este valor es la lista de hosts inteligentes que se configuran en el conector de envío. Los hosts inteligentes pueden configurarse como FQDN, direcciones IP o ambos. Pueden ser de uno de los valores siguientes:</p>
<ul>
<li><p><strong>FQDN</strong>   La sintaxis es <code>&lt;FQDN1,FQDN2,...&gt;</code>. Por ejemplo, <code>smarthost01.contoso.com</code> o <code>smarthost01.contoso.com,smarthost02.fabrikam.com</code>.</p></li>
<li><p><strong>Dirección IP</strong>   La sintaxis es <code>&lt;[IPAddress1],[IPAddress2],...&gt;</code>. Por ejemplo, <code>[10.10.10.100]</code> o <code>[10.10.10.100],[10.10.10.101]</code>.</p></li>
<li><p><strong>FQDN y dirección IP</strong>   La sintaxis es <code>&lt;[IPAddress1],FQDN1,...&gt;</code> y depende de la forma en la que se indican los hosts inteligentes en el conector de envío. Por ejemplo, <code>[172.17.17.7],relay.tailspintoys.com</code> o <code>mail.contoso.com,[192.168.1.50]</code>.</p></li>
</ul></td>
<td><p>Este valor es el GUID del conector de envío. Por ejemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Entrega SMTP a buzón de correo</strong></p></td>
<td><p><strong>SmtpDeliveryToMailbox</strong></p></td>
<td><p>La cola retiene mensajes para la entrega a destinatarios de buzones de correo de Exchange 2013. La base de datos de buzones de correo de destino se encuentra en una de las siguientes ubicaciones:</p>
<ul>
<li><p>El servidor de buzones de correo local de Exchange 2013.</p></li>
<li><p>Un servidor de buzones de correo de Exchange 2013 en el mismo DAG.</p></li>
<li><p>Un servidor de buzones de correo de Exchange 2013 en el mismo sitio de Active Directory en entornos no DAG.</p></li>
</ul></td>
<td><p>Internal</p></td>
<td><p>Este valor es el nombre de la base de datos de buzones de correo de destino. Por ejemplo, <code>Mailbox Database 0471695037</code>.</p></td>
<td><p>Este valor es el GUID de la base de datos de buzones de correo de destino. Por ejemplo, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Retransmisión SMTP para enviar servidores de origen de conector</strong></p></td>
<td><p><strong>SmtpRelayToConnectorSourceServers</strong></p></td>
<td><p>La cola retiene mensajes para la entrega a destinatarios SMTP o no SMTP. Los mensajes se entregan mediante un conector de envío, un conector de agente de entrega o un conector externo que está configurado en un servidor de transporte remoto. El servidor de transporte remoto podría ser un servidor de buzones de correo de Exchange 2013 o un servidor de transporte de concentradores de Exchange 2007 o de Exchange 2010 de una versión anterior de Exchange. El servidor remoto podría estar ubicado en el sitio de Active Directory local o en un sitio de Active Directory remoto.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor es el nombre del conector de envío de destino, el conector de agente de entrega o del conector externo. Por ejemplo, <code>Contoso.com Send Connector</code>.</p></td>
<td><p>Este valor es el GUID del conector de envío de destino, el conector de agente de entrega o del conector externo. Por ejemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Retransmisión SMTP para el grupo de disponibilidad de base de datos</strong></p></td>
<td><p><strong>SmtpRelayToDag</strong></p></td>
<td><p>La cola retiene mensajes para entregar a los destinatarios de buzones de correo de Exchange 2013, donde la base de datos de buzones de correo de destino está ubicada en un DAG remoto. El DAG remoto podría estar ubicado en el sitio de Active Directory local o en un sitio de Active Directory remoto.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor es el nombre del DAG de destino. Por ejemplo, <code>DAG1</code>.</p></td>
<td><p>Este valor es el GUID del DAG de destino. Por ejemplo, <code>6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123</code></p></td>
</tr>
<tr class="even">
<td><p><strong>Retransmisión SMTP al grupo de entrega de buzones de correo</strong></p></td>
<td><p><strong>SmtpRelayToMailboxDeliveryGroup</strong></p></td>
<td><p>La cola retiene mensajes para entregar a los destinatarios de buzones de correo heredados, donde el buzón de destino está en un servidor de buzones de correo de Exchange 2007 o Exchange 2010. El mensaje está relacionado con un servidor de transporte de concentradores que ejecuta la misma versión de Exchange que el buzón de correo de destino. El servidor de transporte de concentradores de destino podría estar ubicado en el sitio de Active Directory local o en un sitio de Active Directory remoto.</p></td>
<td><p>Interno</p></td>
<td><p>El nombre de la cola usa la sintaxis: <code>Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion&gt;</code>, donde <em>&lt;NombreSitioAD&gt;</em> es el nombre del sitio de Active Directory de destino y <em>&lt;VersiónExchange&gt;</em> es la versión de Exchange en el servidor de buzones de correo.</p></td>
<td><p>Este valor está en blanco.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Retransmisión SMTP al sitio remoto de Active Directory</strong></p></td>
<td><p><strong>SmtpRelayToRemoteActiveDirectorySite</strong></p></td>
<td><p>La cola retiene mensajes para entregar a un destino remoto y la topología de enrutamiento requiere que el mensaje se enrute a través de un sitio de Active Directory específico. El sitio es un salto intermedio en la ruta hacia el destino final. Esta situación ocurre en las siguientes circunstancias:</p>
<ul>
<li><p>El mensaje debe enrutarse a través de un sitio del concentrador.</p></li>
<li><p>El mensaje requiere una entrega a través del conector de envío que está configurado en un servidor de transporte perimetral suscrito a un sitio de Active Directory remoto.</p></li>
</ul></td>
<td><p>Interno</p></td>
<td><p>Este valor es el nombre de sitio de Active Directory de destino. Por ejemplo, <code>NorthAmericanSite</code>.</p></td>
<td><p>Este valor es el GUID del sitio de Active Directory de destino. Por ejemplo, <code>bfd6c3df-5b65-8bfb-53f1f2c0d55c</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Retransmisión SMTP a servidores de Exchange especificados</strong></p></td>
<td><p><strong>SmtpRelayToServers</strong></p></td>
<td><p>La cola retiene mensajes para entregar a un grupo de distribución configurado para un servidor de expansión específico. La expansión podría ser un servidor de buzones de correo de Exchange 2013 o un servidor de transporte de concentradores de Exchange 2007 o de Exchange 2010. El servidor podría estar ubicado en el sitio de Active Directory local o en un sitio de Active Directory remoto.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor es el FQDN del servidor de expansión de destino. Por ejemplo, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Este valor es <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Retransmisión SMTP en un sitio de Active Directory al servidor de transporte perimetral</strong></p></td>
<td><p><strong>SmtpRelayWithinAdSiteToEdge</strong></p></td>
<td><p>La cola almacena mensajes para entregarlos a un espacio de dirección SMTP. Los mensajes se entregan a través del conector de envío que está configurado en un servidor de transporte perimetral suscrito a un sitio de Active Directory local.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor es el nombre del conector de envío que envía correo de Internet saliente desde la organización a Internet. Este conector de envío lo crea automáticamente la suscripción perimetral y se denomina <code>EdgeSync - &lt;ADSiteName&gt; to Internet</code>. <em>&lt;NombreSitioAD&gt;</em> es el nombre del sitio de Active Directory local al cual está suscrito el servidor de transporte perimetral.</p></td>
<td><p>Este valor es el GUID del conector de envío. Por ejemplo, <code>4520e633-d83d-411a-bbe4-6a84648674ee</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Heartbeat</strong></p></td>
<td><p><strong>Heartbeat</strong></p></td>
<td><p>Este valor está reservado para uso interno de Microsoft. Para más información sobre latidos, vea <a href="shadow-redundancy-exchange-2013-help.md">Redundancia de instantánea</a>.</p></td>
<td><p>n/d</p></td>
<td><p>n/d</p></td>
<td><p>n/d</p></td>
</tr>
<tr class="odd">
<td><p><strong>Redundancia de instantánea</strong></p></td>
<td><p><strong>ShadowRedundancy</strong></p></td>
<td><p>La cola retiene mensajes en una cola duplicada. Una cola duplicada retiene mensajes de copia redundantes en tránsito en caso de que los mensajes principales no se entreguen correctamente. Para obtener más información, vea <a href="shadow-redundancy-exchange-2013-help.md">Redundancia de instantánea</a>.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor es el FQDN del servidor principal para el cual la cola duplicada retiene copias redundantes de los mensajes principales. Por ejemplo, <code>mailbox01.contoso.com</code>.</p></td>
<td><p>Este valor es <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>Undefined</strong></p></td>
<td><p><strong>Undefined</strong></p></td>
<td><p>Este valor solo se usa en la cola de envío y en la cola de mensajes dudosos.</p></td>
<td><p>Interno</p></td>
<td><p>Para la cola de envío, este valor es <code>Submisssion</code>. Para la cola de mensajes dudosos, este valor es <code>Poison Message</code>.</p></td>
<td><p>Este valor es <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Inaccesible</strong></p></td>
<td><p><strong>Unreachable</strong></p></td>
<td><p>Este valor solo se usa en la cola inaccesible.</p></td>
<td><p>Interno</p></td>
<td><p>Este valor es <code>Unreachable Domain</code>.</p></td>
<td><p>Este valor es <code>00000000-0000-0000-0000-000000000000</code>.</p></td>
</tr>
</tbody>
</table>


Tenga en cuenta que Exchange 2013 es compatible con los valores heredados de **DeliveryType** para la compatibilidad con versiones anteriores de Exchange. Estos valores están disponibles en el Visor de cola y en el Shell, pero Exchange 2013 no los usa. Estos valores **DeliveryType** heredados son:

  - **MapiDelivery**   La cola retiene mensajes para que los entregue un servidor de transporte de concentradores de Exchange 2007 o de Exchange 2010 a un buzón de correo en un servidor de buzones de correo de Exchange 2007 o de Exchange 2010 en el sitio de Active Directory local.

  - **SmtpRelayWithinAdSite**   La cola retiene mensajes para entregar mediante un servidor de transporte de concentradores de Exchange 2007 o de Exchange 2010 a otro servidor de transporte de concentradores en el mismo sitio de Active Directory. El servidor de transporte de concentradores de destino puede ser el servidor de origen de un conector o un servidor de expansión de grupo de distribución.

  - **SmtpRelaytoTiRg**   La cola contiene mensajes para entregar mediante un servidor de transporte de concentradores de Exchange 2007 o de Exchange 2010 a un grupo de enrutamiento de Exchange Server 2003. El servidor de destino puede ser un servidor de origen de un conector, un servidor de expansión de un grupo de distribución o un servidor de cabeza de puente de Exchange 2003.

Volver al principio

## IncomingRate, OutgoingRate y Velocity

Exchange 2013 mide la velocidad de los mensajes que entran y salen de una cola y almacena estos valores en las propiedades de la cola. Puede usar estas tasas como indicador del estado de la cola y del servidor de transporte. Las propiedades son:

  - **IncomingRate**   Esta propiedad es la velocidad a la que los mensajes entran en la cola.
    
    Este valor se calcula a partir del número de mensajes que entran en la cola cada 5 segundos con la media de los últimos 60 segundos. La fórmula se puede expresar como `(i1+i2+i3+i4+i5+i6)/6`, donde i*n* = el número de mensajes entrantes en 5 segundos.

  - **OutgoingRate**   Esta propiedad es la velocidad a la que los mensajes salen de la cola.
    
    Este valor se calcula a partir del número de mensajes que salen de la cola cada 5 segundos con la media de los últimos 60 segundos. La fórmula se puede expresar como `(o1+o2+o3+o4+o5+o6)/6`, donde o*n* = el número de mensajes salientes en 5 segundos.

  - **Velocidad**   Esta propiedad es la velocidad de descarga de la cola y se calcula restando el valor de **IncomingRate** del valor de **OutgoingRate**.
    
    Si el valor de **Velocity** es superior a 0, los mensajes dejan la cola más rápido de lo que entran.
    
    Si el valor de **Velocity** es igual a 0, los mensajes dejan la cola tan rápido como entran en ella. Este es también el valor que verá cuando la cola esté inactiva.
    
    Si el valor de **Velocity** es inferior a 0, los mensajes entran a la cola más rápido de lo que la dejan.

En un nivel básico, un valor positivo de **Velocity** indica una cola en buen estado con una purga eficiente y un valor negativo de **Velocity** indica una cola con una purga ineficiente. Sin embargo, también debe tener en cuenta los valores de las propiedades **IncomingRate**, **OutgoingRate** y **MessageCount**, además de la magnitud del valor de **Velocity** de la cola. Por ejemplo, una cola que tiene un valor negativo grande de **Velocity**, un valor grande de **MessageCount**, un valor pequeño de **OutgoingRate** y un valor grande de **IncomingRate** presenta indicadores precisos de que la cola no se purga correctamente. Sin embargo, una cola con un valor negativo de **Velocity** muy próximo a cero que también tiene valores pequeños de **IncomingRate**, **OutgoingRate** y **MessageCount** no indica ningún problema con la cola.

Volver al principio

## Estado de la cola

El estado actual de la cola se almacena en la propiedad **Status** de la cola. Las colas pueden tener uno de los siguientes estados:

  - **Activa**   La cola está transmitiendo mensajes de forma activa.

  - **Conectando**   La cola está en proceso de conectarse con el siguiente salto.

  - **Preparada**   La cola ha transmitido mensajes recientemente, pero ahora está vacía.

  - **Reintentar**   El último intento de conexión automática o manual falló y la cola espera volver a intentar la conexión.

  - **Suspendida**   Un administrador ha suspendido manualmente la cola para impedir la entrega del mensaje. Los nuevos mensajes pueden entrar en la cola y los que se están transmitiendo al siguiente salto finalizarán la entrega y dejarán la cola. De lo contrario, los mensajes no dejarán la cola hasta que un administrador la reanude manualmente. Tenga en cuenta que la suspensión de una cola no cambia el estado de los mensajes individuales de la cola.
    
    Se pueden suspender las colas que tengan el estado Activo o Reintentar, así como las colas con el estado Inaccesible y Envío.
    
    Si suspende la cola inaccesible, los mensajes no se reenviarán automáticamente al categorizador cuando se detecten actualizaciones de configuración. Para reenviar estos mensajes automáticamente, debe reanudar manualmente la cola inaccesible. Si se suspende la cola Envío, el categorizador no recibirá mensajes hasta que se restaure la cola.

Volver al principio

## Otras propiedades de la cola

Hay otras propiedades de la cola que se explican por sí mismas. La mayoría de las propiedades de la cola se usan como opciones de filtro. Mediante la especificación de criterios de filtro, es posible localizar las colas con rapidez y realizar acciones en ellas. Para una descripción completa de las propiedades filtrables de la cola, vea [Filtros de cola](queue-filters-exchange-2013-help.md).

Una propiedad importante de la cola que también vale la pena mencionar aquí es la propiedad **MessageCount** que muestra el número de mensajes que hay en una cola. Esta propiedad es un indicador importante del estado de la cola. Por ejemplo, una cola de entrega que contiene un gran número de mensajes que continúa creciendo y nunca disminuye podría indicar un problema de enrutamiento o canal de transporte que requiera su atención.

Volver al principio

## Propiedades del mensaje

Un mensaje en una cola tiene muchas propiedades. Muchas de las propiedades reflejan la información que se usó para crear el mensaje. Algunos estados de los mensajes y las propiedades de la información están fuertemente influenciados por las propiedades correspondientes en la cola. Sin embargo, un mensaje individual puede tener un valor diferente a la propiedad correspondiente de la cola. Otras propiedades contienen el estado, la hora y otras indicaciones que se actualizan frecuentemente.

Volver al principio

## Estado del mensaje

El estado actual de un mensaje se almacena en la propiedad **Status** del mensaje. Un mensaje puede tener uno de los siguientes estados:

  - **Activo** Si el mensaje está en una cola de entrega, se entregará a su destino. Si el mensaje está en la cola de envío, el categorizador lo está procesando.

  - **Bloqueado**   Este valor se reserva para uso interno de Microsoft y no se usa en las organizaciones de Exchange locales.

  - **Eliminación pendiente**   El administrador eliminó el mensaje, pero el mensaje ya se estaba transmitiendo al siguiente salto. Si la entrega finaliza con un error que provoca que el mensaje vuelva a entrar en la cola, éste se eliminará. De lo contrario, se proseguirá con la entrega.

  - **Suspender pendientes**   El administrador suspendió el mensaje, pero el mensaje ya se estaba transmitiendo al siguiente salto. Si la entrega finaliza con un error que provoca que el mensaje vuelva a entrar en la cola, éste se suspenderá. De lo contrario, se proseguirá con la entrega.

  - **Ready**   El mensaje está aguardando en la cola y está listo para su procesamiento.

  - **Reintentar**   El último intento de conexión automática o manual por parte de la cola donde se ubica el mensaje fue erróneo. El mensaje está esperando el siguiente reintento de conexión automática de la cola.

  - **Suspendido**   El administrador ha suspendido el mensaje manualmente. Todos los mensajes de la cola de mensajes dudosos se encuentran en un estado permanentemente suspendido.

Volver al principio

## Otras propiedades del mensaje

Hay otras propiedades del mensaje que se explican por sí mismas. La mayoría de las propiedades del mensaje se pueden usar como opciones de filtro. Mediante la especificación de criterios de filtro, es posible buscar los mensajes y realizar acciones en ellos. Para una descripción completa de las propiedades filtrables del mensaje, vea [Filtros de mensajes](message-filters-exchange-2013-help.md).

Volver al principio

## Administración de colas y mensajes en las colas

El Visor de cola y prácticamente todos los cmdlets de administración de mensajes y colas se restringen a un solo servidor de Exchange. Puede ver o trabajar en colas o mensajes individuales o en varias colas y mensajes, pero en un servidor específico.

Exchange 2013 presenta el cmdlet **Get-QueueDigest** que proporciona una vista agregada de alto nivel del estado de las colas en todos los servidores dentro de un ámbito concreto, por ejemplo, un DAG, un sitio de Active Directory, una lista de servidores o todo un bosque de Active Directory. Observe que las colas de un servidor de transporte perimetral suscrito en una red perimetral no aparecen entre los resultados. De igual modo, **Get-QueueDigest** está disponible en un servidor de transporte perimetral, pero los resultados se acotan a las colas en el servidor de transporte perimetral.


> [!NOTE]
> De forma predeterminada, el cmdlet <STRONG>Get-QueueDigest</STRONG> muestra las colas de entrega que contienen diez o más mensajes y los resultados que tienen entre uno y dos minutos de antigüedad. Si quiere ver las instrucciones para cambiar estos valores predeterminados, consulte <A href="configure-get-queuedigest-exchange-2013-help.md">Configurar Get-QueueDigest</A>.



En la siguiente tabla se describen las tareas de administración que puede realizar en las colas o en los mensajes de las colas.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tarea</th>
<th>Descripción</th>
<th>Herramienta para usar</th>
<th>Instrucciones</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Ver y filtrar colas en un servidor</p></td>
<td><p>Esta acción muestra una o varias colas en un servidor de transporte. Puede usar los resultados para realizar acciones en las colas.</p></td>
<td><p>Visor de cola o el cmdlet <strong>Get-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Administración de colas</a></p></td>
</tr>
<tr class="even">
<td><p>Ver y filtrar colas en servidores específicos en DAG, sitios de Active Directory específicos o en todo el bosque de Active Directory.</p></td>
<td><p>Esta acción muestra una vista resumen de las colas a través de un ámbito definido (servidores, DAG, sitios de Active Directory o todo el bosque de Active Directory).</p></td>
<td><p>Solo el cmdlet <strong>Get-QueueDigest</strong></p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Administración de colas</a></p></td>
</tr>
<tr class="odd">
<td><p>Suspender colas</p></td>
<td><p>Esta acción previene temporalmente la entrega de mensajes que se encuentran actualmente en la cola. La cola continúa aceptando nuevos mensajes, pero éstos no abandonan la cola.</p></td>
<td><p>Visor de cola o el cmdlet <strong>Suspend-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Administración de colas</a></p></td>
</tr>
<tr class="even">
<td><p>Reanudar colas</p></td>
<td><p>Esta acción invierte el efecto de la acción suspender cola y permite la reanudación de la entrega de mensajes en cola.</p></td>
<td><p>Visor de cola o el cmdlet <strong>Resume-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Administración de colas</a></p></td>
</tr>
<tr class="odd">
<td><p>Reintentar colas</p></td>
<td><p>Esta acción intenta conectarse inmediatamente al próximo salto. Sin intervención manual, cuando la conexión al siguiente salto no se realiza correctamente, la conexión se intenta un número específico de veces después de un intervalo específico de tiempo entre cada intento.</p>
<p>Independientemente de que el intento de conexión sea manual o automática, cualquier intento de conexión restablece la siguiente hora de reintento. Para obtener más información, vea <a href="message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md">Intervalos de reintento, reenvío y expiración de mensajes</a>.</p></td>
<td><p>Visor de cola o el cmdlet <strong>Retry-Queue</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Administración de colas</a></p></td>
</tr>
<tr class="even">
<td><p>Volver a enviar mensajes en colas</p></td>
<td><p>Esta acción hace que los mensajes de la cola se reenvíen a la cola de envío y vuelvan a través del proceso de categorización.</p></td>
<td><p><strong>Retry-Queue</strong> con el parámetro <em>Resubmit</em></p>
<p>Tenga en cuenta que puede usar el Visor de cola para reenviar mensajes, pero solo desde la cola de mensajes dudosos. Para reenviar un mensaje en un mensaje dudoso, puede reanudar el mensaje en el Visor de cola o usar el cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-queues-exchange-2013-help.md">Administración de colas</a></p></td>
</tr>
<tr class="odd">
<td><p>Suspender mensajes en colas</p></td>
<td><p>Esta acción impide temporalmente la entrega de un mensaje. Puede usar la acción de suspensión de mensajes para prevenir la entrega de mensajes a todos los destinatarios de una cola específica o a todos los destinatarios de todas las colas.</p></td>
<td><p>Visor de cola o cmdlet <strong>Suspend-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Administrar mensajes en colas</a></p></td>
</tr>
<tr class="even">
<td><p>Reanudar los mensajes en colas</p></td>
<td><p>Esta acción invierte el efecto de la acción suspender mensaje y permite la reanudación de la entrega de mensajes en cola. Puede usar la acción de reanudación de mensajes para reanudar la entrega de mensajes a todos los destinatarios de una cola específica o a todos los destinatarios de todas las colas.</p></td>
<td><p>Visor de cola o el cmdlet <strong>Resume-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Administrar mensajes en colas</a></p></td>
</tr>
<tr class="odd">
<td><p>Quitar mensajes de las colas</p></td>
<td><p>Esta acción impide permanentemente la entrega de mensajes. Puede usar la acción de eliminación de mensajes para prevenir la entrega de mensajes a todos los destinatarios de una cola específica o a todos los destinatarios de todas las colas. Puede también configurar la acción de eliminación de mensajes para enviar un informe de no entrega (NDR) al remitente cuando se elimina el mensaje.</p></td>
<td><p>Visor de cola o el cmdlet <strong>Remove-Message</strong>.</p></td>
<td><p><a href="manage-messages-in-queues-exchange-2013-help.md">Administrar mensajes en colas</a></p></td>
</tr>
<tr class="even">
<td><p>Exportar mensajes de las colas</p></td>
<td><p>Esta acción copia un mensaje a la ruta de archivo que especifique. Los mensajes no se borran de la cola, pero se guarda una copia de los mismos en una ubicación del archivo. Esto permite a los administradores u oficiales en una organización examinar más tarde los mensajes. Antes de exportar un mensaje, debe suspender el mensaje en la cola de modo que la entrega habitual no continúe durante el proceso de exportación.</p></td>
<td><p>Solo el cmdlet <strong>Export-Message</strong>.</p></td>
<td><p><a href="export-messages-from-queues-exchange-2013-help.md">Exportar mensajes de las colas</a></p></td>
</tr>
</tbody>
</table>


Volver al principio

