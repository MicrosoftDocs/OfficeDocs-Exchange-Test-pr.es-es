---
title: 'Habilitar o deshabilitar MAPI para un buzón de correo: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar MAPI para un buzón de correo
ms:assetid: c2c6718c-a2c0-4ed2-b4ed-364c3cb1f592
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124497(v=EXCHG.150)
ms:contentKeyID: 50556878
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar MAPI para un buzón de correo

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2017-12-31_

Puede usar el Centro de administración de Exchange o el Shell de administración de Exchange para habilitar o deshabilitar MAPI para el buzón de un usuario. Cuando se habilita MAPI, Outlook o cualquier otro cliente de correo electrónico MAPI puede obtener acceso al buzón del usuario. Cuando MAPI se deshabilita, ni Outlook ni otros clientes de correo electrónico MAPI podrán obtener acceso. Sin embargo, el buzón seguirá recibiendo mensajes de correo electrónico y, suponiendo que el buzón está habilitado para admitir el acceso de esos clientes, el usuario podrá obtener acceso a él para enviar o recibir correo electrónico a través de Outlook Web App, de un cliente de correo electrónico POP o de un cliente IMAP.


> [!NOTE]
> La compatibilidad con Outlook Web App y con los clientes de correo electrónico POP3, IMAP4 y MAPI se habilita de manera predeterminada cuando se crea un buzón de usuario.



Para consultar otras tareas relacionadas con la administración del acceso de clientes de correo electrónico a un buzón, vea los siguientes temas:

  - [Habilitar o deshabilitar Outlook Web App para un buzón de correo](enable-or-disable-outlook-web-app-for-a-mailbox-exchange-2013-help.md)

  - [Habilitar o deshabilitar el acceso a IMAP4 para un usuario](enable-or-disable-imap4-access-for-a-user-exchange-2013-help.md)

  - [Habilitar o deshabilitar el acceso POP3 para un usuario](enable-or-disable-pop3-access-for-a-user-exchange-2013-help.md)

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Configuración de usuario de acceso de cliente" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso de la EAC para habilitar o deshabilitar MAPI

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la lista de buzones de usuario, haga clic en el buzón para el que desea habilitar o deshabilitar MAPI y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

4.  En **Conectividad de correo**, realice una de las acciones siguientes.
    
      - Para deshabilitar MAPI, en **MAPI: Habilitado**, haga clic en **Deshabilitar**.
        
        Aparece una advertencia para que confirme si desea deshabilitar MAPI. Haga clic en **Sí**.
    
      - Para habilitar MAPI, en **MAPI: Deshabilitado**, haga clic en **Habilitar**.

5.  Haga clic en **Guardar** para guardar el cambio.

## Usar el Shell de administración de Exchange para habilitar o deshabilitar MAPI

En este ejemplo se deshabilita MAPI para el buzón de Ken Sánchez.

    Set-CASMailbox -Identity "Ken Sanchez" -MAPIEnabled $false

En este ejemplo se habilita MAPI para el buzón de Esther Valle.

    Set-CASMailbox -Identity "Esther Valle" -MAPIEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-CASMailbox](https://technet.microsoft.com/es-es/library/bb125264\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si habilitó o deshabilitó MAPI para un buzón de usuario correctamente, siga uno de estos procedimientos:

  - En la EAC, vaya a **Destinatarios**  \> **Buzones de correo**, haga clic en el buzón y, después, en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

  - En la página de propiedades de buzones, haga clic en **Características de buzón de correo**.

  - En **Conectividad de correo**, compruebe si MAPI está habilitado o deshabilitado.

O bien

  - Ejecute el siguiente comando en Shell de administración de Exchange.
    
        Get-CASMailbox <identity>
    
    Si MAPI está habilitado, el valor de la propiedad *MapiEnabled* es `True`. Si MAPI está deshabilitado, el valor es `False`.

