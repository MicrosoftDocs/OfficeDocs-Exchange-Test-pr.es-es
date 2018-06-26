---
title: 'Buzones desconectados: Exchange 2013 Help'
TOCTitle: Buzones desconectados
ms:assetid: 508ebe2b-387d-4867-bdb0-028ef351ce56
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232039(v=EXCHG.150)
ms:contentKeyID: 50556802
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Buzones desconectados

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Cada buzón de correo de Microsoft Exchange está compuesto por una cuenta de usuario de Active Directory y los datos de buzón de correo almacenados en la base de datos de buzones de correo de Exchange. Todos los datos de configuración de un buzón se almacenan en los atributos de Exchange del objeto de usuario de Active Directory. La base de datos de buzones de correo contiene los datos de correo que se encuentran en el buzón de correo asociado a la cuenta de usuario. En la siguiente figura, se muestran los componentes de un buzón de correo.

**Componentes del buzón de correo**

![Partes que componen un buzón](images/Bb201680.5fcb5e6d-656e-42ae-871f-0eef8aea456b(EXCHG.150).gif "Partes que componen un buzón")

Un *buzón desconectado* es un objeto de buzón de la base de datos de buzones de correo que no está asociado con una cuenta de usuario de Active Directory. Existen dos tipos de buzones desconectados:

  - **Buzones deshabilitados**   Cuando se deshabilita o se elimina un buzón de correo en el Centro de administración de Exchange (EAC) o con los cmdlet **Disable-Mailbox** o **Remove-Mailbox** en el Shell de administración de Exchange, Exchange conserva el buzón de correo eliminado en la base de datos de buzones de correo, y cambia el estado del buzón de correo a deshabilitado. Es por eso que los buzones de correo deshabilitados o eliminados se denominan *buzones deshabilitados*. La diferencia es que, cuando deshabilita un buzón de correo, los atributos de Exchange se eliminan de la cuenta de usuario de Active Directory correspondiente, pero la cuenta de usuario se conserva. Cuando elimina un buzón de correo, tanto los atributos de Exchange como la cuenta de usuario de Active Directory se eliminan.
    
    Los buzones de correo deshabilitados y eliminados se conservan en la base de datos de buzones de correo hasta que expira el período de retención del buzón de correo eliminado, que, de manera predeterminada, es de 30 días. Una vez que el período de retención expira, el buzón de correo de elimina permanentemente (lo que también se denomina *purga*). Si el buzón de correo se elimina con el cmdlet **Remove-Mailbox**, también se conserva durante el período de retención.
    

    > [!IMPORTANT]
    > Si el buzón se elimina con el cmdlet <STRONG>Remove-Mailbox</STRONG> y el parámetro <EM>Permanent</EM> o <EM>StoreMailboxIdentity</EM>, se eliminará inmediatamente de la base de datos de buzones de correo.

    
    Para identificar los buzones deshabilitados en su organización, ejecute el siguiente comando en el Shell.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "Disabled" } | ft DisplayName,Database,DisconnectDate

  - **Buzones de correo eliminados temporalmente**   Cuando un buzón de correo se mueve a una base de datos de buzones de correo diferente, Exchange no lo elimina totalmente de la base de datos de buzones de correo de origen cuando el movimiento finaliza. En lugar de hacer eso, el buzón de la base de datos de buzones de correo de origen cambia a un estado de *eliminación temporal*. Al igual que los buzones deshabilitados, los buzones eliminados temporalmente se conservan en la base de datos de origen hasta que expira el período de retención del buzón de correo o hasta que se usa el cmdlet **Remove-StoreMailbox** para purgar el buzón.
    
    Ejecute el siguiente comando para identificar todos los buzones de correo eliminados temporalmente en su organización.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | ft DisplayName,Database,DisconnectDate

**Contenido**

Cómo trabajar con buzones de correo deshabilitados

Cómo trabajar con buzones de archivo deshabilitados

Cómo trabajar con buzones de correo eliminados temporalmente

Resumen de cómo trabajar con buzones de correo desconectados

Documentación de buzón desconectado

## Cómo trabajar con buzones de correo deshabilitados

Es posible realizar varias operaciones en un buzón de correo deshabilitado antes de su purga de la base de datos de buzones de correo:

  - Volver a conectarlo a la misma cuenta de usuario.

  - Conectarlo a una cuenta de usuario diferente que no esté habilitada para correo, lo que significa que la cuenta de usuario no tiene un buzón de correo.

  - Restaurarla a una cuenta de usuario que tenga un buzón existente. Por ejemplo, si un usuario cuyo buzón de correo se eliminó tiene un nuevo buzón de correo, puede restaurar el buzón deshabilitado del usuario a su nuevo buzón.

  - Eliminarlo de forma permanente de la base de datos de buzones de correo de Exchange.

## Conexión o restauración de un buzón de correo deshabilitado

A continuación, se muestran escenarios en los que puede que desee conectar o restaurar un buzón de correo deshabilitado antes de que expire el período de retención del buzón de correo o de que este se elimine de manera permanente:

  - Ha deshabilitado un buzón de correo y ahora desea reconectarlo a la misma cuenta de usuario de Active Directory.

  - Ha eliminado un buzón de correo mediante el EAC o el cmdlet [Remove-Mailbox](https://technet.microsoft.com/es-es/library/aa995948\(v=exchg.150\)) y ahora desea reconectarlo a otra cuenta de usuario de Active Directory distinta.

  - Ha eliminado un buzón de correo y ahora desea restaurarlo a un buzón de correo existente. Por ejemplo, si un usuario cuyo buzón de correo se eliminó tiene un nuevo buzón de correo, puede restaurar el buzón deshabilitado del usuario a su nuevo buzón.

  - Desea convertir un buzón de correo de usuario en un buzón de correo vinculado asociado con una cuenta de usuario externa al bosque en el que se encuentra la organización de Exchange. El escenario del bosque de recursos es un ejemplo de cuando desea asociar un buzón con una cuenta externa. En este escenario, los objetos de usuario del bosque de Exchange tienen buzones de correo, pero los objetos de usuario están deshabilitados para el inicio de sesión. Debe asociar un buzón de correo en el bosque de Exchange con una cuenta de usuario en el bosque de cuenta externa.

Existen dos maneras de reconectar o restaurar un buzón de correo deshabilitado. El primer método es usar el EAC o el cmdlet **Connect-Mailbox** para conectar un buzón de correo deshabilitado a una cuenta de usuario. Para conocer los procedimientos para reconectar buzones de correo deshabilitados, vea [Conectar un buzón de correo deshabilitado](connect-a-disabled-mailbox-exchange-2013-help.md).

El segundo método usa el cmdlet **New-MailboxRestoreRequest** para unificar el contenido del buzón de datos deshabilitado con un buzón de correo existente. Este cmdlet usa el Servicio de replicación de buzones (MRS) para restaurar el buzón de correo. Para conocer los procedimientos para restaurar buzones de correo deshabilitados, vea [Conectar o restaurar un buzón eliminado](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md).

## Eliminación permanente de un buzón de correo deshabilitado

Como se mencionó antes, Exchange retiene los buzones deshabilitados en la base de datos de buzones de correo según la configuración de retención de buzones eliminados definida para la base de datos de buzones de correo en cuestión. Una vez transcurrido el período de retención especificado, un buzón deshabilitado se purga de la base de datos de buzones de correo de Exchange. También puede eliminar de manera permanente un buzón de correo deshabilitado y todo el contenido de sus mensajes de la base de datos de buzones de correo con el cmdlet **Remove-StoreMailbox**. Una vez que un administrador elimina de manera permanente un buzón de correo deshabilitado o este se purga automáticamente, la pérdida de datos es permanente y el buzón no puede recuperarse.

Para obtener más información, vea [Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md).

Cómo trabajar con buzones de correo deshabilitados

## Cómo trabajar con buzones de archivo deshabilitados

Los buzones de archivo personales se desconectan cuando se deshabilitan. De modo similar a los buzones de correo principales deshabilitados, es posible conectar un buzón de archivo desconectado usando el cmdlet **Connect-Mailbox** con el parámetro *Archive*.

El buzón de correo principal y el buzón de archivo comparten el mismo nombre distintivo (DN) heredado, por lo que se debe conectar el buzón de archivo al mismo buzón de correo de usuario al que estaba conectado anteriormente. No es posible conectar el buzón de archivo personal con un buzón de correo de usuario diferente.

Es posible realizar dos operaciones en un buzón de archivo desconectado:

  - **Conectarlo a un buzón de correo principal existente**   Al igual que un buzón de correo principal desconectado, un buzón de archivo desconectado se conserva en la base de datos de buzones de correo hasta que expira el período de retención del buzón de correo eliminado, que, de manera predeterminada, es de 30 días. Durante este tiempo, puede recuperar el buzón de archivo reconectándolo a la misma cuenta de usuario a la que estaba conectado antes de su deshabilitación.
    

    > [!NOTE]
    > Si deshabilita un buzón de archivo para un buzón de correo usuario y, a continuación, habilita otro buzón archivo para el mismo usuario, el usuario obtendrá un nuevo buzón de archivo. Si bien puede usar el cmdlet <STRONG>Connect-Mailbox</STRONG> para conectar un buzón primario a un usuario, debe usar el cmdlet <STRONG>Enable-Mailbox</STRONG> para conectar un buzón de archivos deshabilitado a un buzón existente.

    
    Para obtener más información, vea [Administrar archivos locales en Exchange 2013](manage-in-place-archives-in-exchange-2013-exchange-2013-help.md).

  - **Eliminarlo de forma permanente de la base de datos de buzones de correo de Exchange**    Exchange conserva los buzones de archivo desconectados según la configuración de retención de buzones de correo eliminados definida para la base de datos de buzones de correo. El periodo de retención predeterminado es de 30 días. Una vez transcurrido el período de retención especificado para el buzón de correo, un buzón de archivo desconectado se purga de la base de datos de buzones de correo de Exchange.
    
    Al igual que un buzón de correo principal deshabilitado, es posible eliminar un buzón de archivo deshabilitado en cualquier momento con el cmdlet **Remove-StoreMailbox**. Para obtener más información, vea [Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md).

Cómo trabajar con buzones de correo deshabilitados

## Cómo trabajar con buzones de correo eliminados temporalmente

Un buzón eliminado temporalmente se crea cuando un buzón de correo se mueve de una base de datos de buzones de correo de Exchange a cualquier otra base de datos de buzones de correo. Exchange no elimina totalmente el buzón de correo de la base de datos de origen después de un movimiento, en caso de que ocurra un error que haga que el buzón de correo no funcione en la base de datos de destino. Puede restaurar el buzón de origen y volver a intentarlo en cualquier momento. Exchange retendrá el buzón eliminado temporalmente durante el período de retención del buzón de correo.

Es posible realizar dos operaciones en un buzón de correo eliminado temporalmente:

  - Restaurarlo a un buzón de correo existente.

  - Eliminarlo de forma permanente de la base de datos de buzones de correo de Exchange.

Los procedimientos para restaurar y eliminar un buzón eliminado temporalmente de manera permanente son similares a los de un buzón deshabilitado. Para obtener más información al respecto, vea los temas siguientes:

  - [Restaurar un buzón eliminado temporalmente](restore-a-soft-deleted-mailbox-exchange-2013-help.md)

  - [Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md)

Cómo trabajar con buzones de correo deshabilitados

## Resumen de cómo trabajar con buzones de correo desconectados

En la siguiente tabla, se resume la información sobre los buzones de correo desconectados, incluidos cómo se desconectó el buzón de correo, qué sucede con la cuenta de usuario de Active Directory correspondiente cuando un buzón de correo se desconecta y las opciones y las herramientas que tiene para conectar o restaurar los buzones de correo desconectados.


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
<th>Cómo se deshabilitó el buzón de correo</th>
<th>Valor de la propiedad <em>DisconnectReason</em></th>
<th>¿Se conserva la cuenta de usuario de Active Directory?</th>
<th>Opciones de conexión o de restauración</th>
<th>Herramientas</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>El EAC: <strong>Destinatarios</strong>&gt;<strong>Buzones</strong>&gt;<strong>Deshabilitar</strong></p></li>
<li><p>El Shell: Cmdlet <strong>Disable-Mailbox</strong></p></li>
</ul></td>
<td><p>Deshabilitado</p></td>
<td><p>Sí</p></td>
<td><p>Conectar a la misma cuenta de usuario</p></td>
<td><ul>
<li><p>El EAC: <strong>Destinatarios</strong>&gt;<strong>Buzones</strong>&gt;<strong>Conectar a un buzón</strong></p></li>
<li><p>El Shell: Cmdlet <strong>Connect-Mailbox</strong></p></li>
</ul></td>
</tr>
<tr class="even">
<td><ul>
<li><p>El EAC: <strong>Destinatarios</strong>&gt;<strong>Buzones</strong>&gt;<strong>Eliminar</strong></p></li>
<li><p>El Shell: Cmdlet <strong>Remove-Mailbox</strong></p></li>
</ul></td>
<td><p>Deshabilitado</p></td>
<td><p>No</p></td>
<td><ul>
<li><p>Conectar a una cuenta de usuario diferente</p></li>
<li><p>Restaurar a un buzón de diferente</p></li>
</ul></td>
<td><ul>
<li><p>El EAC: <strong>Destinatarios</strong>&gt;<strong>Buzones</strong>&gt;<strong>Conectar a un buzón</strong></p></li>
<li><p>El Shell: Cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>El Shell: Cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Se movió a una base de datos de buzones de correo diferente</p></td>
<td><p>SoftDeleted</p></td>
<td><p>Sí</p></td>
<td><ul>
<li><p>Conectar a una cuenta de usuario diferente</p></li>
<li><p>Restaurar a un buzón de diferente</p></li>
</ul></td>
<td><ul>
<li><p>El EAC: <strong>Destinatarios</strong>&gt;<strong>Buzones</strong>&gt;<strong>Conectar a un buzón</strong></p></li>
<li><p>El Shell: Cmdlet <strong>Connect-Mailbox</strong></p></li>
<li><p><strong>Enable-Mailbox</strong></p></li>
<li><p>El Shell: Cmdlet <strong>New-MailboxRestore</strong></p></li>
</ul></td>
</tr>
</tbody>
</table>


Cómo trabajar con buzones de correo deshabilitados

## Documentación de buzón desconectado

En la siguiente tabla, se incluyen vínculos a temas que le ayudarán a administrar buzones de correo desconectados. Esto incluye administrar buzones de correo de desconectados, buzones vinculados, buzones de recurso y buzones compartidos.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="disable-or-delete-a-mailbox-exchange-2013-help.md">Deshabilitar o eliminar un buzón de correo</a></p></td>
<td><p>Obtenga información sobre cómo deshabilitar o eliminar buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p><a href="connect-a-disabled-mailbox-exchange-2013-help.md">Conectar un buzón de correo deshabilitado</a></p></td>
<td><p>Obtenga información sobre cómo conectar un buzón deshabilitado a una cuenta de usuario existente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="connect-or-restore-a-deleted-mailbox-exchange-2013-help.md">Conectar o restaurar un buzón eliminado</a></p></td>
<td><p>Obtenga información sobre cómo conectar un buzón de correo eliminado a una cuenta de usuario o restaurar el contenido de un buzón eliminado a un buzón existente.</p></td>
</tr>
<tr class="even">
<td><p><a href="restore-a-soft-deleted-mailbox-exchange-2013-help.md">Restaurar un buzón eliminado temporalmente</a></p></td>
<td><p>Obtenga información sobre cómo conectar un buzón de correo eliminado temporalmente a una cuenta de usuario o restaurar el contenido de un buzón eliminado temporalmente a un buzón existente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-mailbox-restore-requests-exchange-2013-help.md">Administrar solicitudes de restauración de buzones</a></p></td>
<td><p>Obtenga información sobre cómo administrar solicitudes de restauración de buzones de correo con el Shell.</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p><a href="permanently-delete-a-mailbox-exchange-2013-help.md">Eliminar permanentemente un buzón de correo</a></p></td>
<td><p>Obtenga información sobre cómo eliminar un buzón de manera permanente.</p></td>
</tr>
</tbody>
</table>


Cómo trabajar con buzones de correo deshabilitados

