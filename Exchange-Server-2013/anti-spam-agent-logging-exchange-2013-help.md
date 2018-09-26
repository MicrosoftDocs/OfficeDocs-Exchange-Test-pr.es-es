---
title: 'Registro de agente contra correo no deseado: Exchange 2013 Help'
TOCTitle: Registro de agente contra correo no deseado
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 49895957
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registro de agente contra correo no deseado

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los registros de agente graban las acciones realizadas en un mensaje mediante agentes específicos contra correo electrónico no deseado en Microsoft Exchange Server 2013. Únicamente los siguientes agentes pueden escribir información en el registro de agente:

  - Agente de filtro de conexión

  - Agente de filtro de contenido

  - Agente de reglas perimetrales

  - Agente de filtro de destinatarios

  - Agente de filtro de remitentes

  - Agente de Id. de remitente


> [!NOTE]
> El agente de filtrado de conexiones y el agente de reglas perimetrales no están disponibles en los servidores Buzón de correo.



La información escrita en el registro de agentes depende del agente, del evento SMTP y de la acción realizada en el mensaje.

Puede usar el cmdlet **Set-TransportService** del Shell de administración de Exchange para realizar todas las tareas de configuración del registro de agente. Las siguientes opciones están disponibles para los registros de agente:

  - Habilitar o deshabilitar el registro de agente. El valor predeterminado es habilitado.

  - Especificar la ubicación de los archivos de registro de agente. El valor predeterminado es %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

  - Especificar un tamaño máximo para los archivos individuales de registro de agente. El tamaño predeterminado es 10 megabytes (MB).

  - Especificar un tamaño máximo para el directorio que contiene los archivos de registro de agente. El tamaño predeterminado es 250 MB.

  - Especificar la antigüedad máxima para los archivos de registro de agente. La antigüedad predeterminada es 7 días.

Exchange usa un registro circular para limitar los registros de agente en función del tamaño y la antigüedad del archivo para ayudar a controlar el espacio en disco duro utilizado por los archivos de registro.

**Contenido**

Overview of transport agents

Structure of the agent log files

Information written to the agent log

Search the agent logs

## Introducción a los agentes de transporte

Los agentes únicamente pueden actuar sobre los mensajes en puntos específicos de la secuencia de comandos SMTP que se usa para transportar los mensajes a través del servicio de transporte en un servidor de buzones de correo o un servidor de transporte perimetral. Estos puntos de acceso de la secuencia de comandos SMTP se denominan *Eventos SMTP*. Cada agente tiene un valor prioritario que puede asignarse. Sin embargo, los eventos SMTP siempre deben producirse en un orden determinado. Por lo tanto, la prioridad de agentes depende del evento SMTP. Si dos agentes pueden actuar en un mensaje durante el mismo evento SMTP, el agente que tiene mayor prioridad actuará sobre el mensaje en primer lugar.

En la siguiente tabla se enumeran los eventos SMTP en el orden en que suceden y los agentes que escriben la información en el registro de agentes en orden de prioridad (de mayor a menor) para cada evento SMTP.

### Eventos SMTP en el orden en que suceden y agentes que escriben la información en el registro de agentes en orden de prioridad para cada evento SMTP

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento SMTP</th>
<th>Agent</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>OnConnect</strong></p></td>
<td><p>Agente de filtro de conexión</p></td>
</tr>
<tr class="even">
<td><p><strong>OnMailCommand</strong></p></td>
<td><p>Agente de filtro de conexión</p>
<p>Agente de filtro de remitentes</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnRcptCommand</strong></p></td>
<td><p>Agente de filtro de conexión</p>
<p>Agente de filtro de destinatarios</p></td>
</tr>
<tr class="even">
<td><p><strong>OnEndOfHeaders</strong></p></td>
<td><p>Agente de filtro de conexión</p>
<p>Agente de Id. de remitente</p>
<p>Agente de filtro de remitentes</p></td>
</tr>
<tr class="odd">
<td><p><strong>OnEndOfData</strong></p></td>
<td><p>Agente de reglas perimetrales</p>
<p>Agente de filtrado de contenido</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> El agente de filtrado de conexiones y el agente de reglas perimetrales no están disponibles en los servidores Buzón de correo.



Para obtener más información sobre los agentes, eventos SMTP y la prioridad de agentes, consulte [Agentes de transporte](transport-agents-exchange-2013-help.md).

Volver al principio

## Estructura de los archivos de registro de agente

Los registros de agente existen en %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

La convención de la nomenclatura para los archivos de registro de agentes es AGENTLOG*yyyymmdd-nnnn*.log. Los marcadores de posición representan la siguiente información:

  - El marcador de posición *aaaammdd* es la hora UTC (hora universal coordinada) en que se ha creado el archivo de registro. Marcador *aaaa* = año, *mm* = mes y *dd* = día.

  - El marcador de posición *nnnn* es un número de instancia que empieza por el valor 1 para cada día.

La información se escribe en el archivo de registro hasta que el tamaño del archivo alcanza su valor máximo especificado y se abre un nuevo archivo de registro que tiene un número de instancia mayor. Este proceso se repite durante el día. El registro circular elimina los archivos de registro más antiguos cuando el directorio de registro de agente alcanza el tamaño máximo especificado o cuando un archivo de registro alcanza la antigüedad máxima especificada.

Los archivos de registro de agentes son archivos de texto que contienen datos en el formato de archivo de valores separados por comas (CSV). Cada archivo de registro de agentes tiene un encabezado que contiene la siguiente información:

  - **\#Software:**    Nombre del software que crea el archivo de registro de agentes. Normalmente, el valor es Microsoft Exchange Server.

  - **\#Version:**    Número de versión del software que crea el archivo de registro de agentes. Actualmente, el valor es 15.0.0.0.

  - **\#Log-Type:**    Valor de tipo de registro, que es el registro de agentes.

  - **\#Date**   La fecha y hora UTC en el momento de crearse el archivo. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, donde *yyyy* = año, *mm* = mes, *dd* = día, T indica el comienzo del componente tiempo, *hh* = hora, *mm* = minuto, *ss* = segundo, *fff* = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.

  - **\#Fields:**    Nombres de campos delimitados por comas que se usan en los archivos de registro de agentes.

Volver al principio

## Información escrita en el registro de agente

El registro de agentes almacena cada transacción de agentes en una sola línea del registro. La información almacenada en cada línea se organiza por campos. Estos campos se separan con comas. El nombre del campo suele ser lo bastante descriptivo como para determinar el tipo de información que contiene. Sin embargo, algunos campos permanecen en blanco. O el tipo de información almacenada en el campo puede cambiar en función del agente o de la acción que el agente realiza en el mensaje. En la siguiente tabla se describen los campos usados para clasificar cada transacción de agente.

### Campos usados para clasificar cada transacción de agente

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del campo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Timestamp</strong></p></td>
<td><p>Fecha y hora UTC del evento de agente. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, donde <em>yyyy</em> = año, <em>mm</em> = mes, <em>dd</em> = día, T indica el comienzo del componente tiempo, <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo, <em>fff</em> = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>SessionId</strong></p></td>
<td><p>Identificador de sesión SMTP exclusivo. Este identificador se representa con un número hexadecimal de 16 dígitos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocalEndpoint</strong></p></td>
<td><p>Dirección IP local y número de puerto que aceptaron el mensaje. Las sesiones SMTP usan normalmente el puerto 25.</p></td>
</tr>
<tr class="even">
<td><p><strong>RemoteEndpoint</strong></p></td>
<td><p>Dirección IP y número de puerto del servidor SMTP anterior que se conectaron a este servidor para entregar el mensaje. Cuando el correo Internet fluye a través de un servidor de transporte perimetral en la red perimetral, el valor de <strong>RemoteEndpoint</strong> en el registro de agente del servidor de buzones de correo será la dirección IP del servidor de transporte perimetral. Aun cuando el mensaje se haya transmitido por SMTP, el número de puerto usado por el servidor de envío será un número aleatorio mayor que 1.024.</p></td>
</tr>
<tr class="odd">
<td><p><strong>EnteredOrgFromIP</strong></p></td>
<td><p>Dirección IP del servidor SMTP remoto que se conectó en primer lugar a la organización de Exchange para entregar el mensaje. En un servidor de transporte perimetral, el valor de <strong>RemoteEndpoint</strong> y de <strong>EnteredOrgFromIP</strong> es el mismo. Los agentes contra correo electrónico no deseado usan la dirección IP en <strong>EnteredOrgFromIP</strong> para examinar un mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>MessageId</strong></p></td>
<td><p>Valor del campo de encabezado de <code>MessageID</code>. Si este valor está en blanco, el servidor de transporte de Exchange asigna un valor arbitrario, pero solamente si se acepta el mensaje. Una vez que se asigna un valor, el valor de <code>MessageID</code> es constante durante la vigencia del mensaje.</p></td>
</tr>
<tr class="odd">
<td><p><strong>P1FromAddress</strong></p></td>
<td><p>Dirección de correo electrónico del remitente especificada en <code>MAIL FROM</code> en el sobre del mensaje. Este valor se usa para transportar el mensaje entre servidores de mensajería SMTP. Este valor sirve como comparación con el valor de <strong>P2FromAddresses</strong> para saber si la dirección del remitente de la cabecera del mensaje se ha falsificado.</p></td>
</tr>
<tr class="even">
<td><p><strong>P2FromAddresses</strong></p></td>
<td><p>Dirección de correo electrónico del remitente especificada en el campo de encabezado <code>From</code> o en el campo de encabezado <code>Sender</code> en el encabezado de mensaje.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Recipient</strong></p></td>
<td><p>Dirección de correo electrónico de los destinatarios. Aunque el mensaje original puede contener muchos destinatarios, en el registro de agentes sólo se muestra un destinatario por línea.</p></td>
</tr>
<tr class="even">
<td><p><strong>NumRecipients</strong></p></td>
<td><p>Número total de destinatarios del mensaje original.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Agent</strong></p></td>
<td><p>Nombre del agente que ha realizado la acción. Los valores posibles son:</p>
<ul>
<li><p>Agente de filtro de contenido</p></li>
<li><p>Agente de filtro de destinatarios</p></li>
<li><p>Agente de filtro de remitentes</p></li>
<li><p>Agente de Id. de remitente</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>Event</strong></p></td>
<td><p>Evento SMTP en el que el agente realizó la acción. El valor de <strong>Event</strong> depende del agente. Los eventos SMTP disponibles para cada agente se describen en la primera tabla que aparece en este tema. Los posibles valores para el <strong>Event</strong> son los siguientes:</p>
<ul>
<li><p>OnConnect</p></li>
<li><p>OnEndOfHeaders</p></li>
<li><p>OnEndOfData</p></li>
<li><p>OnMailCommand</p></li>
<li><p>OnRcptCommand</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>Action</strong></p></td>
<td><p>Acción que el agente realiza en el mensaje. Los posibles valores para la <strong>Action</strong> son los siguientes:</p>
<ul>
<li><p>AcceptMessage</p></li>
<li><p>DeleteMessage</p></li>
<li><p>DeleteRecipients</p></li>
<li><p>Disconnect</p></li>
<li><p>QuarantineMessage</p></li>
<li><p>QuarantineRecipients</p></li>
<li><p>RejectAuthentication</p></li>
<li><p>RejectCommand</p></li>
<li><p>RejectConnection</p></li>
<li><p>RejectMessage</p></li>
<li><p>RejectRecipients</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>SmtpResponse</strong></p></td>
<td><p>Respuesta SMTP mejorada, tal y como se define en RFC 2034.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Reason</strong></p></td>
<td><p>Motivo de la acción realizada por el agente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ReasonData</strong></p></td>
<td><p>Detalles precisos de la acción realizada por el agente.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Búsqueda de registros de agente

Puede usar el cmdlet **Get-AgentLog** y el script **Get-AntiSpamFilteringReport.ps1** para buscar los registros de agente.

El script **Get-AntiSpamFilteringReport.ps1** se encuentra en `%ExchangeInstallPath%Scripts`. Debe ejecutar el script en el Shell desde la carpeta de scripts. Para cambiar la ubicación en el Shell a la carpeta de scripts, ejecute el siguiente comando:

  ```powershell
  Cd $env:ExchangeInstallPath\Scripts
  ```

Para ejecutar el script en la carpeta de scripts, use la siguiente sintaxis:

  ```powershell
  .\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]
  ```

Para más información sobre el uso del script, ejecute el siguiente comando:

  ```powershell
  Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1
  ```

Volver al principio

