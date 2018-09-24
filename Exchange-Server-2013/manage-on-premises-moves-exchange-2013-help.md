---
title: 'Administración de movimientos locales: Exchange 2013 Help'
TOCTitle: Administración de movimientos locales
ms:assetid: 1691b658-f5af-49c6-9170-5c3cb66c7306
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150487(v=EXCHG.150)
ms:contentKeyID: 48267832
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración de movimientos locales

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-02-25_

Una solicitud de traslado es el proceso de traslado de un buzón de una base de datos de buzones a otra. Una solicitud de movimiento local es una acción de movimiento de buzones que se produce dentro de un mismo bosque. En Microsoft Exchange Server 2013, los buzones de correo y los buzones correo de archivos personales pueden residir en bases de datos independientes. Mediante la función de solicitud de movimiento, puede mover el buzón principal y el archivo asociado a la misma base de datos o a bases de datos independientes. Los procedimientos de este tema le ayudarán con los movimientos de los buzones de correo locales.

Use los procedimientos siguientes para mover los buzones en su organización local. Estos procedimientos utilizan el Shell de administración de Exchange y Exchange Center (EAC).

Cuando usa la solicitud de movimiento para mover buzones, estas solicitudes se procesan con los dos servicios siguientes:

  - Servicio de replicación de buzones de correo de Microsoft Exchange

  - Proxy de replicación de buzones de correo de Microsoft Exchange

Para más información sobre el servidor y proxy de replicación de buzones, consulte [Obtenga más información acerca de Proxy MRS](https://technet.microsoft.com/es-es/library/jj156451\(v=exchg.150\)).

Para obtener más información acerca de los movimiento de buzones de correo, consulte [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 20 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Permisos de movimiento y migración de buzones" en [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Probar si un buzón está listo para la operación de movimiento

En este ejemplo se usa el modificador *WhatIf* para comprobar si el buzón de Tony Smith está listo para moverse a la nueva base de datos DB01 y si el comando presenta errores. Si usa el modificador *WhatIf*, el sistema realiza comprobaciones en el buzón. Si el buzón no está listo para el movimiento, recibirá un error.

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -TargetDatabase DB01 -WhatIf
```

Para obtener más información acerca de la sintaxis y los parámetros, consulte [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\)) y [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## Creación de una solicitud de movimiento local

## Uso del EAC para crear una solicitud de movimiento local

Para crear una solicitud de movimiento local, inicie sesión en EAC y realice los siguientes pasos:

1.  En el EAC, vaya a **Destinatarios** \> **Migración** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el Asistente para **Nuevo movimiento de buzón local**, seleccione el usuario que desee mover y haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

3.  En la página **Mover configuración** especifique un nombre para el nuevo lote. Seleccione las opciones que desee para el buzón de archivo y la ubicación de la base de datos de buzones y haga clic en **Nuevo**.

## Uso del Shell para crear una solicitud de movimiento local

Para obtener un ejemplo sobre cómo crear una solicitud de movimiento local, consulte el Ejemplo 2 en [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - En el EAC, vaya a **Destinatarios** \> **Migración**.

  - Compruebe que el movimiento se realizó correctamente en el EAC. Para ello, haga clic en **Estado de todos los lotes**.

  - Ejecute el siguiente comando en el Shell para recuperar la información de movimiento de buzones.
    
```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

Para obtener más información, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/es-es/library/jj218695\(v=exchg.150\)).

## Crear una solicitud de movimiento por lotes

## Uso del EAC para crear una solicitud de movimiento de lote

Inicie sesión en el EAC y realice los siguientes pasos:

1.  En el EAC, vaya a **Destinatarios** \> **Migración** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el Asistente para **Nuevo movimiento de buzón local**, seleccione los usuarios que desee mover y haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

3.  En la página **Mover configuración** especifique un nombre para el nuevo lote. Seleccione las opciones que desee para el buzón de archivo y la ubicación de la base de datos de buzones y haga clic en **Nuevo**.


> [!WARNING]
> Asegúrese de que no establece el límite de elementos incorrectos en más de 50 elementos. Al hacerlo, el movimiento puede fallar. Si quiere definir el límite de elementos incorrectos en más de 50, debe usar el Shell de administración de Exchange y definir el parámetro –<EM>AcceptLargeDataLoss</EM> en verdadero.



## Uso del Shell para crear una solicitud de movimiento de lote

Este ejemplo crea un lote de migración para un movimiento local, donde los buzones de correo que se encuentran en el archivo .csv especificado se mueven a otra base de datos de buzones de correo. El archivo .csv contiene una sola columna que contiene las direcciones de correo electrónico de cada uno de los buzones de correo que desea mover. El encabezado de esta columna debe denominarse **EmailAddress**. El lote de migración de este ejemplo se debe iniciar de forma manual mediante el cmdlet **Start-MigrationBatch** o el Centro de administración de Exchange (EAC). Como alternativa, puede utilizar el parámetro *AutoStart* para iniciar el lote de migración de forma automática.
```powershell
    New-MigrationBatch -Local -Name LocalMove1 -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\LocalMove1.csv")) -TargetDatabases MBXDB2 -TimeZone "Pacific Standard Time"
```

```powershell
Start-MigrationBatch -Identity LocalMove1
```


Para obtener más información acerca de la sintaxis y los parámetros, consulte [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\)) y [Start-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219165\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - Compruebe que el movimiento se realizó correctamente en el EAC. Para ello, haga clic en **Estado de todos los lotes**.

  - Ejecute el siguiente comando en el Shell para recuperar la información de movimiento de buzones.
    
```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

Para obtener más información, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/es-es/library/jj218695\(v=exchg.150\)).

## Ver lotes de migración

Para un ejemplo de cómo usar el Shell para mostrar un lote de migración, consulte el Ejemplo 2 en [Get-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219164\(v=exchg.150\)).

## Mover únicamente el buzón principal de un usuario

## Use el EAC para mover sólo un buzón de correo principal del usuario

1.  En el EAC, vaya a **Destinatarios** \> **Migración** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el Asistente para **Nuevo movimiento de buzón local**, seleccione el usuario cuyo buzón de correo principal desee mover y haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

3.  En la página **Mover configuración** especifique un nombre para el nuevo lote. Seleccione **Mover sólo el buzón de correo principal**, seleccione las opciones que desee para la ubicación de la base de datos de buzones de correo y, a continuación, haga clic en **Nuevo**.

## Usar el Shell para mover sólo el buzón principal de un usuario

En este ejemplo se mueve sólo el buzón principal de Tony Smith a DB01. No se mueve el archivo de almacenamiento.

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -PrimaryOnly -TargetDatabase "DB01"
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - En el EAC, haga clic en **Estado de todos los lotes**.

  - Ejecute el siguiente comando en el Shell para recuperar la información de movimiento de buzones.
    
```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

Para obtener más información, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/es-es/library/jj218695\(v=exchg.150\)).

## Crear un movimiento entre bosques usando un archivo de lotes .csv

Este ejemplo configura el extremo de la migración y, a continuación, crea un movimiento de lotes entre bosques del bosque de origen al bosque de destino usando un archivo .csv.
```powershell
    New-MigrationEndpoint -Name Fabrikam -ExchangeRemote -Autodiscover -EmailAddress tonysmith@fabrikam.com -Credentials (Get-Credential fabrikam\tonysmith) 
    
    $csvData=[System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\batch.csv")
    New-MigrationBatch -CSVData $csvData -Timezone "Pacific Standard Time" -Name FabrikamMerger -SourceEndpoint Fabrikam -TargetDeliveryDomain "mail.contoso.com"
```

Para obtener más información acerca de la preparación de su bosque para los movimientos entre bosques, consulte los siguientes temas:

  - [Preparar los buzones para las solicitudes de movimiento entre bosques](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Preparar buzones para movimientos entre bosques mediante código de ejemplo](prepare-mailboxes-for-cross-forest-moves-using-sample-code-exchange-2013-help.md)

  - [Preparar buzones para moverlos entre bosques con el script Prepare-MoveRequest.ps1 en el Shell](prepare-mailboxes-for-cross-forest-moves-using-the-prepare-moverequest-ps1-script-in-the-shell-exchange-2013-help.md)

Para obtener más información acerca de la sintaxis y los parámetros, consulte [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\)) y [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - Ejecute el siguiente comando en el Shell para recuperar la información de movimiento de buzones.
    
```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

Para obtener más información, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/es-es/library/jj218695\(v=exchg.150\)).

## Mover solamente un buzón de archivo

## Use el EAC para mover sólo un buzón de archivo

1.  En el EAC, vaya a **Destinatarios** \> **Migración** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el Asistente para **Nuevo movimiento de buzón local**, seleccione el usuario cuyo buzón de archivo desee mover y haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

3.  En la página **Mover configuración** especifique un nombre para el nuevo lote. Seleccione **Mover sólo el buzón de archivo**, seleccione las opciones que desee para la ubicación de la base de datos de buzones de correo y, a continuación, haga clic en **Nuevo**.

## Usar el Shell para mover sólo un buzón de archivo

En este ejemplo se mueve sólo buzón del archivo de Tony Smith a DB03. No se mueve el buzón principal.

```powershell
New-MoveRequest -Identity 'tony@alpineskihouse.com' -ArchiveOnly -ArchiveTargetDatabase "DB03"
```

Para obtener más información acerca de la sintaxis y los parámetros, consulte [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\)) y [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - Ejecute el siguiente comando en el Shell para recuperar la información de movimiento de buzones.
    
```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

Para obtener más información, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/es-es/library/jj218695\(v=exchg.150\)).

## Mover el buzón de archivo y el buzón principal de un usuario a bases de datos independientes

En este ejemplo se mueve el buzón principal y el buzón de archivo de Ayla a dos bases de datos diferentes. La base de datos principal se mueve a DB01 y la de archivo a DB03.
```powershell
    New-MoveRequest -Identity 'ayla@humongousinsurance.com' -TargetDatabase DB01 -ArchiveTargetDatabase -DB03
```

Para obtener más información acerca de la sintaxis y los parámetros, consulte [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\)) y [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - Ejecute el siguiente comando en el Shell para recuperar la información de movimiento de buzones.
    
```powershell
Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
```

Para obtener más información, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/es-es/library/jj218695\(v=exchg.150\)).

## Mover el buzón principal de un usuario y permitir un límite de elementos defectuosos elevado

## Usar el EAC para mover el buzón principal de un usuario y permitir un límite de elementos defectuosos elevado

1.  En el EAC, vaya a **Destinatarios** \> **Migración** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En el Asistente para **Nuevo movimiento de buzón local**, seleccione el usuario cuyo buzón de correo principal desee mover y haga clic en **Aceptar** y, a continuación, haga clic en **Siguiente**.

3.  En la página **Mover configuración** especifique un nombre para el nuevo lote. Seleccione **Mover sólo el buzón de correo principal**, y, a continuación, seleccione las opciones que desee para la ubicación de la base de datos de buzones de correo.

4.  Haga clic en **Más opciones**![Icono Más opciones](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif "Icono Más opciones"), escriba el límite de elementos defectuosos y, a continuación, haga clic en **Aceptar**.

## Usar el Shell para mover el buzón principal de un usuario y permitir un límite de elementos defectuosos elevado

En este ejemplo se mueve el buzón principal de Lisa a la base de datos de buzones DB01 y se establece el límite de elementos defectuosos en `100`. Para establecer un límite de elementos defectuosos elevado, debe usar el parámetro *AcceptLargeDataLoss*.
```powershell
New-MoveRequest -Identity 'Lisa' -PrimaryOnly -TargetDatabase "DB01" -BadItemLimit 100 -AcceptLargeDataLoss
```

Para obtener más información acerca de la sintaxis y los parámetros, consulte [New-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219166\(v=exchg.150\)) y [New-MoveRequest](https://technet.microsoft.com/es-es/library/dd351123\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que la migración se completó correctamente, realice lo siguiente:

  - Ejecute el siguiente comando en el Shell para recuperar la información de movimiento de buzones.
    
    ```powershell
    Get-MigrationUserStatistics -Identity BatchName -Status | Format-List
    ```

Para obtener más información, consulte [Get-MigrationUserStatistics](https://technet.microsoft.com/es-es/library/jj218695\(v=exchg.150\)).

