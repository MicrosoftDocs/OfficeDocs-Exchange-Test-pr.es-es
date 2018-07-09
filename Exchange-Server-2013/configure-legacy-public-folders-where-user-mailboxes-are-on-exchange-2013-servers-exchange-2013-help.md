---
title: 'Configurar las carpetas públicas heredadas en las que se encuentran los buzones de usuario en los servidores de Exchange 2013: Exchange 2013 Help'
TOCTitle: Configurar las carpetas públicas heredadas en las que se encuentran los buzones de usuario en los servidores de Exchange 2013
ms:assetid: 1d5ca19e-696e-4054-a634-15dd34d952b7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn690134(v=EXCHG.150)
ms:contentKeyID: 62281085
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar las carpetas públicas heredadas en las que se encuentran los buzones de usuario en los servidores de Exchange 2013

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2017-03-27_

Cómo habilitar a los usuarios 2013 de Exchange o Exchange 2016 acceso Exchange 2010 o anteriores carpetas públicas (también conocido como carpetas públicas heredadas).

## ¿Qué necesita saber antes de comenzar?

Los usuarios cuyos buzones se encuentran en 2013 de Exchange Server o Exchange Server 2016 no podrán tener acceso a carpetas públicas heredadas desde Outlook Web App, Outlook en el web o Outlook para Mac. Los pasos descritos en este artículo funcionan para 2013 de Exchange y Exchange 2016.


> [!NOTE]
> 2016 de Outlook para usuarios de Mac puede tener acceso a carpetas públicas heredadas después de seguir los pasos de este artículo. Si los clientes de su organización utilizan Outlook 2016 para Mac, asegúrese de que han instalado la actualización de abril de 2016. De lo contrario, esos usuarios no podrá tener acceso a las carpetas públicas en una topología de híbridos o coexistencia. Para obtener más información, consulte <A href="accessing-public-folders-with-outlook-2016-for-mac-exchange-2013-help.md">Acceso a las carpetas públicas con Outlook 2016 para Mac</A>.



## Paso 1: permitir que las carpetas públicas de Exchange 2010 sean reconocibles

1.  Si son las carpetas públicas en Exchange 2010 o posterior, debe instalar la función del servidor acceso de cliente en todos los servidores de buzones que tienen una base de datos de carpetas públicas. Esto permite al servicio de RpcClientAccess de Microsoft Exchange esté en ejecución, lo que permite a todos los clientes de acceso a carpetas públicas. La función de acceso de cliente no es necesaria para los servidores de carpetas públicas de Exchange 2007, y este paso no es necesario. Para obtener más información, consulte [instalar Exchange Server 2010](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md).
    

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
    ```
        New-Mailbox -Name <PFMailbox1> -Database <NewMDBforPFs> 
    ```
    ```
        Set-Mailbox -Identity <PFMailbox1> -HiddenFromAddressListsEnabled $true
    ```
    
4.  Para Exchange 2010, habilite la detección automática para devolver los buzones proxy de carpetas públicas. Este paso no es necesario para Exchange 2007.
    
        Set-MailboxDatabase <NewMDBforPFs> -RPCClientAccessServer <PFServerName_with_CASRole>

5.  Repita los pasos anteriores para cada servidor de carpetas públicas que haya en la organización.

## Paso 2: configurar buzones de usuario para obtener acceso a las carpetas públicas heredadas

El último paso de este procedimiento consiste en configurar los buzones de usuario para permitir el acceso a las carpetas públicas heredadas locales.

Permita que los usuarios locales de Exchange Server 2013 tengan acceso a las carpetas públicas heredadas. Para ello, apunte a todos los buzones proxy de carpetas públicas que creó en el [Step 2: Make remote public folders discoverable](configure-legacy-on-premises-public-folders-for-a-hybrid-deployment-exchange-2013-help.md). Ejecute el siguiente comando desde un servidor Exchange 2013 con CU5 o una actualización posterior.

    Set-OrganizationConfig -PublicFoldersEnabled Remote -RemotePublicFolderMailboxes ProxyMailbox1,ProxyMailbox2,ProxyMailbox3


> [!NOTE]
> Deberá esperar a que la sincronización de Active&nbsp;Directory finalice para ver los cambios reflejados. Este proceso puede tardar varias horas.



## ¿Cómo saber si el proceso se ha completado correctamente?

Inicie sesión en Outlook para un usuario cuyo buzón de correo esté en Exchange Server 2013 CU5 o un servidor superior y realice las siguientes pruebas en las carpetas públicas:

1.  Asegúrese de que el cliente de Outlook se esté ejecutando.

2.  Mantenga presionada la tecla CTRL y luego haga clic con el botón derecho en el icono de Outlook en el área de notificación en el lado derecho de la barra de tareas de Windows.

3.  Seleccione **Probar la configuración automática de correo electrónico…**

4.  Asegúrese de que la herramienta de prueba de la configuración automática de correo electrónico devuelva la siguiente información en la pestaña XML:
    
      - \<PublicFolderInformation\>
    
      - \<SmtpAddress\>\<Dirección SMTP para buzón de carpeta pública\</SmtpAddress\>
    
      - \</PublicFolderInformation\>

5.  En el cliente de Outlook, realice las siguientes tareas:
    
      - Vea la jerarquía de carpetas públicas.
    
      - Compruebe los permisos.
    
      - Cree y elimine carpetas públicas.
    
      - Publique contenido en una carpeta pública y elimine contenido de ella.

