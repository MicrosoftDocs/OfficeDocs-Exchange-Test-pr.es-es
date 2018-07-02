---
title: 'Restaurar carpetas públicas y buzones de carpetas públicas de movimientos fallidos: Exchange 2013 Help'
TOCTitle: Restaurar carpetas públicas y buzones de carpetas públicas de movimientos fallidos
ms:assetid: 2ade83c9-5f9b-4945-bf32-48fa8185b515
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ983802(v=EXCHG.150)
ms:contentKeyID: 52062020
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Restaurar carpetas públicas y buzones de carpetas públicas de movimientos fallidos

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-13_

Si falla una solicitud de movimiento para una carpeta pública o un buzón de carpetas públicas, puede restaurar la carpeta o el buzón siempre y cuando se den las siguientes condiciones:

  - **Movimiento de carpeta pública erróneo:**  una copia eliminada temporalmente de la carpeta pública sigue existiendo en el buzón de carpetas públicas de origen y está todavía en período de retención.

  - **Movimiento de buzón de carpetas públicas erróneo:**  una copia eliminada temporalmente del buzón de carpetas públicas sigue existiendo en la base de datos de buzones de origen y está todavía en período de retención de buzón.

Si ha transcurrido el período de retención de buzón, puede recuperar un buzón de carpetas públicas individuales a partir de la copia de seguridad. A continuación, se extraen los datos del buzón restaurado y se copian a una carpeta de destino o se combinan con otro buzón. Para obtener más información, consulte [Restauración de datos mediante una base de datos de recuperación](restore-data-using-a-recovery-database-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las carpetas públicas, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Solicitud de restauración de buzón" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - No puede usar la EAC para realizar este proceso. Debe usar el Shell.

  - Para crear una solicitud de restauración, debe indicar los valores de los parámetros *DisplayName*, *LegacyDN* o *MailboxGUID* del buzón de carpetas públicas eliminado temporalmente.

  - De forma predeterminada, las carpetas de contenedor se restaurarán junto con las carpetas habituales. Esto puede evitarse usando el parámetro *ExcludeDumpster*.

  - La restauración de buzones de carpetas públicas es diferente a la restauración de buzones habituales dado que las carpetas no se crearán si no existen en el buzón de destino. Las carpetas que faltan se mostrarán en un mensaje de advertencia al final de la solicitud de restauración.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Restaurar una carpeta pública eliminada temporalmente

En este ejemplo se restaura la carpeta pública \\Dev\\CustomerEnagagements en el buzón de carpetas públicas de destino Development01.

    New-MailboxRestoreRequest -SourceStoreMailbox Development -SourceDatabase MBX_DB01 -TargetMailbox Development01 -AllowLegacyDNMismatch -IncludeFolders \Dev\CustomerEngagements

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)).

## Restaurar un buzón de carpetas públicas eliminado temporalmente

En este ejemplo se restaura el buzón de carpetas públicas PF\_Singapore en el nuevo buzón de carpetas públicas PF\_Singapore\_Restore.

    New-MailboxRestoreRequest -SourceStoreMailbox PF_Singapore -SourceDatabase MBX_DB01 -TargetMailbox PF_Singapore_Restore -AllowLegacyDNMismatch

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MailboxRestoreRequest](https://technet.microsoft.com/es-es/library/ff829875\(v=exchg.150\)).

