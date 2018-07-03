---
title: 'Configurar carpetas públicas locales heredadas para una implementación híbrida: Exchange 2013 Help'
TOCTitle: Configurar carpetas públicas locales heredadas para una implementación híbrida
ms:assetid: bcb0ac98-2949-486b-a8ab-8549c021651b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn249373(v=EXCHG.150)
ms:contentKeyID: 54914853
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar carpetas públicas locales heredadas para una implementación híbrida

 

_**Se aplica a:** Exchange Online, Exchange Server 2010, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2018-05-22_

**Resumen:**  Siga los pasos de este artículo para sincronizar las carpetas públicas entre Office 365 y su implementación local de Exchange 2007 o Exchange 2010.

En una implementación híbrida, los usuarios pueden estar hospedados en Exchange Online, de forma local o ambos, mientras que las carpetas públicas lo pueden estar en Exchange Online o localmente. Las carpetas públicas solo pueden estar en una ubicación, de modo que deberá decidir si colocarlas en Exchange Online o localmente. No pueden estar en ambas ubicaciones. Los buzones de correo de carpeta pública se sincronizan en Exchange Online mediante el servicio de sincronización de directorios. Sin embargo, las carpetas públicas habilitadas para correo no se sincronizan entre locales.

En este tema se explica cómo sincronizar carpetas públicas habilitadas para correo cuando los usuarios están en Office 365 y las carpetas públicas de Exchange 2010 SP3 o Exchange 2007 SP3 RU10 se encuentran en una implementación local. Sin embargo, un usuario de Office 365 que no esté representado por un objeto MailUser local (local en la jerarquía de carpetas públicas de destino) no podrá acceder a carpetas públicas locales heredadas o de Exchange 2013.


> [!NOTE]
> En esta sección nos referiremos a los servidores de Exchange 2010&nbsp;SP3 y Exchange 2007&nbsp;SP3&nbsp;RU10 como <EM>servidor de Exchange heredado</EM>.



Sincronizaremos las carpetas públicas habilitadas para correo con los siguientes scripts, que se inician mediante una tarea de Windows que se ejecuta en el entorno local:

1.  `Sync-MailPublicFolders.ps1`   Este script sincroniza objetos de carpeta pública habilitada para correo desde la implementación de Exchange local con Office 365. Usa la implementación de Exchange local como patrón para determinar los cambios que deben aplicarse a O365. El script creará, actualizará o eliminará objetos de carpeta pública habilitada para correo en Active Directory de O365 según lo que exista en la implementación de Exchange local.

2.  `SyncMailPublicFolders.strings.psd1`   Es un archivo de compatibilidad que usa el script de sincronización anterior y debe copiarse en la misma ubicación que el script anterior.

Cuando finalice este procedimiento, los usuarios locales y de Office 365 podrán acceder a la misma infraestructura de carpetas públicas local.

## ¿Qué versiones híbridas de Exchange funcionan con las carpetas públicas?

En la siguiente tabla se reflejan las posibles combinaciones de versión y ubicación de buzones de usuario y carpetas públicas. “Híbrido no válido” sigue siendo un escenario factible, pero no se considera como escenario híbrido, dado que las carpetas públicas y los usuarios se encuentran en la misma ubicación.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th></th>
<th>Buzón de usuario de Exchange 2007 o Exchange 2010 local</th>
<th>Buzón de usuario de Exchange 2013 local</th>
<th>Buzón de usuario de Exchange Online</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Carpetas públicas de Exchange 2007 o Exchange 2010 locales</p></td>
<td><p>Híbrido no válido</p></td>
<td><p>Híbrido no válido</p></td>
<td><p>Se admite</p></td>
</tr>
<tr class="even">
<td><p>Carpetas públicas de Exchange 2013 locales</p></td>
<td><p>Híbrido no válido</p></td>
<td><p>Híbrido no válido</p></td>
<td><p>Se admite</p></td>
</tr>
<tr class="odd">
<td><p>Carpetas públicas de Exchange Online</p></td>
<td><p>No se admite</p></td>
<td><p>Se admite</p></td>
<td><p>Híbrido no válido</p></td>
</tr>
</tbody>
</table>


Una configuración híbrida con carpetas públicas de Exchange 2003 no es posible. Si su organización usa Exchange 2003, debe mover todas las bases de datos y réplicas de las carpetas públicas a Exchange 2007 SP3 RU10 o a una versión posterior. No pueden quedar réplicas de carpetas públicas en Exchange 2003.


> [!NOTE]
> Outlook 2016 no es compatible con el acceso a las carpetas públicas heredadas de Exchange 2007. Si tiene usuarios con Outlook 2016, deberá mover las carpetas públicas a una versión más reciente de Exchange. Puede encontrar más información acerca de la compatibilidad de Outlook 2016 y Office 2016 con Exchange 2007 y con las versiones anteriores en <A href="https://go.microsoft.com/fwlink/p/?linkid=849053">este artículo</A>.



## Paso 1: ¿qué necesita saber antes de comenzar?

1.  En estas instrucciones se da por hecho que se ha usado el Asistente para configuración híbrida con el propósito de configurar y sincronizar los entornos local y de Exchange Online y, asimismo, que los registros DNS utilizados para la característica Detección automática de la mayoría de los usuarios hacen referencia a un extremo local. Para obtener más información, vea [Asistente de configuración híbrida](https://technet.microsoft.com/es-es/library/hh529921\(v=exchg.150\)).

2.  Estas instrucciones suponen que Outlook en cualquier lugar está habilitado y funciona en los servidores de Exchange locales heredados. Para obtener información sobre cómo habilitar Outlook en cualquier lugar, vea [Outlook en cualquier lugar](outlook-anywhere-exchange-2013-help.md).

3.  Implementar la coexistencia de carpetas públicas heredadas para una implementación híbrida de Exchange con Office 365 puede requerir que resuelva conflictos durante el procedimiento de importación. Los conflictos pueden aparecer debido a direcciones de correo no enrutables asignadas a carpetas públicas habilitadas, conflictos con otros usuarios y grupos de Office 365, y otros atributos.

4.  En estas instrucciones se da por hecho que la organización de Exchange Online se ha actualizado a una versión que admite carpetas públicas.

5.  En Exchange Online, debe ser miembro del grupo de roles de administración de la organización. Este grupo de roles es diferente de los permisos que se le asignan cuando se suscribe a Exchange Online. Para obtener información detallada sobre cómo habilitar el grupo de roles de administración de la organización, vea [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

6.  En Exchange 2010, debe ser miembro de los grupos de roles RBAC de administración de la organización o administración del servidor. Para obtener información detallada, vea [Agregar miembros a un grupo de funciones](https://go.microsoft.com/fwlink/?linkid=299212).

7.  En Exchange 2007, debe tener asignado el rol de Administrador de organización de Exchange o Administrador de servidores de Exchange. Además, debe tener asignado el rol de Administrador de carpetas públicas y el grupo de administradores locales para el servidor de destino. Para obtener más información, vea [Cómo agregar un usuario o grupo a una función de administrador](https://go.microsoft.com/fwlink/p/?linkid=81779).

8.  Si Exchange Server 2007 se ejecuta en Windows Server 2008 x64, deberá actualizar a [Windows PowerShell 2.0 y WinRM 2.0 para Windows Server 2008 x64 Edition](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930). Si Exchange Server 2007 se ejecuta en Windows Server 2003 x64, deberá actualizar a Windows PowerShell 2.0. Para obtener información detallada, vea la [Actualización para Windows Server 2003 x64 Edition](https://www.microsoft.com/es-es/download/details.aspx?id=10512).

9.  Los usuarios deben actualizar sus clientes de Outlook a la actualización pública de Outlook de noviembre de 2012 (o posterior) para poder acceder a las carpetas públicas entre locales.
    
    1.  Para descargar la actualización de Outlook de noviembre de 2012 para Outlook 2010, vea [Actualización para Microsoft Outlook 2010 (KB2687623), edición de 32 bits](https://www.microsoft.com/es-es/download/details.aspx?id=35702).
    
    2.  Para descargar la actualización de Outlook de noviembre de 2012 para Outlook 2007, vea [Actualización para Microsoft Office Outlook 2007 (KB2687404)](https://www.microsoft.com/es-es/download/details.aspx?id=35718).

10. Outlook 2016 para Mac, así como las versiones anteriores, y Outlook para Mac para Office 365 no se admiten en las carpetas públicas heredadas entre locales. Los usuarios deben estar en la misma ubicación que las carpetas públicas para poder obtener acceso a ellas con Outlook para Mac o Outlook para Mac para Office 365. Además, los usuarios cuyos buzones están en Exchange Online no podrán obtener acceso a las carpetas públicas locales mediante Outlook Web App.

11. Después de haber seguido las instrucciones de este artículo para configurar las carpetas públicas locales para una implementación híbrida, los usuarios externos a la organización no podrán enviar mensajes a sus carpetas públicas locales, a menos que se tomen medidas adicionales. Puede establecer el dominio aceptado de las carpetas públicas en Retransmisión interna (consulte [Administrar dominios aceptados en Exchange Online](https://technet.microsoft.com/es-es/library/jj945194\(v=exchg.150\)) para obtener más información) o puede deshabilitar el Bloqueo perimetral basado en directorios (DBEB), tal y como se describe en [Usar bloqueo perimetral basado en directorios para rechazar mensajes enviados a destinatarios no válidos](https://technet.microsoft.com/es-es/library/dn600322\(v=exchg.150\)).

## Paso 2: hacer que las carpetas públicas puedan detectarse

1.  Si las carpetas públicas están en servidores con Exchange 2010 posterior, necesita instalar el rol de servidor Acceso de clientes en todos los servidores de buzones de correo que tengan una base de datos de carpeta pública. Esto posibilita el funcionamiento del servicio RpcClientAccess de Microsoft Exchange, que permite que todos los clientes puedan acceder a carpetas públicas. No se necesita el rol de acceso de cliente para los servidores de carpetas públicas de Exchange 2007, y este paso no es necesario. Para obtener más información, vea [Instalar Exchange Server 2010](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md). Este paso no es necesario en las carpetas públicas de Exchange 2007.
    

    > [!NOTE]
    > Este servidor no tiene que formar parte del equilibrio de carga de Acceso de clientes. Para obtener más información, vea <A href="https://technet.microsoft.com/es-es/library/ff625247(v=exchg.141).aspx">Descripción del equilibrio de carga en Exchange 2010</A>.



2.  Cree una base de datos de buzones vacía en cada servidor de carpetas públicas.
    
    Para Exchange 2010, ejecute el siguiente comando. Este comando excluye la base de datos de buzones del equilibrador de carga de aprovisionamiento de buzones. Esto impide que se agreguen nuevos buzones automáticamente a esta base de datos.
    
        New-MailboxDatabase -Server <PFServerName_with_CASRole> -Name <NewMDBforPFs> -IsExcludedFromProvisioning $true
    
    Para Exchange 2007, ejecute el siguiente comando:
    
        New-MailboxDatabase -StorageGroup "<PFServerName>\StorageGroup>" -Name <NewMDBforPFs>
    

    > [!NOTE]
    > El único buzón de correo que se recomienda agregar a esta base de datos es el buzón proxy que creará en el paso&nbsp;3. No es aconsejable crear otros buzones en esta base de datos de buzones de correo.



3.  Cree un buzón proxy en la nueva base de datos de buzones de correo y ocúltelo de la libreta de direcciones. La detección automática devolverá el SMTP de este buzón de correo como *DefaultPublicFolderMailbox* SMTP, de modo que al resolver este SMTP, el cliente podrá llegar al servidor Exchange heredado para el acceso a carpetas públicas.
    
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs>
    
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true

4.  Para Exchange 2010, habilite la detección automática para devolver los buzones proxy de carpetas públicas. Este paso no es necesario para Exchange 2007.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  Repita los pasos anteriores por cada servidor de carpetas públicas que haya en la organización.

## Paso 3: descargar los scripts

1.  Descargue los siguientes archivos desde [Mail-enabled Public Folders - directory sync script (Carpetas públicas habilitadas para correo: script de sincronización de directorios)](https://www.microsoft.com/es-es/download/details.aspx?id=46381):
    
      - `Sync-MailPublicFolders.ps1`
    
      - `SyncMailPublicFolders.strings.psd1`

2.  Guarde los archivos en el equipo local en el que vaya a ejecutar PowerShell. Por ejemplo, C:\\PFScripts.

## Paso 4: configurar la sincronización de directorios

El servicio de sincronización de directorios no sincroniza carpetas públicas habilitadas para correo. La ejecución del siguiente script sincronizará las carpetas públicas habilitadas para correo entre las diversas ubicaciones. Los permisos especiales asignados a las carpetas públicas habilitadas para correo tendrán que volver a crearse en la nube, ya que el permiso entre locales no se admite en escenarios de implementación híbrida. Para obtener más información, vea [Implementación híbrida de Exchange Server 2013](https://technet.microsoft.com/es-es/59e32000-4fcf-417f-a491-f1d8f9aeef9b\(exchg.150\)#doc).


> [!NOTE]
> Las carpetas públicas habilitadas para correo sincronizadas aparecerán como objetos de contacto de correo para fines relacionados con el flujo de correo y no podrán verse en el Centro de administración de Exchange. Vea el comando Get-MailPublicFolder. Para volver a crear los permisos SendAs en la nube, use el comando Add-RecipientPermission.



1.  En el servidor de Exchange heredado, ejecute el siguiente comando para sincronizar las carpetas públicas habilitadas para correo de Active Directory local con O365.
    
        Sync-MailPublicFolders.ps1 -Credential (Get-Credential) -CsvSummaryFile:sync_summary.csv
    
    Donde `Credential` es su nombre de usuario y contraseña de Office 365 y `CsvSummaryFile` es la ruta donde desea registrar las operaciones de sincronización y los errores en formato .csv.


> [!NOTE]
> Antes de ejecutar el script, le recomendamos que simule las acciones que llevará a cabo el script en el entorno. Para ello, ejecútelo tal como se indicó anteriormente con el parámetro <CODE>-WhatIf</CODE>.<BR>También se recomienda ejecutar este script a diario para sincronizar las carpetas públicas habilitadas para correo.



## Paso 5: configurar los usuarios de Exchange Online para que tengan acceso a las carpetas públicas locales

El último paso de este procedimiento consiste en configurar la organización de Exchange Online y permitir el acceso a las carpetas públicas heredadas locales.

Permita que la organización de Exchange Online tenga acceso a las carpetas públicas locales. Para ello, apuntará a todos los buzones proxy de carpetas públicas que creó en el Paso 2: hacer que las carpetas públicas puedan detectarse.

En **Windows PowerShell**, ejecute el comando siguiente:

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes PFMailbox1,PFMailbox2,PFMailbox3

Deberá esperar a que la sincronización de Active Directory finalice para ver los cambios. Este proceso puede tardar hasta 3 horas en completarse. Si no desea esperar las sincronizaciones recurrentes que se producen cada tres horas, puede forzar la sincronización de directorios en cualquier momento. Para ver pasos detallados para forzar la sincronización de directorios, vea [Forzar la sincronización de directorios](http://technet.microsoft.com/es-es/library/jj151771.aspx). Office 365 selecciona aleatoriamente uno de los buzones de carpetas públicas que se proporciona en este comando.


> [!IMPORTANT]
> Un usuario de Office 365 que no esté representado por un objeto MailUser local (local en la jerarquía de carpetas públicas de destino) no podrá acceder a carpetas públicas locales heredadas o de Exchange 2013. Vea el artículo de Knowledge Base <A href="https://go.microsoft.com/fwlink/p/?linkid=699451">Los usuarios de Exchange Online no pueden acceder a carpetas públicas locales heredadas</A> para obtener una solución.



## ¿Cómo saber si el proceso se ha completado correctamente?

1.  Inicie sesión en Outlook como un usuario que esté en Exchange Online y realice las siguientes pruebas de carpeta pública:
    
      - Ver la jerarquía
    
      - Comprobar los permisos
    
      - Crear y eliminar carpetas públicas
    
      - Publique contenido en una carpeta pública y elimine contenido de ella.

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

