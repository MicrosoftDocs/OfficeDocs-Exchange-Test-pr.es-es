---
title: 'Obtener estadísticas de la carpeta Elementos recuperables: Exchange 2013 Help'
TOCTitle: Obtener estadísticas de la carpeta Elementos recuperables
ms:assetid: dee77958-ee87-4908-85e4-ad053bacd8b0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff714343(v=EXCHG.150)
ms:contentKeyID: 52062068
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Obtener estadísticas de la carpeta Elementos recuperables

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-01-22_

La carpeta Elementos recuperables contiene los elementos que han eliminado los usuarios de Microsoft Outlook y Microsoft OfficeOutlook Web App o el asistente de buzones de correo. El tiempo que los elementos eliminados permanecen en esta carpeta se basa en la configuración de la retención de elementos eliminados establecida para la base de datos del buzón o para el buzón. De forma predeterminada, una base de datos de buzones está configurada para retener los elementos eliminados durante 14 días, y la cuota de advertencia de elementos recuperables y la cuota de elementos recuperables están configuradas a 20 gigabytes (GB) y 30 GB respectivamente. No obstante, si se habilita una conservación local o una retención por juicio para el buzón de correo, la carpeta Elementos recuperables puede acumular elementos eliminados durante más tiempo del que se estipula en el período de retención, así como conservar versiones diferentes de los elementos del buzón de correo modificados.

Cuando la carpeta Elementos recuperables alcance la cuota de advertencia de los elementos recuperables, se registrará un evento de advertencia en el registro de eventos de la aplicación. Si el buzón no está en retención por juicio, los elementos se eliminarán de acuerdo con el método “primero en entrar, primero en salir” (FIFO). No obstante, si el buzón está en retención por juicio, no se vaciará nunca y, al alcanzar la cuota de Elementos recuperables, la funcionalidad del buzón se verá afectada.

Por consiguiente, resulta importante supervisar si el registro de eventos presenta alertas generadas cuando los buzones alcanzan las cuotas de elementos recuperables. También se puede utilizar este procedimiento para notificar estadísticas de la carpeta Elementos recuperables, en concreto en el caso de buzones en retención por juicio.

Para obtener más información, consulte los siguientes temas:

  - [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md)

  - [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Carpetas del buzón" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - No se puede usar el Centro de administración de Exchange (EAC) para obtener las estadísticas de la carpeta Elementos recuperables de un buzón de correo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## ¿Qué desea hacer?

## Obtener estadísticas de la carpeta Elementos recuperables de un buzón de correo

En este ejemplo se obtienen las estadísticas de la carpeta Elementos recuperables de Soumya Singhi y se muestra una lista con los resultados.

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-List

En este ejemplo se obtienen las estadísticas de la carpeta Elementos recuperables de Soumya Singhi y se muestra una tabla con el nombre, la ruta, el número de elementos que contiene y el tamaño de la carpeta.

    Get-MailboxFolderStatistics -Identity "Soumya Singhi" -FolderScope RecoverableItems | Format-Table Name,FolderPath,ItemsInFolder,FolderAndSubfolderSize

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-MailboxFolderStatistics](https://technet.microsoft.com/es-es/library/aa996762\(v=exchg.150\)).

## Obtener estadísticas de la carpeta Elementos recuperables de todos los buzones de correo en retención por juicio

En este ejemplo se recupera una lista de todos los buzones en retención por juicio y las estadísticas de carpeta de buzón de la carpeta Elementos recuperables y sus subcarpetas de cada uno de los buzones. Las propiedades **Identity** (identidad de la carpeta de buzón) y **FolderAndSubfolderSize** se muestran en una tabla.

    Get-Mailbox -ResultSize Unlimited -Filter {LitigationHoldEnabled -eq $true} | Get-MailboxFolderStatistics | Format-Table Identity,FolderAndSubfolderSize

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) y [Get-MailboxFolderStatistics](https://technet.microsoft.com/es-es/library/aa996762\(v=exchg.150\)).

## Obtener la cuota de Elementos recuperables para un buzón

En este ejemplo se muestran la cuota y la cuota de advertencia para la carpeta Elementos recuperables de un buzón de usuario. El ejemplo también recupera información acerca de si se coloca una retención por juicio o conservación local en el buzón.

    Get-Mailbox -Identity <identity of mailbox> | Format-List RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

En este ejemplo se muestran la cuota y la cuota de advertencia para la carpeta Elementos recuperables de todos los buzones de usuario en su organización. El ejemplo también recupera información de retención.

    Get-Mailbox -ResultSize Unlimited -Filter {RecipientTypeDetails -eq "UserMailbox"} | Format-List Name,RecoverableItems*,LitigationHoldEnabled,InPlaceHolds

