---
title: 'Seguimiento de mensajes: Exchange 2013 Help'
TOCTitle: Seguimiento de mensajes
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 51406546
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Seguimiento de mensajes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

En Microsoft Exchange Server 2013, el registro de seguimiento de mensajes es un registro detallado de toda la actividad de mensajes cuando estos se transfieren desde y hacia el servicio de transporte en los servidores de buzones de correo, los buzones de correo en los servidores de buzones de correo y en los servidores de transporte perimetral. Puede utilizar los registros de seguimiento de mensajes para análisis de mensajes, análisis del flujo de correo, elaboración de informes y solución de problemas.

En Exchange 2013, puede usar el cmdlet **Set-TransportService** o el cmdlet **Set-MailboxServer** para todas las tareas de configuración de seguimiento de mensajes, ya que el servidor de buzones de correo de Exchange 2013 almacena el servicio de transporte y los buzones de correo. Puede usar uno de estos cmdlets para realizar los siguientes cambios en la configuración del seguimiento de mensajes:

  - Habilitar o deshabilitar el seguimiento de mensajes. El valor predeterminado es habilitado.

  - Especificar la ubicación de los archivos de registro de seguimiento de mensajes.

  - Especificar el tamaño máximo para los archivos de registro de seguimiento de mensajes individuales. El valor predeterminado es 10 MB.

  - Especificar el tamaño máximo del directorio que contiene los archivos de registro de seguimiento de mensajes: El valor predeterminado es 1.000 MB.

  - Especificar la antigüedad máxima de los archivos de registro de seguimiento de mensajes: El valor predeterminado es 30 días.

  - Habilitar o deshabilitar el registro de asuntos de mensajes en los registros de seguimiento de mensajes. El valor predeterminado es habilitado.


> [!NOTE]
> También puede usar el Centro de administración de Exchange (EAC) para habilitar o deshabilitar el seguimiento de mensajes y para especificar la ubicación de los archivos de registro de seguimiento de mensajes.



Exchange usa de forma predeterminada un registro circular para limitar los registros de seguimiento de mensajes según el tamaño de archivo y la antigüedad del mismo, lo que ayuda a controlar el espacio de disco duro usado por los archivos de registro de seguimiento de mensajes.

**Contenido**

Búsqueda en el registro de seguimiento de mensajes

Estructura de los archivos de registro de seguimiento de mensajes

Campos de los archivos de registro de seguimiento de mensajes

Tipos de evento en el registro de seguimiento de mensajes

Valores de origen en el registro de seguimiento de mensajes

Entradas de ejemplo en el registro de seguimiento de mensajes

Problemas de seguridad del registro de seguimiento de mensajes

## Búsqueda en el registro de seguimiento de mensajes

Los registros de seguimiento de mensajes contienen grandes cantidades de datos a medida que los mensajes de mueven por un servidor de buzones de correo de Exchange 2013. Cuando se trata de buscar los registros de seguimiento de mensajes, tiene varias opciones.

  - **Get-MessageTrackingLog**   Los administradores pueden usar este cmdlet para realizar búsquedas en los registros de seguimiento de mensajes con objeto de obtener información sobre los mensajes usando una gran cantidad de criterios de filtro. Para obtener más información, consulte [Buscar en registros seguimiento de mensajes](search-message-tracking-logs-exchange-2013-help.md).

  - **Informes de entrega para administradores**   Los administradores pueden usar la pestaña **Informes de entrega** en el Centro de administración de Exchange (EAC) o los cmdlets **Search-MessageTrackingReport** y **Get-MesageTrackingReport** subyacentes para buscar información en los registros de seguimiento de mensajes acerca de los mensajes enviados o recibidos por un buzón de correo concreto en la organización. Para obtener más información, vea [Informes de entrega para administradores](delivery-reports-for-administrators-exchange-2013-help.md).

  - **Informes de entrega para usuarios**   Los usuarios pueden usar la pestaña **Informes de entrega** en Outlook Web App para buscar información en los registros de seguimiento de mensajes acerca de los mensajes enviados a o enviados por su propio buzón de correo. Para obtener más información, consulte [Informes de entrega](https://go.microsoft.com/fwlink/?linkid=279920).

Volver al principio

## Estructura de los archivos de registro de seguimiento de mensajes

Los archivos de registro de seguimiento de mensajes se encuentran de forma predeterminada en %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking.

La convención de nomenclatura de los archivos de registro en el directorio de registros de seguimiento de mensajes es `MSGTRK`*yyyymmdd-nnnn*`.log`, `MSGTRKMA`*yyyymmdd-nnnn*`.log`, `MSGTRKMD`*yyyymmdd-nnnn*`.log` y `MSGTRKMS`*yyyymmdd-nnnn*`.log`. Los siguientes servicios hacen uso de los diferentes registros:

  - **MSGTRK**   Estos registros están asociados con el servicio de transporte.

  - **MSGTRKMA**   Estos registros están asociados con las aprobaciones y los rechazos usados por el transporte moderado. Para obtener más información, consulte [Administrar la aprobación de mensajes](https://docs.microsoft.com/es-es/exchange/security-and-compliance/mail-flow-rules/manage-message-approval).

  - **MSGTRKMD**   Estos registros están asociados con los mensajes que el servicio de entrega de transporte de buzones de correo entrega en los buzones de correo.

  - **MSGTRKMS**   Estos registros están asociados con los mensajes que el servicio de entrega de transporte de buzones de correo envía desde los buzones de correo.

Los marcadores de los nombres de archivos de registro representan la siguiente información:

  - El marcador de posición *yyyymmdd* es la fecha UTC (hora universal coordinada) en que se ha creado el archivo de registro. *yyyy* = año, *mm* = mes y *dd* = día.

  - El marcador de posición *nnnn* es un número de instancia que empieza por el valor 1 diario para cada prefijo de nombre de archivo de registro de seguimiento de mensajes.

La información se escribe en cada archivo de registro hasta que el tamaño del archivo alcanza el valor máximo especificado para cada uno de dichos archivos. A continuación, se abre un archivo de registro nuevo con un número de instancia incrementado. Este proceso se repite durante el día. La funcionalidad de rotación de archivos de registro elimina los archivos de registro más antiguos si se cumple alguna de las siguientes condiciones:

  - Un archivo de registro alcanza la antigüedad máxima especificada.

  - El directorio de registro de seguimiento de mensajes alcanza el tamaño máximo especificado.
    

    > [!IMPORTANT]
    > El tamaño máximo del directorio de registros de seguimiento de mensajes se calcula como el tamaño total de todos los archivos de registro que tengan el mismo prefijo de nombre. Otros archivos que no sigan la convención de prefijos de nombre no se cuentan en el cálculo total del tamaño del directorio. El cambio de nombre de archivos de registro antiguos y la copia de otros archivos en el directorio de registros de seguimiento de mensajes podría hacer que se superara su tamaño máximo especificado.<BR>En los servidores de buzones de correo de Exchange&nbsp;2013, el tamaño máximo del directorio de registro de seguimiento de mensajes es el triple del valor especificado. Aunque los archivos del registro de seguimiento de mensajes generados por los cuatro servicios diferentes tienen cuatro prefijos de nombre distintos, la cantidad y la frecuencia de los datos escritos en los archivos de registros <STRONG>MSGTRKMA</STRONG> es insignificante en comparación con los otros prefijos de archivos de registro.



Los archivos de registro de seguimiento de mensajes son archivos de texto que contienen datos en el formato de valores separados por comas (CSV). Cada archivo de registro de seguimiento de mensajes tiene un encabezado con la siguiente información:

  - **\#Software:**    Nombre del software que crea el archivo de registro de seguimiento de mensajes. Normalmente, el valor es Microsoft Exchange Server.

  - **\#Version:**    Número de versión del software que crea el archivo de registro de seguimiento de mensajes. Actualmente, el valor es 15.0.0.0.

  - **\#Log-Type:**    Valor de tipo de registro, que es el registro de seguimiento de mensajes.

  - **\#Fecha:**    La fecha y hora UTC en el momento de crearse el archivo. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, donde *yyyy* = año, *mm* = mes, *dd* = día, T indica el comienzo del componente tiempo, *hh* = hora, *mm* = minuto, *ss* = segundo, *fff* = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.

  - **\#Fields:**    Nombres de campos delimitados por comas que se usan en los archivos de registro de seguimiento de mensajes.

Volver al principio

## Campos de los archivos de registro de seguimiento de mensajes

El registro de seguimiento de mensajes almacena cada evento de mensaje en una sola línea del registro. La información de evento de mensajes se organiza por campos separados mediante comas. El nombre del campo suele ser lo bastante descriptivo como para determinar el tipo de información que contiene. Sin embargo, puede que algunos campos estén en blanco, o que el tipo de información almacenada en los campos cambie según el tipo de evento de mensaje y el tipo de archivo de registro de seguimiento de mensaje donde se haya registrado el evento. En la siguiente tabla se detallan de forma genérica los campos que se usan para clasificar cada evento de seguimiento de mensajes.


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
<td><p><strong>date-time</strong></p></td>
<td><p>Fecha y hora UTC del evento de seguimiento de mensajes. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, donde <em>yyyy</em> = año, <em>mm</em> = mes, <em>dd</em> = día, T indica el comienzo del componente tiempo, <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo, <em>fff</em> = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>client-ip</strong></p></td>
<td><p>Dirección IPv4 o IPv6 del servidor o el cliente de mensajería que ha enviado el mensaje.</p></td>
</tr>
<tr class="odd">
<td><p><strong>client-hostname</strong></p></td>
<td><p>Nombre de host o FQDN del servidor o el cliente de mensajería que ha enviado el mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>server-ip</strong></p></td>
<td><p>Dirección IPv4 o IPv6 del servidor Exchange de origen o destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>server-hostname</strong></p></td>
<td><p>Nombre de host o FQDN del servidor de destino.</p></td>
</tr>
<tr class="even">
<td><p><strong>source-context</strong></p></td>
<td><p>Información adicional asociada al campo <strong>source</strong>. Por ejemplo, información del agente de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>connector-id</strong></p></td>
<td><p>Nombre del conector de envío o el conector de recepción de origen o destino. Por ejemplo, <em>ServerName</em>\<em>ConnectorName</em> o <em>ConnectorName</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>source</strong></p></td>
<td><p>Componente del transporte de Exchange que se ocupa del evento de seguimiento de mensajes. Los valores de este campo se describen en la sección Valores de origen en el registro de seguimiento de mensajes, más adelante en este tema.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event-id</strong></p></td>
<td><p>El tipo de evento de mensaje. Los tipos de evento se describen en la sección Tipos de evento en el registro de seguimiento de mensajes, más adelante en este tema.</p></td>
</tr>
<tr class="even">
<td><p><strong>internal-message-id</strong></p></td>
<td><p>Identificador de mensaje asignado por el servidor Exchange que procesa el mensaje actualmente.</p>
<p>El valor de mensaje específico de <strong>internal-message-id</strong> es diferente en el registro de seguimiento de mensajes de cada servidor Exchange implicado en la transmisión del mensaje. Un valor de ejemplo es <code>73014444033</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-id</strong></p></td>
<td><p>Valor del campo de encabezado de <strong>Message-Id:</strong> que hay en el encabezado del mensaje. Si el campo de encabezado <strong>Message-Id:</strong> no existe o está en blanco, se asigna un valor arbitrario. Este valor es constante mientras dura el mensaje. Para los mensajes creados en Exchange, el valor presenta el formato <code>&lt;GUID@ServerFQDN&gt;</code>, incluyendo los corchetes angulares (<code>&lt; &gt;</code>). Por ejemplo, <code>&lt;4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com&gt;</code>. Otros sistemas de mensajería pueden utilizar sintaxis o valores diferentes.</p></td>
</tr>
<tr class="even">
<td><p><strong>network-message-id</strong></p></td>
<td><p>Valor de identificador de mensaje único que persiste en todas las copias del mensaje que se pueden crear debido a la bifurcación o ampliación de los grupos de distribución. Un valor de ejemplo es <code>1341ac7b13fb42ab4d4408cf7f55890f</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>recipient-address</strong></p></td>
<td><p>Direcciones de correo electrónico de los destinatarios del mensaje. Si hay varias direcciones de correo electrónico, se separan por punto y coma (;).</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-status</strong></p></td>
<td><p>Este campo contiene el estado del destinatario de cada destinatario separado por punto y coma (;). Los valores del estado se presentan para los destinatarios en el mismo orden que los valores en el campo <strong>recipient-address</strong>. Los ejemplos de los valores de estado incluyen <code>250 2.1.5 Recipient OK</code> o <code>550 4.4.7 QUEUE.Expired;&lt;ErrorText&gt;</code>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>total-bytes</strong></p></td>
<td><p>El tamaño del mensaje que incluye datos adjuntos en bytes.</p></td>
</tr>
<tr class="even">
<td><p><strong>recipient-count</strong></p></td>
<td><p>Número de destinatarios del mensaje.</p></td>
</tr>
<tr class="odd">
<td><p><strong>related-recipient-address</strong></p></td>
<td><p>Este campo se usa con los eventos <strong>EXPAND</strong>, <strong>REDIRECT</strong> y <strong>RESOLVE</strong> para mostrar otras direcciones de correo electrónico de destinatarios asociadas al mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>reference</strong></p></td>
<td><p>Este campo contiene información extra para tipos de evento específicos. Por ejemplo:</p>
<p><strong>DSN</strong>   Contiene el vínculo al informe, que es el valor <strong>Message-Id</strong> de la notificación del estado de entrega asociado (DSN) si un DSN se genera posteriormente a este evento. Si es un mensaje DSN, el campo <strong>Reference</strong> contiene el valor <strong>Message-Id</strong> del mensaje original para el que se generó este DNS.</p>
<p><strong>EXPAND</strong>   El campo de referencia contiene el valor <strong>related-recipient-address</strong> de los mensajes relacionados.</p>
<p><strong>RECEIVE</strong>   El campo de referencia puede contener el valor <strong>Message-Id</strong> del mensaje relacionado si el mensaje fue generado por otros procesos, por ejemplo, registro de diario o reglas de buzón.</p>
<p><strong>SEND</strong>   El campo de referencia contiene el valor <strong>Internal-Message-Id</strong> de todos los mensajes DSN.</p>
<p><strong>THROTTLE</strong>   El campo de referencia contiene el motivo de las limitaciones del mensaje.</p>
<p><strong>TRANSFER</strong>   El campo de referencia contiene el id. de mensaje interno del mensaje bifurcado.</p>
<p>En los mensajes generados por las reglas de buzón, el campo <strong>Reference</strong> contiene el valor <strong>Internal-Message-Id</strong> del mensaje entrante que hizo que la regla de buzón generara el mensaje saliente.</p>
<p>Para otros tipos de evento, el campo <strong>Reference</strong> puede contener el valor <strong>Internal-Message-Id</strong> de los mensajes bifurcados.</p>
<p>Para el resto de los tipos de eventos, el campo <strong>Reference</strong> normalmente está en blanco.</p></td>
</tr>
<tr class="odd">
<td><p><strong>message-subject</strong></p></td>
<td><p>Asunto del mensaje en el campo de encabezado <code>Subject:</code>. El seguimiento de los asuntos de los mensajes se controla por medio del parámetro <em>MessageTrackingLogSubjectLoggingEnabled</em> en los cmdlets <strong>Set-TransportService</strong> o <strong>Set-MailboxServer</strong>. De forma predeterminada, el seguimiento de asuntos de mensajes está habilitado.</p></td>
</tr>
<tr class="even">
<td><p><strong>sender-address</strong></p></td>
<td><p>Dirección de correo electrónico especificada en el campo de encabezado <code>Sender:</code> o en el campo de encabezado <code>From:</code> si <code>Sender:</code> no está presente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>return-path</strong></p></td>
<td><p>Dirección de correo electrónico especificada por <code>MAIL FROM:</code> en el sobre del mensaje. Aunque este campo nunca está en blanco, puede contener un valor de dirección de remitente nulo representado como <code>&lt;&gt;</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>message-info</strong></p></td>
<td><p>Información extra sobre el mensaje. Por ejemplo:</p>
<ul>
<li><p>Fecha y hora UTC de creación del mensaje de los eventos <strong>DELIVER</strong> y <strong>SEND</strong>. La fecha y hora de creación hacen referencia al momento en que se especifica el mensaje por primera vez en la organización de Exchange. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, donde <em>yyyy</em> = año, <em>mm</em> = mes, <em>dd</em> = día, T indica el comienzo del componente tiempo, <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo, <em>fff</em> = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.</p></li>
<li><p>Errores de autenticación. Por ejemplo, puede que vea el valor <code>11a</code> y el tipo de autenticación cuando se produzcan errores de autenticación.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>directionality</strong></p></td>
<td><p>Dirección del mensaje. Algunos valores de ejemplo son <code>Incoming</code>, <code>Undefined</code> y <code>Originating</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>tenant-id</strong></p></td>
<td><p>Este campo no se usa en las organizaciones de Exchange 2013 locales.</p></td>
</tr>
<tr class="odd">
<td><p><strong>original-client-ip</strong></p></td>
<td><p>Dirección IPv4 o IPv6 del cliente original.</p></td>
</tr>
<tr class="even">
<td><p><strong>original-server-ip</strong></p></td>
<td><p>Dirección IPv4 o IPv6 del servidor original.</p></td>
</tr>
<tr class="odd">
<td><p><strong>custom-data</strong></p></td>
<td><p>Este campo contiene datos relacionados con un tipo de evento específico. Por ejemplo, el agente de reglas de transporte usa este campo para registrar el GUID de la regla de transporte o la directiva DLP que actuó en dicho mensaje. Para obtener más información sobre estos valores del agente de reglas de transporte, consulte la sección &quot;Registro de datos&quot; en el tema <a href="view-dlp-policy-detection-reports-exchange-2013-help.md">Ver informes de detección de directivas de DLP</a>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Tipos de evento en el registro de seguimiento de mensajes

Varios tipos de eventos en el campo **event-id** se usan para clasificar los eventos de mensaje en el registro de seguimiento de mensajes. Algunos eventos de mensaje solo aparecen en un tipo de archivo de registro de seguimiento de mensajes, mientras que otros aparecen en todos los tipos de archivos de registro de seguimiento de mensajes. En la siguiente tabla se explican los tipos de evento usados para clasificar cada evento de mensaje.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Nombre del evento</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>AGENTINFO</strong></p></td>
<td><p>Los agentes de transporte usan este evento para registrar datos personalizados.</p></td>
</tr>
<tr class="even">
<td><p><strong>BADMAIL</strong></p></td>
<td><p>Mensaje enviado por el directorio de recogida o el directorio de reproducción que no se puede entregar o devolver.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DEFER</strong></p></td>
<td><p>Se ha retrasado la entrega del mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>DELIVER</strong></p></td>
<td><p>Un mensaje ha llegado a un buzón de correo local.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DROP</strong></p></td>
<td><p>Se quitó un mensaje sin una notificación de estado de entrega (también conocida como DSN, mensaje de rebote, informe de no entrega o NDR). Por ejemplo:</p>
<ul>
<li><p>Mensajes de solicitud de aprobación de moderación acabados.</p></li>
<li><p>Mensajes de correo no deseado que se anularon en modo silencioso sin un NDR.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>Se ha generado una notificación de estado de entrega (DSN).</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEDELIVER</strong></p></td>
<td><p>Se ha entregado un mensaje duplicado al destinatario. La duplicación puede ocurrir si un destinatario es miembro de varios grupos de distribución anidados. El almacén de información se encarga de detectar y quitar los mensajes duplicados.</p></td>
</tr>
<tr class="even">
<td><p><strong>DUPLICATEEXPAND</strong></p></td>
<td><p>Se detectó un destinatario duplicado durante la ampliación del grupo de distribución.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DUPLICATEREDIRECT</strong></p></td>
<td><p>Un destinatario alternativo para el mensaje ya era un destinatario.</p></td>
</tr>
<tr class="even">
<td><p><strong>EXPAND</strong></p></td>
<td><p>Se ha ampliado un grupo de distribución.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FAIL</strong></p></td>
<td><p>Error al entregar el mensaje. Los orígenes incluyen <strong>SMTP</strong>, <strong>DNS</strong>, <strong>QUEUE</strong> y <strong>ROUTING</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>HADISCARD</strong></p></td>
<td><p>Se descartó un mensaje de instantánea después de que la copia principal se entregara al siguiente salto. Para obtener más información, consulte <a href="shadow-redundancy-exchange-2013-help.md">Redundancia de instantánea</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HARECEIVE</strong></p></td>
<td><p>El servidor recibió un mensaje de instantánea en el grupo de disponibilidad de la base de datos local (DAG) o sitio de Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>HAREDIRECT</strong></p></td>
<td><p>Se creó un mensaje de instantánea.</p></td>
</tr>
<tr class="odd">
<td><p><strong>HAREDIRECTFAIL</strong></p></td>
<td><p>No se ha podido crear un mensaje de instantánea. Los detalles se almacenan en el campo <strong>source-context</strong>.</p></td>
</tr>
<tr class="even">
<td><p><strong>INITMESSAGECREATED</strong></p></td>
<td><p>Se envió un mensaje a un destinatario moderado, así que el mensaje se envió al buzón de correo de arbitraje para su aprobación. Para obtener más información, consulte <a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/mail-flow-rules/manage-message-approval">Administrar la aprobación de mensajes</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LOAD</strong></p></td>
<td><p>Un mensaje se cargó correctamente durante el arranque.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATIONEXPIRE</strong></p></td>
<td><p>Un moderador de un destinatario moderado nunca aprobó ni rechazó el mensaje, así que expiró. Para obtener más información sobre los destinatarios moderados, consulte <a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/mail-flow-rules/manage-message-approval">Administrar la aprobación de mensajes</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORAPPROVE</strong></p></td>
<td><p>Un moderador de un destinatario moderado aprobó el mensaje, así que el mensaje se entregó al destinatario moderado.</p></td>
</tr>
<tr class="even">
<td><p><strong>MODERATORREJECT</strong></p></td>
<td><p>Un moderador de un destinatario moderado rechazó el mensaje, así que el mensaje no se entregó al destinatario moderado.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MODERATORSALLNDR</strong></p></td>
<td><p>No se pudo entregar ninguna de las solicitudes de aprobación enviadas a todos los moderadores de un destinatario moderado, lo que resultó en informes de no entrega (NDR).</p></td>
</tr>
<tr class="even">
<td><p><strong>NOTIFYMAPI</strong></p></td>
<td><p>Se detectó un mensaje en la bandeja de salida de un buzón del servidor local.</p></td>
</tr>
<tr class="odd">
<td><p><strong>NOTIFYSHADOW</strong></p></td>
<td><p>Se detectó un mensaje en la bandeja de salida del servidor local, y se debe crear una copia instantánea del mensaje.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>Se incluyó o quitó un mensaje de la cola de mensajes dudosos.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PROCESS</strong></p></td>
<td><p>El mensaje se procesó correctamente.</p></td>
</tr>
<tr class="even">
<td><p><strong>PROCESSMEETINGMESSAGE</strong></p></td>
<td><p>El servicio de entrega de transporte de buzones de correo ha procesado un mensaje de reunión.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RECEIVE</strong></p></td>
<td><p>El componente de recepción SMTP del servicio de transporte o de los directorios de recogida o de reproducción recibió un mensaje (origen: <code>SMTP</code>), o se envió un mensaje desde un buzón de correo al servicio de entrega de transporte de buzones de correo (origen: <code>STOREDRIVER</code>).</p></td>
</tr>
<tr class="even">
<td><p><strong>REDIRECT</strong></p></td>
<td><p>Se redirigió un mensaje a un destinatario alternativo tras una búsqueda de Active Directory.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESOLVE</strong></p></td>
<td><p>Los destinatarios de un mensaje se resolvieron para una dirección de correo electrónico distinta tras una búsqueda de Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMIT</strong></p></td>
<td><p>Un mensaje se reenvió automáticamente desde la red de seguridad. Para obtener más información, consulte <a href="safety-net-exchange-2013-help.md">Red de seguridad</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>RESUBMITDEFER</strong></p></td>
<td><p>Se aplazó un mensaje reenviado automáticamente desde la red de seguridad.</p></td>
</tr>
<tr class="even">
<td><p><strong>RESUBMITFAIL</strong></p></td>
<td><p>Error de un mensaje reenviado automáticamente desde la red de seguridad.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SEND</strong></p></td>
<td><p>SMTP envió un mensaje entre servicios de transporte.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMIT</strong></p></td>
<td><p>El servicio de entrega de transporte de buzones de correo transmitió correctamente el mensaje al servicio de transporte. Para los eventos <strong>SUBMIT</strong>, la propiedad <strong>source-context</strong> contiene los siguientes detalles:</p>
<ul>
<li><p><strong>MDB</strong>   Base de datos de buzones de correo de GUID.</p></li>
<li><p><strong>Mailbox</strong>   Buzón de correo de GUID.</p></li>
<li><p><strong>Event</strong>   Número de secuencia del evento.</p></li>
<li><p><strong>MessageClass</strong>   Tipo de mensaje. Por ejemplo, <code>IPM.Note</code>.</p></li>
<li><p><strong>CreationTime</strong>   Fecha y hora del envío del mensaje.</p></li>
<li><p><strong>ClientType</strong>   Por ejemplo, <code>User</code>, <code>OWA</code> o <code>ActiveSync</code>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>SUBMITDEFER</strong></p></td>
<td><p>La transmisión de mensajes desde el servicio de entrega de transporte de buzones al servicio de transporte se aplazó.</p></td>
</tr>
<tr class="even">
<td><p><strong>SUBMITFAIL</strong></p></td>
<td><p>Error en la transmisión de mensajes desde el servicio de entrega de transporte de buzones al servicio de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SUPPRESSED</strong></p></td>
<td><p>La transmisión del mensaje se suprimió.</p></td>
</tr>
<tr class="even">
<td><p><strong>THROTTLE</strong></p></td>
<td><p>El mensaje se limitó.</p></td>
</tr>
<tr class="odd">
<td><p><strong>TRANSFER</strong></p></td>
<td><p>Los destinatarios se han movido a un mensaje bifurcado debido a la conversión del contenido, los límites de destinatarios de mensajes o los agentes. Los orígenes incluyen <strong>ROUTING</strong> o <strong>QUEUE</strong>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Valores de origen en el registro de seguimiento de mensajes

Los valores en el campo **source** en el registro de seguimiento de mensajes indican el componente que es responsable del evento de seguimiento del mensaje. En la siguiente tabla se describen los valores del campo **source**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor de origen</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ADMIN</strong></p></td>
<td><p>El origen del evento fue la intervención humana. Por ejemplo, un administrador usó el Visor de cola para eliminar un mensaje o envió archivos de mensaje mediante el directorio de reproducción.</p></td>
</tr>
<tr class="even">
<td><p><strong>AGENT</strong></p></td>
<td><p>El origen del evento fue un agente de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>APPROVAL</strong></p></td>
<td><p>El origen del evento fue el marco de la aprobación que se usa con los destinatarios moderados. Para obtener más información, consulte <a href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/mail-flow-rules/manage-message-approval">Administrar la aprobación de mensajes</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>BOOTLOADER</strong></p></td>
<td><p>El origen del evento consistía en mensajes sin procesar que hay en el servidor durante el arranque. Esto está relacionado con el tipo de evento <strong>LOAD</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DNS</strong></p></td>
<td><p>El origen del evento fue una DNS.</p></td>
</tr>
<tr class="even">
<td><p><strong>DSN</strong></p></td>
<td><p>El origen del evento fue una notificación de estado de entrega (DSN). Por ejemplo, un informe de no entrega (NDR).</p></td>
</tr>
<tr class="odd">
<td><p><strong>GATEWAY</strong></p></td>
<td><p>El origen del evento fue un conector externo. Para obtener más información, consulte <a href="foreign-connectors-exchange-2013-help.md">Conectores externos</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>MAILBOXRULE</strong></p></td>
<td><p>El origen del evento fue una regla de la bandeja de entrada. Para obtener más información, consulte <a href="https://go.microsoft.com/fwlink/?linkid=285479">Reglas de Bandeja de entrada</a>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MEETINGMESSAGEPROCESSOR</strong></p></td>
<td><p>El origen del evento ha sido el procesador de mensajes de reunión, que actualiza los calendarios según las actualizaciones de las reuniones.</p></td>
</tr>
<tr class="even">
<td><p><strong>ORAR</strong></p></td>
<td><p>El origen del evento fue un destinatario alternativo solicitado del originador (ORAR). Puede habilitar o deshabilitar la compatibilidad con ORAR en los conectores de recepción mediante el parámetro <em>OrarEnabled</em> en los cmdlets <strong>New-ReceiveConnector</strong> o <strong>Set-ReceiveConnector</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>PICKUP</strong></p></td>
<td><p>El origen del evento fue el directorio de recogida. Para obtener más información, consulte <a href="pickup-directory-and-replay-directory-exchange-2013-help.md">Directorio de recogida y directorio de reproducción</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>POISONMESSAGE</strong></p></td>
<td><p>El origen del evento fue el identificador de mensaje dudoso. Para obtener más información sobre la cola de mensajes dudosos, consulte <a href="queues-exchange-2013-help.md">Colas</a></p></td>
</tr>
<tr class="odd">
<td><p><strong>PUBLICFOLDER</strong></p></td>
<td><p>El origen del evento fue una carpeta pública habilitada para correo.</p></td>
</tr>
<tr class="even">
<td><p><strong>QUEUE</strong></p></td>
<td><p>El origen del evento fue una cola.</p></td>
</tr>
<tr class="odd">
<td><p><strong>REDUNDANCY</strong></p></td>
<td><p>El origen del evento fue la redundancia de instantáneas. Para obtener más información, consulte <a href="shadow-redundancy-exchange-2013-help.md">Redundancia de instantánea</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>ROUTING</strong></p></td>
<td><p>El origen del evento fue el componente de resolución de enrutamiento del categorizador en el servicio de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SAFETYNET</strong></p></td>
<td><p>El origen del evento fue la red de seguridad. Para obtener más información, consulte <a href="safety-net-exchange-2013-help.md">Red de seguridad</a>.</p></td>
</tr>
<tr class="even">
<td><p><strong>SMTP</strong></p></td>
<td><p>El mensaje fue enviado por el componente de envío SMTP o el componente de recepción SMTP del servicio de transporte.</p></td>
</tr>
<tr class="odd">
<td><p><strong>STOREDRIVER</strong></p></td>
<td><p>El origen del evento fue un envío MAPI desde un buzón de correo en el servidor local.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Entradas de ejemplo en el registro de seguimiento de mensajes

Un mensaje sin eventos enviado entre dos usuarios genera varias entradas en el registro de seguimiento de mensajes. Puede ver los resultados usando el cmdlet **Get-MessageTrackingLog**. Para obtener más información, consulte [Buscar en registros seguimiento de mensajes](search-message-tracking-logs-exchange-2013-help.md).

Este es un ejemplo condensado de entradas del registro de seguimiento de mensajes creadas cuando el usuario chris@contoso.com envía correctamente un mensaje de prueba al usuario michelle@contoso.com. Ambos usuarios tienen buzones de correo en el mismo servidor.

```powershell
EventId    Source      Sender            Recipients             MessageSubject
-------    ------      ------            ----------             --------------
NOTIFYMAPI STOREDRIVER                   {}
RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
```

Volver al principio

## Problemas de seguridad del registro de seguimiento de mensajes

No se almacena ningún contenido de mensaje en el registro de seguimiento de mensajes. De manera predeterminada, la línea de asunto de un mensaje de correo electrónico se almacena en el registro de seguimiento de mensajes. Puede que desee deshabilitar el registro de asuntos de mensajes para cumplir con los requisitos de aumento de la seguridad o la privacidad. Para habilitar o deshabilitar el registro de asuntos de mensajes, compruebe la directiva de la organización sobre la revelación de información de las líneas de asunto. Para obtener más información, consulte [Configurar el seguimiento de mensajes](configure-message-tracking-exchange-2013-help.md).

Volver al principio

