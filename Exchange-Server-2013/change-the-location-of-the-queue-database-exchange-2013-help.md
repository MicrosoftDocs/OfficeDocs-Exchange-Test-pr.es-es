---
title: 'Cambio de la ubicación de la base de datos de colas: Exchange 2013 Help'
TOCTitle: Cambio de la ubicación de la base de datos de colas
ms:assetid: f170cb0c-04a9-4fa7-b594-206e3a787e14
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125177(v=EXCHG.150)
ms:contentKeyID: 51406574
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cambio de la ubicación de la base de datos de colas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Una *cola* es una ubicación temporal para hospedar mensajes que esperan a entrar en la próxima etapa de procesamiento. Cada cola representa un conjunto lógico de mensajes que procesa el servidor de transporte en un orden específico.

Como en versiones anteriores de Exchange, Microsoft Exchange Server 2013 usa una base de datos del motor de almacenamiento extensible (ESE) para el almacenamiento de los mensajes en cola. Todas las diferentes colas se almacenan en una única base de datos ESE. Las colas solo existen en los servidores de buzones o en los servidores de transporte perimetral.

La ubicación de la base de datos de colas y de los registros de transacciones de bases de datos de colas la controlan las claves en el archivo de configuración de la aplicación XML `%ExchangeInstallPath%Bin\EdgeTransport.exe.config`. Este archivo está asociado con el servicio de transporte de Microsoft Exchange. La tabla siguiente explica todas las claves con mayor detalle.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>QueueDatabasePath</em></p></td>
<td><p>Esta clave especifica la ubicación de los archivos de la base de datos de colas. Los archivos son:</p>
<ul>
<li><p>Mail.que</p></li>
<li><p>Trn.chk</p></li>
</ul>
<p>La ubicación predeterminada es <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>QueueDatabaseLoggingPath</em></p></td>
<td><p>Esta clave especifica la ubicación de los archivos de registros de transacciones de la base de datos de colas. Los archivos son:</p>
<ul>
<li><p>Trn.log</p></li>
<li><p>Trntmp.log</p></li>
<li><p>Trn<em>nnn</em>.log</p></li>
<li><p>Trnres00001.jrs</p></li>
<li><p>Trnres00002.jrs</p></li>
<li><p>Temp.edb</p></li>
</ul>
<p>Tenga en cuenta que Temp.edb se usa para comprobar el esquema de la base de datos de colas cuando se inicia el servicio de transporte de Microsoft Exchange. Aunque Temp.edb no es un archivo de registro de transacción, se mantiene en la misma ubicación que los archivos de registro de transacción.</p>
<p>La ubicación predeterminada es <code>%ExchangeInstallPath%TransportRoles\data\Queue</code>.</p></td>
</tr>
</tbody>
</table>


## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  15 minutos.

  - Los permisos de Exchange no se aplican a los procedimientos de este tema. Estos procedimientos se realizan en el sistema operativo de Exchange Server.

  - Cuando detiene o reinicia el servicio de transporte de Microsoft Exchange, el flujo de correo en el servidor se interrumpe.

  - Al modificar la ubicación de la base de datos de colas o de los registros de transacción, la base de datos de colas y los archivos de registros de transacciones existentes no se mueven. En la nueva ubicación se crean nuevos registros de transacciones y una nueva base de datos de colas. Los archivos existentes se conservan en la antigua ubicación. No obstante, ya no se usan. Si desea volver a usar los archivos de registros de transacción o la base de datos de colas existentes en la nueva ubicación, debe mover los archivos existentes a la nueva ubicación cuando el servicio de transporte de Microsoft Exchange se detenga, pero antes de que se inicie el servicio.

  - Si la carpeta de destino de la base de datos de colas o de los registros de transacción no existe, se creará automáticamente si la carpeta primaria tiene aplicados los siguientes permisos:
    
      - Servicio de red: Control total
    
      - Sistema: Control total
    
      - Administradores: Control total

  - Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

## ¿Qué desea hacer?

## Usar el símbolo del sistema para crear una base de datos de colas y registros de transacciones nuevos en una nueva ubicación

1.  Cree las carpetas donde desee mantener los registros de transacciones y la base de datos de colas. Asegúrese de que se aplican los permisos correctos a las carpetas.

2.  En una ventana del símbolo del sistema, abra el archivo EdgeTransport.exe.config en el Bloc de notas mediante el comando siguiente:
    
    ```powershell
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

3.  Modifique las claves siguientes en la sección `<appSettings>`.
    
    ```powershell
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    ```
    
    Por ejemplo, para crear una base de datos de colas nueva en D:\\Queue\\QueueDB y nuevos registros de transacciones en D:\\Queue\\QueueLogs, use los siguientes valores:
    
    ```powershell
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />
    ```

4.  Cuando haya terminado, guarde y cierre el archivo EdgeTransport.exe.config.

5.  Reinicie el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
    ```powershell
        net stop MSExchangeTransport && net start MSExchangeTransport
    ```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya creado una base de datos de colas y registros de transacciones nuevos en una nueva ubicación, realice lo siguiente:

1.  Compruebe que los nuevos archivos de bases de datos Mail.que y Trn.chk existan en la nueva ubicación.

2.  Compruebe que los nuevos archivos de transacciones Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs y Temp.edb existan en la nueva ubicación.

3.  Si puede eliminar las bases de datos de colas y los archivos de registros de transacciones antiguos de la ubicación anterior una vez iniciado el servicio de transporte de Microsoft Exchange, dichos archivos dejarán de usarse.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Qué desea hacer?

## Usar el símbolo del sistema para mover la base de datos de colas y los registros de transacciones existentes a una nueva ubicación

Solo las situaciones de recuperación ante desastres en las que el servicio de transporte de Microsoft Exchange no se cerró correctamente o en las que hubo un error de disco duro necesitarán la restauración y reubicación de una base de datos de colas existente y de sus registros de transacción.

En circunstancias normales, no debe volver a usar los archivos de transacción que ya existen. Un cierre normal del servicio de transporte de Microsoft Exchange escribe todas las entradas de registro de transacción no confirmadas en la base de datos de colas. Además, se usa un registro circular, así que los registros de transacciones que contengan cambios en las bases de datos confirmados previamente no se conservarán.

Use el siguiente procedimiento para mover la base de datos de colas y los registros de transacciones existentes a una nueva ubicación:

1.  Cree las carpetas donde desee mantener los registros de transacciones y la base de datos de colas. Asegúrese de que se aplican los permisos correctos a las carpetas.

2.  En una ventana del símbolo del sistema, abra el archivo EdgeTransport.exe.config en el Bloc de notas mediante el comando siguiente:
    
    ```powershell
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config
    ```

3.  Modifique las claves siguientes en la sección `<appSettings>`:
    
    ```powershell
        <add key="QueueDatabasePath" value="<LocalPath>" />
        <add key="QueueDatabaseLoggingPath" value="<LocalPath>" />
    ```
    
    Por ejemplo, para cambiar la ubicación de la base de datos de colas a D:\\Queue\\QueueDB y los registros de transacciones a D:\\Queue\\QueueLogs, use los siguientes valores:
    
    ```powershell
        <add key="QueueDatabasePath" value="D:\Queue\QueueDB" />
        <add key="QueueDatabaseLoggingPath" value="D:\Queue\QueueLogs" />
    ```

4.  Cuando haya terminado, guarde y cierre el archivo EdgeTransport.exe.config.

5.  Detenga el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
    ```powershell
        net stop MSExchangeTransport
    ```

6.  Mueva los archivos de base de datos existentes Mail.que y Trn.chk desde la ubicación original a la nueva ubicación.

7.  Mueva los archivos de registros de transacción existentes Trn.log, Trntmp.log, Trn*nnnnn*.log, Trnres00001.jrs, Trnres00002.jrs y Temp.edb de la antigua ubicación a la nueva ubicación.

8.  Inicie el servicio de transporte de Microsoft Exchange ejecutando el siguiente comando:
    
    ```powershell
        net start MSExchangeTransport
    ```

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya movido correctamente la base de datos de colas y los registros de transacciones existentes a la nueva ubicación, realice lo siguiente:

1.  Compruebe que los archivos de base de datos de colas Mail.que y Trn.chk existan en la nueva ubicación.

2.  Compruebe que los archivos de registro de transacciones Trn.log, Trntmp.log, Trnres00001.jrs, Trnres00002.jrs y Temp.edb existan en la nueva ubicación.

3.  Compruebe que no haya bases de datos de colas o archivos de registros de transacciones en la ubicación original.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Qué desea hacer?

