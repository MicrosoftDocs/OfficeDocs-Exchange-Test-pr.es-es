---
title: 'Registro de administración de derechos de información: Exchange 2013 Help'
TOCTitle: Registro de administración de derechos de información
ms:assetid: e06f57f9-a9e2-43a2-b88c-288b324d71f0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff461940(v=EXCHG.150)
ms:contentKeyID: 49895969
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Registro de administración de derechos de información

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

En Microsoft Exchange Server 2013, las operaciones de Information Rights Management (IRM) se graban en registros de IRM. Los registros de IRM lo ayudan a controlar y solucionar los problemas de interacciones entre el cliente de Rights Management Services (RMS) en un servidor de Exchange 2013 y el clúster de Active Directory Rights Management Services (AD RMS) en su organización.

Para conocer más detalles acerca de IRM, vea [Information Rights Management](information-rights-management-exchange-2013-help.md).

**Contenido**

Structure of IRM logs

Logging process

Information written to IRM logs

Managing IRM logs

¿Está buscando tareas de administración relacionadas con IRM? Vea [Procedimientos de Information Rights Management](information-rights-management-procedures-exchange-2013-help.md).

## Estructura de registros de IRM

De forma predeterminada, estos registros se encuentran en la carpeta C:\\Program Files\\Microsoft\\Exchange Server\\V14\\Logging\\IRMLogs.

La convención de nomenclatura de los archivos de registro de IRM es \<*Process*\>\_\<*Process identifier* o *IIS AppPool identifier*\>\_IRMLOG*yyyymmdd*-*nnnn*.log, en donde:

  - \<*Process*\>= proceso que crea el archivo de registro. Por ejemplo, en el servicio de transporte, será EdgeTransport.

  - \<*Process identifier* o *IIS AppPool identifier\>* =Id. numérico del proceso.

  - *yyyymmdd* = es la hora UTC (hora universal coordinada) en que se ha creado el archivo de registro.

  - *nnnn* = número de instancia, que comienza en 1 para cada día.

Un nombre del archivo de registro de IRM es EdgeTransport\_1056\_IRMLOG20101201-1.log.

En la siguiente tabla se describen los registros generados en los roles de servidor diferentes.

### Registros en los roles de servidor

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de servidor</th>
<th>Nombre del archivo de registro de IRM</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servicio de transporte</p></td>
<td><p>EdgeTransport_&lt;<em>Process identifier</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>Este registro se usa para grabar todas las transacciones de RMS realizadas por la canalización de transporte en el servicio de transporte (por ejemplo, reglas de protección de transporte y descifrado de informes de diario). El identificador del proceso (PID) del proceso edgetransport.exe se usa para generar el nombre del archivo de registro.</p></td>
</tr>
<tr class="even">
<td><p>Buzón de correo</p></td>
<td><p>msftefd_&lt;<em>Process identifier</em>&gt;_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>El registro se usa para registrar todas las transacciones del RMS que ocurren durante las solicitudes de índice y búsqueda. Exchange 2013 Los servidores Buzón de correo usa el proceso msftefd.exe para la indización de contenido. El PID del proceso msftefd.exe se usa para generar el nombre del archivo de registro.</p></td>
</tr>
<tr class="odd">
<td><p>Acceso de cliente</p></td>
<td><p>w3wp_MSExchangeOWAAppOol_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>Este registro se usa para registrar todas las transacciones del IRM en Microsoft OfficeOutlook Web App.</p></td>
</tr>
<tr class="even">
<td><p>Todos los roles del servidor de Exchange 2013</p></td>
<td><p>w3wp_MSExchangePowerShellAppPool_IRMLOG<em>yyyymmdd</em>-<em>nnnn</em>.log</p></td>
<td><p>Este registro se usa para registrar todas las transacciones de IRM RMS emitidas desde Windows PowerShell, por ejemplo, al emitir el cmdlet <strong>Test-IRMConfiguration</strong>.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Proceso de registro

La información se escribe en el archivo de registro hasta que el tamaño del archivo alcanza el valor máximo especificado. Cuando se alcanza el tamaño máximo, se crea un registro de archivo que tiene un número de instancia incremental. Este proceso se repite durante el día. El registro circular elimina los archivos de registro más antiguos cuando el directorio de registro de IRM alcanza su tamaño máximo especificado o su antigüedad máxima especificada en la configuración de registro del IRM en cada servidor.

Volver al principio

## Información escrita en los registros de IRM

Los archivos de registro de IRM son archivos de texto que contienen datos en el formato de valores separados por comas (CSV). Cada registro de IRM tiene un encabezado que contiene la siguiente información:

  - **\#Software:** el nombre del software que creó el archivo de registro de IRM. Normalmente, el valor es `Microsoft Exchange Server`.

  - **\#Versión:** el número de versión del software que creó el archivo de registro de IRM.

  - **\#Log-type**   valor del tipo de registro, que es `Rms Client Manager Log`.

  - **\#Fecha:**   La fecha y la hora UTC en el momento de crearse el archivo. La fecha y la hora UTC se representa mediante el formato de fecha y hora conforme a ISO 8601: *yyyy*-*mm*-*dd*T*hh*:*mm*:*ss.fff*Z, donde:
    
      - yyyy = año
    
      - *mm* = mes
    
      - *dd* = día
    
      - T = designador de tiempo usado para mostrar el inicio del componente de tiempo
    
      - *hh* = hora
    
      - *mm* = minuto
    
      - *ss* = segunda
    
      - *fff* = fracciones de un segundo
    
      - Z = Zulu, que es otra forma de denotar UTC

  - **\#Campos:** los nombres de campos delimitados por comas que se usan en los archivos de registro del IRM.
    
    El registro de IRM almacena todos los eventos de transacciones RMS en una sola línea, organizada en campos separados por comas. En la siguiente tabla, se detallan los campos en los registros de IRM para todas las funciones del servidor que tienen las características IRM habilitadas.
    
    ### Campos usados en los registros IRM
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Campo</th>
    <th>Descripción</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Date-time</strong></p></td>
    <td><p>Muestra la marca de tiempo UTC.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Feature</strong></p></td>
    <td><p>Muestra la característica del cliente de RMS usada. Los valores válidos son:</p>
    <ul>
    <li><p><code>RacClc</code></p></li>
    <li><p><code>Template</code></p></li>
    <li><p><code>Prelicense</code></p></li>
    <li><p><code>UseLicense</code></p></li>
    <li><p>Comprobación de firma</p></li>
    <li><p><code>ServerInfo</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Event-Type</strong></p></td>
    <td><p>Muestra el tipo de evento. Los valores válidos son:</p>
    <ul>
    <li><p><code>Acquire</code>   Se solicita una licencia o plantilla de RMS.</p></li>
    <li><p><code>Success</code>   Se adquiere correctamente una licencia o plantilla de RMS.</p></li>
    <li><p><code>Exception</code>   Se ha producido un error.</p></li>
    <li><p><code>Queued</code>   Está pendiente una solicitud.</p></li>
    </ul></td>
    </tr>
    <tr class="even">
    <td><p><strong>Tenant-Id</strong></p></td>
    <td><p>Reservado para uso interno de Microsoft.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Server-url</strong></p></td>
    <td><p>Muestra la dirección URL del servidor de RMS al que se obtuvo acceso durante la operación.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Context</strong></p></td>
    <td><p>Usado por el proceso de que llama para enlazar varias transacciones de RMS juntas. Los valores válidos son:</p>
    <ul>
    <li><p><code>MessageID: &lt;Actual message ID&gt;</code></p></li>
    <li><p><code>MailboxGuid: &lt;Mailbox GUID&gt;</code></p></li>
    <li><p><code>AttachmentFileName: &lt;File name&gt;</code></p></li>
    </ul></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Transaction-id</strong></p></td>
    <td><p>Identifica una única transacción. Todos los eventos que suceden durante una transacción tienen el mismo Id. de transacción.</p></td>
    </tr>
    </tbody>
    </table>


Volver al principio

## Administración de registros de IRM

En cada rol de servidor que tiene las características de IRM habilitadas, el registro de IRM se habilita de forma predeterminada. Para cada rol de servidor, puede modificar la siguiente configuración de registro de IRM mediante el rol de servidor correspondiente al cmdlet **Set**. Por ejemplo, el cmdlet **Set-MailboxServer** se usa para configurar el registro de IRM de un servidor Buzón de servidores.

### Parámetros de configuración para registros IRM

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
<td><p><em>IrmLogEnabled</em></p></td>
<td><p>Habilita el registro de transacciones IRM. El registro de IRM está habilitado de forma predeterminada. Para deshabilitar el registro de IRM para una función de servidor, establezca el parámetro en <code>$false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxAge</em></p></td>
<td><p>Especifica la antigüedad máxima del archivo de registro de IRM. Los archivos anteriores a la antigüedad especificada se eliminan. El valor predeterminado es <code>30.00:00:00</code> (30 días).</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogMaxDirectorySize</em></p></td>
<td><p>Especifica el tamaño máximo de todos los registros de IRM del directorio de registro de conectividad. Cuando un directorio alcanza su tamaño de archivo máximo, el servidor elimina primero los archivos de registro más antiguos. El valor predeterminado es <code>250 MB</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>IrmLogMaxFileSize</em></p></td>
<td><p>Especifica el tamaño de archivo máximo para un único archivo de registro. Cuando el archivo alcanza el tamaño especificado, se crea un archivo de registro y aumenta el número de instancia. El valor predeterminado es <code>10 MB</code>.</p></td>
</tr>
<tr class="odd">
<td><p><em>IrmLogPath</em></p></td>
<td><p>Especifica la ubicación de registro de IRM. La ruta de acceso predeterminada es %ExchangeInstallPath%Logging\IRMLogs.</p></td>
</tr>
</tbody>
</table>


Para obtener información detallada acerca de la sintaxis y los parámetros, vea estos temas:

  - [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\))

  - [Set-ClientAccessServer](https://technet.microsoft.com/es-es/library/bb125157\(v=exchg.150\))

  - [Set-TransportService](https://technet.microsoft.com/es-es/library/jj215682\(v=exchg.150\))

Volver al principio

