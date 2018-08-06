---
title: 'Mover un buzón de carpetas públicas a una base de datos de buzones diferente | Microsoft Docs'
TOCTitle: Mover un buzón de carpetas públicas a una base de datos de buzones diferente
ms:assetid: 67601d45-4824-4ae6-9a7e-b645ec3af4d3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ906434(v=EXCHG.150)
ms:contentKeyID: 51406523
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Mover un buzón de carpetas públicas a una base de datos de buzones diferente

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-07-21_

Es posible que necesite mover un buzón de una carpeta pública a una base de datos de buzones distinta para equilibrar la carga o para acercar recursos a su ubicación física. De forma similar a mover un buzón normal, puede usar los cmdlets **MoveRequest** para mover un buzón de una carpeta pública. Para obtener más información acerca del movimiento de buzones, vea [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las carpetas públicas, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - El tiempo estimado de finalización depende del tamaño del buzón de la carpeta pública.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Sección "Permisos de movimiento y migración de buzones" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - No puede realizar este procedimiento en el EAC. Puede realizar este procedimiento en el Shell.

  - En función del tamaño del buzón de la carpeta pública, el movimiento podría tardar varias horas en finalizar. Durante ese tiempo, los usuarios no podrán acceder a las carpetas públicas. Los usuarios tampoco podrán acceder a las carpetas públicas durante un breve periodo mientras la carpeta se encuentre en estado "Finalización en curso".

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear una solicitud de movimiento

El cmdlet **New-MoveRequest** pone en cola el buzón de la carpeta pública en la cola del servicio Replicación de buzones de Microsoft Exchange. Cuando el servicio Replicación de buzones de Microsoft Exchange esté disponible, atenderá la solicitud de movimiento y empezará a mover el buzón de la carpeta pública. Completará la solicitud de principio a fin.

En este ejemplo se inicia la solicitud de movimiento para el buzón de la carpeta pública PF\_SanFrancisco a la base de datos de buzones MBX\_DB01.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## Crear una solicitud de movimiento para completar en un momento posterior

Durante la fase final de la solicitud de movimiento, en la fase `CompletionInProgress`, los usuarios no podrán acceder al buzón de la carpeta pública. Si es necesario, puede suspender la solicitud de movimiento antes de que llegue a dicha fase y proseguir con ella en un momento de menor impacto para los usuarios.

En este ejemplo se inicia la solicitud de movimiento para el buzón de la carpeta pública PF\_SanFrancisco a la base de datos de buzones MBX\_DB01 y la suspende cuando el movimiento está listo para finalizar.

    New-MoveRequest -Identity "PF_SanFrancisco" -TargetDatabase MBX_DB01 -SuspendWhenReadyToComplete

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

En este ejemplo se recupera el estado del movimiento de buzones en curso para el buzón de la carpeta pública PF\_SanFrancisco.

    Get-MoveRequest -Identity "PF_SanFrancisco"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-MoveRequest](https://technet.microsoft.com/es-es/library/dd335227\(v=exchg.150\)).

Cuando la solicitud de movimiento alcanza el estado de Suspendido, puede reanudar la solicitud. En este ejemplo se reanuda la solicitud de movimiento para el buzón de la carpeta pública PF\_SanFrancisco.

    Resume-MoveRequest -Identity "PF_SanFrancisco"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Resume-MoveRequest](https://technet.microsoft.com/es-es/library/ee332320\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la solicitud de movimiento se creó correctamente, ejecute el siguiente comando:

    Get-MoveRequestStatistics -Identity PF_SanFrancisco | Format-List Status

Un estado de `Completed` indica que la solicitud de movimiento se realizó correctamente.

Si el movimiento no se realizó correctamente, es posible que deba restaurar la carpeta pública. Para obtener más información, consulte [Restaurar carpetas públicas y buzones de carpetas públicas de movimientos fallidos](restore-public-folders-and-public-folder-mailboxes-from-failed-moves-exchange-2013-help.md).

