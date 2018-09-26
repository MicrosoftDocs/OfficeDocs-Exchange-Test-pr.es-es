---
title: 'Administrar solicitudes de restauración de buzones: Exchange 2013 Help'
TOCTitle: Administrar solicitudes de restauración de buzones
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50556854
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar solicitudes de restauración de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Las solicitudes de restauración de buzones de correo se utilizan para restaurar buzones desconectados. Un buzón de correo desconectado es una base de datos de buzones de correo de Exchange que no está asociada con una cuenta de usuario de Active Directory. Los buzones se desconectan cuando está desactivados, eliminados o se mueven a otra base de datos. Para obtener más información, consulte [Buzones desconectados](disconnected-mailboxes-exchange-2013-help.md).

Los buzones desconectados permanecen en la base de datos del buzón de correo durante el plazo especificado en las configuraciones de retención de buzón eliminado de la base de datos de buzón. De forma predeterminada, los buzones desconectados se retienen durante 30 días. Durante este período de retención, los contenidos de un buzón eliminado se pueden restaurar (copiar) en un buzón existente. Este tema describe cómo usar el Shell para administrar las solicitudes de restauración de buzones de correo.

Para otras tareas de administración relacionadas con buzones de correo desconectados, consulte los siguientes temas:

[Deshabilitar o eliminar un buzón de correo](disable-or-delete-a-mailbox-exchange-2013-help.md)

[Conectar un buzón de correo deshabilitado](connect-a-disabled-mailbox-exchange-2013-help.md)

[Conectar o restaurar un buzón eliminado](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

[Restaurar un buzón eliminado temporalmente](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

[Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Solicitud de restauración de buzón" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Los procedimientos de este tema sólo pueden realizarse en el Shell. No puede utilizar el EAC para administrar las solicitudes de restauración del buzón.

  - Para mostrar el valor de la propiedad *Identity* de todas las solicitudes de restauración de buzones, ejecute el siguiente comando.
    
    ```powershell
    Get-MailboxRestoreRequest | Format-Table Identity
    ```
    
    Puede usar este valor de identidad para especificar una solicitud de restauración del buzón de correo específica al realizar los procedimientos de este tema.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para ver las propiedades de las solicitudes de restauración

Puede ver las propiedades de una solicitud de restauración de buzón, que le proporcionan la información básica acerca del estado de una solicitud de restauración de buzón.

Para mostrar una lista del valor de la propiedad *Identity* de todas las solicitudes de restauración de buzones, ejecute el siguiente comando.

```powershell
Get-MailboxRestoreRequest | Format-Table Identity
```

Puede usar la identidad para obtener información acerca de solicitudes de restauración de buzón concretas.

Este ejemplo devuelve el estado de la solicitud de restauración "Pilar Pinilla \\MailboxRestore" usando el parámetro *Identity*.

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"
```

Este ejemplo devuelve toda la información de la segunda solicitud de restauración del buzón de correo de destino Pilar Pinilla.

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List
```

Este ejemplo devuelve el estado de las solicitudes de restauración que se están restaurando de la base de datos de origen MBD01.

```powershell
Get-MailboxRestoreRequest -SourceDatabase MBD01
```

Este ejemplo devuelve todas las solicitudes de restauración que están actualmente en curso.

```powershell
Get-MailboxRestoreRequest -Status InProgress
```

Otros estados útiles incluyen `Queued`, `Completed`, `Suspended` y `Failed`.

Este ejemplo devuelve todas las solicitudes de restauración que han sido suspendidas.

```powershell
Get-MailboxRestoreRequest -Suspend $true
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829907\(v=exchg.150\)).

## Resultados de Get-MailboxRestoreRequest

De forma predeterminada, el cmdlet **Get-MailboxRestoreRequest** devuelve el nombre de la solicitud, el buzón de destino para el que se realiza la restauración y el estado de la solicitud. La siguiente tabla muestra una lista de la información útil que se devuelve si se canaliza el cmdlet al cmdlet **Format-List**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Especifica la base de datos que contiene el buzón desconectado en proceso de restauración.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetMailbox</code></p></td>
<td><p>Especifica el buzón en el que se están restaurando los datos.</p></td>
</tr>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Especifica el nombre de la solicitud.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Este valor especifica la base de datos en la que el Servicio de replicación de buzones de Exchange (MRS) almacena el estado detallado de la solicitud.</p></td>
</tr>
<tr class="odd">
<td><p><code>Status</code></p></td>
<td><p>Especifica el estado de la solicitud.</p></td>
</tr>
<tr class="even">
<td><p><code>Suspend</code></p></td>
<td><p>Especifica si se suspende la solicitud. Una restauración de buzón de correo se puede suspender si se crea usando el cmdlet <strong>New-MailboxRestoreRequest</strong> con el parámetro <em>Suspend</em>. También se puede suspender si la operación de restauración del buzón de correo falla o si un administrador usa el cmdlet <strong>Suspend-MailboxRestoreRequest</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Especifica la identidad de la solicitud. Esta identidad es una combinación del nombre del buzón de destino y el nombre de la solicitud.</p></td>
</tr>
</tbody>
</table>


## ¿Cómo saber si el proceso se ha completado correctamente?

Ejecute el cmdlet **Get-MailboxRestoreRequest** para verificar que puede ver las propiedades de las solicitudes de restauración del buzón. Si el cmdlet devuelve un error, verifique que usa la sintaxis y la identidad correctas. En algunos casos, puede que el cmdlet sea correcto y no devuelva resultados. Por ejemplo, si envió una solicitud de restauración de buzón de correo y ejecutó el comando `Get-MailboxRestoreRequest -Status InProgress` y no se devolvieron resultados, actualmente no se ejecuta ninguna de las solicitudes de restauración.

## Uso del Shell para ver las estadísticas de las solicitudes

Puede ver las estadísticas de una solicitud de restauración de buzón de correo, que le ofrecen información detallada que se puede usar para solucionar problemas.

En este ejemplo, se devuelven las estadísticas predeterminadas de la solicitud de restauración danp\\MailboxRestore1. De forma predeterminada, la información que se devuelve incluye el nombre, el buzón, el estado y el porcentaje completado.

```powershell
Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1
```

En este ejemplo se devuelven las estadísticas para el buzón de Dan Park y se exporta el informe a un archivo .csv.

```powershell
Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv
```

En este ejemplo, se devuelve información adicional acerca de la solicitud de restauración del buzón de Pilar Pinilla mediante el parámetro *IncludeReport* y canalizando los resultados al cmdlet **Format-List**.

```powershell
Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List 
```

En este ejemplo, se devuelve información adicional para todas las solicitudes de restauración con un estado de `Failed` mediante el parámetro *IncludeReport* y, a continuación, se guarda la información en el archivo AllRestoreReports.txt, en la ubicación en que se esté ejecutando el comando.

```powershell
Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt
```

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/es-es/library/ff829912\(v=exchg.150\)) y [Get-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829907\(v=exchg.150\)).

## Resultados de Get-MailboxRestoreRequestStatistics

De manera predeterminada, el cmdlet [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/es-es/library/ff829912\(v=exchg.150\)) devuelve el nombre de la solicitud, el estado de la solicitud, el alias del buzón de destino y el porcentaje completado. La siguiente tabla muestra una lista de la información útil que se devuelve si se canaliza el cmdlet al cmdlet **Format-List**.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Valor</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Name</code></p></td>
<td><p>Especifica el nombre de la solicitud.</p></td>
</tr>
<tr class="even">
<td><p><code>Status</code></p></td>
<td><p>Especifica el estado de la solicitud.</p></td>
</tr>
<tr class="odd">
<td><p><code>StatusDetail</code></p></td>
<td><p>Especifica más detalles sobre el estado de la solicitud. Por ejemplo, si el valor <code>Status</code> devuelve <code>InProgress</code>, el valor<code>StatusDetail</code> devolverá las etapas específicas para el estado <code>InProgress</code>, como <code>CreatingFolderHierarchy</code> y <code>CopyingMessages</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>SyncStage</code></p></td>
<td><p>Especifica cuán lejos está la solicitud mediante el proceso de restauración.</p></td>
</tr>
<tr class="odd">
<td><p><code>Suspend</code></p></td>
<td><p>Especifica si se suspende la solicitud de restauración. Este valor es <code>true</code> en las siguientes situaciones:</p>
<ul>
<li><p>MRS se detuvo o está en proceso de detener la solicitud debido a un error.</p></li>
<li><p>Un administrador suspendió la solicitud.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><code>SourceExchangeGuid</code></p></td>
<td><p>Especifica el GUID del buzón de origen desde el que se están restaurando los datos.</p></td>
</tr>
<tr class="odd">
<td><p><code>SourceRootFolder</code></p></td>
<td><p>Especifica el nombre de la carpeta raíz de la jerarquía del buzón de origen desde el que se están restaurando los datos. Si este valor está vacío, los datos se restauran desde la carpeta Principio del almacén de información.</p></td>
</tr>
<tr class="even">
<td><p><code>SourceDatabase</code></p></td>
<td><p>Especifica el nombre de la base de datos en la que está ubicado el buzón de origen.</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxRestoreFlags</code></p></td>
<td><p>Especifica que el buzón que se está restaurando es <code>Disabled</code> o <code>Soft-Deleted</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetAlias</code></p></td>
<td><p>Especifica el alias del buzón de correo de destino.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetIsArchive</code></p></td>
<td><p>Especifica si el buzón está siendo restaurado en un archivo.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetExchangeGuid</code></p></td>
<td><p>Especifica el GUID del buzón de correo de destino.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetRootFolder</code></p></td>
<td><p>Especifica el nombre de la carpeta raíz de la jerarquía del buzón de origen en la que se están restaurando los datos. Si este valor está vacío, los datos se restauran en la carpeta Principio del almacén de información.</p></td>
</tr>
<tr class="even">
<td><p><code>TargetDatabase</code></p></td>
<td><p>Especifica el nombre de la base de datos en la que está ubicado el buzón de destino.</p></td>
</tr>
<tr class="odd">
<td><p><code>TargetMailboxIdentity</code></p></td>
<td><p>Especifica la identidad de los buzones de correo de destino.</p></td>
</tr>
<tr class="even">
<td><p><code>IncludeFolders</code></p></td>
<td><p>Especifica la lista de carpetas para incluir durante la restauración. Si este valor se encuentra en blanco, no se especificó ninguna carpeta al crearse la solicitud y se restaurarán todas las carpetas en el buzón de correo (salvo que se use el parámetro <em>ExcludeFolders</em> para excluir carpetas específicas).</p></td>
</tr>
<tr class="odd">
<td><p><code>ExcludeFolders</code></p></td>
<td><p>Especifica la lista de carpetas para excluir durante la restauración. Si este valor se encuentra en blanco, no se especificó ninguna carpeta al crearse la solicitud y se restaurarán todas las carpetas en el buzón de correo (salvo que se use el parámetro <em>IncludeFolders</em> para incluir carpetas específicas).</p></td>
</tr>
<tr class="even">
<td><p><code>ExcludeDumpster</code></p></td>
<td><p>Este valor especifica si la carpeta de elementos recuperables se excluyó al crearse la solicitud.</p></td>
</tr>
<tr class="odd">
<td><p><code>ConflictResolutionOption</code></p></td>
<td><p>Especifica la acción que MRS debe realizar si hay mensajes que coinciden en las carpetas de destino y de origen.</p></td>
</tr>
<tr class="even">
<td><p><code>AssociatedMessagesCopyOption</code></p></td>
<td><p>Especifica si se copian los mensajes asociados cuando se procesa la solicitud. Los mensajes asociados son mensajes especiales que contienen datos ocultos con información sobre reglas, vistas y formularios.</p></td>
</tr>
<tr class="odd">
<td><p><code>BadItemLimit</code></p></td>
<td><p>Especifica el número de elementos incorrectos que MRS omitirá si la solicitud encuentra mensajes dañados.</p></td>
</tr>
<tr class="even">
<td><p><code>BadItemsEncountered</code></p></td>
<td><p>Especifica el número de mensajes dañados encontrados por el comando. Si el valor <em>BadItemsEncountered</em> es mayor que el valor <em>BadItemLimit</em>, la solicitud produce un error.</p></td>
</tr>
<tr class="odd">
<td><p><code>QueuedTimeStamp</code></p></td>
<td><p>Especifica la fecha y la hora en la que se inició la solicitud para MRS.</p></td>
</tr>
<tr class="even">
<td><p><code>StartTimeStamp</code></p></td>
<td><p>Especifica la fecha y la hora en que MRS empezó a procesar la solicitud de restauración.</p></td>
</tr>
<tr class="odd">
<td><p><code>LastUpdateTimeStamp</code></p></td>
<td><p>Especifica la fecha y la hora en que se realizó el último cambio en la solicitud. El cambio puede haber sido realizado por un administrador o por MRS.</p></td>
</tr>
<tr class="even">
<td><p><code>SuspendTimeStamp</code></p></td>
<td><p>Especifica la fecha y la hora en que se suspendió la solicitud.</p></td>
</tr>
<tr class="odd">
<td><p><code>OverallDuration</code></p></td>
<td><p>Especifica la cantidad de tiempo que llevó completar la solicitud. Si la solicitud se encuentra en un estado <code>Failed</code>, este valor especifica la cantidad de tiempo entre el inicio y el error de la solicitud. Si la solicitud no se ha completado, este valor especifica la cantidad de tiempo entre el inicio de la solicitud y la ejecución del cmdlet <strong>Get-MailboxRestoreRequestStatistics</strong>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalSuspendedDuration</code></p></td>
<td><p>Especifica la cantidad de tiempo que la solicitud estuvo en estado <code>Suspended</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalFailedDuration</code></p></td>
<td><p>Especifica la cantidad de tiempo que la solicitud estuvo en estado <code>Failed</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalQueuedDuration</code></p></td>
<td><p>Especifica la cantidad de tiempo que la solicitud estuvo en estado <code>Queued</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>TotalInProgressDuration</code></p></td>
<td><p>Especifica la cantidad de tiempo que la solicitud estuvo en estado <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>TotalStalledDueToHADuration</code></p></td>
<td><p>Especifica la cantidad de tiempo que la solicitud se detuvo debido a una alta disponibilidad.</p></td>
</tr>
<tr class="odd">
<td><p><code>MRSServerName</code></p></td>
<td><p>Especifica el nombre del servidor de acceso de cliente que procesó la solicitud.</p></td>
</tr>
<tr class="even">
<td><p><code>EstimatedTransferSize</code></p></td>
<td><p>Especifica el tamaño de archivo que se restauró o el tamaño de archivo que MRS espera restaurar si la solicitud está en el estado <code>In Progress</code>.</p></td>
</tr>
<tr class="odd">
<td><p><code>EstimatedTransferItemCount</code></p></td>
<td><p>Especifica el número de elementos que se restauraron o el número de elementos que MRS espera restaurar si la solicitud se encuentra en el estado <code>In Progress</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>BytesTransferredPerMinute</code></p></td>
<td><p>Especifica el número promedio de bytes que se transfirieron por minuto.</p></td>
</tr>
<tr class="odd">
<td><p><code>ItemsTransferred</code></p></td>
<td><p>Especifica el número de elementos que se han transferido.</p></td>
</tr>
<tr class="even">
<td><p><code>PercentComplete</code></p></td>
<td><p>Especifica el porcentaje de la solicitud que se ha completado.</p></td>
</tr>
<tr class="odd">
<td><p><code>CompletedRequestAgeLimit</code></p></td>
<td><p>Especifica el tiempo en que se retendrá una solicitud de restauración antes de que se elimine. El valor predeterminado es 30 días.</p></td>
</tr>
<tr class="even">
<td><p><code>PositionInQueue</code></p></td>
<td><p>Si la solicitud no se ha iniciado, este valor especifica la posición de la solicitud en la cola.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureCode</code></p></td>
<td><p>Si se ha producido un error, este valor especifica el código de error.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureType</code></p></td>
<td><p>Si se ha producido un error, este valor especifica el tipo de error.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureSide</code></p></td>
<td><p>Si hay un error, este valor especifica si el error ocurrió en el buzón de destino o en el buzón de origen.</p></td>
</tr>
<tr class="even">
<td><p><code>Message</code></p></td>
<td><p>Si se ha producido un error, este valor especifica el mensaje de error. Este valor también puede especificar el comentario de suspensión.</p></td>
</tr>
<tr class="odd">
<td><p><code>FailureTimestamp</code></p></td>
<td><p>Si se produjeron errores en la solicitud, este valor especifica la fecha y la hora en que se produjeron errores en la solicitud.</p></td>
</tr>
<tr class="even">
<td><p><code>FailureContext</code></p></td>
<td><p>Si la solicitud falló, este valor especifica la información acerca de la acción que se está realizando al momento del error.</p></td>
</tr>
<tr class="odd">
<td><p><code>ValidationMessage</code></p></td>
<td><p>Si la solicitud no es válida, este valor especifica el motivo.</p></td>
</tr>
<tr class="even">
<td><p><code>RequestQueue</code></p></td>
<td><p>Especifica la base de datos en la que MRS almacena el estado detallado de la solicitud.</p></td>
</tr>
<tr class="odd">
<td><p><code>Identity</code></p></td>
<td><p>Especifica la identidad de la solicitud.</p></td>
</tr>
<tr class="even">
<td><p><code>Report</code></p></td>
<td><p>Si usó el parámetro <em>IncludeReport</em>, este valor especifica la información que se puede usar para solucionar el problema de la solicitud.</p></td>
</tr>
</tbody>
</table>


## ¿Cómo saber si el proceso se ha completado correctamente?

Ejecute el cmdlet **Get-MailboxRestoreRequestStatistics** para verificar que puede ver las estadísticas de las solicitudes de restauración del buzón. Si el cmdlet devuelve un error, verifique que usa la identidad correcta para la solicitud de restauración.

## Usar el Shell para cambiar las propiedades de las solicitudes de restauración

Si una solicitud de restauración de buzón de correo falla, puede usar el cmdlet **Set-MailboxRestoreRequest** para cambiar las propiedades de la solicitud para intentar recuperarse del fallo.

En este ejemplo se especifica que la solicitud de restauración MailboxRestore1 para el buzón de Debra Garcia omite 10 elementos dañados de buzón.

```powershell
Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10
```

En este ejemplo se especifica que la solicitud de restauración MailboxRestore1 para el buzón de Florence Flipo omite 100 elementos dañados. Puesto que el valor de *BadItemLimit* es mayor que 50, se debe especificar el parámetro *AcceptLargeDataLoss*.

```powershell
Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829909\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya cambiado correctamente las propiedades de una solicitud de restauración, ejecute el cmdlet **Get-MailboxRestoreRequestStatistics** para mostrar las propiedades revisadas de la solicitud de restauración. Si la solicitud de restauración se creó correctamente, la propiedad *Status* tendrá un valor de `Queued`, `InProgress` o `Completed`. Una vez completada la solicitud de restauración, los contenidos del buzón de correo eliminados temporalmente aparecerán en el buzón de correo de destino.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/es-es/library/ff829912\(v=exchg.150\)).

## Usar la consola para suspender una solicitud de restauración

Es posible suspender una solicitud de restauración en cualquier momento después de crear la solicitud, pero antes de que llegue al estado `Completed`. Consulte Usar la consola para reanudar una solicitud de restauración más adelante en este tema acerca de la sintaxis del comando para reanudar la solicitud de restauración con el cmdlet [Resume-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829908\(v=exchg.150\)).

En este ejemplo se suspende la solicitud de restauración MailboxRestore1 buzón de correo de Pilar Pinilla.

```powershell
Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

En este ejemplo se suspenden todas las solicitudes de restauración en curso recuperando primero todas las solicitudes que tienen el estado `InProgress` y, a continuación canalizando los resultados al cmdlet **Suspend-MailboxRestoreRequest** e incluyendo el comentario de suspensión "Reanudar después del mantenimiento FY13Q2."

```powershell
Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Suspend-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829906\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya suspendido correctamente una solicitud de restauración de buzón de correo, ejecute el siguiente comando.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

Si el valor de la propiedad *Suspend* es igual a `True`, la solicitud de restauración se suspendió correctamente. Además, un valor de `Suspended` de la propiedad *Status* indica que la solicitud de restauración se suspendió.

## Usar la consola para reanudar una solicitud de restauración

Utilice el cmdlet **Resume-MailboxRestoreRequest** para reanudar una solicitud de restauración suspendida o que dio error.

En este ejemplo se reanuda la petición de restauración Pilar Pinilla\\MailboxRestore1.

```powershell
Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

En este ejemplo se reanudan todas las solicitudes de restauración que tengan el estado Error.

```powershell
Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Resume-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829908\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se ha reanudado una solicitud de restauración, ejecute el siguiente comando.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

Si el valor de la propiedad *Suspend* es igual a `False`, la solicitud de restauración se reanudó correctamente. Además, un valor de `InProgress` de la propiedad *Status* indica que la solicitud de restauración se reanudó.

## Usar el Shell para quitar una solicitud de restauración

Puede usar el cmdlet **Remove-MailboxRestoreRequest** para quitar solicitudes de restauración de buzones de correo. Si quita una solicitud de restauración después de que los datos del buzón comienzan a copiarse al buzón de destino, los datos del buzón que se copian permanecen en el buzón de destino.


> [!NOTE]
> Como se indicó anteriormente, las solicitudes de restauración completadas se retienen durante 30 días de forma predeterminada antes de que se eliminen automáticamente.



Este ejemplo elimina la petición de restauración Pilar Pinilla\\MailboxRestore1.

```powershell
Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

En este ejemplo se quitan todas las solicitudes de restauración que tengan el estado Completado.

```powershell
Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
```

En este ejemplo se cancela la solicitud de restauración mediante el parámetro *RequestGuid* para una solicitud almacenada en MBXDB01. El conjunto de parámetros que requiere los parámetros *RequestGuid* y *RequestQueue* sólo se utiliza para fines de depuración de Microsoft Replication Service. Utilice este conjunto de parámetros exclusivamente si se lo indica el Servicio de soporte técnico y atención al cliente de Microsoft.

```powershell
Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829910\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya eliminado correctamente una solicitud de restauración de buzón de correo, ejecute el siguiente comando.

```powershell
Get-MailboxRestoreRequest -Identity <identity of removed restore request>
```

El comando devolverá un error que indique que la solicitud de restauración no existe.

También puede ejecutar el cmdlet **Get-MailboxRestoreRequest**. Si una solicitud de restauración no se eliminó correctamente, no se incluirá en los resultados.

