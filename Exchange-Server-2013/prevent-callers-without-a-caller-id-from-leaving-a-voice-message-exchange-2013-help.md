---
title: 'Impedir que los llamadores sin un ID dejando un mensaje de voz'
TOCTitle: Impedir que los llamadores sin un ID dejando un mensaje de voz
ms:assetid: dd5dad32-2f69-4bf4-8ff0-545c413d395a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673571(v=EXCHG.150)
ms:contentKeyID: 49895961
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Impedir que los llamadores sin un ID dejando un mensaje de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede permitir o impedir que los usuarios habilitados para mensajería unificada reciban mensajes de voz de personas anónimas. De forma predeterminada, cuando los usuarios se habilitan para mensajería unificada (MU) o correo de voz, pueden recibir llamadas anónimas que no contengan información de identificación del usuario.

En la mayoría de los casos, las llamadas que reciben los servidores de Exchange contienen un identificador de llamada que se puede usar para determinar el origen de la llamada entrante. Sin embargo, es posible que las llamadas entrantes no incluyan información del Id. de la persona que llama por los siguientes motivos:

  - El equipo de telefonía de la organización está configurado para no incluir información del Id. de la persona que llama.

  - La llamada entrante proviene de un teléfono móvil o externo.

  - La persona que llama ha deshabilitado el Id. de la persona que llama en su teléfono.

Dado que el parámetro *AnonymousCallersCanLeaveMessages* está habilitado de manera predeterminada, un usuario habilitado para mensajería unificada puede recibir un mensaje de voz aun si no se incluye la información de la persona que llama. Si la opción *AnonymousCallersCanLeaveMessages* está deshabilitada y el usuario habilitado para mensajería unificada recibe una llamada que no incluye información de la persona que llama, la llamada se identificará como anónima y el usuario habilitado para mensajería unificada no recibirá un mensaje de voz.

Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario esté habilitado para MU. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para evitar que los usuarios reciban mensajes de voz de personas anónimas

En este ejemplo, se impide que el usuario habilitado para mensajería unificada tonysmith@contoso.com reciba mensajes de voz de llamadas que no contienen información sobre la persona que llama.

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $false

