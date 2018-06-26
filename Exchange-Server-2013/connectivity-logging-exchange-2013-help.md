---
title: 'Registro de conectividad: Exchange 2013 Help'
TOCTitle: Registro de conectividad
ms:assetid: c31fd710-4ae4-4d9a-8936-d056e7ca2748
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124500(v=EXCHG.150)
ms:contentKeyID: 49895895
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registro de conectividad

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

El registro de conectividad registra la actividad de conexión saliente que se utiliza para transmitir mensajes de un servicio de transporte en el servidor de Exchange. El objetivo del registro de conectividad no es realizar el seguimiento de la transmisión de los mensajes individuales de correo electrónico, sino realizar el seguimiento del registro de conexión desde una fuente hasta el destino, independientemente de la cantidad de mensajes que se transmiten. Está habilitado el registro de conectividad en el servicio de transporte de front-end en servidores de Acceso de clientes, el servicio de transporte en servidores Buzón de correo y el servicio de transporte de buzones en servidores Buzón de correo. En la siguiente lista se describe el tipo de información registrada en el registro de conectividad:

  - Origen

  - Destination

  - Información de resolución DNS

  - Información detallada acerca de los errores de conexión

  - Número de mensajes y bytes transmitidos

Los cdmlets **Set-TransportService**, **Set-FrontEndTransportService** y **Set-MailboxTransportService** en el Shell de administración de Exchange se utilizan para realizar todas las tareas de configuración de registro de conectividad. Las siguientes opciones se encuentran disponibles para los registros de conectividad:

  - Habilitar o deshabilitar el registro de conectividad. El valor predeterminado es habilitado.

  - Especificar la ubicación de los archivos de registro de conectividad.

  - Especificar el tamaño máximo para cada archivo de registro de conectividad. El tamaño predeterminado es 10 megabytes (MB).

  - Especificar el tamaño máximo para el directorio que contiene los archivos de registro de conectividad. El tamaño predeterminado es 1.000 MB.

  - Especificar la antigüedad máxima para los archivos de registro de conectividad. La antigüedad predeterminada es 30 días.

De forma predeterminada, Exchange utiliza un registro circular para limitar los registros de conectividad según el tamaño y la antigüedad del archivo, con el fin de controlar mejor el espacio en el disco duro que utilizan los archivos de registro de conectividad.

**Contenido**

Estructura de los archivos de registro de conectividad

Información que se escribe en el registro de conectividad

## Estructura de los archivos de registro de conectividad

De forma predeterminada, los archivos del registro de conectividad se encuentran en las siguientes ubicaciones:

  - **Transport service** %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\Connectivity

  - **Front End Transport service** %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd\\Connectivity

  - **Mailbox Transport service** %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox\\Connectivity

La convención de nomenclatura para los archivos de registro de conectividad es CONNECTLOG*yyymmdd-nnnn*.log. Los marcadores de posición representan la siguiente información:

  - El marcador de posición *aaaammdd* es la hora UTC (hora universal coordinada) en que se ha creado el archivo de registro. El marcador de posición *aaaa* = año, *mm* = mes y *dd* = día.

  - El marcador de posición *nnnn* es un número de instancia que empieza por el valor 1 para cada día.

La información se escribe en el archivo de registro hasta que el tamaño del archivo alcanza su valor máximo especificado y se abre un nuevo archivo de registro que tiene un número de instancia mayor. Este proceso se repite durante el día. El registro circular elimina los archivos de registro más antiguos cuando el directorio de registro de conectividad alcanza su tamaño máximo especificado o su antigüedad máxima especificada.

Los archivos de registro de conectividad son archivos de texto que contienen datos en el formato de valores separados por comas (CSV). Cada archivo de registro de conectividad tiene un encabezado que contiene la siguiente información:

  - **\#Software**   El nombre del software que creó el archivo de registro de conectividad. Normalmente, el valor es Microsoft Exchange Server.

  - **\#Version**   El número de versión del software que creó el archivo de registro de conectividad. Actualmente, el valor es 15.0.0.0.

  - **\#Log-Type**   Valor del tipo de registro, que es el registro de conectividad de transporte.

  - **\#Date**   La fecha y hora UTC en el momento de crearse el archivo. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: *yyyy-mm-dd*T*hh:mm:ss.fff*Z, donde *yyyy* = año, *mm* = mes, *dd* = día, T indica el comienzo del componente tiempo, *hh* = hora, *mm* = minuto, *ss* = segundo, *fff* = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.

  - **\#Fields**   Los nombres de los campos delimitados por comas que se usan en los archivos de registro de conectividad.

Volver al principio

## Información que se escribe en el registro de conectividad

El registro de conectividad almacena cada evento de conexión del servicio de transporte saliente en una única línea del registro de conectividad. La información almacenada en cada línea se organiza por campos. Estos campos se separan con comas. La siguiente tabla describe los campos utilizados para clasificar cada evento de conexión saliente.

### Campos utilizados para clasificar cada evento de conexión

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
<td><p>Fecha y hora UTC del evento de conexión. La fecha y hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: <em>yyyy-mm-dd</em>T<em>hh:mm:ss.fff</em>Z, donde <em>yyyy</em> = año, <em>mm</em> = mes, <em>dd</em> = día, T indica el comienzo del componente tiempo, <em>hh</em> = hora, <em>mm</em> = minuto, <em>ss</em> = segundo, <em>fff</em> = fracciones de un segundo, y Z significa Zulu, que es otra forma de denominar UTC.</p></td>
</tr>
<tr class="even">
<td><p><strong>session</strong></p></td>
<td><p>Un GUID que es exclusivo para cada sesión de SMTP pero que es el mismo para cada evento que está asociado a la sesión de SMTP. Para las sesiones MAPI en el servicio de transporte de buzones, el campo sesión está en blanco.</p></td>
</tr>
<tr class="odd">
<td><p><strong>source</strong></p></td>
<td><p><strong>SMTP</strong> para conexiones SMTP, <strong>MAPI</strong> para conexiones del servicio de transporte de buzones para la base de datos de buzones locales.</p></td>
</tr>
<tr class="even">
<td><p><strong>destination</strong></p></td>
<td><p>Nombre del destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>direction</strong></p></td>
<td><p>Un carácter único que representa el inicio, la fase intermedia o el fin de la conexión. Los valores posibles para el campo de dirección son los siguientes:</p>
<ul>
<li><p><strong>+</strong>   Conectar</p></li>
<li><p><strong>-</strong>   Desconectar</p></li>
<li><p><strong>&gt;</strong>   Enviar</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>description</strong></p></td>
<td><p>Información de texto asociada al evento de conexión. Los siguientes valores son ejemplos de valores para el campo de descripción:</p>
<ul>
<li><p>Número y tamaño de los mensajes transmitidos</p></li>
<li><p>Información de resolución del registro de recursos MX de DNS para los dominios de destino</p></li>
<li><p>Información de resolución de DNS para los servidores de buzones de correo de destino</p></li>
<li><p>Mensajes de establecimiento de conexión</p></li>
<li><p>Mensajes de error de conexión</p></li>
</ul></td>
</tr>
</tbody>
</table>


Cuando el servicio de transporte establece una conexión a un destino, el servicio de transporte puede estar preparado para enviar un mensaje o varios mensajes. Los procesos de conexión y transmisión de mensajes generan varios eventos escritos en varias líneas en el registro de conectividad. Las conexiones simultáneas con varios destinos generan entradas de registro de conectividad relacionadas con los distintos destinos entrelazados. No obstante, puede usar los campos de fecha y hora, sesión, origen y dirección para organizar las entradas del registro de conectividad para cada conexión independiente, de principio a fin.

Volver al principio

