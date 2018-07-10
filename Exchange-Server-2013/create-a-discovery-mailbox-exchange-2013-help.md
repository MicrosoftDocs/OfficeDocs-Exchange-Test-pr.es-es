---
title: 'Crear un buzón de correo de detección: Exchange 2013 Help'
TOCTitle: Crear un buzón de correo de detección
ms:assetid: bc20285d-35e2-4e49-9bd3-38abf96114ba
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638177(v=EXCHG.150)
ms:contentKeyID: 49895872
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un buzón de correo de detección

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Durante la instalación de Microsoft Exchange Server 2013 se crea un buzón de correo de detección de forma predeterminada. En Exchange Online, también se crea un buzón de correo de detección de forma predeterminada. Los buzones de correo de detección están disponibles como buzones de destino para las búsquedas de [Exhibición de documentos electrónicos en contexto](in-place-ediscovery-exchange-2013-help.md) en el Centro de administración de Exchange (EAC). Puede crear buzones de correo de detección adicionales según sea necesario. Después de crear un nuevo buzón de correo de detección, tendrá que asignar permisos de acceso total a los usuarios adecuados para que puedan acceder a los resultados de la búsqueda de eDiscovery que se copian en el buzón de correo de detección.


> [!WARNING]
> Después de que un administrador de detección copia los resultados de una búsqueda de eDiscovery en un buzón de correo de detección, el buzón puede contener potencialmente información confidencial. Debe controlar el acceso a los buzones de correo de detección y asegurarse de que solo los usuarios autorizados puedan acceder a ellos.



Para más información, vea [Discovery mailboxes](in-place-ediscovery-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Crear buzones de detección"en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Los buzones de correo de detección tienen una cuota de almacenamiento de 50 gigabytes (GB). No se puede incrementar la cuota de almacenamiento.

  - No puede usar el EAC para crear un buzón de correo de detección ni asignar permisos para acceder a él. Para ello debe usar el Shell. En Office 365, use PowerShell remoto conectado a su organización de Exchange Online.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Paso 1 (opcional): Conectarse a Exchange Online mediante PowerShell remoto

Solo necesita realizar este paso si tiene una organización de Exchange Online o Office 365. Si tiene una organización de Exchange Server 2013, vaya al paso siguiente y ejecute el comando en el Shell de administración de Exchange.

1.  En el equipo local, abra Windows PowerShell y ejecute el siguiente comando.
    
        $UserCredential = Get-Credential
    
    En el cuadro de diálogo **Solicitud de credenciales de Windows PowerShell**, escriba el nombre de usuario y la contraseña de una cuenta de administrador global de Office 365 y, después, haga clic en **Aceptar**.

2.  Ejecute el comando siguiente.
    
        $Session = New-PSSession -ConfigurationName Microsoft.Exchange -ConnectionUri https://outlook.office365.com/powershell-liveid/ -Credential $UserCredential -Authentication Basic -AllowRedirection

3.  Ejecute el comando siguiente.
    
        Import-PSSession $Session

4.  Para comprobar que se ha conectado a su organización de Exchange Online, ejecute el comando siguiente para obtener una lista de todos los buzones de correo de su organización.
    
        Get-Mailbox

Para obtener más información o si tiene problemas para conectarse a su organización de Exchange Online, consulte [Conectarse a Exchange Online mediante PowerShell remoto](https://go.microsoft.com/fwlink/p/?linkid=517283).

## Paso 2: Crear un buzón de correo de detección

En este ejemplo se crea un buzón de correo de detección con el nombre SearchResults.

    New-Mailbox -Name SearchResults -Discovery 

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-Mailbox](https://technet.microsoft.com/es-es/library/aa997663\(v=exchg.150\)).

Para mostrar una lista de todos los buzones de correo de detección en una organización de Exchange, ejecute este comando:

    Get-Mailbox -Resultsize unlimited -Filter {RecipientTypeDetails -eq "DiscoveryMailbox"}

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).

## Paso 3: Asignar permisos a un buzón de correo de detección

Tiene que asignar a los usuarios los permisos necesarios para abrir un buzón de correo de detección que haya creado. Use la sintaxis siguiente para asignar a un usuario o a un grupo los permisos para abrir un buzón de correo de detección y ver los resultados de búsqueda:

    Add-MailboxPermission <Name of the discovery mailbox> -User <Name of user or group> -AccessRights FullAccess -InheritanceType all

Por ejemplo, este comando asigna el permiso de acceso completo al grupo Litigation Managers, para que los miembros del grupo puedan abrir el buzón de correo de detección Fabrikam Litigation.

    Add-MailboxPermission "Fabrikam Litigation" -User "Litigation Managers" -AccessRights FullAccess -InheritanceType all

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Add-MailboxPermission](https://technet.microsoft.com/es-es/library/bb124097\(v=exchg.150\)).

## Más información

  - De forma predeterminada, los miembros del grupo de roles Administración de la detección solo tienen permisos de acceso completo al buzón de correo de detección predeterminado. Tendrá que asignar expresamente el permiso de acceso total al grupo de roles Administración de la detección si desea que sus miembros puedan abrir un buzón de correo de detección que ha creado.

  - Aunque se muestren en la lista de direcciones de Exchange, los usuarios no pueden enviar correo electrónico a un buzón de correo de detección. La entrega de correo electrónico a los buzones de correo de detección está prohibida por restricciones de entrega. Esto conserva la integridad de los resultados de la búsqueda que se copiaron a un buzón de detección.

  - Un buzón de correo detección no se puede redirigir ni convertir en otro tipo de buzón.

  - Para quitar un buzón de correo de detección, solo tiene que hacer lo mismo que con cualquier otro tipo de buzón de correo.

