---
title: 'Habilitar o deshabilitar Outlook Web App para buzón correo: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar Outlook Web App para un buzón de correo
ms:assetid: abc19646-6211-4f18-a060-e347452dcc53
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124124(v=EXCHG.150)
ms:contentKeyID: 50556849
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar Outlook Web App para un buzón de correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-11-14_

Puede usar el EAC o el Shell para habilitar o deshabilitar Outlook Web App para un buzón de correo de usuario. Cuando Outlook Web App se habilita, un usuario puede usar Outlook Web App y enviar y recibir correo electrónico. Cuando Outlook Web App está deshabilitado, el buzón de correo continuará recibiendo mensajes de correo electrónico y un usuario puede acceder al mismo para enviar y recibir correo usando un cliente MAPI, como Microsoft Outlook, o un cliente de correo POP o IMAP, si el buzón de correo está habilitado para admitir el acceso de dichos clientes.


> [!NOTE]
> La compatibilidad de Outlook Web App y los clientes de correo electrónico MAPI, POP3 e IMAP4 se habilita de forma predeterminada cuando se crea un buzón de correo de usuario.



Para consultar otras tareas de administración relacionadas para administrar el acceso de clientes de correo electrónico a un buzón de correo, consulte los siguientes temas:

  - [Habilitar o deshabilitar MAPI para un buzón de correo](enable-or-disable-mapi-for-a-mailbox-exchange-online-help.md)

  - [Habilitar o deshabilitar el acceso a IMAP4 para un usuario](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Habilitar o deshabilitar el acceso POP3 para un usuario](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Configuración de usuario de acceso de cliente" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar o deshabilitar Outlook Web App

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón cuya Outlook Web App desee habilitar o deshabilitar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones de correo, haga clic en **Características de buzón**.

4.  En **Conectividad de correo**, realice una de las acciones siguientes:
    
      - Para deshabilitar Outlook Web App, en **Outlook Web App: Habilitado**, haga clic en **Deshabilitar**.
        
        Aparece una advertencia para que confirme si desea deshabilitar Outlook Web App. Haga clic en **Sí**.
    
      - Para habilitar Outlook Web App, en **Outlook Web App: Deshabilitado**, haga clic en **Habilitar**.

5.  Haga clic en **Guardar** para guardar el cambio.


> [!NOTE]
> Puede habilitar y deshabilitar Outlook Web App para varios buzones de correo de usuarios usando la característica de edición masiva de EAC. Para obtener más información acerca de cómo hacerlo, consulte la sección "Edición masiva de buzones de correo de usuario" en <A href="manage-user-mailboxes-exchange-2013-help.md">Administrar los buzones de usuario</A>.



## Usar el Shell para habilitar o deshabilitar Outlook Web App

Este ejemplo deshabilita Outlook Web App en el buzón de correo de Yan Li.

    Set-CASMailbox -Identity "Yan Li" -OWAEnabled $false

Este ejemplo habilita Outlook Web App en el buzón de correo de Elly Nkya.

    Set-CASMailbox -Identity Ellyn@contoso.com -OWAEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha habilitado o deshabilitado Outlook Web App correctamente para un buzón de correo de usuario,siga uno de estos procedimientos:

  - En el EAC, vaya a **Destinatarios** \> **Buzones de correo**, haga clic en el buzón de correo y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

  - En la página de propiedades de buzones de correo, haga clic en **Características de buzón**.

  - En **Conectividad de correo**, compruebe si Outlook Web App está habilitado o deshabilitado.

O bien

  - Ejecute el siguiente comando en el Shell.
    
        Get-CASMailbox <identity>
    
    Si Outlook Web App está habilitado, el valor de la propiedad para *OWAEnabled* es `True`. Si Outlook Web App está deshabilitado, el valor es `False`.

