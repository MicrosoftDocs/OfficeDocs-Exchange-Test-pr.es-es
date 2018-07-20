---
title: 'Utilizar lotes de migración para migrar carpetas públicas de Exchange 2010 a Office 365 grupos: Exchange 2013 Help'
TOCTitle: Utilizar lotes de migración para migrar carpetas públicas de Exchange 2010 a Office 365 grupos
ms:assetid: d018558d-3075-4dd3-9ff7-91ce66b8d5fb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt843875(v=EXCHG.150)
ms:contentKeyID: 74468744
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Utilizar lotes de migración para migrar carpetas públicas de Exchange 2010 a Office 365 grupos

 

_**Se aplica a:** Exchange Server 2010, Exchange Server 2013_

_**Última modificación del tema:** 2018-04-30_

**Resumen:**  cómo mover las carpetas públicas de Exchange 2010 a Office 365 grupos.

Mediante un proceso conocido como *migración de lote*, puede mover algunas o todas las carpetas públicas de Exchange 2010 a los grupos de Office 365. Grupos es una nueva oferta de Microsoft que ofrece ciertas ventajas sobre las carpetas públicas de colaboración. Consulte [Migrar las carpetas públicas a grupos de Office 365](migrate-your-public-folders-to-office-365-groups-exchange-2013-help.md) para obtener una introducción de las diferencias entre carpetas públicas y grupos y razones por la organización podrá o no podrá acogerse a los grupos de conmutación.

Este artículo contiene los procedimientos paso a paso para llevar a cabo la migración real del lote de las carpetas públicas de Exchange 2010.

## ¿Qué necesita saber antes de comenzar?

Asegúrese de que se cumplen todas las condiciones siguientes antes de comenzar a preparar la migración.

  - El servidor de Exchange 2010 debe ejecutar **RU8 de Exchange 2010 Service Pack 3** o posterior.

  - En Exchange Online, debe ser miembro del grupo de roles de administración de la organización. Este grupo de roles es diferente de los permisos que se le asignan cuando se suscribe a Office 365 o Exchange Online. Para obtener más información sobre cómo habilitar el grupo de roles de administración de la organización, vea [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - En Exchange 2010, debe ser miembro de los grupos de funciones de administración de organización o servidor administración RBAC. Para obtener información detallada, vea [Agregar miembros a un grupo de funciones](https://go.microsoft.com/fwlink/?linkid=299212).

  - Antes de migrar las carpetas públicas a grupos de Office 365, se recomienda mover los buzones de usuario a Office365 para aquellos usuarios que necesitan acceso a Office 365 grupos después de la migración.

  - Outlook Anywhere debe habilitarse en el servidor de Exchange 2010 que aloja las bases de datos de carpetas públicas. Para obtener más información acerca de cómo habilitar Outlook Anywhere en los servidores de Exchange 2010, consulte [Habilitar Outlook en cualquier lugar](https://go.microsoft.com/fwlink/p/?linkid=187249).

  - No puede utilizar el centro de administración de Exchange (EAF) o la Consola de administración de Exchange (EMC) para realizar este procedimiento. En los servidores de Exchange 2010, debe usar el Shell de administración de Exchange. Para Exchange Online, necesitará usar PowerShell en línea de Exchange. Para obtener más información, vea [conectarse a Exchange Online mediante PowerShell remoto](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx).

  - Sólo se pueden migrar las carpetas públicas de tipo calendario y el correo a Office 365 grupos en este momento; no se admite la migración de otros tipos de carpetas públicas. Además, los grupos de destino en Office 365 deben crearse antes de la migración.

  - El proceso de migración por lotes sólo copia elementos de calendario y mensajes de carpetas públicas para la migración a Office 365 grupos. No copia otras entidades de las carpetas públicas como las directivas, reglas y permisos.

  - Office 365 grupos viene con un buzón de 50GB. Asegúrese de que la suma de datos de carpetas públicas que está migrando totales de menos de 50GB. Además, deje espacio de almacenamiento para contenido adicional agregar los usuarios en el futuro, después de la migración. Le recomendamos que migrar carpetas públicas no superiores a 25GB en total.

  - No es una migración de "todo o nada". Puede elegir y seleccionar las carpetas públicas específicas para migrar y se migrarán únicamente las carpetas públicas. Si la carpeta pública que se está migrando contiene subcarpetas, las subcarpetas no se incluirá automáticamente en la migración. Si necesita migrar de ellos, debe incluirlos explícitamente.

  - Las carpetas públicas no se verán afectadas de ninguna manera por esta migración. Sin embargo, una vez utilice nuestra secuencia de comandos de bloqueo para que las carpetas públicas migradas de sólo lectura, que los usuarios se verán obligados a utilizar Office 365 grupos en lugar de carpetas públicas.

  - Antes de empezar, se recomienda que lea este artículo en su totalidad, como el tiempo de inactividad es necesario para algunos pasos.

## Paso 1: Obtener las secuencias de comandos

La migración por lotes a Office 365 grupos requiere la ejecución de una serie de secuencias de comandos en diferentes puntos de la migración, tal como se describe en este artículo. Descargar las secuencias de comandos y apoyo a sus archivos [desde esta ubicación](https://www.microsoft.com/en-us/download/details.aspx?id=55985). Después de descargaron todos los archivos y secuencias de comandos, guardarlos en la misma ubicación, por ejemplo, `c:\PFtoGroups\Scripts`.

Antes de continuar, compruebe que ha descargado y guardado todos los scripts y los archivos siguientes:


> [!NOTE]
> Asegúrese de guardar todos los scripts y archivos en la misma ubicación.



  - **AddMembersToGroups.ps1**. esta secuencia de comandos agrega miembros y propietarios a Office 365 grupos basan en las entradas de permisos en las carpetas públicas de origen.

  - **AddMembersToGroups.strings.psd1**. este archivo de ayuda es utilizado por la secuencia de comandos `AddMembersToGroups.ps1`.

  - **LockAndSavePublicFolderProperties.ps1**. esta secuencia de comandos hace que las carpetas públicas de sólo lectura para evitar modificaciones y transfiere las propiedades relacionadas con el correo de carpetas públicas (siempre que las carpetas públicas están habilitados para correo) a los grupos de destino, que le reconducirá correos electrónicos de las carpetas públicas a los grupos de destino. Esta secuencia de comandos también copia las entradas de permisos y las propiedades de correo antes de modificarlas.

  - **LockAndSavePublicFolderProperties.strings.psd1:**  este archivo de ayuda es utilizado por la secuencia de comandos `LockAndSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.ps1**. esta secuencia de comandos restaura los derechos de acceso y las propiedades de correo de las carpetas públicas mediante archivos de copia de seguridad creados por `LockandSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.strings.psd1**. este archivo de ayuda es utilizado por la secuencia de comandos `UnlockAndRestorePublicFolderProperties.ps1`.

  - **WriteLog.ps1**. esta secuencia de comandos permite la anteriores tres secuencias de comandos escribir los registros.

  - **RetryScriptBlock.ps1**. esta secuencia de comandos permite que las secuencias de comandos `AddMembersToGroups`, `LockAndSavePublicFolderProperties`y `UnlockAndRestorePublicFolderProperties` a intentar determinadas acciones en caso de errores transitorios.

Para obtener más información acerca de `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1`y `UnlockAndRestorePublicFolderProperties.ps1`y las tareas que se ejecutan en su entorno, consulte las secuencias de comandos de migración más adelante en este artículo.

## Paso 2: Preparación para la migración

Los pasos siguientes son necesarios para preparar su organización para la migración:

1.  Compilar una lista de las carpetas públicas (tipos de correo y calendario) que va a migrar a Office 365 grupos.

2.  Tiene una lista de los grupos de destino correspondientes para cada carpeta pública que se está migrando. Puede crear un grupo nuevo en Office 365 para cada carpeta pública o utilice un grupo existente. Si va a crear un grupo nuevo, consulte [Obtenga información acerca de los grupos de Office 365](https://go.microsoft.com/fwlink/p/?linkid=858521) para conocer los parámetros que debe tener un grupo. Si una carpeta pública que se va a migrar tiene el permiso predeterminado al **autor** o superior, debe crear el grupo correspondiente en Office 365 con la configuración de privacidad **públicas**. Sin embargo, para que los usuarios vean el grupo público bajo el nodo **grupos** en Outlook, aún tendrán que unirse al grupo.

3.  Cambiar el nombre de las carpetas públicas que contienen una barra diagonal inversa (\\) en su nombre. De lo contrario, pueden que las carpetas públicas no se migran correctamente.

4.  Debe tener la función de migración **de la pata** habilitado para los clientes de Office 365. Para comprobar esto, ejecute el siguiente comando de PowerShell en línea de Exchange:
    
        Get-MigrationConfig
    
    Si la salida en **características de** listas **de la pata**, entonces la característica está habilitada y se puede seguir *paso 3: crear el archivo .csv*.
    
    Si PATA todavía no ha habilitado para el arrendatario, podría ser debido a que algunas secciones de migración existentes, lotes lotes de carpetas públicas o de usuario. Estos lotes podrían estar en cualquier estado, incluyendo completado. Si éste es el caso, rellene y quitar los lotes de migración existente hasta que no se devuelven registros al ejecutar `Get-MigrationBatch`. Una vez eliminados todos los lotes existentes, PATA debe habilita automáticamente. Tenga en cuenta que el cambio puede no reflejar en `Get-MigrationConfig` inmediatamente, que es correcto. Una vez completado este paso, puede continuar la creación de nuevos lotes de migraciones de usuarios.

## Paso 3: Crear el archivo .csv

Crear un archivo .csv, que proporcionará la entrada de una de las secuencias de comandos de migración.

El archivo .csv debe contener las siguientes columnas:

  - **FolderPath**. Ruta de acceso de la carpeta pública que se migrarán.

  - **TargetGroupMailbox**. Dirección SMTP del grupo de destino en Office 365. Puede ejecutar el comando siguiente para ver la dirección SMTP principal.
    
        Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress

Un .csv de ejemplo:

    "FolderPath","TargetGroupMailbox"
    "\Sales","sales@contoso.onmicrosoft.com"
    "\Sales\EMEA","emeasales@contoso.onmicrosoft.com"

Tenga en cuenta que una carpeta mail y una carpeta de calendario se pueden combinar en un solo grupo en Office 365. Sin embargo, no se admite cualquier otro escenario de varias carpetas públicas al combinar en un grupo dentro de un lote de migración. Si necesita asignar varias carpetas públicas para el mismo grupo de Office 365, puede hacerlo mediante la ejecución de lotes diferentes de migración, que se deben ejecutar consecutivamente, uno tras otro. Puede tener hasta 500 entradas en cada lote de migración.

Una carpeta pública debe migrarse a un único grupo de lote de una migración.

## Paso 4: Iniciar la solicitud de migración

En este paso, recopilar información del entorno de Exchange y, a continuación, utilizar esa información en Exchange Online PowerShell para crear un lote de migración. A continuación, iniciar la migración.

1.  En el servidor de Exchange 2010, ejecute los siguientes comandos para recopilar la información necesaria para crear el lote de migración:
    
    1.  Buscar el **atributo LegacyExchangeDN** de la cuenta de un usuario que es miembro de la función de administrador de carpeta pública, escriba el comando siguiente. Tenga en cuenta que esto es el mismo usuario cuyas credenciales tendrá más adelante, en el paso 3 de este procedimiento.
        
            Get-Mailbox <PublicFolder_Administrator_Account> | Select-Object LegacyExchangeDN
    
    2.  Buscar el valor LegacyExchangeDN de cualquier servidor de buzones con una base de datos de carpetas públicas escribiendo el comando siguiente:
        
            Get-ExchangeServer <public folder server> | Select-Object -Expand ExchangeLegacyDN
    
    3.  Buscar el nombre de dominio completo (FQDN) del host de Outlook en cualquier lugar. Este es el nombre de Host externo. Si tiene varias instancias de Outlook en cualquier lugar, recomendamos que seleccione la instancia que es uno más cercana al extremo de la migración o el más cercano a las réplicas de carpetas públicas en la organización de Exchange Server 2010. El comando siguiente encontrará todas las instancias de Outlook en cualquier lugar:
        
            Get-OutlookAnywhere | Format-Table Identity, ExternalHostName

2.  En Exchange Online PowerShell, utilice la información que devolvió anteriormente en el paso 1 para ejecutar los siguientes comandos. Las variables de estos comandos serán los valores del paso 1.
    
    1.  Pasar las credenciales de un usuario con permisos de administrador en el entorno de Exchange 2010 en la variable `$Source_Credential`. Cuando finalmente ejecuta la solicitud de migración en Exchange Online, utilizará esta credencial para tener acceso a los servidores de Exchange 2010 mediante Outlook en cualquier lugar con el fin de copiar el contenido a través de.
        
            $Source_Credential = Get-Credential
            <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  Utilice la ExchangeLegacyDN del usuario de migración en el servidor de Exchange heredado que encontró anteriormente en el paso 1a y pasar ese valor a la variable `$Source_RemoteMailboxLegacyDN`.
        
            $Source_RemoteMailboxLegacyDN = "<LegacyExchangeDN from step 1a>"
    
    3.  Utilice la ExchangeLegacyDN del servidor de carpetas públicas, que se encuentra anteriormente en el paso 1b anterior y pasar ese valor a la variable `$Source_RemotePublicFolderServerLegacyDN`.
        
            $Source_RemotePublicFolderServerLegacyDN = "<LegacyExchangeDN from step 1b>"
    
    4.  Utilice el externo Host nombre de Outlook en cualquier lugar que se ha devuelto en el paso 1c anterior y pasar ese valor a la variable `$Source_OutlookAnywhereExternalHostName`.
        
            $Source_OutlookAnywhereExternalHostName = "<ExternalHostName from step 1c>"

3.  En Exchange Online PowerShell, ejecute el comando siguiente para crear un extremo de la migración:
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RPCProxyServer $Source_OutlookAnywhereExternalHostName -Credentials $Source_Credential -SourceMailboxLegacyDN $Source_RemoteMailboxLegacyDN -PublicFolderDatabaseServerLegacyDN $Source_RemotePublicFolderServerLegacyDN -Authentication Basic

4.  Ejecute el comando siguiente para crear un nuevo lote de migración de 365 grupo de carpeta a la oficina pública. En este comando:
    
      - **CSVData** es el archivo .csv que creó anteriormente en*paso 3: crear el archivo .csv*. Asegúrese de proporcionar la ruta de acceso completa de este archivo. Si el archivo se ha movido por algún motivo, asegúrese de comprobar y utilizar la nueva ubicación.
    
      - **NotificationEmails** es un parámetro opcional que puede utilizarse para establecer direcciones de correo electrónico que recibirán notificaciones sobre el estado y progreso de la migración.
    
      - **AutoStart** es un parámetro opcional que, cuando se utiliza, se inicia el proceso de migración en cuanto se crea.
    
      - **PublicFolderToUnifiedGroup** es el parámetro para indicar que se trata de una carpeta pública para el proceso de migración de grupos de Office 365.
    
    <!-- end list -->
    
        New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

5.  Ejecutando el comando siguiente en Exchange Online PowerShell para iniciar la migración. Tenga en cuenta que este paso sólo es necesario si no se utilizó el parámetro `-AutoStart` al crear el lote anteriormente en el paso 4.
    
        Start-MigrationBatch PublicFolderToGroupMigration

Mientras que las migraciones de lote deben crearse mediante el cmdlet de `New-MigrationBatch` en Exchange Online PowerShell, puede verse el progreso de la migración y administran en Centro de administración de Exchange. También puede ver el progreso de la migración mediante la ejecución de los cmdlets [Get-MigrationBatch](https://technet.microsoft.com/es-es/library/jj219164\(v=exchg.150\)) y [Get-MigrationUser](https://technet.microsoft.com/es-es/library/jj218702\(v=exchg.150\)) . El cmdlet `New-MigrationBatch` inicia un usuario de migración para cada buzón de correo de grupo de Office 365, y puede ver el estado de estas solicitudes usando la página migración de buzones.

Para ver la página migración de buzones:

1.  En Exchange Online, abra Centro de administración de Exchange.

2.  Desplazarse a **los destinatarios** y, a continuación, seleccione **migración**.

3.  Seleccione la solicitud de migración que acaba de crear y, después, en el panel **Detalles**, seleccione **Ver detalles**.

Cuando el estado del lote está **completado**, puede mover a *paso 5: agregar miembros a los grupos de Office 365 desde carpetas públicas*.

## Paso 5: Agregar a miembros a los grupos de Office 365 desde carpetas públicas

Puede agregar a miembros al grupo de destino en Office 365 manualmente según sea necesario. Sin embargo, si desea agregar a miembros al grupo basado en las entradas de permisos en carpetas públicas, debe hacerlo mediante la ejecución de la secuencia de comandos `AddMembersToGroups.ps1` en el servidor de Exchange 2010 como se muestra en el siguiente comando. Los buzones de usuario deben sincronizar con Exchange Online para poder añadir como miembros de un grupo de Office 365. Para saber qué permisos de carpetas públicas están pueden agregar como miembros de un grupo en Office 365, vea secuencias de comandos de migración más adelante en este artículo.

En el siguiente comando:

  - **MappingCsv** es el archivo .csv que creó anteriormente en *paso 3: crear el archivo .csv*. Asegúrese de proporcionar la ruta de acceso completa de este archivo. Si el archivo se ha movido por algún motivo, asegúrese de comprobar y utilizar la nueva ubicación.

  - **DirectorioDeCopiaDeSeguridad** es el directorio donde se almacenarán los archivos de registro de migración.

  - **ArePublicFoldersOnPremises** es un parámetro para indicar si las carpetas públicas están ubicados en instalaciones o en Exchange Online.

  - **Credencial** es el nombre de usuario de Exchange Online y la contraseña.

<!-- end list -->

    .\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

Una vez que los usuarios se han agregado a un grupo de Office 365, puedan comenzar a usar de él.

## Paso 6: Bloquear el público carpetas (carpetas públicas requerida tiempo de inactividad)

Cuando la mayoría de los datos de las carpetas públicas se ha migrado a Office 365 grupos, puede ejecutar el script `LockAndSavePublicFolderProperties.ps1` en el servidor de Exchange 2010 para que las carpetas públicas de sólo lectura. Este paso garantiza que ningún dato nuevo se agrega a las carpetas públicas antes de que finalice la migración.


> [!NOTE]
> Si hay carpetas públicas habilitadas para correo (MEPFs) entre el público en carpetas que se migran, este paso se copiar algunas propiedades del MEPFs, como las direcciones SMTP, en el grupo correspondiente en Office 365 y, a continuación, deshabilitar la carpeta pública para correo. Debido a la MEPFs de migración se pueden deshabilitar después de la ejecución de esta secuencia de comandos, empezará a ver los mensajes enviados a MEPFs en su lugar ser recibidos en los grupos correspondientes. Para obtener más detalles, consulte las secuencias de comandos de migración más adelante en este artículo.



En el siguiente comando:

  - **MappingCsv** es el archivo .csv que creó anteriormente en *paso 3: crear el archivo .csv*. Asegúrese de proporcionar la ruta de acceso completa de este archivo. Si el archivo se ha movido por algún motivo, asegúrese de comprobar y utilizar la nueva ubicación.

  - **DirectorioDeCopiaDeSeguridad** es el directorio donde se almacenarán los archivos de copia de seguridad en las entradas de permisos, las propiedades MEFP y archivos de registro de migración. Esta copia de seguridad será útil en caso de que necesite volver a las carpetas públicas.

  - **ArePublicFoldersOnPremises** es un parámetro para indicar si las carpetas públicas están ubicados en instalaciones o en Exchange Online.

  - **Credencial** es el nombre de usuario de Exchange Online y la contraseña.

<!-- end list -->

    .\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

## Paso 7: Finalizar la carpeta pública a la migración de grupos de Office 365

Una vez tomadas las carpetas públicas de sólo lectura, debe realizar la migración de nuevo. Esto es necesario para una copia incremental final de los datos. Antes de ejecutar la migración de nuevo, tendrá que quitar el lote existente, lo que puede hacer ejecutando el siguiente comando:

    Remove-MigrationBatch <name of migration batch>

A continuación, cree un nuevo lote con el mismo archivo .csv ejecutando el siguiente comando. En este comando:

  - **CsvData** es el archivo .csv que creó anteriormente en *paso 3: crear el archivo .csv*. Asegúrese de proporcionar la ruta de acceso completa de este archivo. Si el archivo se ha movido por algún motivo, asegúrese de comprobar y utilizar la nueva ubicación.

  - **NotificationEmails** es un parámetro opcional que puede utilizarse para establecer direcciones de correo electrónico que recibirán notificaciones sobre el estado y progreso de la migración.

  - **AutoStart** es un parámetro opcional que, cuando se utiliza, se inicia el proceso de migración en cuanto se crea.

<!-- end list -->

    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

Una vez creado el nuevo lote, iniciar la migración ejecutando el siguiente comando en Exchange Online PowerShell. Tenga en cuenta que este paso sólo es necesario si no se utilizó el parámetro `-AutoStart` en el comando anterior.

    Start-MigrationBatch PublicFolderToGroupMigration

Cuando haya terminado este paso (el estado del lote es **completado** ), compruebe que se ha copiado todos los datos a los grupos de Office 365. En ese momento, siempre y cuando esté satisfecho con la experiencia de los grupos, puede empezar a eliminar las carpetas públicas migradas desde su entorno de Exchange 2010.


> [!IMPORTANT]
> Aunque existen procedimientos que pueden utilizar para deshacer la migración y volver a las carpetas públicas, esto no es posible una vez que se han eliminado las carpetas públicas de origen. Vea cómo deshacer a las carpetas públicas desde Office 365 grupos? para obtener más información.



## Problemas conocidos

Los problemas conocidos siguientes pueden producir durante una típica carpetas públicas a la migración de grupos de Office 365.

  - La secuencia de comandos que la dirección de transferencias SMTP desde carpetas públicas habilitadas para correo en Office 365 grupo sólo agrega las direcciones como correo electrónico secundaria direcciones de Exchange en línea. Por este motivo, si tiene el programa de instalación de Exchange Online Protection (elevación de privilegios) o el flujo de correo centralizado en su entorno, tendrá problemas de envío de correo electrónico para el posterior a la migración de grupos (a las direcciones de correo electrónico secundaria).

  - Si el archivo .csv de asignación tiene una entrada con la ruta de la carpeta pública no válido, el lote de migración muestra como **completada** sin producir un error y no se copia ningún dato adicional.

## Secuencias de comandos de migración

Como referencia, esta sección ofrece descripciones detalladas en tres de las secuencias de comandos de migración y las tareas que se ejecutan en su entorno Exchange. Todas las secuencias de comandos y archivos auxiliares pueden ser [descargado desde esta ubicación](https://www.microsoft.com/en-us/download/details.aspx?id=55985).

## AddMembersToGroups.ps1

Esta secuencia de comandos leerá los permisos de las carpetas públicas que se está migrando y, a continuación, agregar miembros y propietarios a Office 365 grupos como sigue:

  - Los usuarios con las siguientes funciones de permiso se agregarán como miembros a un grupo de Office 365. **Roles de permisos:**  propietario, PublishingEditor, Editor, PublishingAuthor, autor

  - Además de los usuarios anteriores, con el siguiente acceso mínimo derechos se agregará también como miembros a un grupo de Office 365. **Derechos de acceso:**  ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems

  - Usuarios con acceso derecho "Propietario" se agregará como propietarios a un grupo y los usuarios con otros derechos de acceso elegibles se agregarán como miembros.

  - Grupos de seguridad no se puede agregar como miembros a los grupos de Office 365. Por lo tanto, se expandirá y, a continuación, se agregarán los usuarios individuales como miembros o propietarios a los grupos según los derechos de acceso del grupo de seguridad.

  - Cuando los usuarios de los grupos de seguridad que tienen los derechos de acceso sobre una carpeta pública tenga ellos mismos permisos explícitos en la misma carpeta pública, los permisos explícitos se dará preferencia. Por ejemplo, considere un caso en el que un grupo de seguridad llamado "SG1" tiene miembros Usuario1 y Usuario2. Las entradas de permisos para la carpeta pública "PF1" son los siguientes:
    
    SG1: Autor en PF1
    
    Usuario1: Propietario en PF1
    
    En este caso, usuario1 se agregará como un propietario para el grupo de Office 365.

  - El permiso predeterminado de una carpeta pública que se está migrando 'Author' o superior, la secuencia de comandos sugerirá la configuración de privacidad del grupo correspondiente estableciendo como 'Public'.

Esta secuencia de comandos se puede ejecutar incluso tras el bloqueo de carpetas públicas, con el parámetro de la `ArePublicFoldersLocked` establecido en` $true`. En este escenario, la secuencia de comandos leerá los permisos desde la copia de seguridad archivo creado durante el bloqueo.

## LockAndSavePublicFolderProperties.ps1

Esta secuencia de comandos crea las carpetas públicas que se está migrando de sólo lectura. Al migraron carpetas públicas habilitadas para correo, se primero se deshabilitó para correo y sus direcciones SMTP se agregarán a los grupos respectivos en Office 365. A continuación, se modificarán las entradas de permisos para que sean de sólo lectura. Una copia de seguridad de las propiedades de correo de las carpetas públicas habilitadas para correo, así como las entradas de permiso de todas las carpetas públicas, se copiará, antes de realizar cualquier modificación en ellos.

Si hay varias secciones de migración, debe utilizarse un directorio de copia de seguridad diferente con cada archivo .csv de asignación.

Las siguientes propiedades de correo se almacenará junto con los respectivas carpetas públicas habilitadas para correo y grupos de Office 365:

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - Lista de confianza de SendAs

Las propiedades de correo anteriores se almacenarán en un archivo .csv, que se puede utilizar en el nuevo proceso rollo (si desea volver a utilizar las carpetas públicas, consulte cómo deshacer a las carpetas públicas desde Office 365 grupos? para obtener más información). Una instantánea de las propiedades de las carpetas habilitadas para correo pública de también se almacenarán en un archivo denominado PfMailProperties.csv. Este archivo no es necesario para el proceso posterior de rollo, pero puede utilizarse para su referencia.

Las siguientes propiedades de correo se trasladarán al grupo de destino como parte del bloqueo:

  - PrimarySMTPAddress

  - EmailAddresses

  - Lista de confianza de SendAs

  - GrantSendOnBehalfTo

La secuencia de comandos garantiza que se agregará el PrimarySMTPAddress y EmailAddresses de migrar carpetas públicas habilitadas para correo como direcciones SMTP secundarias de los grupos correspondientes en Office 365. Además, SendAs y SendOnBehalfTo los permisos de los usuarios en carpetas públicas habilitadas para correo se dará permisos equivalentes en los grupos de destino correspondiente.

**Derechos de acceso permitidos**

Se permitirán los siguientes derechos de acceso para que los usuarios garantizar que las carpetas públicas son de sólo lectura para todos los usuarios.

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

Las entradas de permiso se modificará como sigue:

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Antes de bloqueo</th>
    <th>Después de bloqueo</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Ninguno</p></td>
    <td><p>Ninguno</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>Colaborador</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Reviewer</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Aughor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>Editor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Propietario</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  Derechos de acceso para los usuarios sin permisos de lectura permanecerán intactos y siguen bloqueadas de derechos de lectura.

3.  Para los usuarios con roles personalizados, si los derechos de acceso no son ReadItems, CreateSubfolders, FolderContact o FolderVisible, se eliminarán. En caso de que los usuarios no tienen los derechos de acceso de la lista de permitidos después de la filtración, derecho de acceso de estos usuarios se establecerá en 'None'.

Puede que haya una interrupción en el envío de correos electrónicos a carpetas públicas habilitadas para correo durante el tiempo entre cuando las carpetas están habilitados para correo y sus direcciones SMTP se agregan a los grupos de Office 365.

## UnlockAndRestorePublicFolderProperties.ps1

Esta secuencia de comandos reasignar permisos a las carpetas públicas, basados en la copia de seguridad tomado durante la carpeta pública bloquear. Esta secuencia de comandos se también correo Habilitar carpetas públicas que habían sido habilitados para correo, después de que se quitan las direcciones SMTP de las carpetas de sus respectivos grupos en Office 365. Podría haber downtime ligero durante este proceso.

## ¿Cómo deshacer a las carpetas públicas de los grupos de Office 365?

En caso de que cambia de opinión y desea volver a utilizar las carpetas públicas después utilizando grupos de Office 365, el comando que aparece a continuación restaurará su entorno al estado era antes de la migración. Un rollo nuevo puede realizarse mientras existan los archivos de copia de seguridad y que no ha eliminado la posteriores a la migración de carpetas públicas.

En el servidor de Exchange 2010, ejecute el siguiente comando. En este comando:

  - **DirectorioDeCopiaDeSeguridad** es el directorio donde se almacenarán los archivos de copia de seguridad en las entradas de permisos, las propiedades MEFP y archivos de registro de migración. Asegúrese de que utiliza la misma ubicación que especificó en *paso 6: bloqueo de las carpetas públicas a cut-over (carpeta pública requerida tiempo de inactividad)*.

  - **ArePublicFoldersOnPremises** es un parámetro para indicar si las carpetas públicas están ubicados en instalaciones o en Exchange Online.

  - **Credencial** es el nombre de usuario de Exchange Online y la contraseña.

<!-- end list -->

    .\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

Tenga en cuenta que todos los elementos agregados al grupo de Office 365, o las operaciones de edición realizadas en los grupos, no se copian a las carpetas públicas. Suponiendo que los nuevos datos se agregó, por tanto, habrá pérdida de datos, mientras que la carpeta pública era un grupo.

Tenga en cuenta también que no es posible restaurar un subconjunto de carpetas públicas, lo que significa que todas las carpetas públicas se migraron debe restaurarse.

No se eliminarán los grupos correspondientes en Office 365 como parte del proceso nuevo rollo. Tendrá que limpiar o eliminar manualmente dichos grupos.

