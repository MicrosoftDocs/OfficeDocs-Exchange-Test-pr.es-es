---
title: 'Eliminación de una copia de base de datos de buzones: Exchange 2013 Help'
TOCTitle: Eliminación de una copia de base de datos de buzones
ms:assetid: 99fecdde-b158-4dfc-9ca7-ff7c0ada7819
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298164(v=EXCHG.150)
ms:contentKeyID: 48268468
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminación de una copia de base de datos de buzones

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-11-06_

Estos procedimientos le muestran cómo quitar una copia de una base de datos de buzones. No puede usar estos procedimientos para eliminar la última copia de una base de datos de buzones. Para obtener instrucciones detalladas sobre cómo quitar la última copia de una base de datos de buzones, vea [Remove a mailbox database](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md) o [Remove-MailboxDatabase](https://technet.microsoft.com/es-es/library/aa997931\(v=exchg.150\)).

¿Busca otras tareas de administración relacionadas con copias de bases de datos de buzones? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Las copias de una base de datos de buzones solo se puede quitar desde un grupo de disponibilidad de base de datos (DAG) que funcione correctamente. Si el DAG no funciona correctamente (por ejemplo, el clúster subyacente del DAG no está activo porque se perdió quórum), no podrá quitar ninguna copia de bases de datos de buzones.

  - Si elimina la última copia pasiva de la base de datos, no debe estar habilitado el registro circular de replicación continua (CRCL) para la base de datos del buzón especificado. Si CRCL está habilitado, primero debe deshabilitarlo. Después de que se haya eliminado la copa de base de datos de buzones, puede habilitarse el registro circular. Después de habilitarlo para una base de datos de buzones no replicada, se usa el registro circular JET en lugar de CRCL. Si no elimina la última copia pasiva de una base de datos, CRCL puede permanecer habilitado.

  - Después de quitar una copia de base de datos, debe eliminar del servidor del cual se está quitando la copia cualquier archivo de base de datos y archivo de registro de forma manual.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para quitar una copia de base de datos de buzones de correo

1.  En el EAC, navegue a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos de buzones de correo cuya copia desea quitar.

3.  En el panel Detalles, ubique la copia pasiva que desea quitar y haga clic en **Quitar**.

4.  Para confirmar la eliminación, en el cuadro de diálogo de advertencia, haga clic en **Sí**.

5.  Haga clic en **Aceptar** para confirmar la eliminación y cualquier mensaje de advertencia.

6.  Elimine de forma manual cualquier archivo de registro de transacciones y base de datos del servidor desde el cual se eliminará la copia de base de datos.

## Usar el Shell para quitar una copia de base de datos de buzones

En este ejemplo se quita una copia de base de datos de buzones de correo DB1 del servidor de buzones de correo MBX1.

    Remove-MailboxDatabaseCopy -Identity DB1\MBX1 -Confirm:$False

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha eliminado una Retención local correctamente, siga uno de estos procedimientos:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos pertinente y, en el panel Detalles dejará de aparecer la copia pasiva que haya quitado.

  - En el Shell, ejecute el siguiente comando para comprobar que ha quitado la copia.
    
        Get-MailboxDatabase <DatabaseName> | Format-List DatabaseCopies
    
    La copia pasiva eliminada ya no aparece.

