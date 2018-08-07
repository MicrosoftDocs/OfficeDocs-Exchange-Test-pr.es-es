---
title: 'Usar migrar lote migrar carpeta pública heredada a Office 365 Exchange Online'
TOCTitle: Usar la migración por lotes para migrar carpetas públicas heredadas a Office 365 y Exchange Online
ms:assetid: e8ab9309-7d12-4f02-bfc4-14e61a373958
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn874017(v=EXCHG.150)
ms:contentKeyID: 63892247
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar la migración por lotes para migrar carpetas públicas heredadas a Office 365 y Exchange Online

 

_**Se aplica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:** 2018-03-26_

**Resumen:**  Use estos procedimientos para mover las carpetas públicas de Exchange 2007 y Exchange 2010 a Office 365.

En este tema se describe cómo migrar carpetas públicas en una migración preconfigurada o una migración total desde el paquete acumulativo de actualizaciones 8 de Exchange Server 2010 Service Pack 3 (SP3) o el paquete acumulativo de actualizaciones 15 de Exchange 2007 SP3 a Office 365 o Exchange Online.

En este tema haremos referencia a los servidores de Exchange 2010 SP3 RU8 y Exchange 2007 SP3 RU15 como el *servidor de Exchange heredado*. Además, los pasos enumerados en este tema sea aplican tanto a Exchange Online como a Office 365. Las indicaciones pueden utilizarse indistintamente.


> [!NOTE]
> El método de migración por lotes que se describe en este artículo es el único método admitido para la migración de carpetas públicas heredadas a Office 365 y a Exchange Online. El antiguo método de migración por serie para la migración de carpetas públicas está en desuso y Microsoft ya no lo admite.



Se recomienda no usar la característica de exportación de PST de Outlook para migrar carpetas públicas a Office 365 o Exchange Online. El crecimiento de los buzones de la carpeta pública de Office 365 y Exchange Online se administra mediante una característica de división automática que divide el buzón de carpeta pública cuando supera las cuotas de tamaño. La división automática no puede controlar el crecimiento repentino de los buzones de la carpeta pública cuando se usa la exportación de PST para migrar las carpetas públicas y puede que tenga que esperar hasta dos semanas para que la división automática mueva los datos desde el buzón principal. Se recomienda usar las instrucciones basadas en el cmdlet de este documento para migrar carpetas públicas a Office 365 y Exchange Online. Sin embargo, si opta por migrar carpetas públicas mediante la exportación de PST, vea la sección Migrar carpetas públicas a Office 365 mediante la exportación de archivos PST de Outlook más adelante en este tema.

Puede realizar la migración con los cmdlets **\*-MigrationBatch**, además de los siguientes scripts de PowerShell:

  - `Export-PublicFolderStatistics.ps1`   Este script crea el nombre de carpeta para el archivo de asignación del tamaño de la carpeta. Deberá ejecutar este script en el servidor de Exchange heredado.

  - `Export-PublicFolderStatistics.psd1`   El script `Export-PublicFolderStatistics.ps1` usa este archivo de compatibilidad, por lo que debe descargarse en la misma ubicación.

  - `PublicFolderToMailboxMapGenerator.ps1`   Este script crea el archivo de asignación de carpetas públicas al buzón de correo mediante el uso de la salida del script `Export-PublicFolderStatistics.ps1`. Deberá ejecutar este script en el servidor de Exchange heredado.

  - `PublicFolderToMailboxMapGenerator.strings.psd1`   El script `PublicFolderToMailboxMapGenerator.ps1` usa este archivo de compatibilidad, por lo que debe descargarse en la misma ubicación.

  - `Create-PublicFolderMailboxesForMigration.ps1` Este script crea los buzones de carpetas públicas de destino para la migración. Además, el script calcula el número de buzones necesarios para administrar la carga de usuarios estimada, en función de las directrices para el número de inicios de sesión de usuario por buzón de carpetas públicas que se recomienda en [Límites de las carpetas públicas](limits-for-public-folders-exchange-2013-help.md).

  - `Create-PublicFolderMailboxesForMigration.strings.psd1` Este archivo de compatibilidad se usa en el script Create-PublicFolderMailboxesForMigration.ps1 y debe descargarse en la misma ubicación.

  - `Sync-MailPublicFolders.ps1`   Este script sincroniza objetos de carpeta pública habilitada para correo entre la implementación local de Exchange y Office 365. Deberá ejecutar este script en el servidor de Exchange heredado.

  - `SyncMailPublicFolders.strings.psd1`   Es un archivo de compatibilidad que usa el script de `Sync-MailPublicFolders.ps1` y debe copiarse en la misma ubicación que los scripts anteriores.

En el Paso 1: Descarga de los scripts de migración se proporciona información detallada sobre dónde puede descargar los scripts mencionados. Asegúrese de que todos los scripts se descargan en la misma ubicación.

Para otras tareas de administración relacionadas con las carpetas públicas, vea [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

## ¿Qué versiones de Exchange son compatibles para la migración de carpetas públicas a Office 365 y Exchange Online?

Exchange admite la migración de carpetas públicas a Office 365 y Exchange Online desde las siguientes versiones heredadas de Exchange Server:

  - Exchange 2010 SP3 RU8 o versiones posteriores

  - Exchange 2007 SP3 RU15 o versiones posteriores

Si necesita mover las carpetas públicas a Exchange Online, pero los servidores locales no cuentan con las versiones de compatibilidad mínima de Exchange 2010 o Exchange 2007, se recomienda actualizar los servidores locales y usar la migración por lotes, que es el único método de migración de carpetas públicas compatible.

No se pueden migrar carpetas públicas directamente desde Exchange 2003. Si su organización utiliza Exchange 2003, debe mover todas las bases de datos y réplicas de las carpetas públicas a Exchange 2010 SP3 RU8, Exchange 2007 SP3 RU10 o a una versión posterior. No pueden quedar réplicas de carpetas públicas en Exchange 2003. Además, el correo destinado a una carpeta pública de Exchange 2013 no se puede enrutar a través de un servidor de Exchange 2003.

## ¿Qué debe saber antes de comenzar?

  - El servidor de Exchange 2010 debe ejecutar Exchange 2010 SP3 RU8 o versiones posteriores.

  - El servidor de Exchange 2007 debe ejecutar Exchange 2007 SP3 RU15 o versiones posteriores.

  - En Office 365 y Exchange Online, debe ser miembro del grupo de roles de administración de la organización. Este grupo de roles es diferente de los permisos que se le asignan cuando se suscribe a Office 365 o Exchange Online. Para más información sobre cómo habilitar el grupo de roles de administración de la organización, vea [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - En Exchange 2010, debe ser miembro de los grupos de roles RBAC de administración de servidores o de administración de la organización. Para más información, vea [Agregar miembros a un grupo de funciones](https://go.microsoft.com/fwlink/?linkid=299212).

  - En Exchange 2007, debe tener asignado el rol Administrador de organización de Exchange o Administrador de servidores de Exchange. Asimismo, debe tener asignado el rol de administrador de carpetas públicas y el grupo de administradores locales para el servidor de destino. Para más información, vea [Cómo agregar un usuario o grupo a una función de administrador](https://go.microsoft.com/fwlink/p/?linkid=81779).

  - En el servidor de Exchange 2007, actualice a [Windows PowerShell 2.0 y WinRM 2.0 para Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Antes de la migración, si el tamaño de alguna de las carpetas públicas de la organización es mayor que 2 GB, recomendamos eliminar el contenido de dicha carpeta o dividirlo en varias carpetas públicas. Si ninguna de estas opciones no es viable, recomendamos que no mueva sus carpetas públicas a Office 365 y Exchange Online.

  - En Office 365 y Exchange Online, puede crear un máximo de 1000 buzones de carpeta pública.

  - Antes de migrar las carpetas públicas, se recomienda que primero mueva todos los buzones de correo de usuario a Office 365 y Exchange Online. Para obtener más información, vea [Formas de migrar varias cuentas de correo electrónico a Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

  - Debe habilitarse Outlook en cualquier lugar en el servidor de Exchange heredado. Para obtener más información sobre cómo habilitar Outlook en cualquier lugar en los servidores de Exchange 2010, vea [Habilitar Outlook en cualquier lugar](https://go.microsoft.com/fwlink/p/?linkid=187249). Para obtener más información sobre cómo habilitar Outlook en cualquier lugar en los servidores de Exchange 2007, vea [Cómo habilitar Outlook en cualquier lugar](https://go.microsoft.com/fwlink/p/?linkid=167210).

  - No puede usar el Centro de administración de Exchange (EAC) ni la Consola de administración de Exchange (EMC) para realizar este procedimiento. En los servidores de Exchange heredados, debe usar el Shell de administración de Exchange. Para Exchange Online, debe usar Exchange Online PowerShell. Para obtener más información, consulte [Conectarse a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/es-es/library/jj984289\(v=exchg.150\)).

  - Antes de comenzar, recomendamos leer este tema en su totalidad, ya que para llevar a cabo algunos pasos, se requiere tiempo de inactividad.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Descarga de los scripts de migración

1.  Descargue todos los scripts y archivos auxiliares desde [Scripts de migración de carpetas públicas](https://go.microsoft.com/fwlink/?linkid=299838).

2.  Guarde los scripts en el equipo local en el que ejecutará PowerShell. Por ejemplo, C:\\PFScripts. Asegúrese de que todos los scripts se guardan en la misma ubicación.

3.  Descargue los siguientes archivos desde el artículo [Carpetas públicas habilitadas para correo y script de sincronización de directorios](https://go.microsoft.com/fwlink/p/?linkid=532376):
    
    1.  `Sync-MailPublicFolders.ps1`
    
    2.  `SyncMailPublicFolders.strings.psd1`

4.  Guarde los scripts en la misma ubicación que usó en el paso 2. Por ejemplo, C:\\PFScripts.

## Paso 2: Preparación para la migración

Siga estos pasos de requisitos previos antes de iniciar la migración.

**Pasos generales de los requisitos previos**

  - Asegúrese de que no hay ningún objeto de correo huérfano en las carpetas públicas en Active Directory, es decir, objetos en Active Directory sin objeto correspondiente de Exchange.

  - Confirme que la dirección de correo electrónico SMTP configurada para las carpetas públicas de Active Directory coincide con la dirección de correo electrónico SMTP en los objetos de Exchange.

  - Asegúrese de que no hay ningún objeto de carpeta pública duplicado en Active Directory, para evitar una situación en la que dos o más objetos de Active Directory apunten a la misma carpeta pública habilitada para correo.

**Pasos de requisitos previos sobre el servidor de Exchange heredado**

1.  En el servidor Exchange heredado, asegúrese de que el enrutamiento a las carpetas públicas habilitadas para correo que existirán en Office 365 o Exchange Online sigue funcionando hasta que se actualicen todas las cachés DNS a través de Internet para que apunten al DNS de Office 365 o Exchange Online en el que ahora reside la organización. Para ello, ejecute el siguiente comando para configurar un dominio aceptado con un nombre conocido que enrute adecuadamente los mensajes de correo electrónico al dominio de Office 365 o Exchange Online.
    
        New-AcceptedDomain -Name "PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99" -DomainName contoso.onmicrosoft.com -DomainType InternalRelay 

2.  Si el nombre de una carpeta pública contiene una barra diagonal inversa **\\**, las carpetas públicas se crearán en la carpeta pública principal durante la migración. Antes de migrar, recomendamos cambiar el nombre de las carpetas públicas que tengan una barra diagonal inversa en el nombre.
    
    1.  Para localizar las carpetas públicas con una barra diagonal inversa en el nombre en Exchange 2010, ejecute este comando:
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Where {($_.Name -like "*\*") -or ($_.Name -like "*/*") } | Format-List Name, Identity
    
    2.  Para localizar las carpetas públicas con una barra diagonal inversa en el nombre en Exchange 2007, ejecute este comando:
        
            Get-PublicFolderDatabase | ForEach {Get-PublicFolderStatistics -Server $_.Server | Where {$_.Name -like "*\*"}}
    
    3.  Si el resultado devuelve alguna carpeta pública, puede cambiarle el nombre con este comando:
        
            Set-PublicFolder -Identity <public folder identity> -Name <new public folder name>

3.  Asegúrese de que no exista ningún registro anterior de migración correcta. Si encuentra uno, deberá establecer ese valor como `$false`. Si el valor se establece en `$true`, la solicitud de migración no se realizará correctamente.
    
    1.  El ejemplo siguiente comprueba el estado de la migración de carpetas públicas.
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete
    
    2.  Si el estado de las propiedades *PublicFoldersLockedforMigration* o *PublicFolderMigrationComplete* es `$true`, ejecute el siguiente comando para establecer el valor como `$false`.
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false
    

    > [!WARNING]
    > Después de restablecer estas propiedades, debe esperar a que Exchange detecte la nueva configuración. Esta acción puede tardar hasta dos horas en completarse.



4.  Para realizar las comprobaciones pertinentes al finalizar la migración, le recomendamos ejecutar primero los siguientes comandos Shell de administración de Exchange en el servidor de Exchange heredado para tomar instantáneas de su implementación de carpeta pública actual.
    
    1.  Ejecute el siguiente comando para tomar una instantánea de la estructura de la carpeta original.
        
            Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Legacy_PFStructure.xml
    
    2.  Ejecute el siguiente comando para tomar una instantánea de las estadísticas de carpetas públicas, como recuento de elementos, tamaño y propietario.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Legacy_PFStatistics.xml
    
    3.  Ejecute el siguiente comando para tomar una instantánea de los permisos.
        
            Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML C:\PFMigration\Legacy_PFPerms.xml
    
    Guarde la información de los comandos anteriores para compararlos al finalizar la migración.

5.  Si utiliza Microsoft Azure Active Directory Connect (Azure Connect de AD) para sincronizar los directorios locales con Azure Active Directory, debe hacer lo siguiente (si no está utilizando Azure Connect de AD, puede omitir este paso):
    
    1.  En un equipo local, abra Microsoft Azure Active Directory conectar y, a continuación, seleccione **Configurar**.
    
    2.  En la pantalla de **tareas adicionales**, seleccione **Personalizar las opciones de sincronización** y, a continuación, haga clic en **siguiente**.
    
    3.  En la pantalla **Conectar a Azure AD**, escriba las credenciales adecuadas y, a continuación, haga clic en **siguiente**. Una vez conectado, continúe haciendo clic en **siguiente** hasta que esté en la pantalla **Funciones opcionales** .
    
    4.  Asegúrese de que **Las carpetas públicas de Exchange Mail** no está activada. Si no está activada, puede continuar a la siguiente sección, *que requisito previo de pasos de Exchange Online o de Office 365*. Si está seleccionada, haga clic para desactivar la casilla de verificación y, a continuación, haga clic en **siguiente**.
        

        > [!NOTE]
        > Si no puede ver <STRONG>Las carpetas públicas de Exchange Mail</STRONG> como una opción en la pantalla de <STRONG>Características opcionales</STRONG>, puede salir de Microsoft Azure Active Directory Connect y continúe con la sección siguiente, <EM>que requisito previo pasos en Office 365 o Exchange Online</EM>.

    
    5.  Después de haber desactivado la selección de **Carpetas públicas de Exchange Mail**, mantener hasta que se encuentra en la pantalla **listo para configurar**, haga clic en **siguiente** y, a continuación, haga clic en **Configurar**.

Para más información sobre la sintaxis y los parámetros, vea los siguientes temas:

  - [New-AcceptedDomain](https://technet.microsoft.com/es-es/library/aa995975\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/es-es/library/aa997615\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/es-es/library/jj733416\(v=exchg.150\))

  - [Set-PublicFolder](https://technet.microsoft.com/es-es/library/aa998596\(v=exchg.150\))

  - [Get-PublicFolderStatistics](https://technet.microsoft.com/es-es/library/aa998663\(v=exchg.150\))

  - [Get-PublicFolderClientPermission](https://technet.microsoft.com/es-es/library/bb124365\(v=exchg.150\))

  - [Get-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183212)

  - [Set-OrganizationConfig](https://go.microsoft.com/fwlink/p/?linkid=183213)

**Pasos previos en Office 365 o Exchange Online**

1.  Asegúrese de que no hay ninguna solicitud de migración de carpetas públicas existente. Si la hay, desactívela o se producirá un error en su propia solicitud de migración. Este paso no es necesario en todos los casos; solo es necesario si piensa que puede haber una solicitud de migración existente en la canalización.
    
    Una solicitud de migración existente puede ser de dos tipos: migración por lotes o series. Los comandos para detectar las solicitudes de cada tipo y para quitar las solicitudes de cada tipo son los siguientes.
    

    > [!IMPORTANT]
    > Antes de quitar una solicitud de migración, es importante comprender por qué ya había una. La ejecución del siguiente comando determinará el momento en el que se realizó una solicitud anterior y ayudará a diagnosticar cualquier problema que haya ocurrido. Es posible que deba comunicarse con otros administradores de la organización para determinar por qué se realizó el cambio.

    
    En el ejemplo siguiente se detectará cualquier solicitud de migración serie existente.
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics -IncludeReport | Format-List
    
    El ejemplo siguiente quita cualquier solicitud de migración serie de carpetas públicas existente.
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    En el ejemplo siguiente se detectará cualquier solicitud de migración de lote existente.
    
        $batch = Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    El ejemplo siguiente quita cualquier solicitud de migración de lote de carpetas públicas existente.
    
        $batch | Remove-MigrationBatch -Confirm:$false

2.  Asegúrese de que no existan carpetas públicas ni buzones de carpetas públicas en Office 365.
    

    > [!IMPORTANT]
    > Si ve carpetas públicas en Exchange Online o de Office 365, es importante determinar por qué están ahí y que en su organización inició una jerarquía de carpetas públicas antes de quitar las carpetas públicas y buzones de carpetas públicas.

    
    1.  En Office 365 o Exchange Online PowerShell, ejecute el siguiente comando para ver si existe algún buzón de carpetas públicas.
        
            Get-Mailbox -PublicFolder 
    
    2.  Si el comando no devuelve ningún buzón de carpetas públicas, continúe con el Step 3: Generate the CSV files. Si el comando devuelve algún buzón de carpetas públicas, ejecute el siguiente comando para comprobar si hay alguna carpeta pública:
        
            Get-PublicFolder
    
    3.  Si tiene algunas carpetas públicas en Office 365 o Exchange Online, ejecute el siguiente comando de PowerShell para quitarlas. Asegúrese de haber guardado toda la información que estaba en las carpetas públicas de Office 365. Toda la información que se incluye en las carpetas públicas se eliminará de forma permanente cuando quite las carpetas públicas.
        
            Get-MailPublicFolder | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            
            
            Get-PublicFolder -GetChildren \ | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Una vez que se quitaron las carpetas públicas, ejecute los siguientes comandos para quitar todos los buzones de carpetas públicas.
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false
            
            Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false

Para más información sobre la sintaxis y los parámetros, vea los siguientes temas:

  - [Get-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219164\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218718\(v=exchg.150\))

  - [Remove-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218625\(v=exchg.150\))

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Get-PublicFolder](https://technet.microsoft.com/es-es/library/aa997615\(v=exchg.150\))

  - [Get-MailPublicFolder](https://technet.microsoft.com/es-es/library/bb124772\(v=exchg.150\))

  - [Disable-MailPublicFolder](https://technet.microsoft.com/es-es/library/bb123781\(v=exchg.150\))

  - [Remove-PublicFolder](https://technet.microsoft.com/es-es/library/bb124894\(v=exchg.150\))

  - [Remove-Mailbox](https://technet.microsoft.com/es-es/library/aa995948\(v=exchg.150\))

## Paso 3: Generar los archivos .csv

1.  En el servidor de Exchange heredado, ejecute el script `Export-PublicFolderStatistics.ps1` para crear el nombre de carpeta para el archivo de asignación de tamaño de carpeta. Este script siempre debe ejecutarlo un administrador local. El archivo tendrá dos columnas: **FolderName** y **FolderSize**. Los valores de la columna **FolderSize** se mostrarán en bytes. Por ejemplo, **\\PublicFolder01,10000**.
    
        .\Export-PublicFolderStatistics.ps1  <Folder to size map path> <FQDN of source server>
    
      - *FQDN of source server* equivale al nombre de dominio completo del servidor de buzones de correo en el que se hospeda la jerarquía de la carpeta pública.
    
      - *Folder to size map path* equivale al nombre de archivo y a la ruta de acceso de la carpeta compartida de red en la que desea guardar el archivo .csv. Más adelante en este tema, deberá usar Exchange Online PowerShell para obtener acceso a este archivo. Si especifica solo el nombre del archivo, el archivo se generará en el directorio actual de PowerShell en el equipo local.
    
      - Si es necesario, quite todas las carpetas del sistema habilitadas para correo de la salida del script antes de continuar.

2.  Ejecute el script `PublicFolderToMailboxMapGenerator.ps1` para crear el archivo de asignación de carpetas públicas al buzón de correo. Este archivo se usa para calcular el número correcto de buzones de carpetas públicas en Exchange Online.
    
        .\PublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes> <Folder to size map path> <Folder to mailbox map path>
    

    > [!IMPORTANT]
    > El archivo de asignación de buzón de carpeta pública no debe superar los 1.000 filas. Si este archivo excede de 1000 filas, debe simplificarse la estructura de carpetas públicas. Continuar con un archivo de más de 1.000 filas no se recomienda y podría producir errores de migración.

    
      - Antes de ejecutar la secuencia de comandos, utilice el siguiente cmdlet para comprobar los límites de carpetas públicas actual en los inquilinos Exchange Online. A continuación, observe los valores de cuota actuales para las carpetas públicas. `Get-OrganizationConfig | fl *quota*`
        
        En Exchange Online, el valor predeterminado es 1,7 GB para **DefaultPublicFolderIssueWarningQuota** y 2 GB para **DefaultPublicFolderProhibitPostQuota**.
    
      - *Maximum mailbox size in bytes* equivale al tamaño máximo que desea establecer para los nuevos buzones de carpetas públicas. En Exchange Online, el tamaño máximo de los buzones de carpetas públicas es 100 GB. Se recomienda utilizar un valor de 15 GB para que cada buzón de la carpeta pública tiene espacio para crecer. Exchange Online tiene una cuota predeterminada de "Prohibir el post" de la carpeta pública de 2 GB. Si tiene carpetas públicas individuales que son mayores de 2 GB, puede utilizar cualquiera de las opciones siguientes para corregir este problema:
        
          - Antes de iniciar el proceso de migración, aumente la cuota de "Prohibir el post" de carpetas públicas predeterminada ejecutando el siguiente cmdlet:
            
            `Set-OrganizationConfig -DefaultPublicFolderProhibitPostQuota <size value> -DefaultPublicFolderIssueWarningQuota <size value>`
        
          - Antes de iniciar el proceso de migración, elimine la carpeta pública contenido para reducir el tamaño del contenido a 2 GB o menos.
        
          - Antes de iniciar el proceso de migración, divida la carpeta pública en varias carpetas públicas que están cada 2 GB o menos.
        

        > [!NOTE]
        > Si la carpeta pública es mayor que 30 GB, y si no es factible para eliminar contenido o dividirla en varias carpetas públicas, se recomienda no mover las carpetas públicas a Exchange Online.

    
      - *Folder to size map path* es igual a la ruta de acceso del archivo .csv que creó cuando ejecutó la secuencia de comandos `Export-PublicFolderStatistics.ps1` .
    
      - es igual a *Folder to mailbox map path* el nombre de archivo y la ruta del archivo .csv de buzón de carpeta que se crea en este paso. Si especifica sólo el nombre del archivo, el archivo se genera en el directorio actual de PowerShell en el equipo local.


> [!NOTE]
> Después se ejecutan las secuencias de comandos y se generan los archivos .csv, no se recopilará ningún nuevas carpetas públicas o las actualizaciones de las carpetas públicas existentes.



## Paso 4: Creación de los buzones de carpetas públicas en Exchange Online

1.  Ejecute el siguiente comando para crear el buzón de carpetas públicas de destino. El script creará un buzón de destino para cada buzón del archivo .csv que generó anteriormente en el paso 3, mediante la ejecución del script PublicFoldertoMailboxMapGenerator.ps1.
    
        .\Create-PublicFolderMailboxesForMigration.ps1 -FolderMappingCsv Mapping.csv -EstimatedNumberOfConcurrentUsers:<estimate>
    
    *Mapping.csv* es el archivo que se genera mediante el script PublicFoldertoMailboxMapGenerator.ps1 en el paso 3. El número estimado de conexiones de usuario simultáneas que exploran una jerarquía de carpetas públicas suele ser menor que el número total de usuarios de una organización.

## Paso 5: Inicio de la solicitud de migración

1.  En el servidor Exchange heredado, ejecute el siguiente comando para sincronizar las carpetas públicas habilitadas para correo entre su Active Directory local y Exchange Online.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    `Credential` es su nombre de usuario y contraseña de Office 365. `CsvSummaryFile` es la ruta del archivo en el que desea registrar, en formato .CSV, las operaciones de sincronización y los errores.
    

    > [!NOTE]
    > Le recomendamos que primero simule las acciones que llevará a cabo el script antes de ejecutarlo realmente. Para ello, ejecute el script con un parámetro <CODE>-WhatIf</CODE>.



2.  En el servidor de Exchange heredado, obtenga la siguiente información necesaria para ejecutar la solicitud de migración:
    
    1.  Busque el valor `LegacyExchangeDN` de la cuenta del usuario que es miembro del rol de administrador de carpetas públicas. Se trata del mismo usuario cuyas credenciales usó en el paso 3 de este procedimiento.
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  Busque el `LegacyExchangeDN` de cualquier servidor de buzones de correo que tenga una base de datos de carpetas públicas.
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  Busque el nombre de dominio completo del nombre de host de Outlook en cualquier lugar. Si tiene varias instancias de Outlook en cualquier lugar, le recomendamos que seleccione la instancia que esté más cerca del extremo de migración o la que esté más cerca de las réplicas de las carpetas públicas en la organización de Exchange heredada. El siguiente comando encontrará todas las instancias de Outlook en cualquier lugar:
        
            Get-OutlookAnywhere | Format-Table Identity,ExternalHostName

3.  En el PowerShell de Office 365, ejecute los siguientes comandos para pasar la información que se le proporcionó en el paso anterior a variables que luego se usarán en la solicitud de migración.
    
    1.  Pase la credencial de un usuario con permisos administrativos en el servidor de Exchange heredado a la variable `$Source_Credential`. La solicitud de migración que se ejecuta en Exchange Online usará esta credencial para obtener acceso a los servidores de Exchange heredados para copiar el contenido.
        
            $Source_Credential = Get-Credential <source_domain\PublicFolder_Administrator_Account>
    
    2.  Use el valor `ExchangeLegacyDN` del usuario de migración en el servidor de Exchange heredado que encontró en el paso 2a y páselo a la variable `$Source_RemoteMailboxLegacyDN`.
        
            $Source_RemoteMailboxLegacyDN = "<paste the value here>"
    
    3.  Use el `ExchangeLegacyDN` del servidor de carpetas públicas que encontró en el paso 2b anterior y páselo a la variable `$Source_RemotePublicFolderServerLegacyDN`.
        
            $Source_RemotePublicFolderServerLegacyDN = "<paste the value here>"
    
    4.  Use el nombre de host externo de Outlook en cualquier lugar que encontró en el paso 2c y páselo a la variable `$Source_OutlookAnywhereExternalHostName`.
        
            $Source_OutlookAnywhereExternalHostName = "<paste the value here>"

4.  Por último, en Exchange Online PowerShell, ejecute los siguientes comandos para crear la solicitud de migración.
    

    > [!NOTE]
    > El método de autenticación del siguiente ejemplo del Shell de administración de Exchange tiene que coincidir con la configuración de Outlook en cualquier lugar o se producirá un error en el comando.

    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic
        
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    
    Donde el archivo \<*folder\_mapping.csv*\> es el archivo que se generó en el Step 3: Generate the .csv files.

5.  Inicie la migración con el siguiente comando:
    
        Start-MigrationBatch PublicFolderMigration

Aunque las migraciones por lotes deben crearse con el cmdlet **New-MigrationBatch** en el Shell de administración de Exchange, el progreso y la finalización de la migración se pueden ver y administrar en el EAC. Como el cmdlet **New-MigrationBatch** inicia una solicitud de migración de buzones para cada buzón de carpetas públicas, puede ver el estado de estas solicitudes usando la página migración de buzones. Para acceder a la página de migración de buzones y crear informes de migración que pueda recibir por correo electrónico, haga lo siguiente:

1.  Inicie sesión en Exchange Online y abra el EAC.

2.  Vaya a **Buzón** \> **Migración**.

3.  Seleccione la solicitud de migración que acaba de crear y haga clic en **Ver detalles** en el panel **Detalles**.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Get-ExchangeServer](https://technet.microsoft.com/es-es/library/bb123873\(v=exchg.150\))

  - [Get-OutlookAnywhere](https://technet.microsoft.com/es-es/library/bb124263\(v=exchg.150\))

  - [New-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218636\(v=exchg.150\))

  - [Get-PublicFolderDatabase](https://technet.microsoft.com/es-es/library/jj733416\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequest](https://technet.microsoft.com/es-es/library/jj218718\(v=exchg.150\))

  - [Get-PublicFolderMigrationRequestStatistics](https://technet.microsoft.com/es-es/library/jj218697\(v=exchg.150\))

## Paso 6: Bloquear las carpetas públicas del servidor de Exchange heredado para la migración final (se requiere tiempo de inactividad)

Hasta este punto del proceso de migración, los usuarios han podido obtener acceso a las carpetas públicas. En los siguientes pasos, los usuarios deberán cerrar la sesión en las carpetas públicas heredadas y bloquear las carpetas mientras la migración completa su sincronización final. Los usuarios no podrán tener acceso a las carpetas públicas durante este proceso. Además, cualquier correo enviado a carpetas públicas habilitadas para correo se colocará en cola y no se entregará hasta que haya finalizado la migración de dichas carpetas públicas.

Antes de ejecutar el comando `PublicFoldersLockedForMigration` como se describe a continuación, asegúrese de que todos los trabajos están en el estado **sincronizadas**. Para ello, ejecute el comando `Get-PublicFolderMailboxMigrationRequest` . Siga con este paso sólo después de haber comprobado que todos los trabajos están en el estado **sincronizadas**.

En el servidor de Exchange heredado, ejecute el comando siguiente para bloquear las carpetas públicas heredadas para poder finalizar la migración.

    Set-OrganizationConfig -PublicFoldersLockedForMigration:$true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)).

Si su organización dispone de varias bases de datos de carpetas públicas, deberá esperar a que se complete la replicación de carpetas públicas para confirmar que todas las bases de datos han seleccionado la marca `PublicFoldersLockedForMigration` y que los cambios pendientes realizados por los usuarios en las carpetas convergen en toda la organización. Esto puede tardar varias horas.

## Paso 7: Finalización de la migración de carpetas públicas (se requiere tiempo de inactividad)

Para completar la migración de carpetas públicas, ejecute el siguiente comando:

    Complete-MigrationBatch PublicFolderMigration

Cuando termine la migración, Exchange realizará una sincronización entre el servidor de Exchange heredado y Exchange Online. Si la sincronización se realiza correctamente, las carpetas públicas de Exchange Online se desbloqueará y se cambia el estado del lote de migración a **completada**. Es habitual que el lote de migración tomar unas pocas horas antes de su estado cambia de **sincronizadas** para **finalización**, momento en el que comenzará la sincronización.

Si configuró una implementación híbrida entre los servidores Exchange locales y Office 365, necesita ejecutar el siguiente comando en Exchange Online PowerShell una vez completada la migración:

    Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Paso 8: Prueba y desbloqueo de la migración de carpetas públicas

Después de completar la migración de carpetas públicas, debe ejecutar la prueba siguiente para asegurarse de que dicha migración se realizó correctamente. Así podrá probar la jerarquía de carpetas públicas migradas antes de pasar a usar carpetas públicas de Office 365 o Exchange Online.

1.  En el PowerShell de Office 365 o Exchange Online, asigne algunos buzones de correo de prueba para poder usar cualquier buzón de carpetas públicas recientemente migrado como buzón predeterminado.
    
        Set-Mailbox -Identity <Test User> -DefaultPublicFolderMailbox <Public Folder Mailbox Identity>

2.  Inicie sesión en Outlook 2007 o versiones posteriores con el usuario de prueba identificado en el paso anterior y luego realice las pruebas siguientes para las carpetas públicas:
    
      - Ver la jerarquía
    
      - Compruebe los permisos.
    
      - Cree y elimine carpetas públicas.
    
      - Publique contenido en una carpeta pública y elimine contenido de ella.

3.  Si surge algún problema, consulte revertir la migración más adelante en este tema. Si la jerarquía y el contenido de carpetas públicas es aceptables y funciona como se esperaba, continúe con el paso siguiente.

4.  En el servidor de Exchange heredado, ejecute el siguiente comando para indicar que ya se ha completado la migración de carpetas públicas:
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$true

5.  Tras haber comprobado que la migración está completada, ejecute el siguiente comando en Exchange Online PowerShell para asegurarse de que el parámetro *PublicFoldersEnabled* en **Set-OrganizationConfig** se establece en `Local`:
    
        Set-OrganizationConfig -PublicFoldersEnabled Local

Para más información sobre la sintaxis y los parámetros, vea los siguientes temas:

[Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

[Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

[Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

En Step 2: Prepare for the migration, se le pidió que tomara instantáneas de la estructura de las carpetas públicas, estadísticas y permisos antes de que empezara la migración. Mediante los siguientes pasos podrá comprobar si la migración de carpetas públicas se realizó correctamente. Para esto, se tomarán las mismas instantáneas una vez que la migración haya finalizado. De esta manera, podrá comparar los datos de ambos archivos para comprobar que el proceso haya sido correcto.

1.  En Exchange Online PowerShell, ejecute el siguiente comando para tomar una instantánea de la nueva estructura de carpetas.
    
        Get-PublicFolder -Recurse | Export-CliXML C:\PFMigration\Cloud_PFStructure.xml

2.  En Exchange Online PowerShell, ejecute el siguiente comando para tomar una instantánea de las estadísticas de carpetas públicas, como recuento de elementos, tamaño y propietario.
    
        Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML C:\PFMigration\Cloud_PFStatistics.xml

3.  En Exchange Online PowerShell, ejecute el siguiente comando para tomar una instantánea de los permisos.
    
        Get-PublicFolder -Recurse | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML  C:\PFMigration\Cloud_PFPerms.xml

## Quitar bases de datos de carpetas públicas de los servidores de Exchange heredados

Una vez que se haya completado la migración y haya comprobado que las carpetas públicas de Exchange Online funcionan tal y como se esperaba, deberá quitar las bases de datos de carpetas públicas de los servidores de Exchange heredados.


> [!IMPORTANT]
> Como todos sus buzones se han migrado a Office 365 antes de la migración de carpetas públicas, le recomendamos que dirija el tráfico mediante Office 365 (flujo de correo descentralizado) en lugar del flujo de correo centralizado mediante su entorno local. Si decide mantener el flujo de correo centralizado, puede provocar problemas de entrega en sus carpetas públicas, ya que ha quitado las bases de datos de buzones de carpetas públicas de su organización local.



  - Para más información sobre cómo quitar las bases de datos de carpetas públicas de los servidores de Exchange 2007, vea [Quitar bases de datos de carpetas públicas](https://go.microsoft.com/fwlink/?linkid=123678).

  - Para más información sobre cómo quitar las bases de datos de carpetas públicas de los servidores de Exchange 2010, vea [Quitar bases de datos de carpetas públicas](https://go.microsoft.com/fwlink/?linkid=81409).

## Revertir la migración

Si tiene problemas con la migración y necesita reactivar sus carpetas públicas de Exchange heredadas, realice los pasos siguientes.


> [!WARNING]
> Si revierte su migración a los servidores de Exchange heredados, perderá todos los correos electrónicos que se enviaron a las carpetas públicas habilitadas para correo o el contenido que se publicó en las carpetas públicas después de la migración. Para guardar este contenido, debe exportar el contenido de la carpeta pública a un archivo .pst y luego importarlo a las carpetas públicas heredadas cuando se completa la reversión.



1.  En el servidor de Exchange heredado, ejecute el comando siguiente para desbloquear las carpetas públicas heredadas de Exchange. Este proceso puede tardar varias horas.
    
        Set-OrganizationConfig -PublicFoldersLockedForMigration:$False

2.  En Exchange Online PowerShell, ejecute los siguientes comandos para quitar todas las carpetas públicas de Exchange Online.
    
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        
        Get-Mailbox -PublicFolder:$true | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force

3.  En el servidor de Exchange heredado, ejecute el comando siguiente para establecer la marca `PublicFolderMigrationComplete` como `$false`.
    
        Set-OrganizationConfig -PublicFolderMigrationComplete:$False

## Migrar carpetas públicas a Office 365 mediante la exportación de archivos PST de Outlook

Se recomienda que no utilice la característica de exportación de PST de Outlook para migrar carpetas públicas a Office 365 o Exchange Online si la jerarquía de carpetas públicas local es superior a 30 GB. El crecimiento de los buzones de la carpeta pública en línea de Office 365 se administra mediante una característica de división automática que divide el buzón de carpetas públicas cuando supera las cuotas de tamaño. La división automática no puede controlar el crecimiento repentino de los buzones de la carpeta pública cuando se usa la exportación de PST para migrar las carpetas públicas y puede que tenga que esperar hasta dos semanas para que la división automática mueva los datos desde el buzón principal. Además, tenga en cuenta lo siguiente antes de utilizar PST de Outlook para exportar las carpetas públicas a Office 365 o Exchange Online:

  - Los permisos de carpetas públicas se perderán durante este proceso. Capture los permisos actuales antes de la migración y vuelva a agregarlos manualmente una vez completada la migración.

  - Si utiliza permisos complejos o tiene muchas carpetas que migrar, se recomienda usar el método de cmdlet para la migración.

  - Se perderán los cambios de elemento y carpeta realizados en las carpetas públicas de origen durante la migración de la exportación de PST. Por lo tanto, se recomienda usar el método de cmdlet si este proceso de exportación e importación tarda mucho tiempo en completarse.

Si desea migrar las carpetas públicas mediante archivos PST, siga estos pasos para garantizar una migración exitosa.

1.  Use las instrucciones en Step 1: Download the migration scripts para descargar los scripts de migración. Solo necesita descargar el archivo `PublicFolderToMailboxMapGenerator.ps1`.

2.  Siga el paso 2 de Step 3: Generate the .csv files para crear el archivo de asignación de carpetas públicas al buzón de correo. Este archivo se usa para calcular el número correcto de buzones de carpetas públicas en Exchange Online.

3.  Cree los buzones de carpeta pública que necesite en función del archivo de asignación. Para obtener más información, consulte [Crear un buzón de carpetas públicas](create-a-public-folder-mailbox-exchange-2013-help.md).

4.  Use el cmdlet New-PublicFolder para crear la carpeta pública principal en cada uno de los buzones de la carpeta pública mediante el parámetro *Mailbox*.

5.  Exporte e importe los archivos PST con Outlook.

6.  Establezca los permisos en las carpetas públicas mediante el EAC. Para obtener más información, siga el [Step 3: Assign permissions to the public folder](set-up-public-folders-in-a-new-organization-exchange-2013-help.md) en el tema [Configurar las carpetas públicas de una nueva organización](set-up-public-folders-in-a-new-organization-exchange-2013-help.md).


> [!WARNING]
> Si ya inició una migración de PST y se topa con un problema en el que el buzón principal está lleno, tiene dos opciones para recuperar la migración de PST: 
> <OL>
> <LI>
> <P>Espere a que la división automática mueva los datos desde el buzón principal. Esto puede tardar hasta dos semanas. Sin embargo, todas las carpetas públicas en un buzón completamente lleno de carpetas públicas no podrán recibir el contenido nuevo hasta que se complete la división automática.</P>
> <LI>
> <P><A href="create-a-public-folder-mailbox-exchange-2013-help.md">Crear un buzón de carpetas públicas</A> y, a continuación, use el cmdlet <STRONG>New-PublicFolder</STRONG> con el parámetro <EM>Mailbox</EM> para crear las carpetas públicas restantes en el buzón de carpeta pública secundario. En este ejemplo se crea una nueva carpeta pública denominada PF201 en el buzón de carpeta pública secundario.</P><PRE><CODE>New-PublicFolder -Name PF201 -Mailbox SecondaryPFMbx</CODE></PRE></LI></OL>



## ¿Es la primera vez que usa Office 365?


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><img src="images/Bb123521.eac8a413-9498-4220-8544-1e37d1aaea13(EXCHG.150).png" title="Icono reducido de LinkedIn Learning" alt="Icono reducido de LinkedIn Learning" /> <strong>¿Es la primera vez que usa Office 365?</strong><br />
LinkedIn Learning pone a su disposición vídeos gratuitos de cursos de <a href="https://support.office.com/es-es/article/office-365-admin-and-it-pro-courses-68cc9b95-0bdc-491e-a81f-ee70b3ec63c5">Office 365 admins and IT pros</a>.</p></td>
</tr>
</tbody>
</table>

