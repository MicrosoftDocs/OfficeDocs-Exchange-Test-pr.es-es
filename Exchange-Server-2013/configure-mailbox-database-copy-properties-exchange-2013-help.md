---
title: 'Configuración propiedades de copia de base datos buzones: Exchange 2013 Help'
TOCTitle: Configuración de las propiedades de una copia de base de datos de buzones
ms:assetid: cf186561-ab2c-45c0-90f5-8d3ecfabeeac
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351151(v=EXCHG.150)
ms:contentKeyID: 48268684
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configuración de las propiedades de una copia de base de datos de buzones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-11-01_

Cada copia de base de datos de buzones tiene sus propiedades, configurables por el usuario. Consisten en la cantidad de tiempo, si lo hay, de retardo de reproducción y del retardo de truncamiento, así como el número de la preferencia de activación. Para obtener más información sobre el tiempo de retardo de reproducción y el de retardo de truncamiento y el número de la preferencia de activación, consulte [Administración de copias de bases de datos de buzones de correo](managing-mailbox-database-copies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar esta tarea: 1 minuto

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte elEntrada "Copias de base de datos de buzones" en el tema [Permisos de alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar las propiedades de copia de bases de datos de buzones

1.  En el EAC, vaya a **Servidores** \> **Bases de datos**.

2.  Seleccione la base de datos que desea configurar.

3.  En el panel de detalles, en **Copias de bases de datos**, haga clic en **Ver detalles** para la copia de base de datos deseada y, a continuación, vea o configure lo siguiente:
    
      - **Base de datos**   Muestra el nombre de la base de datos seleccionada.
    
      - **Servidor de buzones**   Muestra el nombre del servidor de buzones que hospeda la copia de base de datos seleccionada.
    
      - **Estado del índice de contenido** Muestra el estado actual del índice de contenido de la copia de base de datos seleccionada.
    
      - **Estado**   Muestra el estado actual de la copia de base de datos seleccionada.
    
      - **Longitud de cola de copia**   Indica el número de archivos de registro a la espera de copiarse en la copia de base de datos seleccionada. Este campo es relevante sólo para copias de bases de datos pasivas.
    
      - **Longitud de cola de reproducción**   Indica el número de archivos de registro a la espera de reproducirse en la copia de base de datos seleccionada. Este campo es relevante sólo para copias de bases de datos pasivas.
    
      - **Mensajes de error**   Muestra los mensajes de error para las copias de bases de datos que tengan un estado de `Failed` o `Failed and Suspended`.
    
      - **Hora del último registro disponible**   Muestra la fecha y marca de tiempo del último archivo de registro generado en la copia activa de la base de datos. Este campo es relevante sólo para copias de bases de datos pasivas. En las copias de bases de datos activas (replicadas e independientes), este campo mostrará **nunca**.
    
      - **Hora del último registro inspeccionado**   Muestra la fecha y la marca de tiempo del último archivo que LogInspector inspeccionó en la copia de base de datos seleccionada. Este campo es relevante sólo para copias de bases de datos pasivas. En las copias de bases de datos activas (replicadas e independientes), este campo mostrará **nunca**.
    
      - **Hora del último registro copiado**   Muestra la fecha y la marca de tiempo del último archivo que LogCopier copió en la copia de base de datos seleccionada. Este campo es relevante sólo para copias de bases de datos pasivas. En las copias de bases de datos activas (replicadas e independientes), este campo mostrará **nunca**.
    
      - **Hora del último registro reproducido**   Muestra la fecha y la marca de tiempo del último archivo que LogReplayer reprodujo en la copia de base de datos seleccionada. Este campo es relevante sólo para copias de bases de datos pasivas. En las copias de bases de datos activas (replicadas e independientes), este campo mostrará **nunca**.
    
      - **Número de preferencia de activación**   Muestra el número de preferencia de activación. Este número se usa como parte del proceso de selección de mejor copia de Active Manager y para redistribuir las bases de datos de buzones activas en el DAG para equilibrarlo mediante el script RedistributeActiveDatabases.ps1. El valor para la preferencia de activación es un número igual o superior a 1, donde 1 está al principio de la orden de preferencia. El número no puede ser más grande que el número de copias de la base de datos de buzones.
    
      - **Reproducir tiempo de posposición (días)**   Muestra el tiempo que debe esperar el servicio de almacén de información de Microsoft Exchange hasta que se reproduzcan los archivos de registro que el servicio de replicación de Microsoft Exchange copió en una copia de base de datos pasiva. Si se establece este parámetro en un valor mayor que 0, se crea una copia de la base de datos retrasada. La configuración predeterminada para este valor es 0 días. El valor máximo permitido para esta configuración es 14 días. El valor mínimo permitido es 0 días. Si este valor se configura en 0, se desactiva el retraso de reproducción.

## Uso del Shell para configurar las propiedades de copia de base de datos de buzones

En este ejemplo se configura una copia de base de datos de buzones con un número de la preferencia de activación de 3.

```powershell
Set-MailboxDatabaseCopy -Identity DB3\EX3 -ActivationPreference 3
```

En este ejemplo se configura una copia de la base de datos DB1 que se hospeda en Server1 con tiempos de retardo de reproducción y de retardo de truncamiento de 1 día y un número de preferencia de activación de 2.

    Set-MailboxDatabaseCopy -Identity DB1\Server1 -ReplayLagTime 1.0:0:0 -TruncationLagTime 1.0:0:0 -ActivationPreference 2

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la copia de la base de datos de buzones se configuró correctamente, realice lo siguiente:

  - En el EAC, vaya a **Servidores** \> **Bases de datos**. Seleccione la base de datos adecuada y, en el panel Detalles, haga clic en **Ver detalles** para ver las propiedades de la copia de base de datos.

  - En el Shell, ejecute el siguiente comando para mostrar la información de configuración de una copia de base de datos.
    
    ```powershell
Get-MailboxDatabaseCopyStatus <DatabaseCopyName> | Format-List
```

## Más información

[Set-MailboxDatabaseCopy](https://technet.microsoft.com/es-es/library/dd298104\(v=exchg.150\))

[Get-MailboxDatabaseCopyStatus](https://technet.microsoft.com/es-es/library/dd298044\(v=exchg.150\))

[Get-MailboxDatabase](https://technet.microsoft.com/es-es/library/bb124924\(v=exchg.150\))

