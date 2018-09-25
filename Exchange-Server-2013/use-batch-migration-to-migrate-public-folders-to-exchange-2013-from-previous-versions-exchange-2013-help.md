---
title: 'Usar migración por lotes para migrar carpetas públicas a Exchange 2013 desde versiones anteriores: Exchange 2013 Help'
TOCTitle: Usar migración por lotes para migrar carpetas públicas a Exchange 2013 desde versiones anteriores
ms:assetid: da808e27-d2b7-4fbd-915c-a600751f526c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn912663(v=EXCHG.150)
ms:contentKeyID: 64129766
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar migración por lotes para migrar carpetas públicas a Exchange 2013 desde versiones anteriores

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2018-03-26_

**Resumen:**  En este artículo se describe cómo mover las carpetas públicas de Exchange 2007 o Exchange 2010 a Exchange 2013.

En este artículo se describe cómo migrar las carpetas públicas de Exchange Server 2010 SP3 RU8 o Exchange 2007 SP3 RU15 a Microsoft Exchange Server 2013 CU7 o posterior dentro del mismo bosque.

Haremos referencia a los servidores de Exchange 2010 SP3 RU8 y Exchange 2007 SP3 RU15 como el *servidor de Exchange heredado*.


> [!NOTE]
> El método de migración por lotes que se describe en este artículo es el único método admitido para la migración de carpetas públicas heredadas a Exchange 2013. El antiguo método de migración en serie para la migración de carpetas públicas está en desuso y Microsoft ya no lo admite.



Puede efectuar la migración mediante el uso de los cmdlets **\*MigrationBatch** y los cmdlets **\*PublicFolderMigrationRequest** para la solución de problemas. Además, usará los siguientes scripts de PowerShell:

  - `Export-PublicFolderStatistics.ps1`   Este script crea el nombre de carpeta para el archivo de asignación del tamaño de la carpeta.

  - ` Export-PublicFolderStatistics.psd1` Este archivo de compatibilidad se usa en el script Export-PublicFolderStatistics.ps1 y debe descargarse en la misma ubicación.

  - `PublicFolderToMailboxMapGenerator.ps1`   Este script crea el archivo de asignación del buzón de carpetas públicas.

  - `PublicFolderToMailboxMapGenerator.strings.psd1` Este archivo de compatibilidad se usa en el script PublicFolderToMailboxMapGenerator.ps1 y debe descargarse en la misma ubicación.

  - `Create-PublicFolderMailboxesForMigration.ps1` Este script crea los buzones de carpetas públicas de destino para la migración. Además, el script calcula el número de buzones necesarios para administrar la carga de usuarios estimada, en función de las directrices para el número de inicios de sesión de usuario por buzón de carpetas públicas que se recomienda en [Límites de las carpetas públicas](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Este archivo de compatibilidad se usa en el script Create-PublicFolderMailboxesForMigration.ps1 y debe descargarse en la misma ubicación.

En el Paso 1: Descarga de los scripts de migración se proporciona información detallada sobre dónde puede descargar los scripts mencionados. Asegúrese de que todos los scripts se descargan en la misma ubicación.

Para otras tareas de administración relacionadas con las carpetas públicas, vea [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

## ¿Qué versiones de Exchange son compatibles para la migración de carpetas públicas a Exchange 2013?

Exchange admite la migración de carpetas públicas desde las siguientes versiones heredadas de Exchange Server:

  - Exchange 2010 SP3 RU8 o versiones posteriores

  - Exchange 2007 SP3 RU15 o versiones posteriores

Si necesita mover las carpetas públicas a Exchange 2013 pero los servidores locales no ejecutan las versiones de compatibilidad mínimas de Exchange 2010 o Exchange 2007, consulte [Usar la migración en serie para migrar carpetas públicas a Exchange 2013 desde versiones anteriores](https://technet.microsoft.com/es-es/library/jj150486\(v=exchg.150\)). Aunque la migración en serie es una opción, es muy recomendable que actualice los servidores locales y use la migración por lotes. La migración por lotes ofrece mayor confiabilidad y velocidad.

No puede migrar las carpetas públicas directamente desde Exchange 2003. Si ejecuta Exchange 2003 en su organización, debe mover todas las bases de datos de carpetas públicas y las réplicas a Exchange 2010 SP3 RU8 o posterior o a Exchange 2007 SP3 RU15 o posterior. No pueden quedar réplicas de carpetas públicas en Exchange 2003. Además, el correo destinado a una carpeta pública de Exchange 2013 no se puede enrutar a través de un servidor de Exchange 2003.

## ¿Qué necesita saber antes de comenzar?

  - Antes de comenzar, recomendamos leer este tema en su totalidad, ya que para llevar a cabo algunos pasos, se requiere tiempo de inactividad.

  - El servidor de Exchange 2010 debe ejecutar Exchange 2010 SP3 RU8 o versiones posteriores.

  - El servidor de Exchange 2007 debe ejecutar Exchange 2007 SP3 RU15 o versiones posteriores.

  - El número máximo de carpetas públicas que se pueden migrar a Exchange 2013 en una sola migración es 500 000.

  - En Exchange 2013, debe ser miembro del grupo de roles de administración de la organización. Para más información sobre cómo habilitar el grupo de roles de administración de la organización, vea [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - En Exchange 2010, debe ser miembro de los grupos de roles RBAC de administración de servidores o de administración de la organización. Para más información, vea [Agregar miembros a un grupo de funciones](https://go.microsoft.com/fwlink/?linkid=299212).

  - En Exchange 2007, debe tener asignado el rol Administrador de organización de Exchange o Administrador de servidores de Exchange. Asimismo, debe tener asignado el rol de administrador de carpetas públicas y el grupo de administradores locales para el servidor de destino. Para más información, vea [Cómo agregar un usuario o grupo a una función de administrador](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - En el servidor de Exchange 2007, actualice a [Windows PowerShell 2.0 y WinRM 2.0 para Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Antes de migrar, debe tener en cuenta los [Límites de las carpetas públicas](limits-for-public-folders-exchange-2013-help.md).

  - Antes de efectuar la migración, mueva todos los buzones de usuario a Exchange 2013, ya que los usuarios que tienen buzones de Exchange 2007 o Exchange 2010 no tendrán acceso a las carpetas públicas de Exchange 2013. Para obtener más información, consulte [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - En un entorno de varios dominios, las carpetas públicas habilitadas para correo dejará de funcionar después de la migración a Exchange de 2013 si está ejecutando Exchange en un dominio secundario. Esto es porque en Exchange 2013, objetos de carpetas públicas con correo habilitado tienen que estar bajo el dominio raíz. Para resolver este problema, debe deshabilitar correo las carpetas públicas con correo habilitado y, a continuación, habilitar el correo en ellos de nuevo, que le permitirá moverlos a la ubicación correcta del dominio.

  - Una vez que haya completado la migración, si desea que los remitentes externos envíen correo a las carpetas públicas migradas habilitadas para correo, se debe conceder al menos el permiso **Crear elementos** al usuario **Anónimo**. Si no realiza esta acción, los remitentes externos recibirán una notificación de error de entrega y no se entregarán los mensajes a la carpeta pública migrada habilitada para correo. Para leer más acerca de cómo establecer permisos en el usuario Anónimo, consulte [Habilitar o deshabilitar el correo para una carpeta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Descarga de los scripts de migración

1.  Descargue todos los scripts y archivos auxiliares desde [Scripts de migración de carpetas públicas](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Guarde los scripts en el equipo local en el que ejecutará PowerShell. Por ejemplo, C:\\PFScripts. Asegúrese de que todos los scripts se guardan en la misma ubicación.

## Paso 2: Preparación para la migración

Siga estos pasos de requisitos previos antes de iniciar la migración.

**Pasos de requisitos previos sobre el servidor de Exchange heredado**

1.  Para realizar las comprobaciones pertinentes al finalizar la migración, le recomendamos ejecutar primero los siguientes comandos en el servidor de Exchange heredado para tomar instantáneas de su implementación de carpeta pública actual:
    
      - Ejecute el siguiente comando para tomar una instantánea de la estructura de la carpeta de origen original:
        
        ```powershell
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
        ```
    
      - Ejecute el siguiente comando para tomar una instantánea de las estadísticas de carpetas públicas, como recuento de elementos, tamaño y propietario:
        
        ```powershell
        Get-PublicFolderStatistics | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
        ```
    
      - Ejecute el siguiente comando para tomar una instantánea de los permisos:
        
        ```powershell
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
        ```
    
    Guarde la información de los comandos anteriores para compararlos al finalizar la migración.

2.  Si el nombre de una carpeta pública contiene una barra diagonal inversa **\\**, las carpetas públicas se crearán en la carpeta pública principal durante la migración. Antes de migrar, recomendamos cambiar el nombre de las carpetas públicas que tengan una barra diagonal inversa en el nombre.
    
    1.  Para localizar las carpetas públicas con una barra diagonal inversa en el nombre en Exchange 2010, ejecute este comando:
        
        ```powershell
        Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
        ```
    
    2.  Para localizar las carpetas públicas con una barra diagonal inversa en el nombre en Exchange 2007, ejecute este comando:
        
        ```powershell
        Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
        ```
    
    3.  Si el resultado devuelve alguna carpeta pública, puede cambiarle el nombre con este comando:
        
        ```powershell
        Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>
        ```

3.  Asegúrese de que no exista ningún registro anterior de migración correcta.
    
    1.  El ejemplo siguiente comprueba el estado de la migración de carpetas públicas.
        
        ```powershell
        Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
        ```
        
        Si anteriormente se efectuó una migración correcta, el valor de las propiedades *PublicFoldersLockedforMigration* o *PublicFolderMigrationComplete* es `$true`. Use el comando del paso 3b para establecer el valor en `$false`. Si el valor se establece en `$true`, se producirá un error en la solicitud de migración.
    
    2.  Si el estado de las propiedades *PublicFoldersLockedforMigration* o *PublicFolderMigrationComplete* es `$true`, ejecute el siguiente comando para establecer el valor como `$false`.
        
        ```powershell
        Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
        ```
    

    > [!WARNING]
    > Después de restablecer estas propiedades, debe esperar a que Exchange detecte la nueva configuración. Esta acción puede tardar hasta dos horas en completarse.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-PublicFolder](https://technet.microsoft.com/es-es/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/es-es/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/es-es/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/es-es/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/es-es/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Pasos de requisitos previos en el servidor Exchange 2013**

1.  Asegúrese de que no hay ninguna solicitud de migración de carpetas públicas existente. Si la hay, desactívela o se producirá un error en su propia solicitud de migración. Este paso no es necesario en todos los casos; solo es necesario si piensa que puede haber una solicitud de migración existente en la canalización.
    
    Una solicitud de migración existente puede ser de dos tipos: migración por lotes o series. Los comandos para detectar las solicitudes de cada tipo y para quitar las solicitudes de cada tipo son los siguientes.
    

    > [!IMPORTANT]
    > Antes de quitar una solicitud de migración, es importante comprender por qué ya había una. La ejecución del siguiente comando determinará el momento en el que se realizó una solicitud anterior y ayudará a diagnosticar cualquier problema que haya ocurrido. Es posible que deba comunicarse con otros administradores de la organización para determinar por qué se realizó el cambio.

    
    En el ejemplo siguiente se detectará cualquier solicitud de migración serie existente.
    
    ```powershell
    Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    ```
    
    El ejemplo siguiente quita cualquier solicitud de migración serie de carpetas públicas existente.
    
    ```powershell
    Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    ```
    
    En el ejemplo siguiente se detectará cualquier solicitud de migración de lote existente.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    El ejemplo siguiente quita cualquier solicitud de migración de lote de carpetas públicas existente.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Asegúrese de que no haya ninguna carpeta pública ni ningún buzón de carpetas públicas en los servidores de Exchange 2013.
    
    1.  Ejecute el siguiente comando para comprobar si hay algún buzón de carpetas públicas.
        
        ```powershell
        Get-Mailbox -PublicFolder
        ```
    
    2.  Si el comando no devuelve ningún buzón de carpetas públicas, continúe con el Step 3: Generate the CSV files. Si el comando devuelve alguna carpeta pública, ejecute el siguiente comando para comprobar si hay alguna carpeta pública:
        
        ```
        powershellGet-PublicFolder
        ```
    
    3.  Si tiene alguna carpeta pública, ejecute los siguientes comandos de PowerShell para quitarlas. Asegúrese de haber guardado toda la información que estaba en las carpetas públicas.
        

        > [!NOTE]
        > Se eliminará definitivamente toda la información contenida en las carpetas públicas cuando se eliminen.

         ```powershell
        Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```
        
        ```powershell
        Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
        ```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/es-es/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/es-es/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/es-es/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/es-es/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/es-es/library/aa995948\(v=exchg.150\))

## Paso 3: Generación de los archivos .csv

1.  En el servidor de Exchange heredado, ejecute el script `Export-PublicFolderStatistics.ps1` para crear el nombre de carpeta para el archivo de asignación de tamaño de carpeta. Este script debe ejecutarse mediante un administrador local. El archivo tendrá dos columnas: **FolderName** y **FolderSize**. Los valores de la columna **FolderSize** se mostrarán en bytes. Por ejemplo, **\\PublicFolder01,10000**.
    
    ```powershell
    .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    ```
    
      - *FQDN of source server* equivale al nombre de dominio completo del servidor de buzones de correo en el que se hospeda la jerarquía de la carpeta pública.
    
      - *Folder to size map path* equivale al nombre de archivo y a la ruta de acceso de la carpeta compartida de red en la que desea guardar el archivo .csv. En un punto posterior de este tema deberá tener acceso a este archivo desde el servidor de Exchange 2013. Si especifica solo el nombre del archivo, el archivo se generará en el directorio actual de PowerShell en el equipo local.

2.  Ejecute el script `PublicFolderToMailboxMapGenerator.ps1` para crear el archivo de asignación de carpetas públicas al buzón de correo. Este archivo se usa para calcular el número correcto de buzones de carpetas públicas del servidor de buzones de Exchange 2013.
    

    > [!NOTE]
    > Si el nombre de una carpeta pública contiene una barra inversa <STRONG>\</STRONG>, las carpetas públicas se crearán en la carpeta pública principal. Se recomienda que revise el archivo .csv y edite todos los nombres que contienen una barra diagonal inversa.

    
    ```powershell
    .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    ```
    
      - *Maximum mailbox size in bytes* equivale al tamaño máximo que quiere establecer para los nuevos buzones de carpetas públicas. Cuando especifique esta configuración, asegúrese de permitir la expansión para que el buzón de carpetas públicas tenga espacio para aumentar su tamaño.
    
      - *Folder to size map path* equivale a la ruta de acceso del archivo .csv que creó al ejecutar el script `Export-PublicFolderStatistics.ps1`.
    
      - *Folder to mailbox map path* equivale al nombre de archivo y la ruta del archivo .csv de carpeta a buzón de correo que creará con este paso. Si especifica solo el nombre del archivo, el archivo se generará en el directorio actual de PowerShell en el equipo local.

## Paso 4: Crear buzones de carpetas públicas en Exchange 2013

1.  Ejecute el siguiente comando para crear el buzón de carpetas públicas de destino. El script creará un buzón de destino para cada buzón del archivo .csv que generó anteriormente en el paso 3, mediante la ejecución del script PublicFoldertoMailboxMapGenerator.ps1.
    
    ```powershell
    .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    ```
    
    *Mapping.csv* es el archivo que se genera mediante el script PublicFoldertoMailboxMapGenerator.ps1 en el paso 3. El número estimado de conexiones de usuario simultáneas que exploran una jerarquía de carpetas públicas suele ser menor que el número total de usuarios de una organización.

## Paso 5: Inicio de la solicitud de migración

Los pasos para migrar carpetas públicas de Exchange 2007 son distintos de los pasos para migrar carpetas públicas de Exchange 2010.


> [!TIP]
> Si se efectúa la migración desde Exchange 2007 o Exchange 2010, una vez creadas las solicitudes de migración de un lote con el cmdlet correspondiente, puede verlas y administrarlas en el EAC.



**Migrar carpetas públicas de Exchange 2007**

1.  Exchange 2013 no reconocerá las carpetas públicas del sistema heredado, como OWAScratchPad y el subárbol de carpeta raíz de esquema de Exchange 2007; por lo tanto, se considerarán elementos "incorrectos". En este caso, la migración no se realizará correctamente. Como parte de la solicitud de migración, debe especificar un valor para el parámetro `BadItemLimit`. Este valor dependerá del número de bases de datos de carpetas públicas que tenga. Los siguientes comandos determinarán las bases de datos de carpetas públicas de las que dispone y calculará el `BadItemLimit` para la solicitud de migración.

    ```powershell
        $PublicFolderDatabasesInOrg = @(Get-PublicFolderDatabase)
    ```

    ```powershell
        $BadItemLimitCount = 5 + ($PublicFolderDatabasesInOrg.Count -1)
    ```
    
2.  En el servidor de Exchange 2013, ejecute el siguiente comando:
    
        New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> -BadItemLimit $BadItemLimitCount 

3.  Inicie la migración con el siguiente comando:
    
    ```powershell
    Start-MigrationBatch PFMigration
    ```

**Migrar carpetas públicas de Exchange 2010**

1.  En el servidor de Exchange 2013, ejecute el siguiente comando.
    
    ```powershell
    New-MigrationBatch -Name PFMigration -SourcePublicFolderDatabase (Get-PublicFolderDatabase -Server <Source server name>) -CSVData (Get-Content <Folder to mailbox map path> -Encoding Byte) -NotificationEmails <email addresses for migration notifications> 
    ```
    
    El parámetro `NotificationEmails` es opcional.

2.  Inicie la migración con el siguiente comando:
    
    ```powershell
    Start-MigrationBatch PFMigration
    ```
    
    O:
    
    Puede iniciar la migración en el EAC.
    
    1.  Inicie sesión en Exchange Online y abra el EAC.
    
    2.  Vaya a **Destinatarios** \> **Migración**.
    
    3.  Seleccione el lote de migración que acaba de crear y, a continuación, haga clic en el botón Inicio.

La columna **Estado** mostrará el estado del lote inicial como **Creado**. El estado cambia a **Sincronizando** durante la migración. Una vez completada la solicitud de migración, el estado será **Sincronizado**. Haga doble clic en un lote para ver el estado de los buzones individuales dentro del lote. Los trabajos de buzón comienzan con el estado **En cola**. Al iniciarse el trabajo, el estado es **Sincronizando**; al completarse la `InitialSync`, el estado será **Sincronizado**.

Puede ver y administrar el progreso y la finalización de la migración en el EAC. Como el cmdlet **New-MigrationBatch** inicia una solicitud de migración de buzones para cada buzón de carpetas públicas, puede ver el estado de estas solicitudes usando la página migración de buzones. Para acceder a la página de migración de buzones y crear informes de migración que pueda recibir por correo electrónico, haga lo siguiente:

1.  Inicie sesión en Exchange Online y abra el EAC.

2.  Vaya a **Buzón** \> **Migración**.

3.  Seleccione la solicitud de migración que acaba de crear y haga clic en **Ver detalles** en el panel **Detalles**.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/es-es/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/es-es/library/jj218697\(v=exchg.150\))

## Paso 6: Bloqueo de las carpetas públicas en el servidor de Exchange heredado para la migración final (se requiere tiempo de inactividad)

Hasta este punto de la migración, los usuarios han podido obtener acceso a las carpetas públicas. En los siguientes pasos, los usuarios deberán cerrar la sesión en las carpetas públicas heredadas y bloquear las carpetas mientras la migración completa su sincronización final. Los usuarios no podrán tener acceso a las carpetas públicas durante este proceso. Además, cualquier correo enviado a carpetas públicas habilitadas para correo se colocará en cola y no se entregará hasta que haya finalizado la migración de dichas carpetas públicas.

Antes de ejecutar el comando `PublicFoldersLockedForMigration` como se describe a continuación, asegúrese de que todos los trabajos están en el estado **sincronizadas**. Para ello, ejecute el comando `Get-PublicFolderMailboxMigrationRequest` . Siga con este paso sólo después de haber comprobado que todos los trabajos están en el estado **sincronizadas**.

En el servidor de Exchange heredado, ejecute el comando siguiente para bloquear las carpetas públicas heredadas para poder finalizar la migración.

```powershell
Set-OrganizationConfig -PublicFoldersLockedForMigration:$true
```


> [!NOTE]
> Si por cualquier razón el archivo por lotes de migración no finaliza (<STRONG>PublicFolderMigrationComplete</STRONG> muestra <STRONG>False</STRONG>), en el servidor heredado, reinicie el Almacén de información (IS).



Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)).

Si su organización dispone de varias bases de datos de carpetas públicas, deberá esperar a que se complete la replicación de carpetas públicas para confirmar que todas las bases de datos han seleccionado la marca `PublicFoldersLockedForMigration` y que los cambios pendientes realizados por los usuarios en las carpetas convergen en toda la organización. Esto puede tardar varias horas.

## Paso 7: Finalizar la migración de carpetas públicas (tiempo de inactividad necesario)

Primero, ejecute el siguiente cmdlet para cambiar el tipo de implementación de Exchange 2013 a **Remoto**:

```powershell
Set-OrganizationConfig -PublicFoldersEnabled Remote
```

A continuación, puede efectuar la migración de carpetas públicas ejecutando el comando siguiente:

```powershell
Complete-MigrationBatch PublicFolderMigration
```

También puede completar la migración en el EAC haciendo clic en **Completar este lote de migración**.

Cuando termine la migración, Exchange realizará una sincronización entre el servidor de Exchange heredado y Exchange 2013 final. Si la sincronización se realiza correctamente, las carpetas públicas en el servidor de Exchange de 2013 se desbloqueará y cambiará el estado del lote de migración de **finalización** y, a continuación, **completado**. Es habitual que el lote de migración tomar unas pocas horas antes de su estado cambia de **sincronizadas** para **finalización**, momento en el que comenzará la sincronización.

## Paso 8: Prueba y desbloqueo de la migración de carpetas públicas

Después de completar la migración de carpetas públicas, debe ejecutar la prueba siguiente para asegurarse de que dicha migración se realizó correctamente. Así podrá probar la jerarquía de carpetas públicas migradas antes de pasar a utilizar carpetas públicas de Exchange 2013.

1.  En PowerShell, ejecute el siguiente comando para asignar algunos buzones de prueba para usar cualquier buzón de carpetas públicas migrado recientemente como buzón de carpetas públicas predeterminado.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Inicie sesión en Outlook 2007 o versiones posteriores con el usuario de prueba identificado en el paso anterior y luego realice las pruebas siguientes para las carpetas públicas:
    
      - Ver la jerarquía
    
      - Compruebe los permisos.
    
      - Cree y elimine carpetas públicas.
    
      - Publique contenido en una carpeta pública y elimine contenido de ella.

3.  Si tiene algún problema, vea Roll back the migration más adelante en este mismo tema. Si el contenido y la jerarquía de las carpetas públicas es aceptable y funcionan correctamente, ejecute el comando siguiente para desbloquear las carpetas para otros usuarios.
    
    ```powershell
    Get-Mailbox -PublicFolder | Set-Mailbox -PublicFolder -IsExcludedFromServingHierarchy $false
    ```
    

    > [!IMPORTANT]
    > No use el parámetro <EM>IsExcludedFromServingHierarchy</EM> después de que se complete la validación de la migración inicial ya que el servicio de administración de almacenamiento automatizado usa este parámetro para Exchange Online.



4.  En el servidor de Exchange heredado, ejecute el siguiente comando para indicar que ya se ha completado la migración de carpetas públicas:
    
    ```powershell
    Set-OrganizationConfig -PublicFolderMigrationComplete:$true
    ```

5.  Después de comprobar que la migración se ha completado, ejecute el siguiente comando:
    
    ```powershell
    Set-OrganizationConfig -PublicFoldersEnabled Local
    ```

6.  Finalmente, si desea que los remitentes externos envíen correo a las carpetas públicas migradas habilitadas para correo, se debe conceder al menos el permiso **Crear elementos** al usuario **Anónimo**. Si no realiza esta acción, los remitentes externos recibirán una notificación de error de entrega y no se entregarán los mensajes a la carpeta pública migrada habilitada para correo.
    
    Puede usar el Shell o Outlook para establecer los permisos para el usuario Anónimo. Para leer más sobre cómo establecer permisos en el usuario Anónimo, consulte [Habilitar o deshabilitar el correo para una carpeta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

## ¿Cómo saber si el proceso se ha completado correctamente?

En Step 2: Prepare for the migration se le pidió que tomara instantáneas de la estructura de las carpetas públicas, estadísticas y permisos antes de que empezara la migración. Mediante los siguientes pasos podrá comprobar si la migración de carpetas públicas se realizó correctamente. Para esto, se tomarán las mismas instantáneas una vez que la migración haya finalizado. De esta manera, podrá comparar los datos de ambos archivos para comprobar que el proceso haya sido correcto.

1.  Ejecute el siguiente comando para tomar una instantánea de la nueva estructura de carpetas.
    
    ```powershell
    Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml
    ```

2.  Ejecute el siguiente comando para tomar una instantánea de la estadística de carpetas públicas, como recuento de elementos, tamaño y propietario.
    
    ```powershell
    Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml
    ```

3.  Ejecute el siguiente comando para tomar una instantánea de los permisos.
    
    ```powershell
    Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml
    ```

## Quitar bases de datos de carpetas públicas de los servidores de Exchange heredados

Una vez que se haya completado la migración y haya comprobado que las carpetas públicas de Exchange 2013 funcionan tal y como se esperaba, deberá quitar las bases de datos de carpetas públicas de los servidores de Exchange heredados.

  - Para más información sobre cómo quitar las bases de datos de carpetas públicas de los servidores de Exchange 2007, vea [Quitar bases de datos de carpetas públicas](https://go.microsoft.com/fwlink/?linkid=123678).

  - Para más información sobre cómo quitar las bases de datos de carpetas públicas de los servidores de Exchange 2010, vea [Quitar bases de datos de carpetas públicas](https://go.microsoft.com/fwlink/?linkid=81409).

## Revertir la migración

Si tiene problemas con la migración y necesita reactivar sus carpetas públicas de Exchange heredadas, realice los pasos siguientes.


> [!WARNING]
> Si revierte la migración en los servidores heredados de Exchange, después de la migración perderá todos los correos electrónicos enviados a las carpetas públicas habilitadas para correo o todo el contenido registrado en las carpetas públicas en Exchange 2013. Para guardar este contenido, debe exportar el contenido de la carpeta pública a un archivo .pst y luego importarlo a las carpetas públicas heredadas cuando se completa la reversión.



1.  En el servidor de Exchange heredado, ejecute el comando siguiente para desbloquear las carpetas públicas heredadas de Exchange. Este proceso puede tardar varias horas.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  En el servidor de Exchange 2013, ejecute los siguientes comandos para quitar los buzones de carpetas públicas.
    
    ```powershell
    Get-Mailbox -PublicFolder | Where{$_.IsRootPublicFolderMailbox -eq $false} | Remove-Mailbox -PublicFolder -Force -Confirm:$false
    ```
        
    ```powershell
    Get-Mailbox -PublicFolder | Remove-Mailbox -PublicFolder -Force -Confirm:$false
    ```

3.  En el servidor de Exchange heredado, ejecute el comando siguiente para establecer la marca `PublicFolderMigrationComplete` como `$false`.
    
    ```powershell
    Set-OrganizationConfig -PublicFolderMigrationComplete:$False
    ```

