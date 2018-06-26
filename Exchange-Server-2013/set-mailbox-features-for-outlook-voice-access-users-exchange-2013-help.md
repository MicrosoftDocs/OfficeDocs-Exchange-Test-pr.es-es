---
title: 'Establecer características de buzón de correo para los usuarios de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Establecer características de buzón de correo para los usuarios de Outlook Voice Access
ms:assetid: 10960bf0-65cf-4d0b-bae5-d203c53662db
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996307(v=EXCHG.150)
ms:contentKeyID: 50556740
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer características de buzón de correo para los usuarios de Outlook Voice Access

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-02-22_

Outlook Voice Access contiene dos interfaces: una interfaz de usuario de teléfono (TUI) y una interfaz de usuario de voz (VUI). Puede configurar las opciones de TUI del usuario habilitado para MU cuando el usuario obtiene acceso al buzón mediante el sistema de mensajería unificada (MU) en Exchange 2013. Cuando modifica los parámetros de TUI del usuario habilitado para MU en una directiva de buzones de MU, los cambios afectan a todos los usuarios que pertenecen o están asociados a dicha directiva de buzones de MU. Puede modificar los siguientes parámetros de TUI en una directiva de buzones de MU:

  - Acceso sin PIN al correo de voz

  - Respuestas de voz a otros mensajes

  - Acceso a su calendario mediante TUI

  - Acceso al directorio mediante TUI

  - Acceso a su correo electrónico mediante TUI

  - Acceso a sus contactos personales mediante TUI


> [!NOTE]
> Solamente puede usar el Shell para modificar la configuración de TUI de Outlook&nbsp;Voice Access para usuarios habilitados para MU.



Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para modificar la configuración de TUI en una directiva de buzones de MU

En este ejemplo, se establecen las opciones relacionadas con TUI en una directiva de buzones de MU denominada `MyUMMailboxPolicy`.

    Set-UMMailbox -identity MyUMMailboxPolicy -AllowSubscriberAccess $true -AllowTUIAccessToCalendar $false -AllowTUIAccessToDirectory $false -AllowTUIAccessToEmail -$true -AllowTUIAccessToPersonalContacts $true

