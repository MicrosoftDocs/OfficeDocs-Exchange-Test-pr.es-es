---
title: 'Uso del Shell de administración de Exchange para administrar colas: Exchange 2013 Help'
TOCTitle: Uso del Shell de administración de Exchange para administrar colas
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 51406517
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Uso del Shell de administración de Exchange para administrar colas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Como en versiones anteriores de Exchange, puede usar el Shell de administración de Exchange en Microsoft Exchange Server 2013 para ver información sobre colas y mensajes en dichas colas, así como para realizar acciones administrativas en ellas. En Exchange 2013, hay colas en los servidores de buzones de correo y en los servidores de transporte perimetral. Este tema hace referencia a estos servidores como *servidores de transporte*.

Cuando utilice el Shell para ver y administrar colas y mensajes en cola en servidores de transporte, es importante entender cómo identificar las colas o los mensajes que quiere administrar. Generalmente, los servidores de transporte contienen una gran cantidad de colas y mensajes por entregar. Puede usar los parámetros de filtrado que están disponibles en los cmdlets de administración de colas y mensajes para identificar las colas y los mensajes que quiere ver o administrar.

Observe que también puede usar el Visor de cola en Exchange Toolbox para administrar colas y mensajes en cola. Sin embargo, los cmdlets para ver colas y mensajes admiten más propiedades y opciones de filtrado que el Visor de cola. Para obtener más información acerca del uso del Visor de cola, vea [Visor de cola](queue-viewer-exchange-2013-help.md).

**Contenido**

  - Queue filtering parameters
    
      - Queue identity
    
      - Queue Filter parameter
    
      - Include and Exclude parameters

  - Get-QueueDigest

  - Message filtering parameters
    
      - Message identity
    
      - Message Filter parameter
    
      - Queue parameter

  - Comparison operators to use when filtering queues or messages

  - Advanced paging parameters

## Parámetros de filtrado de la cola

La siguiente tabla describe los parámetros de filtrado que están disponibles en los cmdlets de administración de cola.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parámetros de filtrado</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Include</em></p>
<p><em>Exclude</em></p></td>
<td><p>No puede usar el parámetro <em>Identity</em> en el mismo comando que los parámetros <em>Filter</em>. Puede usar los parámetros <em>Include</em> y <em>Exclude</em> con el parámetro <em>Filter</em> en el mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><strong>Resume-Queue</strong></p>
<p><strong>Retry-Queue</strong></p>
<p><strong>Suspend-Queue</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>Debe usar el parámetro <em>Identity</em> o bien <em>Filter</em>, pero no puede usarlos ambos en el mismo comando.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get-QueueDigest</strong></p></td>
<td><p><em>Server</em></p>
<p><em>Dag</em></p>
<p><em>Site</em></p>
<p><em>Forest</em></p>
<p><em>Filter</em></p></td>
<td><p>Debe usar el parámetro <em>Server</em>, <em>Dag</em>, <em>Site</em> o <em>Forest</em>, pero no puede combinar ninguno de ellos en el mismo comando. Puede usar el parámetro <em>Filter</em> con cualquier otro parámetro de filtrado.</p></td>
</tr>
</tbody>
</table>


Observe que todos los cmdlets de administración de cola disponen de un parámetro *Server*. En el cmdlet **Get-QueueDigest**, el parámetro *Server* es un parámetro de ámbito que especifica los servidores en los que quiere ver información resumida sobre las consultas. En el resto de los cmdlets de administración de cola, debe usar el parámetro *Server* para conectarse a un servidor específico y ejecutar los comandos de administración de cola en dicho servidor. Puede usar el parámetro *Server* con el parámetro *Filter* o sin él, pero no puede usar el parámetro *Server* con el parámetro *Identity*. Debe usar el nombre de host o FQDN del servidor de transporte con el parámetro *Server*.

Volver al principio

## Identidad de colas

El parámetro *Identity* en los cmdlets de administración de cola identifica una cola determinada. Cuando utiliza el parámetro *Identity*, no puede especificar ningún otro parámetro de filtrado de cola porque ya ha identificado de forma única la cola. El parámetro *Identity* usa la sintaxis básica *\<Servidor\>*\\*\<Cola\>*.

El marcador de posición *\<Servidor\>* es el nombre de host o FQDN del servidor Exchange, por ejemplo `mailbox01` o `mailbox01.contoso.com`. Si omite el calificador *\<Servidor\>*, se utilizará el servidor local.

El marcador de posición \<*Cola*\> acepta uno de los siguientes valores:

  - **Nombre de cola persistente**   Las colas persistentes tienen nombres únicos y consistentes en todos los servidores de buzones de correo o de transporte perimetral. Los nombres de cola persistente son:
    
      - **Envío**   Esta cola contiene mensajes que esperan ser procesados por el categorizador.
    
      - **Inaccesible**   Esta cola contiene mensajes que no pueden enrutarse. Esta cola no existe hasta que los mensajes se colocan en ella.
    
      - **Mensaje dudoso**   Esta cola contiene mensajes que se han determinado como perjudiciales para el servidor Exchange. Esta cola no existe hasta que los mensajes se colocan en ella.

  - **Nombre de cola de entrega**   El nombre de una cola de entrega es el valor de la propiedad **NextHopDomain** de la cola. Por ejemplo, el nombre de la cola podría ser el espacio de direcciones de un conector de envío, el nombre de un sitio de Active Directory o el nombre de un DAG. Para obtener más información consulte la sección "NextHopSolutionKey" en el tema [Colas](queues-exchange-2013-help.md).

  - **Entero de cola**   A las colas de entrega y las colas duplicadas se les asigna un valor entero único en la base de datos de colas. Sin embargo, debe ejecutar el cmdlet **Get-Queue** para encontrar el valor entero de la cola en las propiedades **Identity** o **QueueIdentity**.

  - **Nombre de cola de duplicados** Una cola de duplicados utiliza la sintaxis `Shadow\`*\<QueueInteger\>*

La siguiente tabla resume la sintaxis que puede usar con el parámetro *Identity* en los cmdlets de administración de cola. En todos los valores, *\<Servidor\>* es el nombre de host o el FQDN del servidor.

### Formatos de identidad de cola

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor de parámetro de identidad</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;PersistentQueueName&gt;</code> o <code>&lt;PersistentQueueName&gt;</code></p></td>
<td><p>Una cola persistente en el servidor especificado o en el servidor local.</p>
<p><em>&lt;PersistentQueueName&gt;</em> es <code>Submission</code>, <code>Unreachable</code> o <code>Poison</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\&lt;NextHopDomain&gt;</code> o <code>&lt;NextHopDomain&gt;</code></p></td>
<td><p>Una cola de entrega en el servidor especificado o en el servidor local.</p>
<p><em>&lt;NextHopDomain&gt;</em> es un destino de enrutamiento o un grupo de entrega para los mensajes en cola. Para obtener más información consulte la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;QueueInteger&gt;</code> o <code>&lt;QueueInteger&gt;</code></p></td>
<td><p>Una cola de entrega en el servidor especificado o en el servidor local.</p>
<p><em>&lt;QueueInteger&gt;</em> es el valor entero único de la cola que se muestra en la propiedad <strong>Identity</strong> del cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\Shadow\&lt;QueueInteger&gt;</code> o <code>Shadow\&lt;QueueInteger&gt;</code></p></td>
<td><p>Una cola de duplicados en el servidor especificado o en el servidor local.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;Server&gt;\*</code> o <code>*</code></p></td>
<td><p>Todas las colas en el servidor especificado o en el servidor local. Observe que estos valores sólo pueden usarse con el cmdlet <strong>Get-Queue</strong>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Parámetro Filter de colas

Puede usar el parámetro *Filter* en todos los cmdlets de administración de cola para especificar las colas que quiere ver o administrar en función de sus propiedades. El parámetro *Filter* crea una expresión con operadores de comparación que restringe la operación de la cola a colas que cumplen con los criterios de filtrado. Se puede utilizar el operador lógico `-and` para especificar varias condiciones que los resultandos deben cumplir.

Para obtener una lista completa de las propiedades de la cola que puede usar con el parámetro *Filter*, vea [Colas](queues-exchange-2013-help.md).

Para obtener una lista de operadores de comparación que puede usar con el parámetro *Filter*, vea la sección Comparison operators to use when filtering queues or messages en este tema.

Para ver ejemplos de procedimientos que usan el parámetro *Filter* para ver y administrar colas, vea [Administración de colas](manage-queues-exchange-2013-help.md).

Volver al principio

## Parámetros Include y Exclude

Exchange 2013 dispone de los parámetros *Include* y *Exclude* en el cmdlet `Get-Queue`. Puede usar estos parámetros por separado, juntos, y con el parámetro *Filter* para acotar los resultados de búsqueda en el servidor de transporte local o especificado. Por ejemplo, puede:

  - Excluir las colas vacías de los resultados.

  - Excluir las colas a destinos externos de los resultados.

  - Incluir colas que tengan un determinado valor de **DeliveryType** en los resultados.

Los parámetros *Include* y *Exclude* usan las siguientes propiedades de cola para filtrar colas:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Descripción</th>
<th>Ejemplo de código de Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>DeliveryType</code></p></td>
<td><p>Este valor incluye o excluye colas en función de la propiedad <strong>DeliveryType</strong>. Puede especificar distintos valores separados por comas. Los valores válidos para <strong>DeliveryType</strong> se explican en la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
<td><p>En este ejemplo se devuelven todas las colas de entrega en el servidor local donde el próximo salto es un conector de envío en el servidor local que está configurado para un enrutamiento inteligente de hosts.</p>
<p><code>Get-Queue -Include SmartHostConnectorDelivery</code></p></td>
</tr>
<tr class="even">
<td><p><code>Empty</code></p></td>
<td><p>Este valor incluye o excluye colas vacías. Las colas vacías tienen el valor <code>0</code> en la propiedad <strong>MessageCount</strong>.</p></td>
<td><p>En este ejemplo se devuelven todas las colas en el servidor local que contienen mensajes</p>
<p><code>Get-Queue -Exclude Empty</code></p></td>
</tr>
<tr class="odd">
<td><p><code>External</code></p></td>
<td><p>Este valor incluye o excluye colas que tienen el valor <code>External</code> en la propiedad <strong>NextHopCategory</strong>.</p>
<p>Las colas externas siempre presentan uno de los siguientes valores para <strong>DeliveryType</strong>:</p>
<ul>
<li><p><code>DeliveryAgent</code></p></li>
<li><p><code>DnsConnectorDelivery</code></p></li>
<li><p><code>NonSmtpGatewayDelivery</code></p></li>
<li><p><code>SmartHostConnectorDelivery</code></p></li>
</ul>
<p>Para obtener más información consulte la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
<td><p>En este ejemplo se devuelven todas las colas internas en el servidor local</p>
<p><code>Get-Queue -Exclude External</code></p></td>
</tr>
<tr class="even">
<td><p><code>Internal</code></p></td>
<td><p>Este valor incluye o excluye colas que tienen el valor <code>Internal</code> en la propiedad <strong>NextHopCategory</strong>. Para obtener más información consulte la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></td>
<td><p>En este ejemplo se devuelven todas las colas internas en el servidor local.</p>
<p><code>Get-Queue -Include Internal</code></p></td>
</tr>
</tbody>
</table>


Observe que puede duplicar la funcionalidad de los parámetros *Include* y *Exclude* utilizando el parámetro *Filter*. Por ejemplo, el comando `Get-Queue -Exclude Empty` produce el mismo resultado que `Get-Queue -Filter {MessageCount -gt 0}`. Sin embargo, la sintaxis de los parámetros *Include* y *Exclude* es más simple y fácil de recordar.

Volver al principio

## Get-QueueDigest

Exchange 2013 agrega un nuevo cmdlet de cola denominado **Get-QueueDigest**. Este cmdlet le permite ver información acerca de algunas de las colas de su organización de Exchange, o de todas ellas, usando un único comando. Concretamente, el cmdlet **Get-QueueDigest** le permite ver información sobre colas basándose en su ubicación en los servidores, en DAG, en sitios de Active Directory o en todo el bosque de Active Directory. Observe que las colas de un servidor de transporte perimetral suscrito en una red perimetral no aparecen entre los resultados. De igual modo, **Get-QueueDigest** está disponible en un servidor de transporte perimetral, pero los resultados se acotan a las colas en el servidor de transporte perimetral.


> [!NOTE]
> De forma predeterminada, el cmdlet <STRONG>Get-QueueDigest</STRONG> muestra las colas de entrega que contienen diez o más mensajes y los resultados que tienen entre uno y dos minutos de antigüedad. Si quiere ver las instrucciones para cambiar estos valores predeterminados, consulte <A href="configure-get-queuedigest-exchange-2013-help.md">Configurar Get-QueueDigest</A>.



Los parámetros de filtrado y ordenación disponibles con el cmdlet **Get-QueueDigest** se describen en la tabla siguiente.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>Dag</em>, <em>Server</em> o <em>Site</em></p></td>
<td><p>Estos parámetros son mutuamente excluyentes y establecen el ámbito del cmdlet. Necesita especificar uno de estos parámetros en el modificador <em>Forest</em>. Generalmente, usará el nombre del servidor, el DAG o el sitio de Active Directory, pero puede usar cualquier valor que identifique de forma única el servidor, el DAG o el sitio. Puede especificar varios servidores, DAG o sitios separados por comas.</p></td>
</tr>
<tr class="even">
<td><p><em>Forest</em></p></td>
<td><p>Este modificador es necesario si no utiliza los parámetros <em>Dag</em>, <em>Server</em> o <em>Site</em>. No se especifica un valor con este modificador. Usando este modificador, obtiene colas de todos los servidores de buzones de correo Exchange 2013 en el bosque de Active Directory. No puede utilizar el modificador <em>Forest</em> para ver colas en los bosques remotos de Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><em>DetailsLevel</em></p></td>
<td><p>Este parámetro acepta los valores <code>None</code>, <code>Normal</code> y <code>Verbose</code>. El valor predeterminado es <code>Normal</code>. Cuando utiliza el valor <code>None</code>, el nombre de la cola se omite de la columna <strong>Detalles</strong> en los resultados.</p></td>
</tr>
<tr class="even">
<td><p><em>Filter</em></p></td>
<td><p>Este parámetro le permite filtrar las colas en función de sus propiedades. Puede utilizar cualquiera de las propiedades filtrables de la cola tal como se describe en el tema <a href="queue-filters-exchange-2013-help.md">Filtros de cola</a>.</p></td>
</tr>
<tr class="odd">
<td><p><em>GroupBy</em></p></td>
<td><p>Este parámetro agrupa los resultados de la cola. Se pueden agrupar los resultados por una de las siguientes propiedades:</p>
<ul>
<li><p>DeliveryType</p></li>
<li><p>LastError</p></li>
<li><p>NextHopCategory</p></li>
<li><p>NextHopDomain</p></li>
<li><p>NextHopKey</p></li>
<li><p>Status</p></li>
<li><p>ServerName</p></li>
</ul>
<p>De forma predeterminada, los resultados se agrupan por <code>NextHopDomain</code>. Para obtener información acerca de estas propiedades de colas, vea <a href="queue-filters-exchange-2013-help.md">Filtros de cola</a>.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Este parámetro limita los resultados de la cola hasta el valor que especifique. Las colas se ordenan por orden descendente basándose en el número de mensajes en cola, y se agrupan por el valor especificado por el parámetro <em>GroupBy</em>. El valor predeterminado es 1.000. Esto significa que, de forma predeterminada, el comando muestra las primeras 1.000 colas agrupadas por <strong>NextHopDomain</strong> y las ordena de las colas que contienen más mensajes a las que contienen menos.</p></td>
</tr>
<tr class="odd">
<td><p><em>Timeout</em></p></td>
<td><p>El parámetro especifica el número de segundos antes de que la operación agota el tiempo de espera. El valor predeterminado es <code>00:00:10</code> o 10 segundos.</p></td>
</tr>
</tbody>
</table>


En este ejemplo se devuelven todas las colas externas que no estén vacías en los servidores de buzones de correo Exchange 2013 denominados Mailbox01, Mailbox02 y Mailbox03.

    Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty

Volver al principio

## Parámetros de filtrado de mensajes

La siguiente tabla describe los parámetros de filtrado que están disponibles en los cmdlets de administración de mensajes.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cmdlet</th>
<th>Parámetros de filtrado</th>
<th>Comentarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Get-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p>
<p><em>Queue</em></p></td>
<td><p>Todos los parámetros de filtrado son mutuamente excluyentes y puede usarlos juntos en el mismo comando.</p></td>
</tr>
<tr class="even">
<td><p><strong>Remove-Message</strong></p>
<p><strong>Resume-Message</strong></p>
<p><strong>Suspend-Message</strong></p></td>
<td><p><em>Identity</em></p>
<p><em>Filter</em></p></td>
<td><p>Debe usar el parámetro <em>Identity</em> o bien <em>Filter</em>, pero no puede usarlos ambos en el mismo comando.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Export-Message</strong></p></td>
<td><p><em>Identity</em></p></td>
<td><p>El parámetro <em>Identity</em> es obligatorio.</p></td>
</tr>
</tbody>
</table>


Observe que dispone de un parámetro *Server* en todos los cmdlets de administración de mensajes, excepto en el cmdlet **Export-Message**. Puede utilizar el parámetro *Server* para conectarse a un servidor específico y ejecutar los comandos de administración de mensajes en dicho servidor. Puede usar el parámetro *Server* con el parámetro *Filter* o sin él, pero no puede usar el parámetro *Server* con el parámetro *Identity*. Debe usar el nombre de host o FQDN del servidor de transporte con el parámetro *Server*.

Volver al principio

## Identidad de mensaje

El parámetro *Identity* en los cmdlets de administración de mensaje identifica un mensaje específico en una o más colas. Cuando utiliza el parámetro *Identity*, no puede especificar ningún otro parámetro de filtrado de mensajes porque ya ha identificado de forma única el mensaje. El parámetro *Identity* usa la sintaxis básica *\<Servidor\>*\\*\<Cola\>*\\*\<MessageInteger\>*.

El marcador de posición *\<Servidor\>* es el nombre de host o FQDN del servidor Exchange, por ejemplo `mailbox01` o `mailbox01.contoso.com`. Si omite el calificador *\<Servidor\>*, se utilizará el servidor local.

El marcador de posición \<*Cola*\> acepta la identidad de la cola tal como se describe en la sección "Identidad de cola" en este tema. Por ejemplo, puede utilizar el nombre de cola persistente, el valor **NextHopDomain** o el valor entero único de la cola en la base de datos de colas.

El marcador de posición *\<MessageInteger\>* representa el valor entero único que está asignado al mensaje cuando entra por primera vez en la base de datos de colas del servidor. Si el mensaje se envía a varios destinatarios que requieren varias colas, todas las copias del mensaje en todas las colas de la base de datos de colas tendrán el mismo valor entero. Sin embargo, debe ejecutar el cmdlet **Get-Message** para encontrar el valor entero del mensaje en las propiedades **Identity** o **MessageIdentity**.

La siguiente tabla resume la sintaxis que puede usar con el parámetro *Identity* en los cmdlets de administración de mensajes. En todos los valores, *\<Server\>* es el nombre de host o el FQDN del servidor.

### Formatos de identidad de mensaje

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor de parámetro de identidad</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;Server&gt;\&lt;Queue&gt;\&lt;MessageInteger&gt;</code> o <code>&lt;Queue&gt;\&lt;MessageInteger&gt;</code></p></td>
<td><p>Un mensaje en una cola determinada en un servidor determinado o en el servidor local.</p>
<p><em>&lt;MessageInteger&gt;</em> es el valor entero único de la cola que se muestra en la propiedad <strong>Identity</strong> del cmdlet <strong>Get-Message</strong>.</p>
<p><em>&lt;Queue&gt;</em> representa uno de los siguientes valores:</p>
<ul>
<li><p><strong>Nombre de cola persistente</strong>   El valor <code>Submission</code>, <code>Unreachable</code> o <code>Poison</code>.</p></li>
<li><p><strong>Nombre de cola de entrega</strong>   El valor de la propiedad <strong>NextHopDomain</strong> de la cola, que es efectivamente el nombre de la cola. Este valor podría ser un destino de enrutamiento o un grupo de entrega. Para obtener más información, vea la sección &quot;NextHopSolutionKey&quot; en el tema <a href="queues-exchange-2013-help.md">Colas</a>.</p></li>
<li><p><strong>Entero de cola</strong>   El valor entero único de la cola de entrega o la cola de duplicados que se muestra en la propiedad <strong>Identity</strong> de los cmdlets <strong>Get-Message</strong> o <strong>Get-Queue</strong>.</p></li>
<li><p><strong>Identidad de cola de duplicados</strong>   La identidad de cola de duplicados utiliza la sintaxis <code>Shadow\&lt;QueueInteger&gt;</code>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>&lt;Server&gt;\*\&lt;MessageInteger&gt;</code> o <code>*\&lt;MessageInteger&gt;</code> o <code>&lt;MessageInteger&gt;</code></p></td>
<td><p>Todas las copias del mensaje en todas las colas en las base de datos de colas en el servidor especificado o en el servidor local.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Parámetro Filter de mensajes

Puede utilizar el parámetro *Filter* en los cmdlets **Get-Message**, **Remove-Message**, **Resume-Message** y **Suspend-Message** para especificar los mensajes que quiere ver o administrar en función de sus propiedades. El parámetro *Filter* crea una expresión con operadores de comparación que restringe la operación del mensaje a mensajes que cumplen con los criterios de filtrado. Se puede utilizar el operador lógico `-and` para especificar varias condiciones que los resultandos deben cumplir.

Para obtener una lista completa de las propiedades de mensajes que puede usar con el parámetro *Filter*, vea [Colas](queues-exchange-2013-help.md).

Para obtener una lista de operadores de comparación que puede usar con el parámetro *Filter*, vea la sección Comparison operators to use when filtering queues or messages en este tema.

Para ver ejemplos de procedimientos que usan el parámetro *Filter* para ver y administrar mensajes, vea [Administración de colas](manage-queues-exchange-2013-help.md).

Volver al principio

## Parámetro Queue

El parámetro *Queue* se utiliza sólo con el cmdlet **Get-Message**. Puede usar este parámetro para obtener todos los mensajes de una cola específica o todos los mensajes de varias colas usando el carácter comodín (\*). Al usar el parámetro *Queue*, debe emplear el formato de identidad de cola *\<Servidor\>*\\*\<Cola\>* tal como se describe en la sección "Identidad de cola" en este tema.

Volver al principio

## Operadores de comparación que puede utilizar al filtrar colas o mensajes

Cuando crea una expresión de filtrado de colas o mensajes usando el parámetro *Filter*, debe incluir un operador de comparación para el valor de propiedad coincidente. La tabla siguiente muestra los operadores de comparación que se pueden utilizar en una expresión de filtro y cómo funciona cada uno de ellos. Para todos los operadores, los valores comparados no distinguen mayúsculas de minúsculas.

### Operadores de comparación

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Operador</th>
<th>Función</th>
<th>Ejemplo de código de Shell</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>-eq</code></p></td>
<td><p>Este operador se usa para especificar que el resultado debe coincidir exactamente con el valor de la propiedad que se suministra en la expresión.</p></td>
<td><p>Para mostrar una lista de todas las colas cuyo estado es Retry:</p>
<p><code>Get-Queue -Filter {Status -eq &quot;Retry&quot;}</code></p>
<p>Para mostrar una lista de todos los mensajes cuyo estado es Retry:</p>
<p><code>Get-Message -Filter {Status -eq &quot;Retry&quot;}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ne</code></p></td>
<td><p>Este operador se utiliza para especificar que el resultado no debe coincidir exactamente con el valor de la propiedad que se suministra en la expresión.</p></td>
<td><p>Para mostrar una lista de todas las colas cuyo estado no es Active:</p>
<p><code>Get-Queue -Filter {Status -ne &quot;Active&quot;}</code></p>
<p>Para mostrar una lista de todos los mensajes cuyo estado no es Active:</p>
<p><code>Get-Message -Filter {Status -ne &quot;Active&quot;}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-gt</code></p></td>
<td><p>Este operador se utiliza con las propiedades cuyo valor se expresa como un entero o en formato fecha/hora. Los resultados del filtro sólo incluyen colas o mensajes en los que el valor de la propiedad especificada es mayor que el que se suministra en la expresión.</p></td>
<td><p>Para mostrar una lista de colas que actualmente contiene más de mil mensajes:</p>
<p><code>Get-Queue -Filter {MessageCount -gt 1000}</code></p>
<p>Para mostrar una lista de los mensajes cuyo número de reintentos es actualmente superior a 3:</p>
<p><code>Get-Message -Filter {RetryCount -gt 3}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-ge</code></p></td>
<td><p>Este operador se utiliza con las propiedades cuyo valor se expresa como un entero o en formato fecha/hora. Los resultados del filtro sólo incluyen colas o mensajes en los que el valor de la propiedad especificada es mayor o igual que el que se suministra en la expresión.</p></td>
<td><p>Para mostrar una lista de colas que actualmente contiene mil mensajes, o más:</p>
<p><code>Get-Queue -Filter {MessageCount -ge 1000}</code></p>
<p>Para mostrar una lista de los mensajes cuyo número de reintentos es actualmente superior o igual a 3:</p>
<p><code>Get-Message -Filter {RetryCount -ge 3}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-lt</code></p></td>
<td><p>Este operador se utiliza con las propiedades cuyo valor se expresa como un entero o en formato fecha/hora. Los resultados del filtro sólo incluyen colas o mensajes en los que el valor de la propiedad especificada es menor que el que se suministra en la expresión.</p></td>
<td><p>Para mostrar una lista de colas que actualmente contiene menos de mil mensajes:</p>
<p><code>Get-Queue -Filter {MessageCount -lt 1000}</code></p>
<p>Para mostrar una lista de los mensajes cuyo SCL es inferior a 6:</p>
<p><code>Get-Message -Filter {SCL -lt 6}</code></p></td>
</tr>
<tr class="even">
<td><p><code>-le</code></p></td>
<td><p>Este operador se utiliza con las propiedades cuyo valor se expresa como un entero o en formato fecha/hora. Los resultados del filtro sólo incluyen las colas o mensajes en los que el valor de la propiedad especificada es menor o igual que el que se suministra en la expresión.</p></td>
<td><p>Para mostrar una lista de colas que actualmente contiene mil mensajes o menos:</p>
<p><code>Get-Queue -Filter {MessageCount -le 1000}</code></p>
<p>Para mostrar una lista de los mensajes cuyo SCL es inferior o igual a 6:</p>
<p><code>Get-Message -Filter {SCL -le 6}</code></p></td>
</tr>
<tr class="odd">
<td><p><code>-like</code></p></td>
<td><p>Este operador se utiliza con las propiedades en las que el valor se expresa en forma de cadena de texto. Los resultados del filtro sólo incluyen las colas o mensajes en los que el valor de la propiedad especificada contiene la cadena de texto que se suministra en la expresión. El carácter comodín (*) se puede incluir en una expresión <strong>-like</strong> que se aplique a un campo de cadenas de texto, pero no a un campo que tenga el tipo enumeración.</p></td>
<td><p>Para mostrar una lista de colas de entrega que tienen un destino en cualquier dominio SMTP que termine en Contoso.com:</p>
<p><code>Get-Queue -Filter {Identity -like &quot;*contoso.com&quot;}</code></p>
<p>Para mostrar una lista de los mensajes cuyo asunto contiene el texto &quot;préstamo de día de paga&quot;:</p>
<p><code>Get-Messages -Filter {Subject -like &quot;*payday loan*&quot;}</code></p></td>
</tr>
</tbody>
</table>


Puede especificar un filtro que evalúe varias expresiones usando el operador de comparación **-and**. Las colas o mensajes deben cumplir con todas las condiciones del filtro para que aparezcan en los resultados.

En este ejemplo se muestra una lista de las colas que tienen como destino cualquier nombre de dominio SMTP que termine en contoso.com y que actualmente contienen más de 500 mensajes.

    Get-Queue -Filter {Identity -like "*contoso.com*" -and MessageCount -gt 500}

En este ejemplo se muestra una lista de los mensajes que se envían desde cualquier dirección de correo en el dominio contoso.com que tienen un SCL mayor que 5.

    Get-Message -Filter {FromAddress -like "*Contoso.com*" -and SCL -gt 5}

Volver al principio

## Parámetros de paginación avanzados

En función del flujo de correo actual, las consultas a colas y mensajes pueden devolver un conjunto muy amplio de objetos. Puede usar los parámetros de paginación avanzados para controlar cómo se recuperan y muestran los resultados de una consulta.

Si usa el Shell para ver colas y los mensajes en esas colas, la consulta recuperará las páginas de información de a una por vez. Los parámetros de paginación avanzados controlan el tamaño del conjunto de resultados y también se pueden usar para ordenarlos. Los parámetros de paginación avanzados son opcionales y se pueden combinar con aquellos conjuntos de parámetros que se puedan usar con los cmdlets **Get-Queue** y **Get-Message**. Si no se especifican parámetros de paginación avanzados, la consulta devolverá los resultados en orden ascendente de identidad.

De forma predeterminada, si se especifica un criterio de ordenación, la propiedad de identidad de mensaje se incluye siempre y el orden es ascendente. Ésta es la relación de ordenación predeterminada. Se incluye la propiedad de identidad de mensaje porque el resto de las propiedades que se pueden incluir en un criterio de ordenación no son únicas. La inclusión explícita de la propiedad de identidad de mensaje en el criterio de ordenación permite especificar que los resultados muestren la identidad de mensaje en orden descendente.

Puede usar los parámetros *BookmarkIndex* y *BookmarkObject* para marcar una posición en el conjunto de resultados ordenados. Si el objeto de marcador ya no existe cuando se recupera la página de resultados siguiente, la relación de ordenación predeterminada se asegura de que el conjunto de resultados se inicie con el objeto más cercano al marcador. El objeto más cercano depende del criterio de ordenación especificado.

La tabla siguiente describe los parámetros de paginación avanzados.

### Parámetros de paginación avanzados

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parámetro</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>BookmarkIndex</em></p></td>
<td><p>Este parámetro especifica la posición en el conjunto de resultados donde se inician los resultados mostrados. El valor de este parámetro es un índice de base 1 en el conjunto de resultados totales. Si el valor es menor que cero o igual a cero, se devuelve la primera página completa de resultados. Si el valor está establecido en <code>Int.MaxValue</code>, se devuelve la última página completa de resultados.</p></td>
</tr>
<tr class="even">
<td><p><em>BookmarkObject</em></p></td>
<td><p>Este parámetro especifica el objeto en el conjunto de resultados donde se inician los resultados mostrados. Si se especifica un objeto de marcador, éste se usará como punto de inicio para la búsqueda. El valor del parámetro <em>SearchForward</em> determina si se recuperan las filas anteriores o posteriores al objeto. No se puede combinar el parámetro <em>BookmarkObject</em> y el parámetro <em>BookmarkIndex</em> en una sola consulta.</p></td>
</tr>
<tr class="odd">
<td><p><em>IncludeBookmark</em></p></td>
<td><p>Este parámetro especifica si se debe incluir el objeto de marcador en el conjunto de resultados. De forma predeterminada, el valor está establecido en <code>$true</code> y se incluye el objeto de marcador. Puede realizar una consulta para obtener un conjunto de resultados limitado y usar el último elemento de dicho conjunto como marcador para la consulta siguiente. En este caso, es posible que desee establecer <em>IncludeBookmark</em> en <code>$false</code> para que no se incluya al objeto en ambos conjuntos de resultados.</p></td>
</tr>
<tr class="even">
<td><p><em>ResultSize</em></p></td>
<td><p>Este parámetro especifica el número de resultados que se mostrarán por página. Si no se especifica un valor, se usará el tamaño de resultados predeterminado de 1000 objetos. Exchange limita el conjunto de resultados a 250.000.</p></td>
</tr>
<tr class="odd">
<td><p><em>ReturnPageInfo</em></p></td>
<td><p>Este parámetro es un parámetro oculto. Devuelve información acerca del número total de resultados y el índice del primer objeto de la página actual. El valor predeterminado es <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>SearchForward</em></p></td>
<td><p>El parámetro especifica si la búsqueda se realiza hacia adelante o hacia atrás en el conjunto de resultados. Este parámetro no afecta al orden en el que se devuelve el conjunto de resultados. Determina la dirección de búsqueda en relación con el índice de marcador o el objeto. Si no se especifica ningún objeto o índice, el parámetro <em>SearchForward</em> determina si la búsqueda se inicia desde el primero o el último de los objetos del conjunto de resultados.</p>
<p>El valor predeterminado para este parámetro es <code>$true</code>. Si este parámetro se establece en <code>$true</code> y se especifica un marcador, la consulta busca hacia adelante desde dicho marcador. Si usa esta configuración y no se obtienen resultados posteriores al marcador, la consulta devuelve la última página de resultados.</p>
<p>Si se establece el parámetro <em>SearchForward</em> en <code>$false</code> y se especifica un marcador, la consulta busca hacia atrás desde ese marcador. Si usa esta configuración y se obtiene menos de una página completa de resultados posterior al marcador, la consulta devuelve la primera página completa de resultados.</p></td>
</tr>
<tr class="odd">
<td><p><em>SortOrder</em></p></td>
<td><p>El parámetro especifica una matriz de propiedades de mensaje que se usa para controlar el criterio de ordenación del conjunto de resultados. Las propiedades del criterio de ordenación se especifican en orden descendente de precedencia. Las propiedades están separadas por comas y se anexa un signo más (+) para ordenar en orden ascendente, o un signo menos (-) para ordenar en orden descendente.</p>
<p>Si no se especifica un criterio de ordenación explícito con este parámetro, los registros que cumplan la consulta se mostrarán y ordenarán por el campo Identidad del tipo de objeto respectivo. Si no se especifica ningún criterio de ordenación, los resultados se ordenan siempre por identidad en orden ascendente.</p></td>
</tr>
</tbody>
</table>


En el ejemplo de código siguiente se muestra cómo usar los parámetros de paginación avanzados en una consulta. En este ejemplo, el comando se conecta al servidor especificado y recupera un conjunto de resultados que contiene 500 objetos. Los resultados se muestran en función de un criterio de ordenación: primero en orden ascendente por dirección de remitente y, a continuación, en orden ascendente por tamaño de mensaje.

`Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size`

Si desea ver las páginas siguientes, puede establecer un marcador para el último objeto recuperado en un conjunto de resultados y ejecutar una consulta adicional. Para este procedimiento, es necesario utilizar las funciones asociadas a los scripts del Shell.

El en ejemplo siguiente se usan scripts para recuperar la primera página de resultados, se establece el objeto de marcador, se excluye el objeto de marcador del conjunto de resultados y, por último, se recuperan del servidor especificado los 500 objetos siguientes.

1.  Abra el Shell y escriba el comando siguiente para recuperar la primera página de resultados.
    
        $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size

2.  Para establecer el objeto de marcador, escriba el comando siguiente para guardar el último elemento de la primera página en una variable.
    
        $temp=$results[$results.length-1]

3.  Para recuperar los 500 objetos siguientes del servidor especificado y excluir el objeto de marcador, escriba el comando siguiente.
    
        Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size

Volver al principio

