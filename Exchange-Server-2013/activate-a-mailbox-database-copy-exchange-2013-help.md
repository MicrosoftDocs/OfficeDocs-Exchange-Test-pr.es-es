---
title: 'Activación de una copia de base de datos de buzones: Exchange 2013 Help'
TOCTitle: Activación de una copia de base de datos de buzones
ms:assetid: d948269b-c902-4d8d-8c2b-269473359baa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee364750(v=EXCHG.150)
ms:contentKeyID: 48268745
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activación de una copia de base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-01_

La activación de una copia de base de datos de buzones consiste en designar una determinada copia pasiva como la nueva copia activa de una base de datos de buzones. Se hace referencia a este proceso como *cambio de base de datos*. Un cambio de base datos implica desmontar la base de datos que esté activa y montar la copia de la base de datos en un determinado servidor como la nueva copia activa de base de datos de buzones. La copia de base de datos que va a convertirse en la base de datos de buzones activa debe estar al día y encontrarse en buen estado.

¿Busca otras tareas de administración relacionadas con copias de bases de datos de buzones? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para mover una base de datos de buzones activa

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos cuya copia desea activar.

3.  En el panel Detalles, en **Copias de bases de datos**, haga clic en **Activar** en la copia de base de datos que desea activar.

4.  Haga clic en **Sí** para activar la copia de base de datos.

## Usar el Shell para mover una base de datos de buzones de correo activa

En este ejemplo se activa y se monta una copia de la base de datos DB4 hospedada en MBX3 como la nueva base de datos de buzones activa. Este comando activa la nueva base de datos de buzones DB4 sin anular la configuración de marcado de montaje de bases de datos en MBX3.

```powershell
Move-ActiveMailboxDatabase DB4 -ActivateOnServer MBX3 -MountDialOverride:None
```

En este ejemplo se efectúa un cambio de una base de datos denominada DB2 en el servidor de buzón MBX1. Cuando finalice el comando, MBX1 hospeda la copia activa de DB2. Como el parámetro *MountDialOverride* se establece en `None`, MBX1 monta la base de datos usando su propia configuración definida de marcado de montaje automático de base de datos.

```powershell
Move-ActiveMailboxDatabase DB2 -ActivateOnServer MBX1 -MountDialOverride:None
```

En este ejemplo se efectúa un cambio de una base de datos denominada DB1 en el servidor de buzón MBX3. Cuando finalice el comando, MBX3 hospeda la copia activa de DB1. Como el parámetro *MountDialOverride* se especifica con un valor de `Good Availability`, MBX3 monta la base de datos mediante la configuración de marcado de montaje automático de base de datos de *GoodAvailability*.

```powershell
Move-ActiveMailboxDatabase DB1 -ActivateOnServer MBX3 -MountDialOverride:GoodAvailability
```

En este ejemplo se efectúa un cambio de una base de datos denominada DB3 en el servidor de buzón MBX4. Cuando finalice el comando, MBX4 hospeda la copia activa de DB3. Dado que no se ha especificado el parámetro *MountDialOverride*, MBX4 monta la base de datos mediante una configuración de marcado de montaje de base de datos automático de *Lossless*.

```powershell
Move-ActiveMailboxDatabase DB3 -ActivateOnServer MBX4
```

En este ejemplo se efectúa un cambio de servidor en el servidor de buzón MBX1. Todas las copias de base de datos de buzón activo en MBX1 se activarán en uno o más servidores de buzón con copias en buen estado de las bases de datos activas en MBX1.

```powershell
Move-ActiveMailboxDatabase -Server MBX1
```

En este ejemplo se efectúa un cambio de una base de datos denominada DB4 en el servidor de buzón MBX5. En este ejemplo, la copia de base de datos de MBX5 tiene una cola de repetición mayor que 6. Como consecuencia, para activar la copia de base de datos de MBX5 se debe especificar el parámetro *SkipLagChecks*.

```powershell
Move-ActiveMailboxDatabase DB4 MBX5 -SkipLagChecks
```

En este ejemplo se efectúa un cambio de una base de datos denominada DB5 en el servidor de buzón MBX6. En este ejemplo, la copia de base de datos de MBX6 tiene un *ContentIndexState* de Error. Por lo tanto, para activar la copia de base de datos de MBX6 se debe especificar el parámetro *SkipClientExperienceChecks*.

```powershell
Move-ActiveMailboxDatabase DB5 MBX6 -SkipClientExperienceChecks
```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la copia de la base de datos de buzones se activó correctamente, realice lo siguiente:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos adecuada y, en el panel Detalles, haga clic **Ver detalles** para ver las propiedades de la copia de base de datos.

  - En el Shell, ejecute el siguiente comando para mostrar la información de estado de una copia de base de datos.
    
    ```powershell
    Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
    ```

## Más información

[Copias de bases de datos de buzones](mailbox-database-copies-exchange-2013-help.md)

[Configuración de las propiedades de una copia de base de datos de buzones](configure-mailbox-database-copy-properties-exchange-2013-help.md)

