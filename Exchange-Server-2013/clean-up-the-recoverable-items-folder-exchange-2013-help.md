---
title: 'Limpiar la carpeta Elementos recuperables: Exchange 2013 Help'
TOCTitle: Limpiar la carpeta Elementos recuperables
ms:assetid: 82c310f8-de2f-46f2-8e1a-edb6055d6e69
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff678798(v=EXCHG.150)
ms:contentKeyID: 50556839
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Buscar y destruir
- derrame clasificado
- Derrame de mensaje
- derrame de mensaje clasificado
- limpieza de derrames clasificados
- limpieza de derrames de mensaje
- limpieza de derrames de mensaje clasificado
ms.translationtype: HT
---

# Limpiar la carpeta Elementos recuperables

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-09-30_

La carpeta Elementos recuperables (conocida en versiones anteriores de Exchange como *el volcado de archivos*) existe para proteger de eliminaciones accidentales o malintencionadas y para facilitar los esfuerzos de detección comúnmente realizados antes o durante el litigio o las investigaciones. Para obtener más información acerca de la carpeta Elementos recuperables, consulte [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

La forma de limpiar la carpeta Elementos recuperables del buzón depende de si el buzón está ubicado en una conservación local o retención por juicio o si tiene habilitada una recuperación de un único elemento:

  - Si un buzón no está ubicado en la conservación local o retención por juicio o no tiene una recuperación de un único elemento habilitada, simplemente puede eliminar los elementos desde la carpeta Elementos recuperables. Luego de eliminarlos, puede usar la recuperación de un único elemento para recuperar los elementos.

  - Si el buzón está ubicado en una conservación local o retención por juicio o tiene habilitada una recuperación de un único elemento, es importante guardar los datos del buzón hasta que se elimine la espera o se deshabilite la recuperación de un único elemento. En este caso, debe realizar más pasos detallados para limpiar la carpeta Elementos recuperables.

Para obtener más información sobre conservación local y retención por juicio, consulte [Conservación local y retención por juicio](in-place-hold-and-litigation-hold-exchange-2013-help.md). Para más información sobre recuperación de elementos individuales, consulte la "Recuperación de un único elemento" en [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

Para obtener más información acerca de la carpeta Elementos recuperables, consulte [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento:  30 minutos. Esto puede variar dependiendo del tamaño de la carpeta de elementos recuperables

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el La entrada "Eliminar contenido del buzón" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Como la limpieza incorrecta de la carpeta Elementos recuperables puede causar una pérdida de datos, es importante que esté familiarizado con la carpeta Elementos recuperables y el impacto de la eliminación de su contenido. Antes de realizar este procedimiento, se recomienda que revise la información en [Carpeta Elementos recuperables](recoverable-items-folder-exchange-2013-help.md).

  - No puede usar el Centro de administración de Exchange (EAC) para realizar estos procedimientos. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Use el Shell para eliminar los elementos de la carpeta Elementos recuperables para los buzones que no están en retención o no tienen habilitada la recuperación de un único elemento.

Este ejemplo elimina permanentemente los elementos eliminados desde la carpeta Elementos recuperables de Gurinder Saingh y también copia los elementos a la carpeta GurinderSingh-RecoverableItems en el buzón de búsqueda de detección (un buzón de detección creado con la configuración de Exchange).

    Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent


> [!NOTE]
> Para eliminar los elementos del buzón sin copiarlos a otro buzón, use el comando anterior sin los parámetros <EM>TargetMailbox</EM> y <EM>TargetFolder</EM>.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Search-Mailbox](https://technet.microsoft.com/es-es/library/dd298173\(v=exchg.150\)).

## Use el Shell para limpiar los elementos de la carpeta Elementos recuperables para los buzones que están en retención o tienen habilitada la recuperación de un único elemento.

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el La entrada "Eliminar contenido del buzón" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Si un buzón alcanza su cuota de Elementos recuperables, recomendamos que aumente la cuota y no elimine los elementos desde la carpeta. También puede supervisar eventos en el registro de Aplicación relacionado con la cuota de advertencia de los Elementos recuperables y tomar las medidas necesarias (tales como aumentar la cuota o investigar el crecimiento de la carpeta Elementos recuperables para los buzones que alcanzan la cuota de advertencia).

Si las limitaciones de almacenamiento o problemas similares evitan que eleve la cuota de Elementos recuperables, y necesita eliminar los mensajes de la carpeta Elementos recuperables de un buzón en conservación local o retención por juicio o tiene habilitada la recuperación de un único elemento, le recomendamos que primero copie los datos de la carpeta Elementos recuperables del usuario a otro buzón. Si está eliminando elementos debido a limitaciones de almacenamiento en un volumen, puede copiar los elementos en un buzón ubicado en un volumen que tiene el almacenamiento adecuado.

Este procedimiento copia los elementos de la carpeta Elementos recuperables de Gurinder Singh a la carpeta GurinderSingh-RecoverableItems en el buzón de búsqueda de detección. Antes de copiar y eliminar los elementos de la carpeta Elementos recuperables, primero debe realizar varios pasos para asegurarse de que los elementos no estén eliminados en la carpeta Elementos recuperables. Luego de copiar los elementos en un buzón de detección o copia de seguridad y de limpiar la carpeta, puede volver a las configuraciones anteriores del buzón.

1.  Recuperar las siguientes configuraciones de la cuota. Asegúrese de observar los valores para que puede invertir estas configuraciones después de limpiar la carpeta Elementos recuperables.
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    

    > [!NOTE]
    > Si el parámetro <EM>UseDatabaseQuotaDefaults</EM> se establece en <CODE>$true</CODE>, no se aplicaciones las configuraciones de la cuota anterior. Se aplican las configuraciones de la cuota correspondiente configuradas en la base de datos del buzón, incluso si se completan las configuraciones individuales del buzón.

    
        Get-Mailbox "Gurinder Singh" | Format-List RecoverableItemsQuota, RecoverableItemsWarningQuota, ProhibitSendQuota, ProhibitSendReceiveQuota, UseDatabaseQuotaDefaults, RetainDeletedItemsFor, UseDatabaseRetentionDefaults

2.  Recuperar las configuraciones de acceso del buzón para el buzón. Asegúrese de tener en cuenta estas configuraciones más adelante.
    
        Get-CASMailbox "Gurinder Singh" | Format-List EwsEnabled, ActiveSyncEnabled, MAPIEnabled, OWAEnabled, ImapEnabled, PopEnabled

3.  Recuperar el tamaño actual de la carpeta Elementos recuperables. Observe el tamaño para que pueda aumentar las cuotas en el Paso 6.
    
        Get-MailboxFolderStatistics "Gurinder Singh" -FolderScope RecoverableItems | Format-List Name,FolderAndSubfolderSize

4.  Recuperar la configuración del ciclo de trabajo del Asistente de las carpetas administradas. Asegúrese de tener en cuenta estas configuraciones más adelante.
    
        Get-MailboxServer "My Mailbox Server" | Format-List Name,ManagedFolderWorkCycle

5.  Deshabilite el acceso del cliente al buzón para asegurarse de que no se hagan cambios en los datos del buzón durante la duración de este procedimiento.
    
        Set-CASMailbox "Gurinder Singh" -EwsEnabled $false -ActiveSyncEnabled $false -MAPIEnabled $false -OWAEnabled $false -ImapEnabled $false -PopEnabled $false

6.  Para asegurarse de que no se eliminen elementos desde la carpeta Elementos recuperables, aumente la cuota de Elementos recuperables, aumente la cuota de advertencia de Elementos recuperables y establezca el período de retención del elemento eliminado en un valor superior al tamaño actual de la carpeta Elementos recuperables del usuario. Esto es particularmente importante para guardar los mensajes para los buzones ubicados en conservación local o retención por juicio. Recomendamos aumentar estas configuraciones al doble de su tamaño actual.
    
        Set-Mailbox "Gurinder Singh" -RecoverableItemsQuota 50Gb -RecoverableItemsWarningQuota 50Gb -RetainDeletedItemsFor 3650 -ProhibitSendQuota 50Gb -ProhibitSendRecieveQuota 50Gb -UseDatabaseQuotaDefaults $false -UseDatabaseRetentionDefaults $false

7.  Deshabilite el Asistente de carpetas administradas en el servidor del buzón.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle $null
    

    > [!IMPORTANT]
    > Si el buzón reside en una base de datos del buzón en un grupo de disponibilidad de base de datos (DAG), debe deshabilitar el Asistente de carpetas administradas en cada miembro del DAG que aloja una copia de la base de datos. Si la base de datos falla en otro servidor, esto evita que el Asistente de carpetas administradas en ese servidor elimine los datos del buzón.



8.  Deshabilite la recuperación de un único elemento y quite el buzón de la retención por juicio.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $false -LitigationHoldEnabled $false
    

    > [!IMPORTANT]
    > Después de ejecutar este comando, puede tardar hasta una hora deshabilitar la recuperación de un único elemento o la retención por juicio. Le recomendamos que realice el siguiente paso solamente después de que transcurrió este período.



9.  Copie los elementos de la carpeta Elementos recuperables a una carpeta en el Buzón de búsqueda de detección y elimine los contenidos del buzón origen.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    
    Si necesita eliminar solamente los mensajes que coinciden con sus condiciones especificadas, use el parámetro *SearchQuery* para especificar las condiciones. Este ejemplo elimina los mensajes que tienen la secuencia "Su extracto bancario" en el campo **Asunto**.
    
        Search-Mailbox -Identity "Gurinder Singh" -SearchQuery "Subject:'Your bank statement'" -SearchDumpsterOnly -TargetMailbox "Discovery Search Mailbox" -TargetFolder "GurinderSingh-RecoverableItems" -DeleteContent
    

    > [!NOTE]
    > No es necesario copiar los elementos en el buzón de búsqueda de detección. Puede copiar los mensajes en cualquier buzón. Sin embargo, para evitar el acceso a los datos buzón posiblemente confidenciales, recomendamos copiar los mensajes a un buzón que tiene el acceso restringido a los administradores de registros autorizados. De forma predeterminada, el acceso al Buzón de búsqueda de detección está restringido a los miembros del grupo de roles de administración de detección. Para obtener información más detallada, consulte <A href="in-place-ediscovery-exchange-2013-help.md">Exhibición de documentos electrónicos en contexto</A>.



10. Si el buzón estaba en retención por juicio o tenía habilitada anteriormente una recuperación de un único elemento, habilite de nuevo estas características.
    
        Set-Mailbox "Gurinder Singh" -SingleItemRecoveryEnabled $true -LitigationHoldEnabled $true
    

    > [!IMPORTANT]
    > Después de ejecutar este comando, puede tardar hasta una hora habilitar la recuperación de un único elemento o la retención por juicio. Le recomendamos que habilite el Asistente de las carpetas administradas y permita el acceso del cliente (Pasos 11 y 12) solamente después de que transcurrió este período.



11. Invierta las siguientes cuotas a los valores mencionados en el Paso 1:
    
      - *RecoverableItemsQuota*
    
      - *RecoverableItemsWarningQuota*
    
      - *ProhibitSendQuota*
    
      - *ProhibitSendReceiveQuota*
    
      - *UseDatabaseQuotaDefaults*
    
      - *RetainDeletedItemsFor*
    
      - *UseDatabaseRetentionDefaults*
    
    En este ejemplo, el buzón se elimina de la retención, el período de retención del elemento eliminado se restablece al valor predeterminado de 14 días y la cuota de Elementos recuperables se configura para usar el mismo valor que la base de datos del buzón. Si los valores del Paso 1 son diferentes, debe usar los parámetros anteriores para especificar cada valor y establecer el parámetro *UseDatabaseQuotaDefaults* en `$false`. Si los parámetros *RetainDeletedItemsFor* y *and UseDatabaseRetentionDefaults* se establecieron anteriormente en un valor diferente, también debe volver a los valores en el Paso 1.
    
        Set-Mailbox "Gurinder Singh" -RetentionHoldEnabled $false -RetainDeletedItemsFor 14 -RecoverableItemsQuota unlimited -UseDatabaseQuotaDefaults $true

12. Habilite el Asistente de carpetas administradas estableciendo el ciclo de trabajo de nuevo con el valor del Paso 4. Este ejemplo establece el ciclo de trabajo en un día.
    
        Set-MailboxServer MyMailboxServer -ManagedFolderWorkCycle 1

13. Habilite el acceso del cliente.
    
        Set-CASMailbox -ActiveSyncEnabled $true -EwsEnabled $true -MAPIEnabled $true -OWAEnabled $true -ImapEnabled $true -PopEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\))

  - [Get-CASMailbox](https://technet.microsoft.com/es-es/library/bb124754\(v=exchg.150\))

  - [Get-MailboxFolderStatistics](https://technet.microsoft.com/es-es/library/aa996762\(v=exchg.150\))

  - [Get-MailboxServer](https://technet.microsoft.com/es-es/library/bb123539\(v=exchg.150\))

  - [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\))

  - [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\))

  - [Set-MailboxServer](https://technet.microsoft.com/es-es/library/aa998651\(v=exchg.150\))

  - [Search-Mailbox](https://technet.microsoft.com/es-es/library/dd298173\(v=exchg.150\))

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya limpiado correctamente la carpeta de Elementos recuperables de un buzón, use el cmdlet [Get-MailboxFolderStatistics](https://technet.microsoft.com/es-es/library/aa996762\(v=exchg.150\)) para comprobar el tamaño de la carpeta Elementos recuperables.

Este ejemplo recupera el tamaño de la carpeta Elementos recuperables y sus subcarpetas y un recuento de elementos en la carpeta y en cada subcarpeta.

    Get-MailboxFolderStatistics -Identity "Gurinder Singh" -FolderScope RecoverableItems | Format-Table Name,FolderAndSubfolderSize,ItemsInFolderAndSubfolders -Auto

