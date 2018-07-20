---
title: 'Configurar el registro circular para una base de datos de buzones: Exchange 2013 Help'
TOCTitle: Configurar el registro circular para una base de datos de buzones
ms:assetid: 29cbd7cd-382b-4e0d-8368-2e49e75df2fc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn756374(v=EXCHG.150)
ms:contentKeyID: 62524849
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el registro circular para una base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-06-24_

Cuando se habilita el registro circular para una base de datos de buzones, el tipo de registro circular que obtendrá depende de si la base de datos de buzón se replica mediante replicación continua:

  - Si la base de datos de buzones no se replica, utilizará el registro circular de JET. En este caso, para habilitar o deshabilitar el registro circular de JET será necesario desmontar y montar la base de datos.

  - Si la base de datos de buzones se replica, utilizará el registro circular de replicación continua (CRCL). En este caso, la habilitación o deshabilitación de CRCL surte efecto dinámicamente; no es necesario desmontar y volver a montar la base de datos.

Para obtener más información acerca del registro circular y CRCL, consulte [Exchange Native Data Protection](backup-restore-and-disaster-recovery-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Permisos de bases de datos de buzones" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

## Usar el EAC para configurar el registro circular para una base de datos

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos de buzones que quiere configurar y haga clic en ![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Active o desactive la casilla **Habilitar registro circular** y, después, haga clic en **Guardar**.

4.  Si se necesita una operación de montaje y desmontaje, aparecerá un mensaje de advertencia. Haga clic en **Aceptar** para cerrar el mensaje de advertencia.
    
    1.  Para desmontar la base de datos, haga clic en **Más**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, después, haga clic en **Desmontar**. Haga clic en **Sí** cuando se muestre el mensaje de advertencia.
    
    2.  Para montar la base de datos, haga clic en **Más**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones") y, después, haga clic en **Montar**. Haga clic en **Sí** cuando se muestre el mensaje de advertencia.

## Usar el Shell para configurar el registro circular para una base de datos

En este ejemplo se habilita el registro circular para la base de datos DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $True

En este ejemplo se deshabilita el registro circular para la base de datos DB1.

    Set-MailboxDatabase DB1 -CircularLoggingEnabled $False

Para ver otros parámetros de la base de datos de buzones que puede configurar, consulte [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)).

