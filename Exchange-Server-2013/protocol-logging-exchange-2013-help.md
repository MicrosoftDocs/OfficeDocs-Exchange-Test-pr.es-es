---
title: 'Registro de protocolos: Exchange 2013 Help'
TOCTitle: Registro de protocolos
ms:assetid: 40da446b-bcc3-4a97-ace7-a54f6ddebd79
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997624(v=EXCHG.150)
ms:contentKeyID: 49895594
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registro de protocolos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

El registro de protocolo registra las conversaciones del SMTP que se producen entre servidores de mensajería como parte de la entrega de mensajes. Estas conversaciones de SMTP se producen en conectores de envío y de recepción que existen en el servicio de transporte front-end en servidores de acceso de clientes, el servicio de transporte en servidores de buzones de correo y el servicio de transporte de buzones en servidores de buzones de correo. Puede usar el registro de protocolo para diagnosticar problemas del flujo de correo.

De forma predeterminada, el registro de protocolo está deshabilitado en todos los conectores de envío y de recepción. El registro de protocolo está habilitado o deshabilitado en cada conector individual. Otras opciones de registro de protocolo se establecen para todos los conectores de recepción o para todos los conectores de envío que existen en cada servicio de transporte individual en el servidor. Todos los conectores de recepción de un servicio de transporte comparten los mismos archivos de registro de protocolo y opciones de registro de protocolo. Estos archivos y opciones son independientes de los del conector de envío y las opciones de registro de protocolos en el servicio de transporte que se encuentran en el mismo servidor.

Las siguientes opciones están disponibles para los registros de protocolo de todos los conectores de envío o todos los conectores de recepción en cada servicio de transporte del servidor Exchange:

  - Especifique la ubicación de los archivos del registro de protocolo del conector de envío o del conector de recepción.

  - Especifique un tamaño máximo para los archivos del registro de protocolo del conector de envío o del conector de recepción. El tamaño predeterminado es 10 megabytes (MB).

  - Especifique un tamaño máximo para el directorio que contenga los archivos del registro de protocolo del conector de envío o del conector de recepción. El tamaño predeterminado es 250 MB.

  - Especifique una antigüedad máxima para los archivos del registro de protocolo del conector de envío o del conector de recepción. La antigüedad predeterminada es 30 días.

De forma predeterminada, Exchange usa un registro circular para limitar los registros de protocolo según el tamaño de archivo y la antigüedad del mismo, para ayudar así a controlar el espacio de disco duro usado por los archivos de registro.

Existe un conector de envío especial denominado conector de envío interno de la organización en el servicio de transporte en cada servidor de buzones de correo y en el servicio de transporte front-end en cada servidor de acceso de clientes. Este conector se crea implícitamente, es invisible y no necesita administración. El conector de envío interno de la organización lo usan los siguientes servicios de transporte:

  - **Servicio de transporte en servidores Buzón de correo**
    
      - Retransmite mensajes al servicio de transporte y al servicio de transporte de buzones de correo en cada servidor de buzones de correo de Exchange 2013 en la organización.
    
      - Retransmite mensajes a otros servidores de transporte de concentradores de Exchange 2007 o de Exchange 2010 en la organización.
    
      - Retransmite mensajes a servidores de transporte perimetral en la red perimetral.

  - **Servicio de transporte front-end en servidores de acceso de clientes**   Retransmite mensajes al servicio de transporte en los servidores de buzones de correo de Exchange 2013 de la organización.

Existe un conector de envío equivalente denominado conector de envío de entrega de buzones de correo en el servicio de transporte de buzones de correo en cada servidor de buzones de correo. Este conector también se crea de forma implícita, es invisible y no requiere administración. El conector de envío de entrega de buzones de correo se usa para retransmitir mensajes al servicio de transporte y al servicio de transporte de buzones de correo en otros servidores de buzones de correo de la organización.

De forma predeterminada, el registro de protocolo del conector de envío de entrega de buzones de correo está deshabilitado. Puede habilitar o deshabilitar el registro de protocolo para el conector de envío de entrega de buzones de correo mediante el parámetro *MailboxDeliveryConnectorProtocolLoggingLevel* en el cmdlet **Set-MailboxTransportService**. Si habilita el registro de protocolo para el conector de envío de entrega de buzones de correo, el registro tendrá lugar en los registros de protocolo del conector de envío del servicio de transporte de buzones en el servidor de buzones de correo.

**Contenido**

Estructura de los archivos del registro de protocolo

Información que se escribe en el registro del protocolo

## Estructura de los archivos del registro de protocolo

De forma predeterminada, los archivos del registro de protocolo se encuentran en las siguientes ubicaciones:

  - **Recibe archivos de registros de protocolo de conector para el servicio de transporte en servidores de buzones de correo**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpReceive

  - **Recibe archivos de registros de protocolo de conector para el servicio de transporte de buzones de correo en servidores de buzones de correo**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpReceive

  - **Recibe archivos de registros de protocolo de conector para el servicio de transporte front-end en servidores de acceso de clientes**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpReceive

  - **Envía archivos de registros de protocolo de conector para el servicio de transporte en servidores de buzones de correo**   %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\ProtocolLog\\SmtpSend

  - **Envía archivos de registros de protocolo de conector para el servicio de transporte de buzones de correo en servidores de buzones de correo**   %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\ProtocolLog\\SmtpSend

  - **Envía archivos de registros de protocolo de conector para el servicio de transporte front-end en servidores de acceso de clientes**   %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\ProtocolLog\\SmtpSend

La convención de nomenclatura de archivos de registro en cada directorio de registros de protocolo es *prefixyyyymmdd-nnnn*.log. Los marcadores representan la siguiente información:

  - El marcador *prefix* es SEND para conectores de envío o RECV para conectores de recepción.

  - El marcador de posición *ddmmaaaa* es la fecha de hora universal coordinada (UTC) en la cual se creó el archivo de registro. El marcador de posición *aaaa* = año, *mm* = mes y *dd* = día.

  - El marcador *nnnn* es un número de instancia que se inicia en el valor de 1 para cada día.

La información se escribe en el archivo de registro hasta que el tamaño del archivo alcanza su valor máximo especificado y se abre un nuevo archivo de registro que tiene un número de instancia mayor. Este proceso se repite a lo largo del día. El registro circular elimina los archivos de registro más antiguos cuando el directorio de registro del protocolo alcanza su tamaño máximo especificado o su antigüedad máxima especificada.

Los archivos de registro de protocolos son archivos de texto que contienen datos en el formato de archivo de valores separados por comas (CSV). Cada archivo de registro de protocolo tiene un encabezado que contiene la siguiente información:

  - **\#Software:**  el nombre del software que creó el archivo de registro de protocolo. Normalmente, el valor es Microsoft Exchange Server.

  - **\#Versión:**  el número de versión del software que creó el archivo de registro de protocolo. Actualmente, el valor es 15.0.0.0.

  - **\#Tipo de registro:**  el valor de tipo de registro de este campo, que es Registro de protocolo de recepción SMTP o Registro de protocolo de envío SMTP.

  - **\#Fecha:**  la fecha y hora UTC en el momento en que se creó el archivo. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, donde *yyyy* = año, *mm* = mes, *dd* = día, T indica el comienzo del componente tiempo, *hh* = hora, *mm* = minuto, *ss* = segundo, *fff* = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.

  - **\#Campos:**  los nombres de campos delimitados por comas que se usan en los archivos de registro del protocolo.

Volver al principio

## Información que se escribe en el registro del protocolo

El registro de protocolo almacena cada evento de protocolo SMTP en una única línea del registro de protocolo. La información que se almacena en cada línea se organiza por campos. Estos campos se separan con comas. En la tabla siguiente se describen los campos usados para clasificar cada protocolo.

### Campos usados para clasificar cada evento de protocolo

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
<td><p>Fecha y hora UTC del evento de protocolo. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, donde <em>yyyy</em> = año, <em>mm</em> = mes, <em>dd</em> = día, T indica el comienzo del componente tiempo, <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo, <em>fff</em> = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>connector-id</strong></p></td>
<td><p>El nombre completo (DN) del conector que está asociado al evento SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>session-id</strong></p></td>
<td><p>Un GUID que es exclusivo para cada sesión SMTP, pero que es el mismo para cada evento que está asociado con esa sesión SMTP.</p></td>
</tr>
<tr class="even">
<td><p><strong>sequence-number</strong></p></td>
<td><p>Un contador que se inicia en 0 y que aumenta para cada evento de la misma sesión SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>local-endpoint</strong></p></td>
<td><p>El punto final local de una sesión SMTP. Se compone de una dirección IP y un número de puerto TCP cuyo formato es <em>&lt;Dirección IP&gt;</em>:<em>&lt;puerto&gt;</em>.</p></td>
</tr>
<tr class="even">
<td><p><strong>remote-endpoint</strong></p></td>
<td><p>El punto final remoto de una sesión SMTP. Se compone de una dirección IP y un número de puerto TCP cuyo formato es <em>&lt;Dirección IP&gt;</em>:<em>&lt;puerto&gt;</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>event</strong></p></td>
<td><p>Un único carácter que representa el evento del protocolo. Los valores posibles para el evento son los siguientes:</p>
<ul>
<li><p><strong>+</strong>   Conectar</p></li>
<li><p><strong>-</strong>   Desconectar</p></li>
<li><p><strong>&gt;</strong>   Enviar</p></li>
<li><p><strong>&lt;</strong>   Recibir</p></li>
<li><p><strong>*</strong>   Información</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>data</strong></p></td>
<td><p>Información de texto asociada con el evento SMTP.</p></td>
</tr>
<tr class="odd">
<td><p><strong>context</strong></p></td>
<td><p>Información contextual adicional que puede asociarse con el evento de SMTP.</p></td>
</tr>
</tbody>
</table>


Una única conversación de SMTP que representa el envío o recepción de un único mensaje de correo electrónico genera múltiples eventos de SMTP. Estos eventos de SMTP hacen que se escriban múltiples líneas en el registro de protocolo. Pueden producirse al mismo tiempo múltiples conversaciones de SMTP que representan el envío o recepción de múltiples mensajes de correo electrónico. Esto crea entradas de registro de protocolo a partir de diferentes conversaciones de SMTP que se intercalan. Puede usar los campos session-id y sequence-number para clasificar las entradas del registro del protocolo mediante una conversación SMTP.

Volver al principio

