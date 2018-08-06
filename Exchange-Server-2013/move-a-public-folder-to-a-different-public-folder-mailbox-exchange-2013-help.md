---
title: 'Mover una carpeta pública a otro buzón de carpetas públicas Exchange 2013 Help | Microsoft Docs'
TOCTitle: Mover una carpeta pública a otro buzón de carpetas públicas
ms:assetid: b8744934-a3cb-443e-acce-a9a6ca5d88f6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ906435(v=EXCHG.150)
ms:contentKeyID: 51406537
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mover una carpeta pública a otro buzón de carpetas públicas

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-11-16_

Si el contenido de un buzón de carpeta pública empieza a superar sus cuotas de buzón de correo, puede que necesite mover las carpetas públicas a otro buzón de carpetas públicas. Hay dos formas de hacerlo. Para mover una o más carpetas públicas que no contienen subcarpetas, puede usar los cmdlets **PublicFolderMoveRequest**. Si necesita mover toda una rama de carpetas públicas (que incluye la carpeta pública principal y todas las subcarpetas), puede usar el script `Move-PublicFolderBranch.ps1` disponible cuando instale Exchange 2013.

Para otras tareas de administración relacionadas con carpetas públicas, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - El tiempo estimado para completar esta tarea depende del tamaño de la carpeta pública.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Carpetas públicas" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - No puede usar el EAC para realizar estos procedimientos. Debe usar el Shell.

  - Si la carpeta que mueve contiene subcarpetas, dichas subcarpetas no se moverán de forma predeterminada. Si desea mover una carpeta pública y todas sus subcarpetas, use el script **Move-PublicFolderBranch.ps1**.

  - Al mover una carpeta pública, solo se mueve su contenido físico, la jerarquía lógica sigue siendo la misma.

  - En función del tamaño de la carpeta pública y del contenido que haya en ella, el movimiento puede tardar varias horas en completarse. Durante este tiempo, los usuarios podrán acceder a las carpetas públicas. Sin embargo, no podrán acceder a las carpetas públicas durante un breve período mientras la carpeta se encuentre en estado “En curso”.

  - Puede realizar solo una solicitud de movimiento de carpeta pública a la vez. Debe usar el cmdlet **Remove-PublicFolderMoveRequest** para quitar la solicitud una vez completada.

  - Para comprobar el estado de la solicitud de movimiento de la carpeta pública en curso, ejecute el cmdlet [Get-PublicFolderMoveRequest](https://technet.microsoft.com/es-es/library/jj878076\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Mover una sola carpeta pública

En este ejemplo se inicia la solicitud de movimiento de la carpeta pública \\CustomerEnagagements del buzón de carpetas públicas DeveloperReports a DeveloperReports01

    New-PublicFolderMoveRequest -Folders \DeveloperReports\CustomerEngagements -TargetMailbox DeveloperReports01


> [!NOTE]
> El buzón de la carpeta pública de destino se bloqueará mientras la solicitud de traslado esté activa.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-PublicFolderMoveRequest](https://technet.microsoft.com/es-es/library/jj878081\(v=exchg.150\)).

## Mover varias carpetas públicas

En este ejemplo se inicia la solicitud de movimiento de las carpetas públicas de la rama \\Dev al buzón de carpetas públicas de destino DeveloperReports01. La carpeta pública \\Dev no se mueve.

    New-PublicFolderMoveRequest -Folders \Dev\CustomerEngagements,\Dev\RequestsforChange,\Dev\Usability -TargetMailbox DeveloperReports01


> [!NOTE]
> El buzón de la carpeta pública de destino se bloqueará mientras la solicitud de traslado esté activa.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-PublicFolderMoveRequest](https://technet.microsoft.com/es-es/library/jj878081\(v=exchg.150\)).

## Mover una rama de carpetas públicas

En este ejemplo se usa el script `Move-PublicFolderBranch.ps1` para mover una rama de carpetas públicas. Esto inicia la solicitud de movimiento de la carpeta pública \\Dev y todas sus subcarpetas al buzón de carpetas públicas DeveloperReports01. El script está ubicado en la carpeta de scripts y se debe ejecutar desde dicha ubicación.

    CD $env:ExchangeInstallPath\scripts
    
    .\Move-PublicFolderBranch.ps1 -FolderRoot \Dev -TargetPublicFolderMailbox DeveloperReports01

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la solicitud de movimiento de la carpeta pública se ha realizado correctamente, ejecute el siguiente comando:

    Get-PublicFolderMoveRequest | Format-List Status

Un estado de `Completed` indica que la solicitud de movimiento se realizó correctamente.

Si la solicitud de movimiento no se realizó correctamente, puede que tenga que restaurar la carpeta pública o sus contenidos. Para obtener más información, consulte [Restaurar carpetas públicas y buzones de carpetas públicas de movimientos fallidos](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

