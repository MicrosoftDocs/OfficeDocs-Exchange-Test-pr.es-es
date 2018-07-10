---
title: 'Realizar un cambio de servidor: Exchange 2013 Help'
TOCTitle: Realizar un cambio de servidor
ms:assetid: ffcefd56-b0a0-4229-9011-fff4197b7c74
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298187(v=EXCHG.150)
ms:contentKeyID: 62523851
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Realizar un cambio de servidor

 

_**Se aplica a:** Exchange Server 2013 SP1_

_**Última modificación del tema:** 2014-06-23_

Un cambio de servidor es una tarea que se puede efectuar para mover todas las copias activas de la base de datos de buzones del servidor de buzones a uno o más servidores de buzones en un grupo de disponibilidad de la base de datos (DAG). Esta tarea se efectúa como parte de la preparación de una interrupción programada para el servidor de buzones actual.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 30 segundos por base de datos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Grupos de disponibilidad de base de datos" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar EAC para realizar un cambio de servidor

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

1.  En el EAC, vaya a **Servidores** \> **servidores**.

2.  Seleccione el servidor de buzones que quiere cambiar.

3.  En el panel de detalles, seleccione **Cambio de servidor**.

4.  En la página **Cambio de servidor**, realice una de las siguientes acciones:
    
    1.  Acepte el valor predeterminado de **Elegir automáticamente un servidor de destino** (en tal caso, el sistema selecciona de forma automática el servidor de buzones más adecuado para cada base de datos que se intercambia); a continuación, haga clic en **guardar**.
    
    2.  Haga clic en **Usar el servidor especificado como destino del intercambio**, haga clic en **Examinar** para seleccionar un servidor de buzones y haga clic en **guardar**.

5.  Cuando haya completado el cambio, haga clic en **cerrar** para salir de la página **Cambio de servidor**.

## Uso del Shell para efectuar un cambio de conexión de servidor

En este ejemplo, se efectúa un cambio de servidor en el servidor MBX1. El sistema selecciona, de forma automática, el servidor de buzones más adecuado para cada base de datos activa en MBX1.

    Move-ActiveMailboxDatabase -Server MBX1

En este ejemplo, se efectúa un cambio de servidor en el servidor de buzones MBX4. Cuando finaliza el comando, MBX5 hospeda la copia activa de las bases de datos que estaban activas en MBX4.

    Move-ActiveMailboxDatabase -Server MBX4 -ActivateOnServer MBX5

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Move-ActiveMailboxDatabase](https://technet.microsoft.com/es-es/library/dd298068\(v=exchg.150\)).

