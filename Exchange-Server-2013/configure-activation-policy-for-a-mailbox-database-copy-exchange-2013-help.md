---
title: 'Configurar directiva activar para copia base datos buzones: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurar la directiva de activación para una copia de base de datos de buzones
ms:assetid: 6b37ed6e-2e36-4688-b485-8fdbb8193ec8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298046(v=EXCHG.150)
ms:contentKeyID: 48268247
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar la directiva de activación para una copia de base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-02_

*Activación* es el proceso que consiste en cambiar la copia de una base de datos de buzones de una copia pasiva a una copia activa. La activación se lleva a cabo de forma automática en el sistema como parte de la operación de conmutación por error de la base de datos o del servidor. Se puede realizar de forma manual por un administrador como parte de la operación de cambio de la base de datos o del servidor. El bloqueo de la activación de una base de datos impide que se convierta en la copia activa durante un error de base de datos o de servidor.

¿Busca otras tareas de administración relacionadas con copias de bases de datos de buzones? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar la directiva de activación para una copia de base de datos de buzones

1.  
    
    En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos que desea configurar.

3.  
    
    En el panel de detalles, en **Copias de bases de datos**, busque la copia de base de datos que desea configurar y haga clic en **Suspender**.

4.  Puede agregar un comentario de manera opcional y seleccionar la casilla **Solo puede activar esta copia mediante la intervención manual**.

5.  Haga clic en **Guardar** para guardar los cambios de configuración de la copia de base de datos de buzones.

## Usar el Shell para suspender o reanudar una copia de base de datos para activación

En este ejemplo, se bloquea la copia de la base de datos DB1 en el servidor MBX2 para activación.

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX2 -ActivationOnly

En este ejemplo, se reanuda la copia de la base de datos DB1 en el servidor MBX2 para activación.

    Resume-MailboxDatabaseCopy -Identity DB1\MBX2

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd351074\(v=exchg.150\)) o [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335220\(v=exchg.150\)).

## Usar el Shell para configurar la directiva de activación de un servidor

En este ejemplo se configuran las copias de base de datos en el servidor MBX2 como bloqueadas para la activación.

    Set-MailboxServer -Identity MBX2 -DatabaseCopyAutoActivationPolicy Blocked

En este ejemplo se configuran las copias de base de datos en el servidor MBX3 como bloqueadas para la activación fuera del sitio.

    Set-MailboxServer -Identity MBX3 -DatabaseCopyAutoActivationPolicy IntrasiteOnly

En este ejemplo se configuran las copias de base de datos en el servidor MBX4 como desbloqueadas para la activación.

    Set-MailboxServer -Identity MBX4 -DatabaseCopyAutoActivationPolicy Unrestricted

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd351074\(v=exchg.150\)), [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335220\(v=exchg.150\)) o [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya configurado correctamente la directiva de activación, siga estos pasos:

  - En el Shell, ejecute el siguiente comando para comprobar la configuración de activación de una copia de base de datos.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List ActivationSuspended

  - En el Shell, ejecute el siguiente comando para comprobar la configuración de activación de un miembro de DAG.
    
        Get-MailboxServer <ServerName> | Format-List DatabaseCopyAutoActivationPolicy

