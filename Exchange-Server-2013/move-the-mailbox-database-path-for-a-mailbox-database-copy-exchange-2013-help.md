---
title: 'Mover ruta base dato buzón para copia base dato buzón Exchange 2013 Help'
TOCTitle: Mover la ruta de acceso a la base de datos de buzones de correo para la copia de una base de datos de buzones
ms:assetid: 324f255c-d95d-4a8a-a134-c8cee5c5b9cb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979782(v=EXCHG.150)
ms:contentKeyID: 48267961
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover la ruta de acceso a la base de datos de buzones de correo para la copia de una base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-05-07_

Después de crear una base de datos de buzones de correo, es posible moverla a otro volumen u otra carpeta, ubicación o ruta de acceso mediante el EAC o el Shell. Para obtener instrucciones paso a paso acerca de cómo mover la ruta de acceso a una base de datos de buzones de correo no replicada, consulte [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

Si la base de datos de buzones de correo que se está moviendo está replicada en al menos una copia de base de datos de buzones de correo, se deberá seguir el procedimiento de este tema para mover la ruta de acceso. Todas las copias de una base de datos de buzones de correo deben estar ubicadas en la misma ruta de acceso de cada servidor que aloja una copia. Por ejemplo, si la base de datos DB1 está ubicada en la ruta C:\\mountpoints\\DB1 en el servidor EX1, las copias de DB1 que se encuentren en los servidores EX2, EX3, etc. también deben estar ubicadas en C:\\mountpoints\\DB1.

¿Está buscando otras tareas de administración relacionadas con copias de bases de datos de buzones de correo? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 2 minutos, más el tiempo necesario para mover los datos, que depende de varios factores, como el tamaño de la base de datos, la velocidad, el ancho de banda disponible, la latencia de la red y las velocidades de almacenamiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para realizar esta operación, la base de datos debe estar temporalmente desmontada, con lo cual es inaccesible para todos los usuarios. Si la base de datos está desmontada, no se volverá a montar hasta que no se haya completado la operación.

  - Para llevar a cabo la operación de movimiento, se debe deshabilitar la replicación de la base de datos para todas las copias. Suspender la replicación no es suficiente; es necesario deshabilitarla mediante el cmdlet [Remove-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335119\(v=exchg.150\)) para quitar las copias de la base de datos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para mover una base de datos de buzones de correo replicada a una nueva ruta de acceso


> [!NOTE]
> No puede usar el EAC para mover una base de datos de buzones de correo replicada a una nueva ruta de acceso.



1.  Tenga cuenta toda posible configuración de retardo de reproducción o retardo de truncamiento en todas las copias de la base de datos de buzones de correo que se estén moviendo. Esta información puede obtenerse mediante el cmdlet [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\)), como se muestra en este ejemplo.
    
        Get-MailboxDatabase DB1 | Format-List *lag*

2.  Si la base de datos tiene el registro circular habilitado, se lo debe deshabilitar antes de proceder. El registro circular de una base de datos de buzones de correo puede deshabilitarse mediante el cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)), como se muestra en este ejemplo.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $false

3.  Quite todas las copias de base de datos de buzones de correo para la base de datos que se desea mover. Para obtener instrucciones detalladas, consulte [Eliminación de una copia de base de datos de buzones](remove-a-mailbox-database-copy-exchange-2013-help.md). Después de quitar todas las copias, guarde los archivos de registro de base de datos y de transacción que genera cada servidor de los cuales se quitará una copia de la base de datos. Para ello, muévalos a otra ubicación. Estos archivos se guardan para que las copias de la base de datos no soliciten reinicialización después de volverlas a agregar.

4.  Mueva la ruta de acceso a la base de datos de buzones de correo a la nueva ubicación. Para conocer los pasos detallados, consulte [Move a mailbox database path](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Durante la operación de movimiento, se debe desmontar la base de datos trasladada. Hasta que el movimiento se haya completado, este proceso causará una interrupción en el servicio y un corte para todos los usuarios que tengan buzones en la base de datos trasladada. Una vez finalizada la operación de movimiento, la base de datos se montará automáticamente.



5.  Cree la estructura de carpetas necesaria en cada servidor de buzones que anteriormente contenía una copia pasiva de la base de datos de buzones de correo trasladada. Por ejemplo, si movió la base de datos a C:\\mountpoints\\DB1, deberá crear esta misma ruta de acceso en cada servidor de buzones que alojará una copia de la base de datos de buzones de correo.

6.  Después de crear la estructura de carpetas, mueva la copia pasiva de la base de datos de buzones de correo y su secuencia de registro a la nueva ubicación. Se trata de los archivos que quedaron y se guardaron después del paso 3. Repita este proceso para cada copia de la base de datos que se haya quitado en aquel paso.

7.  Agregue todas las copias de la base de datos que se quitaron en el paso 3. Para conocer más información, consulte [Adición de una copia de base de datos de buzones](add-a-mailbox-database-copy-exchange-2013-help.md).

8.  En cada servidor que contenga una copia de la base de datos de buzones de correo trasladada, ejecute los siguientes comandos para detener y reiniciar los servicios de índice de contenido.
    
        Net stop MSExchangeFastSearch
        Net start MSExchangeFastSearch

9.  De manera opcional, es posible habilitar el registro circular mediante el cmdlet [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\)), como se muestra en este ejemplo.
    
        Set-MailboxDatabase DB1 -CircularLoggingEnabled $true

10. Vuelva a configurar todo valor previamente fijado para los tiempos de retardo de reproducción y retardo de truncamiento, mediante el cmdlet [Set-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298104\(v=exchg.150\)), como se muestra en este ejemplo.
    
        Set-MailboxDatabaseCopy DB1\MBX2 -ReplayLagTime 00:15:00

11. A medida que se agrega cada copia, se recomienda comprobar las condiciones y el estado de la copia antes de agregar la siguiente. Puede comprobar las condiciones y el estado de las siguientes maneras:
    
    1.  Mediante un examen del registro de eventos para verificar si existen eventos de error o advertencia relacionados con la base de datos o su copia.
    
    2.  Mediante el uso del cmdlet [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\)) para verificar las condiciones y el estado de replicación continua de la copia de la base de datos.
    
    3.  Mediante el uso del cmdlet [Test-ReplicationHealth](https://technet.microsoft.com/es-es/library/bb691314\(v=exchg.150\)) para comprobar las condiciones y el estado del grupo de disponibilidad de la base de datos y la replicación continua.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\))

  - [Set-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb123971\(v=exchg.150\))

  - [Set-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298104\(v=exchg.150\))

  - [Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\))

  - [Test-ReplicationHealth](https://technet.microsoft.com/es-es/library/bb691314\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya movido correctamente la ruta de una copia de base de datos de buzones de correo, siga uno de estos pasos:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos que se copió. En el panel Detalles se muestra el estado de la copia de base de datos y su índice de contenido, junto con la longitud de cola de la copia actual. Compruebe que esté en buen estado.

  - En el Shell, ejecute el siguiente comando para comprobar que la copia de la base de datos de buzones de correo se haya creado y sea correcta.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName>
    
    Los valores de estado y de estado del índice de contenido deben ser correctos.

