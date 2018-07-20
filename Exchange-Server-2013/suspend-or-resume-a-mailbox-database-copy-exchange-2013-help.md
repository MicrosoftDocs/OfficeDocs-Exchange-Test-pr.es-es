---
title: 'Suspensión o reanudación de una copia de base de datos de buzones: Exchange 2013 Help'
TOCTitle: Suspensión o reanudación de una copia de base de datos de buzones
ms:assetid: 96aa1b82-3e15-4215-843e-3d583af9504b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298159(v=EXCHG.150)
ms:contentKeyID: 48268445
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Suspensión o reanudación de una copia de base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-02_

Es posible que deba suspender o reanudar una copia de base de datos por diversos motivos, como el mantenimiento en el disco que contiene una copia de base de datos o la suspensión de la activación de una copia de base de datos individual con fines de recuperación de desastres.

¿Busca otras tareas de administración relacionadas con copias de bases de datos de buzones? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para suspender una copia de base de datos de buzones de correo

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos cuya copia desea suspender.

3.  En el panel de detalles, bajo **Copias de bases de datos**, haga clic en **Suspender** bajo la copia de base de datos que desea suspender.

4.  En el campo **Comentarios**, agregue un comentario opcional de hasta 512 caracteres para especificar el motivo de la suspensión.

5.  Para suspender que la copia de base de datos se active automáticamente, marque la casilla **Solo puedes activar esta copia mediante la intervención manual**.

6.  Haga clic en **Guardar** para suspender la copia de base de datos.

## Uso del EAC para reanudar una copia de base de datos de buzones de correo

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos cuya copia desea reanudar.

3.  En el panel de detalles, bajo **Copias de bases de datos**, haga clic en **Reanudar** bajo la copia de base de datos que desea reanudar.

4.  Haga clic en **Sí** para reanudar la copia de base de datos.

## Usar el Shell para suspender una copia de base de datos de buzones

Este ejemplo suspende la replicación continua de una copia de la base de datos de DB1 hospedada en el servidor MBX1. También se ha especificado un comentario opcional.

    Suspend-MailboxDatabaseCopy -Identity DB1\MBX1 -SuspendComment "Maintenance on MBX1" -Confirm:$False

Este ejemplo suspende la activación de una copia de la base de datos de DB2 hospedada en el servidor MBX2.

    Suspend-MailboxDatabaseCopy -Identity DB2\MBX2 -ActivationOnly -Confirm:$False

## Usar el Shell para reanudar una copia de base de datos de buzones

En este ejemplo se reanuda una copia de la base de datos DB1 en el servidor MBX1.

    Resume-MailboxDatabaseCopy -Identity DB1\MBX1

Este ejemplo reanuda la copia de la base de datos DB2 en el servidor MBX2 solo para la replicación.

    Resume-MailboxDatabaseCopy -Identity DB2\MBX2 -ReplicationOnly

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha suspendido o reanudado correctamente una copia de base de datos de buzones, siga uno de los procedimientos siguientes:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos pertinente y, en el panel de detalles, haga clic en **Ver detalles** para ver las propiedades de la copia de base de datos.

  - En el Shell, ejecute el siguiente comando para mostrar la información de estado de una copia de base de datos.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

