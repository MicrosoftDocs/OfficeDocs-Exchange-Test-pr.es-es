---
title: 'Deshabilitar característica usuarios Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Deshabilitar las características seleccionadas para los usuarios de Outlook Voice Access
ms:assetid: 37421edf-af60-4ca9-9e8b-262b8b851607
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Gg602126(v=EXCHG.150)
ms:contentKeyID: 50556779
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar las características seleccionadas para los usuarios de Outlook Voice Access

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Outlook Voice Access contiene dos interfaces: la interfaz de usuario de teléfono (TUI) y la interfaz de usuario de voz (VUI). De manera predeterminada, cuando los usuarios marcan en Outlook Voice Access, pueden obtener acceso al calendario, el correo electrónico y los contactos personales, y realizar búsquedas en el directorio. Puede usar el Shell para evitar que los usuarios obtengan acceso a una o más de estas características cuando usen Outlook Voice Access para obtener acceso a su buzón de correo. Cuando modifique las características de Outlook Voice Access en una directiva de buzón de Mensajería unificada (UM), los cambios afectarán a todos los usuarios asociados con la directiva de buzón de MU.

Puede deshabilitar el acceso de los usuarios a las siguientes características de Outlook Voice Access en una directiva de buzón de MU:

  - Calendario

  - Directorio

  - Email

  - Contactos personales

Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

También puede usar el Shell para deshabilitar las características de Outlook Voice Access en el buzón de un único usuario habilitado para MU. Cuando lo hace, estas características se deshabilitarán solo para ese usuario. Si bien no puede deshabilitar todas las características de Outlook Voice Access que se encuentran en una directiva de buzón de MU para un único usuario, puede deshabilitar el acceso al calendario y su correo electrónico.

Para otras tareas de administración relacionadas con buzones de correo de mensajería unificada, consulte [Correo de voz para usuarios](voice-mail-for-users-exchange-2013-help.md).


> [!NOTE]
> Solamente puede usar el Shell para modificar las características de Outlook&nbsp;Voice Access para usuarios habilitados para MU en una directiva de buzón de MU o en el buzón de un único usuario habilitado para MU.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el usuario esté habilitado para la MU. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar la consola para deshabilitar las características seleccionadas de Outlook Voice Access para usuarios habilitados para MU en una directiva de buzón de MU

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

En este ejemplo, se evita que los usuarios asociados con una directiva de MU denominada `MyUMMailboxPolicy` obtengan acceso al calendario al marcar en Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToCalendar $false

En este ejemplo, se evita que los usuarios asociados con la directiva de MU denominada `MyUMMailboxPolicy` obtengan acceso al directorio al marcar en Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToDirectory $false

En este ejemplo, se evita que los usuarios asociados con la directiva de MU denominada `MyUMMailboxPolicy` obtengan acceso a su correo electrónico al marcar en Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToEmail -$false

En este ejemplo, se evita que los usuarios asociados con la directiva de MU denominada `MyUMMailboxPolicy` obtengan acceso a sus contactos personales al marcar en Outlook Voice Access.

    Set-UMMailboxPolicy -id MyUMMailboxPolicy -AllowTUIAccessToPersonalContacts $false

## Usar la consola para deshabilitar las características seleccionadas de Outlook Voice Access en el buzón de un único usuario habilitado para MU

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

Este ejemplo deshabilita el acceso al calendario en un buzón de MU denominado tony@contoso.com cuando el usuario marca en Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToCalendarEnabled $false

En este ejemplo, se deshabilita el acceso al correo electrónico en un buzón de MU denominado tony@contoso.com cuando el usuario marca en Outlook Voice Access.

    Set-UMMailbox -id tony@contoso.com -TUIAccessToEmailEnabled $false

