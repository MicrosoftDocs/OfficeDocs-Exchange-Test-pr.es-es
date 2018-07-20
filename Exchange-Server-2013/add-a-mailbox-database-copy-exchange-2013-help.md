---
title: 'Adición de una copia de base de datos de buzones: Exchange 2013 Help'
TOCTitle: Adición de una copia de base de datos de buzones
ms:assetid: 784bf48f-8af5-422c-a63f-2f01fc0cf151
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298080(v=EXCHG.150)
ms:contentKeyID: 48268305
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Adición de una copia de base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-30_

Cuando agrega una copia a la base de datos del buzón, se habilita automáticamente la replicación continua entre la base de datos existente y la copia de la base de datos. Se asigna una identidad automáticamente a las copias de la base de datos en formato de \<*DatabaseName*\>\\\<*HostMailboxServerName*\>. Por ejemplo, una copia de una base de datos DB1 que se hospeda en el servidor MBX3 sería DB1/MBX3.

¿Busca otras tareas de administración relacionadas con copias de bases de datos de buzones? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: dos minutos, más el tiempo necesario para inicializar la copia de base de datos, que depende de varios factores, como el tamaño de la base de datos, la velocidad, el ancho de banda disponible, la latencia de la red y las velocidades de almacenamiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Se debe montar la copia activa de la base de datos.

  - El servidor de buzones de correo especificado no debe hospedar una copia de la base de datos.

  - La ruta de la copia de base de datos y sus archivos de registro deberán estar disponibles en el servidor de buzones especificado.

  - El servidor que hospeda la copia de base de datos y el servidor que hospedará la copia pasiva deben estar en el mismo grupo de disponibilidad de base de datos (DAG). Además, el DAG deberá tener quórum y estar en buen estado.

  - Al agregar la segunda copia de una base de datos (por ejemplo, crear la primera copia pasiva de la base de datos), el registro circular no debe estar habilitado para la base de datos de buzón de correo especificada. Si el registro circular está habilitado, primero, lo deberá deshabilitar. Después de agregar la copia de la base de datos del buzón, se podrá habilitar el registro circular. Una vez que se haya habilitado el registro circular para una base de datos de buzón de correo replicada, se usa el registro circular de replicación continua (CRCL) en lugar del registro circular JET. Al agregar la tercer copia, o subsiguiente, a una base de datos, el CRCL puede permanecer habilitado.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para agregar una copia de base de datos de buzones de correo

1.  
    
    En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos que desea copiar y, a continuación haga clic en ![Agregar copia de base de datos](images/Dd298080.435c15ff-abf2-4de8-b280-f053db1afa13(EXCHG.150).gif "Agregar copia de base de datos").

3.  
    
    En la página **Agregar copia de base de datos de buzón**, haga clic en **Examinar...**, seleccione el servidor de buzones que hospedará la copia de la base de datos y, a continuación, haga clic en **Aceptar**.

4.  Alternativamente, puede configurar el **Número de preferencia de activación** para la copia de la base de datos.

5.  Haga clic en **Más opciones…** para designar la copia de base de datos como copia carlorifugada configurando un tiempo de retardo de posposición o para posponer la inicialización de la copia de la base de datos.

6.  Haga clic en **Guardar** para guardar los cambios de configuración y agregue la copia de base de datos de buzones de correo.

7.  Haga clic en **Aceptar** para confirmar los mensajes que aparecen.

## Usar el Shell para agregar una copia de base de datos de buzones

En este ejemplo se agrega una copia de la base de datos DB1 al servidor de buzón de correo MBX3. El tiempo de retardo de reproducción y el tiempo de retardo de truncamiento se dejan en los valores predeterminados de cero y la preferencia de activación está configurada con un valor de 2.

    Add-MailboxDatabaseCopy -Identity DB1 -MailboxServer MBX3 -ActivationPreference 2

En este ejemplo se agrega una copia de la base de datos DB2 al servidor de buzón de correo MBX4. El tiempo de retardo de reproducción y el tiempo de retardo de truncamiento se dejan en los valores predeterminados de cero y la preferencia de activación está configurada con un valor de `5`. Además, la inicialización se pospone para esta copia para que se inicialice usando un servidor de origen local en vez de la copia de la base de datos activa actual, geográficamente distante de MBX4.

    Add-MailboxDatabaseCopy -Identity DB2 -MailboxServer MBX4 -ActivationPreference 5 -SeedingPostponed

En este ejemplo se agrega una copia de la base de datos DB3 al servidor de buzón de correo MBX5. El tiempo de retardo de reproducción se establece en 3 días, el tiempo de retardo de truncamiento se deja en los valores predeterminados de cero y la preferencia de activación está configurada con un valor de `4`.

    Add-MailboxDatabaseCopy -Identity DB3 -MailboxServer MBX5 -ReplayLagTime 3.00:00:00 -ActivationPreference 4

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que ha creado una copia de base de datos de buzones correctamente, siga uno de los procedimientos siguientes:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos que se copió. En el panel Detalles se muestra el estado de la copia de base de datos y su índice de contenido, junto con la longitud de cola de la copia actual.

  - En el Shell, ejecute el siguiente comando para comprobar que la copia de la base de datos de buzones se creó y es correcta.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    Los valores de estado y de estado del índice de contenido deben ser correctos.

## Más información

[Copias de bases de datos de buzones](mailbox-database-copies-exchange-2013-help.md)

[Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md)

