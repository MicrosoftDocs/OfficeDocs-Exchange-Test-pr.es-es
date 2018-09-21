---
title: 'Configurar las carpetas públicas de Exchange Online para una implementación híbrida: Exchange 2013 Help'
TOCTitle: Configurar las carpetas públicas de Exchange Online para una implementación híbrida
ms:assetid: d979edb3-967b-4431-8beb-0c236bf7f56d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt729076(v=EXCHG.150)
ms:contentKeyID: 72768736
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar las carpetas públicas de Exchange Online para una implementación híbrida

 

_<strong>Se aplica a:</strong>Exchange Server 2013_

_<strong>Última modificación del tema:</strong>2016-12-15_

**Resumen:**   instrucciones para permitir que los usuarios de Exchange 2013 local tengan acceso a carpetas públicas en Exchange Online.

En una implementación híbrida, los usuarios pueden estar hospedados en Exchange Online, en una ubicación local o de ambas formas, y las carpetas públicas pueden estar tanto en Exchange Online como ubicadas localmente. En ocasiones, los usuarios conectados pueden necesitar acceder a las carpetas públicas del entorno local de Exchange Server 2013. Asimismo, los usuarios de Exchange 2013 pueden necesitar acceder a las carpetas públicas de Exchange Online o de Office 365.

En este artículo se describe cómo permitir que los usuarios de su entorno local de Exchange 2013 tengan acceso a carpetas públicas de Exchange Online/Office 365. Para permitir que los usuarios de Exchange Online/Office 365 tengan acceso a carpetas públicas de un entorno local de Exchange 2013, vea [Configuración de las carpetas públicas de Exchange 2013 para una implementación híbrida](https://docs.microsoft.com/es-es/exchange/collaboration-exo/public-folders/set-up-modern-hybrid-public-folders).


> [!NOTE]
> Si tiene carpetas públicas de Exchange&nbsp;2010 o Exchange&nbsp;2007 locales, vea <A href="configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md">Configurar carpetas públicas locales heredadas para una implementación híbrida</A>.



## ¿Qué necesita saber antes de comenzar?

1.  En estas instrucciones se da por hecho que se ha usado el Asistente para configuración híbrida con el propósito de configurar y sincronizar los entornos local y de Exchange Online y, asimismo, que los registros DNS utilizados para la característica Detección automática de la mayoría de los usuarios hacen referencia a un extremo local. Para obtener más información, vea [Asistente de configuración híbrida](hybrid-configuration-wizard-exchange-2013-help.md).

2.  Estas instrucciones suponen que Outlook en cualquier lugar está habilitado y funciona en los servidores de Exchange locales. Para obtener información sobre cómo habilitar Outlook en cualquier lugar, vea [Outlook en cualquier lugar](https://technet.microsoft.com/es-es/library/bb123741\(v=exchg.150\)).

3.  Implementar la coexistencia de carpetas públicas para una implementación híbrida de Exchange con Office 365 puede requerir que resuelva conflictos durante el procedimiento de importación. Los conflictos pueden aparecer debido a direcciones de correo no enrutables asignadas a carpetas públicas habilitadas, conflictos con otros usuarios y grupos de Office 365, y otros atributos.

4.  Los usuarios deben actualizar sus clientes de Outlook a la actualización pública de Outlook de noviembre de 2012 (o posterior) para poder acceder a las carpetas públicas entre locales.
    
    1.  Para descargar la actualización de Outlook de noviembre de 2012 para Outlook 2010, vea [Actualización para Microsoft Outlook 2010 (KB2687623), edición de 32 bits](https://www.microsoft.com/es-es/download/details.aspx?id=35702).
    
    2.  Para descargar la actualización de Outlook de noviembre de 2012 para Outlook 2007, vea [Actualización para Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/es-es/download/details.aspx?id=35718).

5.  Outlook 2011 para Mac y Outlook para Mac para Office 365 no se admiten en las carpetas públicas entre locales. Los usuarios deben estar en la misma ubicación que las carpetas públicas para obtener acceso a ellas con Outlook 2011 para Mac o Outlook para Mac para Office 365. Además, los usuarios cuyos buzones están en Exchange Online no podrán tener acceso a carpetas públicas locales mediante Outlook Web App.
    

    > [!NOTE]
    > Outlook 2016 para Mac no admite carpetas públicas entre locales. Si los clientes de su organización usan Outlook 2016 para Mac, asegúrese de que tengan instalada la actualización de abril de 2016. En caso contrario, esos usuarios no podrán tener acceso a las carpetas públicas de una topología híbrida o de coexistencia. Para obtener más información, vea <A href="https://technet.microsoft.com/es-es/library/mt788631(v=exchg.150)">Acceso a las carpetas públicas con Outlook 2016 para Mac</A>.



## Paso 1: descargar los scripts

1.  Descargue los siguientes archivos de [Mail-enabled Public Folders - directory sync from EXO to On-prem script](https://go.microsoft.com/fwlink/p/?linkid=797795).
    
      - `Import-PublicFolderMailboxes.ps1`
    
      - `ImportPublicFolderMailboxes.strings.psd1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.ps1`
    
      - `Sync-MailPublicFoldersCloudToOnprem.strings.psd1`

2.  Guarde los archivos en el equipo local en el que vaya a ejecutar PowerShell. Por ejemplo, C:\\PFScripts.

## Paso 2: configurar la sincronización de directorios

Al ejecutar el script `Sync-MailPublicFoldersCloudToOnprem.ps1`, se sincronizarán las carpetas públicas habilitadas para correo entre Exchange Online y el entorno local de Exchange 2013. Necesitará recrear en la nube los permisos especiales asignados a las carpetas públicas habilitadas para correo, ya que los permisos entre locales no son compatibles con escenarios de implementación híbrida. Para obtener más información, vea [Implementación híbrida de Exchange Server 2013](exchange-server-hybrid-deployments-exchange-2013-help.md).


> [!NOTE]
> Las carpetas públicas habilitadas para correo sincronizadas aparecerán como objetos de contacto de correo para fines relacionados con el flujo de correo y no podrán verse en el Centro de administración de Exchange. Consulte el comando Get-MailPublicFolder. Para volver a crear los permisos SendAs en la nube, use el comando Add-RecipientPermission.



1.  En el servidor de Exchange 2013, ejecute el comando siguiente para sincronizar las carpetas públicas habilitadas para correo desde Exchange Online/Office 365 a su implementación local de Active Directory.
    
        Sync-MailPublicFoldersCloudToOnprem.ps1 -Credential (Get-Credential)
    
    Donde `Credential` es su nombre de usuario y contraseña de Office 365.


> [!NOTE]
> También le recomendamos que ejecute este script a diario para sincronizar las carpetas públicas habilitadas para correo.



## Paso 3: Configurar los usuarios locales para que tengan acceso a las carpetas públicas de Exchange Online

El último paso de este procedimiento es configurar la organización local de Exchange 2013 para permitir el acceso a las carpetas públicas de Exchange Online.

Al ejecutar el script `Import-PublicFolderMailboxes.ps1`, se importarán los objetos de buzón de carpeta pública de la nube como usuarios habilitados para correo en su entorno local. El script también configurará los objetos importados como buzones de carpetas públicas remotas.

1.  En el servidor de Exchange 2013, ejecute el comando siguiente para importar los objetos de buzón de carpeta pública de la nube en su entorno local de Active Directory.
    
        Import-PublicFolderMailboxes.ps1 -Credential (Get-Credential)
    
    Donde `Credential` es su nombre de usuario y contraseña de Office 365.
    

    > [!NOTE]
    > Le recomendamos que ejecute este script a diario para importar los objetos de buzón de carpeta pública, ya que, cuando los buzones de carpetas públicas alcancen su capacidad de umbral, se dividirán automáticamente en varios buzones. Por lo tanto, siempre necesita asegurarse de que importó los buzones de carpetas públicas más recientes de la nube.



2.  Permita que la organización local de Exchange 2013 tenga acceso a las carpetas públicas de Exchange Online.
    
        Set-OrganizationConfig -PublicFoldersEnabled Remote


> [!NOTE]
> Deberá esperar a que la sincronización de Active&nbsp;Directory finalice para ver los cambios reflejados. Esto proceso puede tardar hasta 3 horas en completarse. Si no desea esperar las sincronizaciones recurrentes que ocurren cada tres horas, puede forzar la sincronización de directorio en cualquier momento. Para ver pasos detallados para forzar la sincronización de directorios, vea <A href="http://technet.microsoft.com/es-es/library/jj151771.aspx">Forzar sincronización de directorios</A>.



## ¿Cómo saber si el proceso se ha completado correctamente?

1.  Inicie sesión en Outlook como un usuario que esté en Exchange Online y realice las siguientes pruebas de carpeta pública:
    
      - Ver la jerarquía
    
      - Comprobar los permisos
    
      - Crear y eliminar carpetas públicas
    
      - Publique contenido en una carpeta pública y elimine contenido de ella.

