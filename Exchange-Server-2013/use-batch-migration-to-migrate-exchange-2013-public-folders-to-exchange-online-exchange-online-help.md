---
title: 'Usar migración lotes migrar carpetas públicas Exchange 2013 a Exchange Online'
TOCTitle: Usar la migración por lotes para migrar carpetas públicas de Exchange 2013 a Exchange Online
ms:assetid: 25a5234c-dd2c-487b-8541-3655fbeb030a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt798260(v=EXCHG.150)
ms:contentKeyID: 74432707
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar la migración por lotes para migrar carpetas públicas de Exchange 2013 a Exchange Online

 

_**Última modificación del tema:** 2018-03-26_

**Resumen:**  Este artículo le indica cómo mover las carpetas públicas modernas de Exchange 2013 a Office 365.

Migrar las carpetas públicas de Exchange de 2013 a Exchange Online requiere Exchange Server 2013 CU15 o posterior ejecutándose en su entorno local.


> [!NOTE]
> Si tiene carpetas públicas tanto de Exchange 2013 como de Exchange 2016 en su organización y quiere moverlas todas a Exchange Online, use <A href="https://go.microsoft.com/fwlink/p/?linkid=845314">la versión de Exchange 2016 de este artículo</A> para planear y ejecutar la migración. Aun así, sus servidores de Exchange 2013 necesitarán tener instalada la actualización acumulativa 15 o una versión posterior.



## ¿Qué necesita saber antes de comenzar?

  - Cuando actualiza a Exchange Server 2013 CU15 o a una versión posterior, también debe preparar Active Directory o se producirá un error en la migración de las carpetas públicas. Esta preparación de Active Directory garantiza que todos los parámetros y cmdlets de PowerShell relevantes estén disponibles para la preparación y la ejecución de la migración. Vea [Preparar Active Directory y los dominios](prepare-active-directory-and-domains-exchange-2013-help.md) para obtener más información.

  - En Exchange Online, debe ser miembro del grupo de roles de administración de la organización. Este grupo de roles es diferente de los permisos que se le asignan cuando se suscribe a Office 365 o Exchange Online. Para obtener más información sobre cómo habilitar el grupo de roles de administración de la organización, vea [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - En Exchange Server 2013, debe ser miembro de los grupos de roles RBAC de administración de servidores o de administración de la organización. Para obtener más información, vea [Agregar miembros a un grupo de funciones](https://go.microsoft.com/fwlink/?linkid=299212).

  - Antes de que comience la migración de carpetas públicas, si cualquier carpeta pública de su organización es mayor de 25 GB, le recomendamos que elimine contenido de esa carpeta para hacerla más pequeña, o que divida el contenido de la carpeta pública en varias carpetas públicas más pequeñas. Tenga en cuenta que el límite de 25 GB que se ha mencionado aquí solo se aplica a la carpeta pública y no a cualquier elemento secundario ni subcarpetas que pueda tener la carpeta en cuestión. Si ninguna opción es viable, recomendamos que no mueva sus carpetas públicas a Exchange Online. Para obtener más información, vea [Límites de Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=391188).
    

    > [!NOTE]
    > Si las cuotas de sus carpetas públicas actuales en Exchange Online son inferiores a 25&nbsp;GB, puede usar el <A href="https://go.microsoft.com/fwlink/p/?linkid=844062">cmdlet Set-OrganizationConfig</A> para aumentarlas con los parámetros DefaultPublicFolderIssueWarningQuota y DefaultPublicFolderProhibitPostQuota.



  - En Office 365 y Exchange Online, puede crear un máximo de 1000 buzones de carpetas públicas.

  - Si pretende migrar usuarios a Office 365, debe completar la migración de usuarios antes de migrar las carpetas públicas. Para obtener más información, vea [Formas de migrar el correo electrónico de varias cuentas a Office 365](https://go.microsoft.com/fwlink/p/?linkid=842798).

  - El proxy MRS necesita habilitarse en al menos un servidor de Exchange, un servidor que también esté hospedando buzones de carpetas públicas. Para obtener más información, vea [Habilitar el extremo del proxy MRS para movimientos remotos](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md).

  - Para realizar los procedimientos de migración de este artículo, no puede usar el Centro de administración de Exchange (EAC). En su lugar, necesita usar el Shell de administración de Exchange en sus servidores de Exchange 2013. En Exchange Online, debe usar Exchange Online PowerShell. Para obtener más información, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=842801).

  - Se admite la migración de elementos y carpetas eliminadas de Exchange 2013 a Exchange Online. Antes de comenzar la migración, le recomendamos que revise todas las carpetas eliminadas y los elementos de carpeta, y que elimine de manera permanente todo lo que no va a necesitar en Exchange Online. Tenga en cuenta que cuando algo se elimina de manera permanente, no puede recuperarse.
    
    Puede usar los siguientes comandos para mostrar las carpetas públicas eliminadas que se encuentran en el contenedor de Exchange (en su entorno local de Exchange):
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null"} | ft name,foldersize
    
    Para eliminar de manera permanente una carpeta específica, use el siguiente comando (en este ejemplo se usa una carpeta denominada "Calendar2"):
    
        Get-PublicFolder \NON_IPM_SUBTREE\DUMPSTER_ROOT -Recurse | ?{$_.FolderClass -ne "$null" -and $_.Name -eq "Calendar2"} | Remove-PublicFolder

  - Antes de comenzar, lea este artículo en su totalidad. En algunos pasos, se necesita un tiempo de inactividad. Durante este tiempo de inactividad, nadie tendrá acceso a las carpetas públicas.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Paso 1: Descarga de los scripts de migración

1.  Descargue todos los scripts y archivos auxiliares desde [Scripts de migración de carpetas públicas de Exchange 2013/2016](https://go.microsoft.com/fwlink/p/?linkid=844893).

2.  Guarde los scripts en el equipo local en el que ejecutará PowerShell. Por ejemplo, C:\\PFScripts. Asegúrese de que todos los scripts se guardan en la misma ubicación.

Los scripts y los archivos que está descargando son:

  - `Sync-ModernMailPublicFolders.ps1` Este script sincroniza los objetos de carpeta pública habilitada para correo entre el entorno local de Exchange y Office 365. Ejecutará este script en un servidor de Exchange 2013.

  - `SyncModernMailPublicFolders.strings.psd1` Este archivo de compatibilidad se usa en el script Sync-ModernMailPublicFolders.ps1 y debe descargarse en la misma ubicación.

  - `Export-ModernPublicFolderStatistics.ps1` Este script crea el nombre de carpeta para el archivo de asignación del tamaño de la carpeta y del tamaño de los elementos eliminados. Ejecutará este script en el servidor de Exchange 2013.

  - `Export-ModernPublicFolderStatistics.strings.psd1` Este archivo de compatibilidad se usa en el script Export-ModernPublicFolderStatistics.ps1 y debe descargarse en la misma ubicación.

  - `ModernPublicFolderToMailboxMapGenerator.ps1` Este script crea el archivo de asignación de carpetas públicas al buzón de correo mediante el uso de la salida del script Export-ModernPublicFolderStatistics.ps1. Deberá ejecutar este script en un servidor de Exchange 2013.

  - `ModernPublicFolderToMailboxMapGenerator.strings.psd1` Este archivo de compatibilidad se usa en el script ModernPublicFolderToMailboxMapGenerator.ps1 y debe descargarse en la misma ubicación.

  - `SetMailPublicFolderExternalAddress.ps1` Este script actualiza `ExternalEmailAddress` de carpetas públicas habilitadas para correo en su entorno local al de sus equivalentes de Exchange Online. Esto garantiza que, después de la migración, los correos electrónicos dirigidos a las carpetas públicas habilitadas para correo se enrutan correctamente a Exchange Online. Necesita ejecutar este script en un servidor de Exchange 2013.

  - `SetMailPublicFolderExternalAddress.strings.psd1` Este archivo de compatibilidad se usa en el script SetMailPublicFolderExternalAddress.ps1 y debe descargarse en la misma ubicación.

## Paso 2: Preparación para la migración

Realice todos los pasos de requisitos previos de las secciones siguientes antes de comenzar la migración de carpetas públicas.

**Pasos generales de los requisitos previos**

Para que la migración se realice correctamente, debe:

  - Asegurarse de que no hay ningún objeto de correo huérfano en las carpetas públicas en Active Directory. Estos son objetos de Active Directory sin un objeto correspondiente de Exchange.

  - Confirmar que las direcciones de correo electrónico SMTP configuradas para las carpetas públicas de Active Directory coinciden con las direcciones de correo electrónico SMTP en los objetos de Exchange.

  - Asegurarse de que no hay ningún objeto de carpeta pública duplicado en Active Directory. Esto es necesario para evitar tener dos o más objetos de Active Directory que apunten a la misma carpeta pública habilitada para correo.

**Pasos de requisitos previos en el entorno local del servidor de Exchange 2013**

En el Shell de administración de Exchange (local) realice los pasos siguientes:

1.  Una vez que se complete la migración, tardará algún tiempo que las memorias caché DNS en Internet dirijan los mensajes a sus carpetas públicas habilitadas para correo en su nueva ubicación de Exchange Online. Puede asegurarse de que sus carpetas públicas habilitadas para correo recién migradas reciben mensajes durante este período de transición de DNS creando un dominio aceptado con un nombre conocido. Para hacerlo, ejecute el siguiente comando en su entorno local de Exchange. En este ejemplo, `target domain` es su dominio de Office 365 o Exchange Online, para el que ya se ha configurado un conector de envío mediante el Asistente para la configuración híbrida.
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName <target domain> -DomainType InternalRelay
    
    **Ejemplo**:
    
        New-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99 -DomainName "contoso.mail.onmicrosoft.com" -DomainType InternalRelay
    
    Si el dominio aceptado ya existe en su entorno local, cambie su nombre a `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99` y mantenga intactos los demás atributos.
    
    Para comprobar si el dominio aceptado ya está presente en su entorno local:
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" }
    
    Para cambiar el nombre del dominio aceptado a `PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99`, ejecute lo siguiente:
    
        Get-AcceptedDomain | Where { $_.DomainName -eq "<target domain>" } | Set-AcceptedDomain -Name PublicFolderDestination_78c0b207_5ad2_4fee_8cb9_f373175b3f99
    

    > [!NOTE]
    > Si está esperando que sus carpetas públicas habilitadas para correo en Exchange Online reciban correos electrónicos externos de Internet, tiene que deshabilitar el Bloqueo perimetral basado en directorios (DBEB) en Exchange Online y Exchange Online Protection (EOP). Vea <A href="https://technet.microsoft.com/es-es/library/dn600322(v=exchg.150)">Usar bloqueo perimetral basado en directorios para rechazar mensajes enviados a destinatarios no válidos</A> para obtener más información.



2.  Si el nombre de una carpeta pública contiene una barra diagonal inversa **\\** o una barra diagonal **/**, puede que no se migre a su buzón designado durante el proceso de migración. Antes de realizar la migración, cambie el nombre de dichas carpetas para quitar estos caracteres
    
    1.  Para localizar las carpetas públicas con una barra diagonal inversa en el nombre, ejecute el comando siguiente:
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Where {$_.Name -like "*\*" -or $_.Name -like "*/*"} | Format-List Name, Identity, EntryId
    
    2.  Si el resultado devuelve alguna carpeta pública, puede cambiarle el nombre con este comando:
        
            Set-PublicFolder -Identity "<public folder EntryId>" -Name "<new public folder name>"

3.  Realice los pasos siguientes para confirmar que no existe un registro de una migración correcta anterior en su organización. Si encuentra uno, debe establecer ese valor como `$false`.
    
    Antes de cambiar los valores, confirme que el intento de migración anterior puede descartarse, de manera que no realice accidentalmente una segunda migración.
    
    1.  Ejecute el comando siguiente para comprobar cualquier migración anterior, y el estado de esas migraciones:
        
            Get-OrganizationConfig | Format-List PublicFoldersLockedforMigration, PublicFolderMigrationComplete, PublicFolderMailboxesLockedForNewConnections, PublicFolderMailboxesMigrationComplete
        

        > [!NOTE]
        > Si los parámetros <CODE>PublicFoldersLockedforMigration</CODE> o <CODE>PublicFolderMigrationComplete</CODE> son <CODE>$true</CODE>, significa que ha migrado carpetas públicas heredadas en algún momento. Asegúrese de que todas las bases de datos de carpetas públicas heredadas se han retirado antes de que siga con el paso 3b.

    
    2.  Si cualquiera de las anteriores se ha devuelto con un valor establecido en `$true`, conviértalas en `$false` ejecutando:
        
            Set-OrganizationConfig -PublicFoldersLockedforMigration:$false -PublicFolderMigrationComplete:$false -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false

4.  Con el fin de comprobar el éxito de la migración tras su finalización, recomendamos que ejecute los comandos siguientes en todos los servidores de Exchange 2013 apropiados. Esto tomará instantáneas de su implementación de carpetas públicas actual que puede usar más tarde para compararlas con sus carpetas públicas recién migradas.
    

    > [!NOTE]
    > Dependiendo del tamaño de la organización de Exchange, la ejecución de estos comandos puede tardar algún tiempo.

    
      - Ejecute el siguiente comando para tomar una instantánea de la estructura de la carpeta original.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML OnPrem_PFStructure.xml
    
      - Ejecute el siguiente comando para tomar una instantánea de las estadísticas de carpetas públicas, como recuento de elementos, tamaño y propietario.
        
            Get-PublicFolderStatistics -ResultSize Unlimited | Export-CliXML OnPrem_PFStatistics.xml
    
      - Ejecute el siguiente comando para tomar una instantánea de permisos de la carpeta pública.
        
            Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User -ExpandProperty AccessRights | Export-CliXML OnPrem_PFPerms.xml
    
      - Ejecute el siguiente comando para tomar una instantánea de las carpetas públicas habilitadas para correo:
        
            Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML OnPrem_MEPF.xml
    
      - Guarde los archivos que se han generado de los comandos anteriores en un lugar seguro para realizar una comparación al final de la migración.

5.  Si utilizas Microsoft Azure Active Directory Connect (Azure Connect de AD) para sincronizar los directorios locales con Azure Active Directory, debe realizar las acciones siguientes (si no está utilizando Azure Connect de AD, puede omitir este paso):
    
    1.  En un equipo local, abra Microsoft Azure Active Directory conectar y, a continuación, seleccione **Configurar**.
    
    2.  En la pantalla de **tareas adicionales**, seleccione **Personalizar las opciones de sincronización** y, a continuación, haga clic en **siguiente**.
    
    3.  En la pantalla **Conectar a Azure AD**, escriba las credenciales adecuadas y, a continuación, haga clic en **siguiente**. Una vez conectado, continúe haciendo clic en **siguiente** hasta que esté en la pantalla **Funciones opcionales** .
    
    4.  Asegúrese de que **Las carpetas públicas de Exchange Mail** no está activada. Si no está activada, puede continuar a la siguiente sección, *requisito previo pasos en Exchange Online*. Si está seleccionada, haga clic para desactivar la casilla de verificación y, a continuación, haga clic en **siguiente**.
        

        > [!NOTE]
        > Si no puede ver <STRONG>Las carpetas públicas de Exchange Mail</STRONG> como una opción en la pantalla de <STRONG>Características opcionales</STRONG>, puede salir de Microsoft Azure Active Directory Connect y continúe con la sección siguiente, <EM>requisito previo pasos en Exchange Online</EM>.

    
    5.  Después de haber desactivado la selección de **Carpetas públicas de Exchange Mail**, mantener hasta que se encuentra en la pantalla **listo para configurar**, haga clic en **siguiente** y, a continuación, haga clic en **Configurar**.

**Pasos de requisitos previos en Exchange Online**

En Exchange Online PowerShell, haga lo siguiente:

1.  Asegúrese de que no hay ninguna solicitud de migración de carpetas públicas existente. Si la hay, desactívela o se producirá un error en su propia solicitud de migración. Este paso solo es necesario si piensa que puede haber una solicitud de migración existente en la canalización (una que ha fallado o que quiere anular).
    
    Una solicitud de migración existente puede ser de dos tipos: migración por lotes o en serie. Los comandos para detectar, y quitar, cada tipo de solicitud son los siguientes.
    
    En el ejemplo siguiente se detectará cualquier solicitud de migración en serie existente:
    
        Get-PublicFolderMigrationRequest | Get-PublicFolderMigrationRequestStatistics 
    
    En el ejemplo siguiente se quita cualquier solicitud de migración en serie de carpetas públicas existente:
    
        Get-PublicFolderMigrationRequest | Remove-PublicFolderMigrationRequest
    
    En el ejemplo siguiente se detectará cualquier solicitud de migración por lotes existente:
    
        Get-MigrationBatch | ?{$_.MigrationType.ToString() -eq "PublicFolder"}
    
    En el ejemplo siguiente se quita cualquier solicitud de migración por lotes de carpetas públicas existente:
    
        Remove-MigrationBatch <name of migration batch> -Confirm:$false

2.  Necesita tener la característica de migración **PAW** habilitada para su inquilino de Office 365. Puede comprobar esto ejecutando el siguiente comando en Exchange Online PowerShell:
    
        Get-MigrationConfig
    
    Si el resultado en **Características** tiene **PAW**, entonces la característica está habilitada y puede seguir con el paso siguiente.
    
    Si PAW no está habilitada todavía para su inquilino, puede ser porque tiene algunos lotes de migración existentes, lotes de carpeta pública o lotes de usuario. Estos lotes pueden estar en cualquier estado, incluido Completado. Si este es el caso, complete y quite cualquier lote de migración hasta que no se devuelva ningún registro cuando ejecute `Get-MigrationBatch`. Una vez que se quiten todos los lotes existentes, PAW debe habilitarse automáticamente. Tenga en cuenta que el cambio puede que no se refleje en `Get-MigrationConfig` inmediatamente, pero no pasa nada. En el caso de las migraciones de usuario, puede seguir creando lotes nuevos una vez que este paso esté completado.

3.  Asegúrese de que no haya ninguna carpeta pública ni buzones de carpetas públicas existentes en Exchange Online. Si detecta carpetas públicas en Exchange Online después de seguir los pasos anteriores, es importante determinar por qué están allí y qué persona de la organización ha iniciado una jerarquía de carpetas públicas antes de empezar a quitar las carpetas públicas y los buzones de carpetas públicas.
    
    1.  En Office 365 o Exchange Online PowerShell, ejecute el siguiente comando para ver si existe algún buzón de carpetas públicas.
        
            Get-Mailbox -PublicFolder
    
    2.  Si el comando no devuelve ningún buzón de carpetas públicas, continúe con el Paso 3: Generación de los archivos .csv. Si el comando devuelve algún buzón de carpetas públicas, ejecute el siguiente comando para ver si hay alguna carpeta pública:
        
            Get-PublicFolder -Recurse
    
    3.  Si tiene alguna carpeta pública en Office 365 o Exchange Online, ejecute el siguiente comando de PowerShell para quitarlas (después de confirmar que no son necesarias). Asegúrese de que ha guardado la información que había en estas carpetas públicas antes de eliminarlas, porque toda la información se eliminará permanentemente cuando quite las carpetas públicas.
        
            Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
            Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
    
    4.  Una vez que se han quitado las carpetas públicas, ejecute los siguientes comandos para quitar todos los buzones de carpetas públicas:
        
            $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
            Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true 

## Paso 3: Generación de los archivos .csv

Use los scripts que se han descargado anteriormente para generar los archivos .csv que se usarán en la migración.

1.  Desde el Shell de administración de Exchange (local), ejecute el script `Export-ModernPublicFolderStatistics.ps1` para crear el nombre de carpeta para el archivo de asignación del tamaño de la carpeta. Debe tener permisos de administrador local para ejecutar este script. El archivo resultante contendrá tres columnas: **FolderName**, **FolderSize** y **DeletedItemSize**. Los valores de las columnas **FolderSize** y **DeletedItemSize** se mostrarán en bytes. Por ejemplo, **\\PublicFolder01,10240, 100** significa que la carpeta pública en la raíz de la jerarquía denominada PublicFolder01 es 10 240 bytes, o 10 240 MB, de tamaño, y hay 100 bytes de elementos recuperables en esta.
    
        .\Export-ModernPublicFolderStatistics.ps1 <Folder-to-size map path>
    
    **Ejemplo**:
    
        .\Export-ModernPublicFolderStatistics.ps1 stats.csv

2.  Ejecute el script `ModernPublicFolderToMailboxMapGenerator.ps1` para crear un archivo .csv que asigna carpetas públicas de origen a buzones de carpetas públicas en su destino de Exchange Online. Este archivo se usa para calcular el número correcto de buzones de carpetas públicas en Exchange Online.
    

    > [!NOTE]
    > El archivo generado por <CODE>ModernPublicFolderToMailboxMapGenerator.ps1</CODE> no contendrá el nombre de cada carpeta pública de la organización. Contendrá las referencias a las carpetas principales de los árboles de carpetas más grandes o los nombres de carpetas que a su vez es significativamente grandes. Puede pensar en este archivo como un archivo de "excepción" se utiliza para asegurarse de que determinados árboles de carpetas y carpetas más grandes se colocan en el correo de la carpeta pública específicacuadros. Es normal no ver cada una de las carpetas públicas en este archivo. También se migrará a las carpetas secundarias de cualquier carpeta que aparece en este archivo de asignación al mismo buzón de carpetas públicas como su carpeta principal (a menos que se mencione explícitamente en otra línea dentro del archivo de asignación que se dirige a un buzón de carpetas públicas distinto).

    
        .\ModernPublicFolderToMailboxMapGenerator.ps1 <Maximum mailbox size in bytes><Maximum mailbox recoverable item size in bytes><Folder-to-size map path><Folder-to-mailbox map path>
    
      - `Maximum mailbox size in bytes` es la máxima cantidad de datos que quiere migrar a cualquier único buzón de carpetas públicas en Exchange Online. El tamaño máximo de este campo es actualmente 50 GB, pero recomendamos que use un tamaño más pequeño, como el 50 % del tamaño máximo, para permitir un crecimiento futuro.
    
      - `Maximum mailbox recoverable items size in bytes` es la cuota de elementos recuperables de sus buzones de Exchange Online. En Exchange Online, actualmente el tamaño máximo de los buzones de carpetas públicas es 50 GB. Recomendamos que se establezca` RecoverableItemsQuota` en 15 GB o menos.
    
      - `Folder-to-size map path` es la ruta de acceso del archivo .csv que ha creado al ejecutar el script `Export-ModernPublicFolderStatistics.ps1`.
    
      - `Folder-to-mailbox map path` es la ruta de acceso del archivo .csv de carpeta a buzón de correo que está creando en este paso. Si especifica solo el nombre del archivo, el archivo se generará en el directorio actual de PowerShell en el equipo local.

**Ejemplo**:

    .\ModernPublicFolderToMailboxMapGenerator.ps1 -MailboxSize 25GB -MailboxRecoverableItemSize 1GB -ImportFile .\stats.csv -ExportFile map.csv


> [!NOTE]
> No admitimos migrar carpetas públicas a Exchange Online Si el número de buzones únicos de carpetas públicas en Exchange Online es mayor que 100.



## Paso 4: Creación de los buzones de carpetas públicas en Exchange Online

Después, en Exchange Online PowerShell, cree los buzones de carpetas públicas de destino que contendrán sus carpetas públicas migradas.

1.  Ejecute el siguiente script para crear los buzones de carpetas públicas de destino. El script creará un buzón de destino para cada buzón en el archivo .csv que ha generado anteriormente en el *Paso 3: Generación de los archivos .csv*, al ejecutar el script `ModernPublicFoldertoMailboxMapGenerator.ps1`.
    
        $mappings = Import-Csv <Folder-to-mailbox map path>
        $primaryMailboxName = ($mappings | Where-Object FolderPath -eq "\" ).TargetMailbox
        New-Mailbox -HoldForMigration:$true -PublicFolder -IsExcludedFromServingHierarchy:$false $primaryMailboxName 
        ($mappings | Where-Object TargetMailbox -ne $primaryMailboxName).TargetMailbox | Sort-Object -unique | ForEach-Object { New-Mailbox -PublicFolder -IsExcludedFromServingHierarchy:$false $_ }
    
      - `Folder-to-mailbox map path` es la ruta de acceso del archivo .csv de carpeta a buzón de correo que se ha generado mediante el script `ModernPublicFoldertoMailboxMapGenerator.ps1` en el *Paso 3: Generación de los archivos .csv*.

## Paso 5: Inicio de la solicitud de migración

Ahora, necesitará ejecutarse un número de comandos en su entorno local de Exchange 2013 y en Exchange Online.

1.  Desde cualquiera de sus servidores de Exchange 2013 que hospedan buzones de carpetas públicas, ejecute el siguiente script. Este script sincronizará las carpetas públicas habilitadas para correo de su Active Directory local a Exchange Online. Asegúrese de que ha descargado la última versión de este script y que está ejecutándolo desde el Shell de administración de Exchange.
    
        .\Sync-ModernMailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
      - `Credential` es su nombre de usuario administrativo de Exchange Online y su contraseña.
    
      - `CsvSummaryFile` es la ruta de acceso del archivo donde quiere que se encuentre su archivo de registro de operaciones de sincronización y errores. El registro tendrá el formato .csv.

2.  En el servidor de Exchange 2013, encuentre el servidor de punto de conexión del proxy MRS y anótelo. Necesitará esta información para ejecutar la solicitud de migración. Guarde esta información para el paso 3b siguiente.

3.  En Exchange Online PowerShell, ejecute los siguientes comandos para pasar la información de las credenciales y la información de MRS del paso anterior a las variables cmdlet que se usarán en la solicitud de migración.
    
    1.  Pase la credencial de un usuario que tenga permisos de administrador en el entorno local de Exchange 2013 a la variable `$Source_Credential`. La solicitud de migración que ejecuta en Exchange Online usará esta credencial para obtener acceso a sus servidores de Exchange 2013 locales para copiar el contenido de la carpeta pública en Exchange Online.
        
            $Source_Credential = Get-Credential <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  Tome la información del servidor proxy MRS del entorno de Exchange 2013 que ha encontrado en el paso 2 anterior y pásela a la variable:
        
            $Source_RemoteServer = "<paste the value here>"

4.  En Exchange Online PowerShell, ejecute los comandos siguientes para crear el punto de conexión de migración de las carpetas públicas y la solicitud de migración de las carpetas públicas:
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolder -Name PublicFolderEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
         
        [byte[]]$bytes = Get-Content -Encoding Byte <folder_mapping.csv>
        
        New-MigrationBatch -Name PublicFolderMigration -CSVData $bytes -SourceEndpoint $PfEndpoint.Identity -NotificationEmails <email addresses for migration notifications>
    

    > [!NOTE]
    > Separe las diferentes direcciones de correo electrónico con comas.

    
    Donde `folder_mapping.csv` es el archivo de mapa que se generó en *paso 3: crear los archivos .csv*. Asegúrese de proporcionar la ruta de acceso completa al archivo. Si se ha movido el archivo de asignación por algún motivo, asegúrese de utilizar la nueva ubicación.

5.  Por último, inicie la migración con el siguiente comando en Exchange Online PowerShell:
    
        Start-MigrationBatch PublicFolderMigration

Aunque las migraciones por lotes deben crearse con el cmdlet New-MigrationBatch en Exchange Online PowerShell, el progreso y la finalización de la migración se pueden ver y administrar en el EAC o ejecutando el cmdlet Get-MigrationBatch. El cmdlet New-MigrationBatch inicia una solicitud de migración de buzones para cada buzón de carpetas públicas, y puede ver el estado de estas solicitudes usando la página migración de buzones.

Para ir a la página de migración de buzones:

1.  Inicie sesión en Exchange Online y abra el EAC.

2.  Vaya a **Destinatarios** y, después, seleccione **Migración**.

3.  Seleccione la solicitud de migración que acaba de crear y, después, en el panel **Detalles**, seleccione **Ver detalles**.

Antes de pasar al *Paso 6: Bloquear las carpetas públicas en el servidor de Exchange 2013*, compruebe que todos los datos se han copiado y que no hay errores en la migración. Una vez que haya confirmado que el lote se ha movido al estado de **Sincronizado**, ejecute los comandos que se mencionan en el *Paso 2: Preparación para la migración*, en el último paso de **Pasos de requisitos previos en el entorno local del servidor de Exchange 2013**, para tomar una instantánea de las carpetas públicas locales. Una vez que se hayan ejecutado estos comandos, puede seguir con el paso siguiente. Tenga en cuenta que estos comandos pueden tardar un poco en completarse dependiendo del número de carpetas que tenga.

## Paso 6: Bloquear las carpetas públicas en el entorno de Exchange 2013 para la migración final (se requiere tiempo de inactividad de las carpetas públicas)

Hasta este punto del proceso de migración, los usuarios han podido obtener acceso a las carpetas públicas locales. En los siguientes pasos, los usuarios cerrarán ahora la sesión de las carpetas públicas de Exchange 2013 y, después, bloquearán las carpetas mientras el proceso de migración completa su sincronización final. Los usuarios no podrán tener acceso a las carpetas públicas durante este tiempo, y cualquier mensaje que se envíe a estas carpetas públicas habilitadas para correo se pondrá en cola y no se entregará hasta que se complete la migración de las carpetas públicas.

Antes de ejecutar el comando `PublicFolderMailboxesLockedForNewConnections` como se describe a continuación, asegúrese de que todos los trabajos están en el estado **sincronizadas**. Para ello, ejecute el comando `Get-PublicFolderMailboxMigrationRequest` . Siga con este paso sólo después de haber comprobado que todos los trabajos están en el estado **sincronizadas**.

En su entorno local, ejecute el siguiente comando para bloquear las carpetas públicas de Exchange 2013 para la finalización del proceso.

    Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true


> [!NOTE]
> Si no puede acceder al parámetro <CODE>-PublicFolderMailboxesLockedForNewConnections</CODE> , es posible que Active Directory no estaba preparado durante la actualización CU, como se aconsejó anteriormente en <EM>lo que necesita saber antes de empezar?</EM> Consulte <A href="prepare-active-directory-and-domains-exchange-2013-help.md">Preparar Active Directory y los dominios</A> para obtener más información.<BR>Además, tenga en cuenta que cualquier usuario que necesite tener acceso a las carpetas públicas debe migrarse primero, <STRONG>antes</STRONG> de que migre las propias carpetas públicas.



Si su organización tiene buzones de carpetas públicas en varios servidores de Exchange 2013, necesitará esperar hasta que la replicación de AD se complete. Una vez haya finalizado, puede confirmar que todos los buzones de carpetas públicas hayan seleccionado la marca `PublicFolderMailboxesLockedForNewConnections`, y que cualquier cambio pendiente que los usuarios hayan realizado recientemente en sus carpetas públicas se haya convergido en la organización. Todo esto puede prolongarse varias horas.

## Paso 7: Finalización de la migración de carpetas públicas (se requiere tiempo de inactividad de las carpetas públicas)

Para poder completar la migración de carpetas públicas, debe confirmar que hay se mueve ningún otro buzón de carpetas públicas o carpetas públicas mueven continua en su entorno de Exchange local. Para ello, use los cmdlets `Get-MoveRequest` y `Get-PublicFolderMoveRequest` para enumerar cualquier carpeta pública existente se mueve. Si hay cualquier movimiento en curso o en el estado **completado**, quítelas.

A continuación, para completar la migración de carpetas públicas, ejecute el siguiente comando de PowerShell en línea de Exchange:

    Complete-MigrationBatch PublicFolderMigration

Cuando ejecuta este comando, Exchange realizará una sincronización final entre su organización de Exchange local y Exchange Online. Durante este período, el estado del lote de migración cambiará de **sincronizadas** para **finalización** y por último a **completado**. Si la sincronización se realiza correctamente, las carpetas públicas de Exchange Online se desbloqueará.

Es habitual que el lote de migración tomar unas pocas horas antes de su estado cambia de **sincronizadas** para **finalización**, momento en el que comenzará la sincronización.

## Paso 8: Probar y desbloquear las carpetas públicas de Exchange Online

Una vez que la migración de carpetas públicas se haya completado, realice los pasos siguientes para probar el éxito de la migración y para comprobar oficialmente su finalización. Estas tareas finales le permiten probar la jerarquía de carpetas públicas que se han migrado antes de que cambie permanentemente su organización a las carpetas públicas de Exchange Online.

1.  En Exchange Online PowerShell, asigne algunos buzones de usuario de prueba para usar uno de los buzones de carpetas públicas recientemente migrados como su buzón de carpeta pública predeterminado:
    
        Set-Mailbox -Identity <test user> -DefaultPublicFolderMailbox <public folder mailbox identity>
    
    Asegúrese de que los usuarios de prueba tienen permisos necesarios para crear carpetas públicas.

2.  Inicie sesión en Outlook con el usuario de prueba designado en el paso anterior y, a continuación, tome las siguientes pruebas de carpetas públicas. Tenga en cuenta que tardará 15 a 30 minutos para que surtan efecto los cambios. Una vez que Outlook es consciente de los cambios, puede solicitarle que reinicie un par de veces.
    
    1.  Ver la jerarquía
    
    2.  Compruebe los permisos.
    
    3.  Cree algunas carpetas públicas y, después, elimínelas.
    
    4.  Publique contenido en una carpeta pública y elimine contenido de ella.
    
    Si surge algún problema y determinar que no está preparado para cambiar las carpetas públicas de su organización completamente a Exchange Online, consulte [Revertir una migración de carpetas públicas de Exchange 2013 a Exchange Online](roll-back-a-public-folder-migration-from-exchange-2013-to-exchange-online-exchange-2013-help.md).

3.  Ejecute el siguiente comando en Exchange Online PowerShell para desbloquear las carpetas públicas de Exchange en línea. Después de ejecutar el comando, puede tardar aproximadamente 15 a 30 minutos para que los cambios surtan efecto. Después de que Outlook esté consciente de los cambios, podrían pedir los usuarios reiniciar el programa varias veces.
    
        Set-OrganizationConfig -RemotePublicFolderMailboxes $Null -PublicFoldersEnabled Local

## Paso 9: Finalizar la migración local

Para habilitar los mensajes de correo electrónico a las carpetas públicas habilitadas para correo local, siga estos pasos:

1.  En su entorno local, ejecute el script siguiente para asegurarse de que todos los correos electrónicos de las carpetas públicas habilitadas para correo se han enrutado correctamente a Exchange Online. El script marcará las carpetas públicas habilitadas para correo con `ExternalEmailAddress` que las señala para sus equivalentes de Exchange Online:
    
        .\SetMailPublicFolderExternalAddress.ps1 -ExecutionSummaryFile:mepf_summary.csv

2.  Si sus pruebas se han realizado correctamente, en su entorno local, ejecute el siguiente comando para indicar que la migración de carpetas públicas ha finalizado:
    
        Set-OrganizationConfig -PublicFolderMailboxesMigrationComplete:$true -PublicFoldersEnabled Remote

## ¿Cómo saber si el proceso se ha completado correctamente?

En el Paso 2: Preparación para la migración, ha tomado instantáneas de la estructura de las carpetas públicas locales, las estadísticas y los permisos. Los siguientes pasos le ayudarán a comprobar que su migración de carpetas públicas se ha realizado correctamente tomando las mismas instantáneas en Exchange Online después de la migración. Compare los datos de ambos archivos para comprobar que el proceso haya sido correcto.

1.  En Exchange Online PowerShell, ejecute el siguiente comando para tomar una instantánea de la nueva estructura de carpetas:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Export-CliXML Cloud_PFStructure.xml

2.  En Exchange Online PowerShell, ejecute el siguiente comando para tomar una instantánea de las estadísticas de carpetas públicas, incluido el recuento de elementos, el tamaño y el propietario:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderStatistics | Export-CliXML Cloud_PFStatistics.xml

3.  En Exchange Online PowerShell, ejecute el siguiente comando para tomar una instantánea de los permisos:
    
        Get-PublicFolder -Recurse -ResultSize Unlimited | Get-PublicFolderClientPermission | Select-Object Identity,User, AccessRights | Export-CliXML Cloud_PFPerms.xml

4.  En Exchange Online PowerShell, ejecute el siguiente comando para tomar una instantánea de las carpetas públicas habilitadas para correo:
    
        Get-MailPublicFolder -ResultSize Unlimited | Export-CliXML Cloud_MEPF.xml

## Problemas conocidos

Los siguientes son problemas comunes de migración de carpetas públicas que puede experimentar en su organización.

  - No admitimos migrar carpetas públicas a Exchange Online Si el número de buzones únicos de carpetas públicas en Exchange Online es mayor que 100.

  - Los permisos de la carpeta pública raíz y la carpeta EFORMS REGISTRY no se migrarán a Exchange Online, y tendrá que aplicarlos manualmente en Exchange Online. Para hacerlo, ejecute el siguiente comando en Exchange Online PowerShell. Ejecute el comando una vez para cada entrada de permiso que esté presente a nivel local pero falte en Exchange Online:
    
        Add-PublicFolderClientPermission "\" -User <user> -AccessRights <access rights>
        Add-PublicFolderClientPermission "\NON_IPM_SUBTREE\EFORMS REGISTRY" -User <user> -AccessRights <access rights>

  - Algunas migraciones de carpeta pública se producirá un error si algunos buzones de carpetas públicas no están atendiendo a la jerarquía de carpetas públicas. Esto significa que el parámetro `IsExcludedFromServingHierarchy` en uno o más buzones se establece en `$true`. Para evitar este problema, establezca todos los buzones en Exchange Online para servir a la jerarquía.

  - Los permisos **Enviar como** y **Enviar en nombre de** no se migran a Exchange Online. Si esto sucede con su migración, use los siguientes comandos en su entorno local para tener en cuenta quién tiene estos permisos.
    
    Para ver qué carpetas públicas tienen permisos Enviar como a nivel local:
    
        Get-MailPublicFolder | Get-ADPermission | ?{$_.ExtendedRights -like "*Send-As*"}
    
    Para ver qué carpetas públicas tienen permisos Enviar en nombre de a nivel local:
    
        Get-MailPublicFolder | ?{$_.GrantSendOnBehalfTo -ne "$null"} | ft name,GrantSendOnBehalfTo
    
    Para agregar el permiso Enviar como a una carpeta pública habilitada para correo en Exchange Online, escriba en Exchange Online PowerShell:
    
        Add-RecipientPermission -Identity <mail-enabled public folder primary SMTP address> -Trustee <name of user to be assigned permission> -AccessRights SendAs
    
    **Ejemplo**:
    
        Add-RecipientPermission -Identity send1 -Trustee Exo1 -AccessRights SendAs
    
    Para agregar el permiso Enviar en nombre de a una carpeta pública habilitada para correo en Exchange Online, escriba en Exchange Online PowerShell:
    
        Set-MailPublicFolder -Identity <name of public folder> -GrantSendOnBehalfTo <user or comma-separated list of users>
    
    **Ejemplo**:
    
        Set-MailPublicFolder send2 -GrantSendOnBehalfTo exo1,exo2

  - Si la carpeta "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" contiene más de 10 000 carpetas, es posible que la migración sea errónea. Por lo tanto, compruebe si la carpeta "\\NON\_IPM\_SUBTREE\\DUMPSTER\_ROOT" contiene más de 10 000 carpetas (elementos secundarios inmediatos). Puede utilizar el siguiente comando para determinar el número de carpetas públicas en esta ubicación:
    
        (Get-PublicFolder -GetChildren "\NON_IPM_SUBTREE\DUMPSTER_ROOT").Count 
    
    Exchange Online no admite más de 10 000 subcarpetas. Por este motivo, se produce un error en la migración de más de 10 000 carpetas. Estamos desarrollando un script para desbloquear dichas configuraciones. Mientras tanto, le sugerimos que posponga la migración de las carpetas públicas.

  - Los trabajos de migración no progresan o se detienen. Esto puede ocurrir si hay demasiados trabajos ejecutándose en paralelo, lo que causa que los trabajos fallen con errores intermitentes. Puede reducir el número de trabajos simultáneos modificando `MaxConcurrentMigrations` y `MaxConcurrentIncrementalSyncs` a un número menor. Para establecer estos valores, utilice el siguiente ejemplo:
    
        Set-MigrationEndpoint <PublicFolderEndpoint> -MaxConcurrentMigrations 30 -MaxConcurrentIncrementalSyncs 20  -SkipVerification 

  - Los trabajos de migración provocan el error "Error: Contenedor de la carpeta Contenedor". Si ve este error, detenga el lote y vuelva a iniciarlo para solucionarlo.

  - Trabajos de migración fallan y generan una "solicitud fue puesto en cuarentena debido al siguiente error: la clave proporcionada no estaba presente en el diccionario" mensaje de error. Esto sucede cuando un elemento dañado se encuentra en una carpeta que no se pueden copiar trabajos de migración. Para evitar este problema:
    
    1.  Detenga el lote de migración.
    
    2.  Identifique la carpeta que contiene el elemento incorrecto. El informe de migración debe incluir referencias a la carpeta que se estaba copiando cuando ocurrió el error.
    
    3.  En su entorno local, mueva la carpeta afectada al buzón de la carpeta pública principal. Puede utilizar el cmdlet `New-PublicFolderMoveRequest` para mover carpetas.
    
    4.  Espere a que el cambio de carpeta a completar. Una vez completada, quite la solicitud de traslado. A continuación, reinicie el proceso de migración.

## Quitar buzones de carpetas públicas de su entorno local de Exchange

Después de que la migración haya finalizado y que haya comprobado que sus carpetas públicas en Exchange Online funcionan como se esperaba y contienen todos los datos esperados, puede quitar sus buzones de carpetas públicas locales.

Tenga en cuenta que este paso es irreversible, porque una vez que se eliminen buzones de carpetas públicas, no se puede recuperar. Por lo tanto, recomendamos encarecidamente que, además de comprobar el éxito de la migración, también supervisar las carpetas públicas de Exchange Online durante unas semanas, antes de quitar los buzones de carpetas públicas local.

