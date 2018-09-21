---
title: 'Eliminar permanentemente un buzón de correo: Exchange 2013 Help'
TOCTitle: Eliminar permanentemente un buzón de correo
ms:assetid: df35765a-0bef-4561-9846-d91d69c0269c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ863440(v=EXCHG.150)
ms:contentKeyID: 50556898
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Eliminar permanentemente un buzón de correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-11-16_

Cuando se eliminan buzones activos y buzones desconectados de forma permanente, el contenido de los buzones se purga de la base de datos de buzones de Exchange y los datos se pierden de manera irreversible. Cuando se elimina un buzón activo de forma permanente, la cuenta de usuario de Active Directory asociada también se elimina.

Una alternativa a eliminar permanentemente un buzón consiste en desconectarlo. Después de desconectar un buzón, éste se mantiene en la base de datos de buzones durante 30 días de manera predeterminada. Esto ofrece la oportunidad de volver a conectar o restaurar el buzón antes de que se purgue de la base de datos.

Para obtener más información acerca de los buzones desconectados o realizar otras tareas de administración relacionadas, consulte los siguientes temas:

  - [Buzones desconectados](disconnected-mailboxes-exchange-2013-help.md)

  - [Deshabilitar o eliminar un buzón de correo](disable-or-delete-a-mailbox-exchange-2013-help.md)

  - [Conectar un buzón de correo deshabilitado](connect-a-disabled-mailbox-exchange-2013-help.md)

  - [Conectar o restaurar un buzón eliminado](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)


> [!NOTE]
> No se puede utilizar la EAC para eliminar permanentemente un buzón activo o desconectado.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Eliminar un buzón activo de forma permanente

## Uso del Shell para eliminar un buzón desconectado de forma permanente

Ejecute el siguiente comando para eliminar de forma permanente un buzón activo y la cuenta de usuario de Active Directory asociada.

```powershell
Remove-Mailbox -Identity <identity> -Permanent $true
```


> [!NOTE]
> Si no incluye el parámetro <EM>Permanent</EM>, el buzón eliminado se guarda de forma predeterminada en la base de datos de buzones durante 30 días, antes de que se elimine de forma permanente.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-Mailbox](https://technet.microsoft.com/es-es/library/aa995948\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se eliminó permanentemente un buzón activo, haga lo siguiente:

1.  Compruebe que el buzón ya no aparece en la EAC.

2.  Compruebe que la cuenta de usuario asociada ya no aparece en Usuarios y equipos de Active Directory.

3.  Ejecute el siguiente comando para comprobar que el buzón se purgó correctamente de la base de datos de buzones de Exchange.
    
    ```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {         Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
```
    
    Si purgó el buzón correctamente, el comando no devolverá ningún resultado. Si el buzón no se ha purgado, el comando devolverá información acerca del buzón.

## Eliminar permanente un buzón desconectado

## Usar la consola para eliminar de forma permanente un buzón desconectado

Existen dos tipos de buzones desconectados: deshabilitados y eliminados temporalmente. Debe especificar uno de estos tipos al ejecutar el cmdlet para eliminar el buzón de forma permanente. Si el tipo que especifica no coincide con el tipo actual de buzón desconectado, el comando falla.

Ejecute el siguiente comando para determinar si un buzón desconectado está deshabilitado o se eliminó temporalmente.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,MailboxGuid,Database,DisconnectReason

El valor de la propiedad *DisconnectReason* para los buzones desconectados será `Disabled` o `SoftDeleted`.

Ejecute el siguiente comando para mostrar el tipo de todos los buzones desconectados en la organización.

    Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -ne $null } | fl DisplayName,MailboxGuid,Database,DisconnectReason


> [!WARNING]
> Cuando se usa el cmdlet <STRONG>Remove-StoreMailbox</STRONG> para eliminar un buzón desconectado de forma permanente, todo el contenido se purga de la base de datos de buzones y la pérdida de datos es permanente.



En este ejemplo, se elimina permanentemente el buzón desconectado con GUID 2ab32ce3-fae1-4402-9489-c67e3ae173d3 de la base de datos de buzones MBD01.

    Remove-StoreMailbox -Database MBD01 -Identity "2ab32ce3-fae1-4402-9489-c67e3ae173d3" -MailboxState Disabled

En este ejemplo se elimina permanentemente el buzón eliminado temporalmente de Dan Jump de la base de datos de buzones MBD01.

```powershell
Remove-StoreMailbox -Database MBD01 -Identity "Dan Jump" -MailboxState SoftDeleted
```

En este ejemplo, se eliminan permanentemente todos los buzones eliminados temporalmente de la base de datos del buzón MBD01.

    Get-MailboxStatistics -Database MBD01 | where {$_.DisconnectReason -eq "SoftDeleted"} | ForEach {Remove-StoreMailbox -Database $_.Database -Identity $_.MailboxGuid -MailboxState SoftDeleted}

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Remove-StoreMailbox](https://technet.microsoft.com/es-es/library/ff829913\(v=exchg.150\)) y [Get-MailboxStatistics](https://technet.microsoft.com/es-es/library/bb124612\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que eliminó permanentemente un buzón desconectado y que se purgó de forma correcta de la base de datos de buzones de Exchange, ejecute el siguiente comando.

```powershell
Get-MailboxDatabase | Get-MailboxStatistics | Where {     Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" }.DisplayName -eq "<display name>" }
```

Si purgó el buzón correctamente, el comando no devolverá ningún resultado. Si el buzón no se ha purgado, el comando devolverá información acerca del buzón.

