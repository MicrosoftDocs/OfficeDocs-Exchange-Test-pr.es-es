---
title: 'Configurar Grupos de Office 365 con Exchange híbrido local: Exchange 2013 Help'
TOCTitle: Configurar Grupos de Office 365 con Exchange híbrido local
ms:assetid: 184dfcfe-4b8e-450a-adc6-e647213b9501
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Mt668829(v=EXCHG.150)
ms:contentKeyID: 72513078
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar Grupos de Office 365 con Exchange híbrido local

 

_**Última modificación del tema:**2016-12-06_

Obtenga información sobre cómo permitir que los usuarios de Exchange local usen Grupos de Office 365 en una implementación híbrida.

Grupos es un servicio de Office 365 que permite a los equipos comunicarse, programar reuniones y colaborar en documentos más fácilmente. Toda la información compartida con un grupo, desde los mensajes de correo electrónico enviados hasta los archivos almacenados en las bibliotecas de OneDrive para la Empresa o SharePoint del grupo, está disponible para cualquier miembro del mismo. Si ha configurado una implementación híbrida entre su organización de Exchange local y Office 365, puede hacer que los grupos creados en Office 365 estén disponibles para los usuarios locales siguiendo los pasos en este tema.


> [!IMPORTANT]
> Usar Grupos de Office 365 con usuarios locales en una implementación híbrida de Exchange es una nueva característica. Al ser tan reciente, pueden aparecer algunos problemas cuando se configura. Asegúrese de leer la sección Problemas conocidos al final de este tema para encontrar soluciones a los problemas que puedan aparecer.



## Requisitos previos

Antes de empezar, asegúrese de que ha hecho lo siguiente:

  - Ha adquirido licencias de Azure Active Directory Premium para el inquilino. Esto es necesario para habilitar la característica de reescritura de grupos en Azure Active Directory Connect.

  - Ha configurado una implementación híbrida entre su organización de Exchange local y Office 365 y comprobado que funciona correctamente. Podrá obtener más información sobre las implementaciones híbridas de Exchange a continuación:
    
      - [Implementaciones híbridas de Exchange Server](exchange-server-hybrid-deployments-exchange-2013-help.md)
    
      - [Requisitos previos de implementación híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md)

  - Una vez instalada una versión de Exchange compatible, la integración de Exchange local con Grupos de Office 365 está disponible en CU1 y versiones más recientes de Exchange 2016, y en CU11 y versiones más recientes de Exchange de 2013. En cambio, Exchange híbrido requiere que la actualización acumulativa (CU) más reciente de Exchange 2013 o Exchange 2016 esté instalada en los servidores de Exchange locales. Si no puede instalar la CU más reciente, puede usarse la actualización publicada inmediatamente antes de la CU actual.

  - Inicio de sesión único instalado con Azure Active Directory Connect (Azure AD Connect). Esto es necesario para permitir que los usuarios hagan clic en los vínculos **Ver archivos de grupo** o datos adjuntos en la nube en los mensajes de correo electrónico del grupo.
    
    Al configurar Azure AD Connect para el inicio de sesión único en una implementación híbrida de Exchange, recomendamos que use la sincronización de contraseña. Active Directory Federation Services (AD FS) solo debe usarse en los casos siguientes: si pertenece a una organización grande; si tiene una implementación compleja de Active Directory local (por ejemplo, varios bosques de Active Directory); si otro producto de Microsoft necesita AD FS para trabajar con Office 365; o si, debido a directivas de cumplimiento, no puede sincronizar contraseñas fuera de su red local. Para obtener más información sobre el inicio de sesión único, vea [Integración de las identidades locales con Azure Active Directory](http://go.microsoft.com/fwlink/p/?linkid=723513).

## Habilitar la reescritura de grupos en Azure AD Connect

1.  En el asistente de Azure AD Connect, seleccione **Personalizar las opciones de sincronización** y después haga clic en **Siguiente**.

2.  En la página **Conectar con Azure AD**, escriba sus credenciales locales y de Office 365. Haga clic en **Siguiente**.

3.  En la página **Características opcionales**, compruebe que todavía están seleccionadas las opciones que configuró previamente. Las opciones seleccionados con mayor frecuencia son **Exchange híbrido** y **Sincronización por hash de contraseñas**.

4.  Seleccione **Escritura diferida del grupo** y después haga clic en **Siguiente**.

5.  En la página **Reescritura**, seleccione una unidad organizativa (OU) en Active Directory para almacenar los objetos que se sincronizan desde Office 365 a la organización local y haga clic en **Siguiente**.

6.  En la página **Listo para configurar**, haga clic en **Configurar**.

7.  Cuando el asistente haya finalizado, haga clic en **Salir** en la página **Completar la configuración**.

8.  Abra Usuarios y equipos de Active Directory en un controlador de dominio de Active Directory y busque la cuenta de usuario que comienza por **AAD\_**. Anote este nombre de cuenta.

9.  Abra el Shell de administración de Exchange en un servidor de Exchange local y ejecute los siguientes comandos.
    
        $AzureADConnectSWritebackAccount = <AAD_ account name from step 8>
        
        $GroupsOU = <writeback Active Directory OU selected in step 5>
        
        Import-Module "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1"
        
        Initialize-ADSyncGroupWriteBack -ADConnectorAccount $AzureADConnectSWritebackAccount -GroupWriteBackContainerDN $GroupsOU

## Configurar un dominio de grupo

El dominio de SMTP principal de un grupo de Office 365 se denomina *dominio de grupo*. De manera predeterminada, el dominio aceptado predeterminado en su organización se elige como el dominio de grupo. Si quiere agregar un dominio de grupos dedicados, puede agregar un dominio mediante los siguientes pasos. Para obtener más información sobre la compatibilidad de varios dominios con Grupos de Office 365, vea [Compatibilidad con varios dominios para los grupos de Office 365](https://support.office.com/es-es/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a).

1.  Agregue el nuevo dominio a la organización de Office 365. Si necesita ayuda para agregar un dominio a Office 365, vea [Agregar usuarios y dominios en Office 365](https://support.office.com/es-es/article/add-users-and-domain-to-office-365-6383f56d-3d09-4dcb-9b41-b5f5a5efd611?ui=en-us%26rs=en-us%26ad=us).

2.  Agregue el dominio de grupo como un dominio aceptado en su organización de Exchange local mediante el siguiente comando. Esto es necesario para que el conector de envío híbrido pueda usarse para enviar correo saliente al dominio de grupo en Office 365.
    
        New-AcceptedDomain -Name groups.contoso.com -DomainName groups.contoso.com -DomainType InternalRelay

3.  Cree los siguientes registros DNS públicos con su proveedor de DNS.
    
    
    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Nombre de registro de DNS</p></th>
    <th><p>Tipo de registro de DNS</p></th>
    <th><p>Valor de registro de DNS</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>groups.contoso.com</p></td>
    <td><p>MX</p></td>
    <td><p>groups-contoso-com.mail.protection.outlook.com</p>

    > [!NOTE]
    > El formato de este valor de registro de DNS es <EM>&lt;domain key&gt;</EM>.mail.protection.outlook.com. Para conocer cuál es su clave de dominio, vea <A href="https://support.office.com/es-es/article/gather-the-information-you-need-to-create-office-365-dns-records-77f90d4a-dc7f-4f09-8972-c1b03ea85a67?ui=en-us%26rs=en-us%26ad=us">Recopilar la información necesaria para crear los registros de DNS de Office 365</A>.


</td>
    </tr>
    <tr class="even">
    <td><p>autodiscover.groups.contoso.com</p></td>
    <td><p>CNAME</p></td>
    <td><p>autodiscover.outlook.com</p></td>
    </tr>
    </tbody>
    </table>
    

    > [!WARNING]
    > Si el registro de MX de DNS para el dominio de grupo se establece en el servidor de Exchange local, el flujo de correo no funcionará correctamente entre usuarios de la organización de Exchange local y el grupo de Office 365.



4.  Agregue el dominio de grupo para el conector de envío híbrido, creado por el Asistente de configuración híbrida en la organización de Exchange local, usando el siguiente comando.
    
        Set-SendConnector -Identity "Outbound to Office 365" -AddressSpaces "contoso.mail.onmicrosoft.com","groups.contoso.com"
    

    > [!NOTE]
    > Si el conector de envío no está actualizado o el dominio de grupo no está agregado como un dominio aceptado en la organización de Exchange local, el correo que se envíe de un buzón local no se entregará al grupo a menos que este se configure para recibir correo de remitentes externos.



## ¿Cómo saber si el proceso se completó correctamente?

Para asegurarse de que los grupos funcionan con la implementación híbrida de Exchange, debe probarlos mediante un buzón local y uno que se haya trasladado de la organización local a Office 365. Siga los pasos en las secciones siguientes para realizar cada prueba.

## Realizar pruebas mediante un buzón local

1.  Agregue un buzón local a un grupo de Office 365.

2.  Agregue un buzón de Office 365 al mismo grupo de Office 365.

3.  Inicie sesión en el buzón de Office 365 con Outlook en la web.

4.  Publique un mensaje en el grupo mediante el buzón de Office 365.

5.  Abra el buzón local mediante Outlook 2016 o Outlook en la web.

6.  Compruebe que el buzón ha recibido un mensaje de correo electrónico que contiene el mensaje enviado al grupo de Office 365.

7.  En el mismo buzón, redacte una respuesta al mensaje y envíelo al grupo.

8.  Compruebe que todos los miembros del grupo pueden ver el mensaje.

## Realizar pruebas mediante un buzón trasladado a Office 365

1.  Mueva un buzón de la organización de Exchange local a Office 365.

2.  Agregue el buzón a un grupo de Office 365.

3.  En una nueva sesión del explorador, inicie sesión en el buzón que se trasladó a Office 365.

4.  En Outlook en la web, compruebe que el grupo aparece en la barra de navegación de la izquierda.

5.  Publique un mensaje en el grupo.

6.  Compruebe que todos los miembros del grupo pueden ver el mensaje.

## Problemas conocidos

  - **Los grupos no aparecen para los buzones de correo trasladados a Office 365** Cuando se traslada un usuario de su organización de Exchange local a Office 365, los grupos no aparecen en el panel de navegación izquierdo de Outlook o de Outlook en la web. Para corregir el problema, quite el buzón de todos los grupos de los que es miembro y vuelva a agregarlo a cada grupo.

  - **Los nuevos grupos no aparecen en la lista global de direcciones de Exchange local (LGD)** Cuando se crea un nuevo grupo en Office 365, este no aparece en los LGD locales automáticamente. Para solucionar este problema, abra el Shell de administración de Exchange en un servidor de Exchange local y ejecute el siguiente comando.
    
        Update-Recipient "<group name>"

  - **Los grupos no reciben mensajes de usuarios locales** Un usuario local no podrá enviar correos electrónicos a un grupo de Office 365 cuando se cumplan las siguientes condiciones:
    
      - El dominio de grupo está configurado como un dominio autoritativo de su organización de Exchange local.
    
      - El grupo se creó recientemente y su información todavía no se ha escrito en su Active Directory local.
    
    El problema se resolverá cuando Azure AD Connect realice su próxima sincronización entre Office 365 y la organización local. La sincronización de Azure AD Connect se produce cada treinta minutos.

  - **Los usuarios locales no pueden usar los vínculos incluidos en los pies de página de mensajes del grupo** Los usuarios locales no pueden usar los vínculos **Ver conversaciones de grupo** o **Cancelar suscripción** que se incluyen en los pies de página de los mensajes del grupo que les envían. Para cancelar la suscripción de un grupo, los usuarios locales necesitan ponerse en contacto con un administrador de grupo.

  - **Se produce un error en la entrega del correo enviado a la dirección de SMTP secundaria del grupo** Cuando se agregan varias direcciones de correo electrónico a un grupo, sólo la dirección SMTP principal se vuelve a escribir en su Active Directory local. Si un usuario local intenta enviar un mensaje a la dirección SMTP secundaria de un grupo, el mensaje no se entregará. Para evitar este problema, configure una dirección SMTP en cada grupo.

  - **Los usuarios locales no pueden convertirse en administradores de un grupo** Los usuarios locales no pueden acceder directamente al espacio de grupo. Por este motivo, no se pueden agregar como administradores de un grupo.

  - **Se puede producir un error en la entrega de correo externo a un grupo si ha habilitado el flujo de correo centralizado** Si el flujo de correo centralizado está habilitado, el correo que ha enviado un usuario externo a un grupo no se puede entregar, aunque el grupo permita correos de remitentes externos.

  - **Los usuarios locales no pueden enviar correos como grupo** Un usuario local que intente enviar un mensaje como un grupo de Office 365, recibirá un error de permiso denegado aunque se le haya concedido el permiso Enviar como en el grupo. Los permisos Enviar como de un grupo solo funcionan para los usuarios de buzón de correo de Exchange Online.

  - **Seleccionar un grupo desde el panel de navegación izquierdo de Outlook no abre el buzón de grupo** Outlook usa la dirección URL de detección automática para abrir un buzón de grupo. Si la dirección de correo electrónico principal de un grupo se encuentra en un dominio que no señala a la dirección URL de detección automática de Office 365 (autodiscover.outlook.com), Outlook no podrá abrir el buzón de grupo. Para solucionar el problema, los grupos pueden aprovisionarse con una dirección principal en un dominio que señale a la dirección URL de detección automática de Office 365. Puede configurar una directiva de dirección de correo electrónico para agregar una dirección de correo electrónico principal en cada buzón de grupo que señale a la dirección URL de detección automática de Office 365. Para obtener más información, vea [Compatibilidad con varios dominios para los grupos de Office 365](https://support.office.com/es-es/article/multi-domain-support-for-office-365-groups-admin-help-7cf5655d-e523-4bc3-a93b-3ccebf44a01a).

