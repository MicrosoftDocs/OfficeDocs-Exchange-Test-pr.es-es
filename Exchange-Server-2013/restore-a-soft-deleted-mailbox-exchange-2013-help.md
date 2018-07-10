---
title: 'Restaurar un buzón eliminado temporalmente: Exchange 2013 Help'
TOCTitle: Restaurar un buzón eliminado temporalmente
ms:assetid: 4f3f5ce4-9d12-4ed8-9f70-d8a6aa8a1b2e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ863435(v=EXCHG.150)
ms:contentKeyID: 50556799
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Restaurar un buzón eliminado temporalmente

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-11-29_

Use el Shell para conectar un buzón eliminado de manera temporal con una cuenta de usuario de Active Directory. Un buzón de correo se *elimina temporalmente* de la base de datos de buzones de correo de origen cuando se mueve a una base de datos de buzones de correo diferente. Exchange no elimina totalmente el buzón de correo de la base de datos de buzones de correo de origen cuando el movimiento finaliza. En lugar de hacer eso, el buzón de la base de datos de buzones de origen cambia a un estado de eliminación temporal. Esto le permite restaurar el buzón de correo de origen en caso de que se produzcan errores durante el movimiento que provoquen fallas o daños en la base de datos de destino. Si esto sucede, puede restaurar el buzón de correo de origen y volver a realizar el movimiento.

Un buzón de correo eliminado temporalmente se conserva en la base de datos de origen hasta que expira el período de retención o hasta que se usa el cmdlet **Remove-StoreMailbox** para purgar el buzón de correo eliminado temporalmente. Hasta que un buzón de correo eliminado temporalmente se elimine de manera permanente de la base de datos de buzones de correo de Exchange, puede usar el Shell para restaurar el contenido del buzón de correo eliminado temporalmente en el buzón de archivo.

Para obtener más información sobre los buzones de correo eliminados temporalmente y realizar otras tareas de administración relacionadas, consulte los siguientes temas:

  - [Buzones desconectados](disconnected-mailboxes-exchange-2013-help.md)

  - [Conectar o restaurar un buzón eliminado](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)

  - [Administrar solicitudes de restauración de buzones](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Eliminar permanentemente un buzón de correo](permanently-delete-a-mailbox-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de aprovisionamiento de destinatarios" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Los procedimientos de este tema sólo pueden realizarse en el Shell. No puede usar el EAC para restaurar buzones eliminados temporalmente.

  - Ejecute el siguiente comando para comprobar que el buzón de correo eliminado temporalmente al que desea conectar una cuenta de usuario aún exista en la base de datos de buzones de correo y no sea un buzón de correo deshabilitado.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisplayName -eq "<display name>" } | fl DisplayName,DisconnectReason,DisconnectDate
    
    El buzón de correo eliminado temporalmente debe existir en la base de datos de buzones de correo, y el valor para la propiedad *DisconnectReason* debe ser `SoftDeleted`. Si el buzón de correo se purgó de la base de datos, el comando no devolverá ningún resultado.
    
    De manera alternativa, ejecute el siguiente comando para ver todos los buzones de correo eliminados temporalmente en su organización.
    
        Get-MailboxDatabase | Get-MailboxStatistics | Where { $_.DisconnectReason -eq "SoftDeleted" } | fl DisplayName,DisconnectReason,DisconnectDate

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351)..

## Usar la consola para restaurar un buzón eliminado temporalmente

Puede usar el Shell para restaurar un buzón de correo eliminado temporalmente en un buzón de correo existente. Para hacerlo, use el cmdlet **New-MailboxRestoreRequest**. Cuando restaura un buzón de correo eliminado temporalmente, su contenido se copia en un buzón de correo existente, el cual se denomina *buzón de correo de destino*. Después de que una solicitud de restauración de buzón de correo se completa correctamente, de manera predeterminada, la solicitud se conserva por 30 días y, luego, se elimina. Puede eliminarla antes con el cmdlet **Remove-MailboxRestoreRequest**.

Después de que un buzón de correo eliminado temporalmente se restaura, el buzón de correo se conserva en la base de datos de buzones de correo hasta que un administrador lo elimina, o se purga cuando expira el período de retención del buzón de correo eliminado.

A fin de crear una solicitud de restauración de un buzón de correo, debe usar el nombre para mostrar, el GUID del buzón de correo o el nombre distintivo (DN) heredado del buzón de correo eliminado temporalmente. Use el cmdlet **Get-MailboxStatistics** para ver los valores de las propiedades **DisplayName**, **MailboxGuid** y **LegacyDN** del buzón de correo eliminado temporalmente que desea restaurar. Por ejemplo, ejecute el siguiente comando para ver esta información para todos los buzones de correo eliminados temporalmente y deshabilitados en su organización.

    Get-MailboxDatabase | Get-MailboxStatistics | Where {$_.DisconnectReason -eq "SoftDeleted"} | fl DisplayName,MailboxGuid,LegacyDN,Database

En este ejemplo, se restaura un buzón de correo eliminado temporalmente, que se identifica mediante el nombre para mostrar en el parámetro *SourceStoreMailbox* y está ubicado en la base de datos de buzones de correo MBXDB01 o el buzón de correo de destino denominado Debra Garcia. El parámetro *AllowLegacyDNMismatch* se usa para que el buzón de correo de origen pueda restaurarse a un buzón de correo que no tenga el mismo valor de DN heredado que el buzón de correo eliminado temporalmente.

    New-MailboxRestoreRequest -SourceStoreMailbox "Debra Garcia" -SourceDatabase MBXDB01 -TargetMailbox "Debra Garcia" -AllowLegacyDNMismatch

En este ejemplo, se restaura el buzón de archivo eliminado temporalmente de Pilar Pinilla, definido por el GUID del buzón, a su buzón de correo de archivo actual. El parámetro *AllowLegacyDNMismatch* no es necesario porque un buzón de correo principal y su buzón de archivo correspondiente tienen el mismo DN heredado.

    New-MailboxRestoreRequest -SourceStoreMailbox dc35895a-a628-4bba-9aa9-650f5cdb9ae7 -SourceDatabase MBXDB02 -TargetMailbox pilarp@contoso.com -TargetIsArchive

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya restaurado un buzón de correo eliminado temporalmente al buzón de correo de destino de manera correcta, ejecute el cmdlet **Get-MailboxRestoreRequest** o el cmdlet **Get-MailboxRestoreRequestStatistics** para ver información sobre la solicitud de restauración. Si la solicitud de restauración se creó correctamente, la propiedad *Status* tendrá el valor **Queued**, **InProgress** o **Completed**. Una vez que la solicitud de restauración se haya completado, el contenido del buzón de correo eliminado temporalmente aparecerá en el buzón de correo de destino.

Para obtener más información, vea:

  - [Administrar solicitudes de restauración de buzones](manage-mailbox-restore-requests-exchange-2013-help.md)

  - [Get-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829907\(v=exchg.150\))

  - [Get-MailboxRestoreRequestStatistics](https://technet.microsoft.com/es-es/library/ff829912\(v=exchg.150\))

