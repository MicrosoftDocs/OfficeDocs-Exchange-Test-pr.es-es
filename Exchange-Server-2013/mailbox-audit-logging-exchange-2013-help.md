---
title: 'Registro de auditoría de buzones de correo: Exchange 2013 Help'
TOCTitle: Registro de auditoría de buzones de correo
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 49895532
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Registro de auditoría de buzones de correo

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Dado que los buzones de correo pueden contener información confidencial y de alto impacto comercial, así como información de identificación personal, es importante realizar un seguimiento de quién inicia sesión en los buzones de la organización y qué acciones se llevan a cabo. Es especialmente importante que lleve un seguimiento del acceso a los buzones por parte de usuarios que no sean el propietario del buzón en cuestión. Estos usuarios se denominan *usuarios delegados*.

Mediante el *registro de auditoría de buzón*, puede registrar el acceso a buzones por parte de los propietarios, los delegados (incluidos los administradores con permisos de acceso completo a los buzones) y los administradores de los buzones.

Al habilitar el registro de auditoría para un buzón de correo, se pueden especificar las acciones de usuario (por ejemplo, acceso, traslado o eliminación de mensajes) que se registrarán para un tipo de inicio de sesión (administrador, usuario delegado o propietario). Las entradas del registro de auditoría también incluyen información importante, tal como la dirección IP del cliente, el nombre de host y el proceso o cliente utilizado para acceder al buzón. Para los elementos movidos, la entrada incluye el nombre de la carpeta de destino.

## Registros de auditoría de buzón de correo

Los registros de auditoría de buzón se generan para cada buzón que tenga habilitado el registro de auditoría de buzón. Las entradas del registro se almacenan en la carpeta de elementos recuperables en el buzón auditado, en la subcarpeta Auditorías. Esto garantiza que las entradas del registro de auditoría estén disponibles en una ubicación única, independientemente del método de acceso del cliente que se haya usado para acceder al buzón o del servidor o estación de trabajo que un administrador haya usado para acceder al registro de auditoría de buzón. Si mueve un buzón de correo a otro servidor de buzones de correo, también se moverán los registros de auditoría de buzón pertinentes porque se encuentran en el buzón de correo.

De forma predeterminada, las entradas de un registro de auditoría de buzón se conservan en el buzón de correo durante 90 días y luego se eliminan. Puede modificar este período de retención con el parámetro *AuditLogAgeLimit* del cmdlet [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)). Si un buzón está en retención en contexto o en retención por juicio, las entradas del registro de auditoría solo se conservarán hasta que se haya alcanzado el período de retención del registro de auditoría de buzón. Para conservar entradas de auditoría durante más tiempo, tiene que aumentar el período de retención cambiando el valor para el parámetro *AuditLogAgeLimit*. También puede exportar entradas del registro de auditoría antes de que se alcance el período de retención. Para obtener más información, vea:

  - [Exportar registros de auditoría de buzones](export-mailbox-audit-logs-exchange-2013-help.md)

  - [Crear una búsqueda en los registros de auditoría de buzones](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## Habilitación del registro de auditoría de buzón

El registro de auditoría de buzón se habilita por buzón de correo. El cmdlet **Set-Mailbox** permite habilitar o deshabilitar el registro de auditoría de buzón. Para obtener más información, vea [Habilitar o deshabilitar el registro de auditoría de buzones para un buzón](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

Al habilitar el registro de auditoría de buzón en un buzón de correo, el acceso al buzón de correo y algunas acciones realizadas por los administradores y delegados se registran de forma predeterminada. Para registrar las acciones que lleva a cabo el propietario del buzón de correo, es necesario especificar las acciones de propietario que se deben auditar.

## Acciones de buzón de correo registradas por el registro de auditoría de buzón

En la siguiente tabla se enumeran las acciones registradas por el registro de auditoría de buzón de correo, incluidos los tipos de inicio de sesión para los que se puede registrar la acción.


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Acción</th>
<th>Descripción</th>
<th>Administrador</th>
<th>Delegado</th>
<th>Propietario</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Copiar</p></td>
<td><p>Se copia un elemento en otra carpeta.</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Create</p></td>
<td><p>Se crea un elemento en la carpeta Calendario, Contactos, Notas o Tareas en el buzón. Por ejemplo, se crea una nueva convocatoria de reunión. Tenga en cuenta que la creación de carpetas o mensajes no se audita.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>FolderBind</p></td>
<td><p>Se obtiene acceso a una carpeta de buzón de correo.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí**</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>HardDelete</p></td>
<td><p>Se elimina un elemento de la carpeta Elementos recuperables de forma permanente.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>MessageBind</p></td>
<td><p>Se abre o se obtiene acceso a un elemento desde el panel de lectura.</p></td>
<td><p>Sí</p></td>
<td><p>No</p></td>
<td><p>No</p></td>
</tr>
<tr class="even">
<td><p>Mover</p></td>
<td><p>Se mueve un elemento a otra carpeta.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>MoveToDeletedItems</p></td>
<td><p>Se mueve un elemento a la carpeta Elementos eliminados.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="even">
<td><p>SendAs</p></td>
<td><p>Se envía un mensaje con los permisos Enviar como.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="odd">
<td><p>SendOnBehalf</p></td>
<td><p>Se envía un mensaje con los permisos Enviar en nombre de.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
<td><p>No aplicable</p></td>
</tr>
<tr class="even">
<td><p>SoftDelete</p></td>
<td><p>Se elimina un elemento de la carpeta Elementos eliminados.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
<tr class="odd">
<td><p>Actualizar</p></td>
<td><p>Se actualizan las propiedades de un elemento.</p></td>
<td><p>Sí*</p></td>
<td><p>Sí*</p></td>
<td><p>Sí</p></td>
</tr>
</tbody>
</table>


\* Se audita de forma predeterminada si la auditoría está habilitada para el buzón en cuestión.

\*\* Se consolidan las entradas de las acciones de enlace de carpeta realizadas por delegados. Se genera una entrada de registro para el acceso a cada carpeta en un plazo de 24 horas.

Si ya no necesita que se auditen determinados tipos de acciones de buzón de correo, tendrá que modificar la configuración de registro de auditoría del buzón para deshabilitarlas. Las entradas de registro existentes no se purgan hasta que se ha alcanzado el límite de antigüedad de las entradas del registro de auditaría.

## Realización de búsquedas en entradas de registro de auditoría de buzón

Puede usar los métodos indicados a continuación para buscar entradas del registro de auditoría de buzón:

  - **Buscar en un único buzón de forma sincrónica**   Use el cmdlet [Search-MailboxAuditLog](https://technet.microsoft.com/es-es/library/ff522360\(v=exchg.150\)) para buscar de forma sincrónica las entradas de registro de auditoría de buzón en un único buzón de correo. El cmdlet muestra los resultados de la búsqueda en la ventana del Shell de administración de Exchange. Para obtener información detallada, vea [Buscar el registro de auditoría de un buzón](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

  - **Buscar en uno o más buzones de forma asincrónica**   Cree una búsqueda de registros de auditoría de buzón para buscar de forma asincrónica registros de auditoría de buzón en uno o más buzones de correo y, a continuación, envíe los resultados de la búsqueda a una dirección de correo electrónico especificada. Los resultados de la búsqueda se envían como datos adjuntos XML. Para crear la búsqueda, use el cmdlet [New-MailboxAuditLogSearch](https://technet.microsoft.com/es-es/library/ff522362\(v=exchg.150\)). Para obtener más información, vea [Crear una búsqueda en los registros de auditoría de buzones](create-a-mailbox-audit-log-search-exchange-2013-help.md).

  - **Usar informes de auditoría en el Centro de administración de Exchange (EAC):** puede usar la pestaña **Auditoría** en el EAC para ejecutar un informe de acceso al buzón de correo del que no se es propietario o para exportar entradas del registro de auditoría de buzón. Para más información detallada, vea:
    
      - [Ejecución de un informe de acceso al buzón de correo del que no se es propietario](run-a-non-owner-mailbox-access-report-exchange-online-help.md)
    
      - [Exportar registros de auditoría de buzones](export-mailbox-audit-logs-exchange-2013-help.md)

## Entradas de registro de auditoría de buzón

En la siguiente tabla se describen los campos registrados en una entrada del registro de auditoría de buzón.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Campo</th>
<th>Se rellena con</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Operation</strong></p></td>
<td><p>Una de las acciones siguientes:</p>
<ul>
<li><p>Copiar</p></li>
<li><p>Crear</p></li>
<li><p>FolderBind</p></li>
<li><p>HardDelete</p></li>
<li><p>MessageBind</p></li>
<li><p>Mover</p></li>
<li><p>MoveToDeletedItems</p></li>
<li><p>SendAs</p></li>
<li><p>SendOnBehalf</p></li>
<li><p>SoftDelete</p></li>
<li><p>Update</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>OperationResult</strong></p></td>
<td><p>Uno de los resultados siguientes:</p>
<ul>
<li><p>Failed</p></li>
<li><p>PartiallySucceeded</p></li>
<li><p>Succeeded</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>LogonType</strong></p></td>
<td><p>Tipo de inicio de sesión del usuario que realizó la operación. Entre los tipos de inicio de sesión, se incluyen:</p>
<ul>
<li><p>Propietario</p></li>
<li><p>Delegado</p></li>
<li><p>Administrador</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>DestFolderId</strong></p></td>
<td><p>GUID de la carpeta de destino para las operaciones de movimiento.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestFolderPathName</strong></p></td>
<td><p>Ruta de acceso de la carpeta de destino para las operaciones de movimiento.</p></td>
</tr>
<tr class="even">
<td><p><strong>FolderId</strong></p></td>
<td><p>GUID de la carpeta.</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderPathName</strong></p></td>
<td><p>Ruta de acceso de la carpeta.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientInfoString</strong></p></td>
<td><p>Detalles que identifican qué cliente o qué componente de Exchange realizó la operación.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientIPAddress</strong></p></td>
<td><p>Dirección IP del equipo cliente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientMachineName</strong></p></td>
<td><p>Nombre del equipo cliente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ClientProcessName</strong></p></td>
<td><p>Nombre del proceso de la aplicación cliente.</p></td>
</tr>
<tr class="even">
<td><p><strong>ClientVersion</strong></p></td>
<td><p>Versión de la aplicación cliente.</p></td>
</tr>
<tr class="odd">
<td><p><strong>InternalLogonType</strong></p></td>
<td><p>Tipo de inicio de sesión del usuario que realizó la operación. Entre los tipos de inicio de sesión, se incluyen:</p>
<ul>
<li><p>Propietario</p></li>
<li><p>Delegado</p></li>
<li><p>Administrador</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>MailboxOwnerUPN</strong></p></td>
<td><p>Nombre principal de usuario (UPN) del propietario del buzón.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxOwnerSid</strong></p></td>
<td><p>Identificador de seguridad del propietario del buzón (SID).</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerUPN</strong></p></td>
<td><p>Nombre principal de usuario (UPN) del propietario del buzón de destino, registrado para operaciones entre buzones.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DestMailboxOwnerSid</strong></p></td>
<td><p>SID del propietario del buzón de destino, registrado para operaciones entre buzones.</p></td>
</tr>
<tr class="even">
<td><p><strong>DestMailboxOwnerGuid</strong></p></td>
<td><p>GUID del propietario del buzón de destino.</p></td>
</tr>
<tr class="odd">
<td><p><strong>CrossMailboxOperation</strong></p></td>
<td><p>Información sobre si la operación registrada es una operación entre buzones (por ejemplo, copiar o mover mensajes entre buzones).</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserDisplayName</strong></p></td>
<td><p>Nombre para mostrar del usuario que ha iniciado sesión.</p></td>
</tr>
<tr class="odd">
<td><p><strong>DelegateUserDisplayName</strong></p></td>
<td><p>Nombre para mostrar del usuario delegado.</p></td>
</tr>
<tr class="even">
<td><p><strong>LogonUserSid</strong></p></td>
<td><p>SID del usuario que ha iniciado sesión.</p></td>
</tr>
<tr class="odd">
<td><p><strong>SourceItems</strong></p></td>
<td><p>Identificador de elemento de los elementos de buzón donde se haya realizado la acción registrada (por ejemplo, mover o eliminar). Para las operaciones realizados en varios elementos, este campo se devuelve como un conjunto de elementos.</p></td>
</tr>
<tr class="even">
<td><p><strong>SourceFolders</strong></p></td>
<td><p>GUID de la carpeta de origen.</p></td>
</tr>
<tr class="odd">
<td><p><strong>ItemId</strong></p></td>
<td><p>Identificador del elemento.</p></td>
</tr>
<tr class="even">
<td><p><strong>ItemSubject</strong></p></td>
<td><p>Asunto del elemento.</p></td>
</tr>
<tr class="odd">
<td><p><strong>MailboxGuid</strong></p></td>
<td><p>GUID del buzón.</p></td>
</tr>
<tr class="even">
<td><p><strong>MailboxResolvedOwnerName</strong></p></td>
<td><p>Nombre resuelto del usuario de buzón con el formato <em>DOMINIO</em>\<em>NombreCuentaSam</em>.</p></td>
</tr>
<tr class="odd">
<td><p><strong>LastAccessed</strong></p></td>
<td><p>Hora en que se realizó la operación.</p></td>
</tr>
<tr class="even">
<td><p><strong>Identity</strong></p></td>
<td><p>Identificador de entrada de registro de auditoría.</p></td>
</tr>
</tbody>
</table>


## Más información

  - **Acceso de administrador a los buzones:** se considera que un administrador accede a los buzones solo en los siguientes escenarios:
    
      - [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md) si se usa para realizar búsquedas en un buzón.
    
      - El cmdlet [New-MailboxExportRequest](https://technet.microsoft.com/es-es/library/ff607299\(v=exchg.150\)) se usa para exportar un buzón de correo.
    
      - [Microsoft Exchange Server MAPI Editor](https://go.microsoft.com/fwlink/p/?linkid=204086) se usa para acceder al buzón de correo.

  - **Omisión del registro de auditoría del buzón:** el acceso a buzones mediante procesos automatizados autorizados, tales como cuentas utilizadas por herramientas de terceros o por controles legales, puede crear una gran cantidad de entradas de registro de auditoría de buzón que, posiblemente, no sean importantes para la organización. Puede configurar estas cuentas para que se omita el registro de auditoría de buzón. Para obtener más información, vea [Omitir una cuenta de usuario desde el registro de auditoría de buzones](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md).

  - **Registro de acciones del propietario del buzón:** para buzones como el Buzón de búsqueda de detección, que pueden contener información más confidencial, considere la posibilidad de habilitar el registro de auditoría de buzón para las acciones del propietario del buzón de correo, como la eliminación de mensajes.

Registros de auditoría de buzón de correo

