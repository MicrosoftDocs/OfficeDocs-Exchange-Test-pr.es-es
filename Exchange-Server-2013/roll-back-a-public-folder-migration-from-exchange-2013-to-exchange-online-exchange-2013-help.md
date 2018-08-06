---
title: 'Revertir una migración de carpetas públicas de Exchange 2013 a Exchange Online | Microsoft Docs'
TOCTitle: Revertir una migración de carpetas públicas de Exchange 2013 a Exchange Online
ms:assetid: bcd54aa0-aa45-4c68-b504-1475842d4b96
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt798259(v=EXCHG.150)
ms:contentKeyID: 74432706
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Revertir una migración de carpetas públicas de Exchange 2013 a Exchange Online

 

_**Última modificación del tema:** 2017-03-20_

**Resumen:**  Siga estos pasos para revertir la infraestructura de carpeta pública al estado previo a la migración en su organización local de Exchange 2013.

Si tiene problemas con la migración de carpetas públicas a Exchange Online o necesita reactivar las carpetas públicas de Exchange 2013 por cualquier motivo, siga los pasos siguientes.

## Revertir la migración

Tenga en cuenta que, si revierte la migración, perderá todo el contenido que se haya agregado a las carpetas públicas de Exchange Online tras la migración, tanto a través de clientes como mediante correo electrónico en el caso de las carpetas públicas habilitadas para correo. Para guardar este contenido, puede exportar el contenido de las carpetas públicas tras la migración a un archivo .pst. Este se puede importar a las carpetas públicas locales una vez que se ha completado la reversión.

1.  En su entorno local de Exchange, ejecute el comando siguiente para desbloquear las carpetas públicas de Exchange 2013 (tenga en cuenta que el desbloqueo puede tardar varias horas):
    
        Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections:$false -PublicFolderMailboxesMigrationComplete:$false -PublicFoldersEnabled Local 

2.  En su entorno de Exchange local, revierta la `ExternalEmailAddress` de cualquier carpeta pública habilitada para correo que se haya actualizado con SetMailPublicFolderExternalAddress.ps1 (el script utilizado en el *paso 8: Prueba y desbloqueo de la migración de carpetas públicas de Exchange Online* de [Usar la migración por lotes para migrar carpetas públicas de Exchange 2013 a Exchange Online](use-batch-migration-to-migrate-exchange-2013-public-folders-to-exchange-online-exchange-online-help.md)). Puede consultar el archivo de resumen creado por el script para identificar las que se modificaron. También puede utilizar el archivo OnPrem\_MEPF.xml generado anteriormente en el mismo lote del proceso de migración para ver las propiedades originales de todas las carpetas públicas habilitadas para correo.

3.  En PowerShell de Exchange Online, ejecute los comandos siguientes para quitar todas las carpetas y los buzones públicos de Exchange Online:
    
        Get-MailPublicFolder -ResultSize Unlimited | where {$_.EntryId -ne $null}| Disable-MailPublicFolder -Confirm:$false 
        Get-PublicFolder -GetChildren \ -ResultSize Unlimited | Remove-PublicFolder -Recurse -Confirm:$false
        $hierarchyMailboxGuid = $(Get-OrganizationConfig).RootPublicFolderMailbox.HierarchyMailboxGuid
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -ne $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder | Where-Object {$_.ExchangeGuid -eq $hierarchyMailboxGuid} | Remove-Mailbox -PublicFolder -Confirm:$false -Force
        Get-Mailbox -PublicFolder -SoftDeletedMailbox | Remove-Mailbox -PublicFolder -PermanentlyDelete:$true

4.  Ejecute el comando siguiente en su entorno de Exchange Online para redirigir el tráfico de la carpeta pública al entorno local (Exchange 2013):
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote

5.  Consulte [Configuración de las carpetas públicas de Exchange 2013 para una implementación híbrida](configure-exchange-2013-public-folders-for-a-hybrid-deployment-exchange-2013-help.md) para obtener más información sobre cómo volver a configurar el acceso a las carpetas públicas locales, para que los usuarios de Exchange Online puedan acceder a ellas.

