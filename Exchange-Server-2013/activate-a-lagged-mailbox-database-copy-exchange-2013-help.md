---
title: 'Activación de una copia de base de datos de buzones atrasada: Exchange 2013 Help'
TOCTitle: Activación de una copia de base de datos de buzones atrasada
ms:assetid: 493d9c40-644d-49d6-9291-949acbcfdcb6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979786(v=EXCHG.150)
ms:contentKeyID: 48268083
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Activación de una copia de base de datos de buzones atrasada

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2014-01-28_

Una copia de la base de datos de buzones de correo atrasada es una copia de la base de datos de buzones de correo configurada con un valor de tiempo de retardo de reproducción mayor que 0. La activación y la recuperación de una copia de la base de datos de buzones de correo atrasada es un proceso sencillo si desea que la base de datos reproduzca todos los archivos de registro y actualice la copia de la base de datos. Si desea reproducir los archivos de registro hasta un momento dado, la operación es un poco más difícil porque debe modificar los archivos de registro de forma manual y ejecutar Eseutil.

¿Busca otra información relacionada con las copias de bases de datos de buzones atrasadas? Consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).


> [!NOTE]
> El tiempo necesario para activar una copia de la base de datos de buzones de correo atrasada depende de cuántos archivos de registro se deben reproducir y con cuánta rapidez el hardware los puede reproducir. Como mínimo, deberá experimentar una velocidad de reproducción de dos registros por segundo por base de datos.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 minuto, más el tiempo que se tarda en duplicar la copia retrasada, reproducir los archivos de registro necesarios y extraer los datos o montar la base de datos para la actividad del cliente.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada «Copias de base de datos de buzones» en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - La copia de la base de datos de buzones de correo que desea activar debe estar configurada con un tiempo de retardo de reproducción mayor que 0.

  - La copia de la base de datos de buzones de correo que desea activar debe tener todos los archivos de registro en el momento dado en el que desea recuperarla. Tenga en cuenta que las transacciones de bases de datos pueden abarcar varios archivos de registro cuando determine el momento dado en el que desea recuperarla.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para activar una copia de la base de datos de buzones de correo atrasada en un momento dado


> [!NOTE]
> No puede usar el Centro de administración de Exchange para activar una copia de base de datos de buzones de correo atrasada en un momento dado. En su lugar, puede realizar una serie de pasos con el Shell y la línea de comandos.



1.  En este ejemplo, se suspende la replicación para la copia retrasada que se activa usando el cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd351074\(v=exchg.150\)).
    
        Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false

2.  De manera opcional (para preservar una copia atrasada), realice una copia de la copia de la base de datos y de sus archivos de registro.
    

    > [!NOTE]
    > En este punto, si continúa para realizar este procedimiento en el volumen existente, podría incurrir en una penalización de rendimiento de copia en escritura. Si esto no es satisfactorio, puede copiar la base de datos y los archivos de registro en otro volumen para realizar la recuperación.



3.  Determine qué archivos de registro son necesarios para reproducir la base de datos a fin de satisfacer el requisito del momento dado para esta recuperación (de acuerdo con la fecha y la hora del archivo de registro, como se muestra en Windows Explorer). Todos los registros que se creen a partir de este momento se deben mover a un directorio distinto hasta que se complete el proceso de recuperación y ya no sean necesarios.

4.  Elimine el archivo de controles (.chk) para la base de datos.

5.  En este ejemplo, se usa Eseutil para realizar la operación de recuperación.
    
        Eseutil.exe /r eXX /a
    

    > [!NOTE]
    > En el ejemplo anterior, e<EM>XX</EM> es el prefijo de generación de registros para la base de datos (por ejemplo, E00, E01, E02, etc.).

    

    > [!IMPORTANT]
    > Este paso puede insumir un tiempo considerable según varios factores como la duración del tiempo de retardo de reproducción, el número de archivos de registro generados durante ese tiempo y la velocidad a la cual el hardware puede reproducir esos registros en la base de datos que desea recuperar.



6.  Una vez finalizada la reproducción del registro, la base de datos se encuentra en un estado de cierre limpio y se puede copiar y usar con fines de recuperación.

7.  Una vez finalizado el proceso de recuperación, en este ejemplo, se reanuda la replicación de la base de datos que se usó como parte del proceso de recuperación.
    
        Resume-MailboxDatabaseCopy DB1\EX3

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd351074\(v=exchg.150\)) o [Resume-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd335220\(v=exchg.150\)).

## Uso del Shell para activar una copia de base de datos de buzones de correo atrasada mediante la reproducción de todos los archivos de registro no confirmados

1.  De manera opcional (para preservar una copia atrasada), realice una copia de la copia de la base de datos y de sus archivos de registro.
    
    1.  En este ejemplo, se suspende la replicación para la copia retrasada que se activa usando el cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  De manera opcional (para preservar una copia atrasada), realice una copia de la copia de la base de datos y de sus archivos de registro.
        

        > [!NOTE]
        > En este punto, si continúa para realizar este procedimiento en el volumen existente, podría incurrir en una penalización de rendimiento de copia en escritura. Si esto no es satisfactorio, puede copiar la base de datos y los archivos de registro en otro volumen para realizar la recuperación.



2.  En este ejemplo, se activa la copia de base de datos de buzones de correo atrasada usando el cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/es-es/library/dd298068\(v=exchg.150\)) con el parámetro *SkipLagChecks*.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -SkipLagChecks

## Uso del Shell para activar una copia de base de datos de buzones de correo atrasada usando la recuperación de SafetyNet

1.  Opcionalmente (para preservar una copia atrasada), mediante el Servicio de instantáneas de volumen (VSS), tome una instantánea basada en sistema de archivos (sin conocimiento de Exchange) de los volúmenes que contienen la copia de base de datos y los archivos de registro.
    
    1.  En este ejemplo, se suspende la replicación para la copia retrasada que se activa usando el cmdlet [Suspend-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd351074\(v=exchg.150\)).
        
            Suspend-MailboxDatabaseCopy DB1\EX3 -SuspendComment "Activate lagged copy of DB1 on Server EX3" -Confirm:$false
    
    2.  De manera opcional (para preservar una copia atrasada), realice una copia de la copia de la base de datos y de sus archivos de registro.
        

        > [!NOTE]
        > En este punto, si continúa para realizar este procedimiento en el volumen existente, podría incurrir en una penalización de rendimiento de copia en escritura. Si esto no es satisfactorio, puede copiar la base de datos y los archivos de registro en otro volumen para realizar la recuperación.



2.  Determine los registros necesarios para la copia de base de datos atrasada. Para ello, busque el valor «Registro necesario:» en el resultado del encabezado de base de datos ESEUTIL.
    
        Eseutil /mh <DBPath> | findstr /c:"Log Required"
    
    Tome nota de los números hexadecimales entre paréntesis. El primer número es la generación más baja necesaria (denominada LowGeneration) y el segundo número es la generación más alta necesaria (denominada HighGeneration). Mueva todos los archivos de generación de registros que tienen una generación de secuencia más alta que HighGeneration a una ubicación diferente de modo que no se reproduzcan nuevamente en la base de datos.

3.  En el servidor que hospeda la copia activa de la base de datos, elimine los archivos de registro para la copia atrasada que se está activando de la copia activa, o bien detenga el servicio de replicación de Microsoft Exchange.

4.  Realice un cambio de base de datos y active la copia atrasada. Este ejemplo activa la base de datos mediante el cmdlet [Move-ActiveMailboxDatabase](https://technet.microsoft.com/es-es/library/dd298068\(v=exchg.150\)) con varios parámetros.
    
        Move-ActiveMailboxDatabase DB1 -ActivateOnServer EX3 -MountDialOverride BestEffort -SkipActiveCopyChecks -SkipClientExperienceChecks -SkipHealthChecks -SkipLagChecks

5.  En este punto, la base de datos se montará automáticamente y solicitará la entrega de los mensajes faltantes de SafetyNet.

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya activado una copia de base de datos de buzones de correo atrasada correctamente, siga uno de estos pasos:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos adecuada y, en el panel Detalles, haga clic **Ver detalles** para ver las propiedades de la copia de base de datos.

  - En el Shell, ejecute el siguiente comando para mostrar la información de estado de una copia de base de datos.
    
        Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List

