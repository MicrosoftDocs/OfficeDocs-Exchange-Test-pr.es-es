---
title: 'Permitir quien llama sin identificar para dejar mensaje voz Exchange 2013 Help'
TOCTitle: Permitir a quienes llaman sin un identificador para dejar un mensaje de voz
ms:assetid: 51367d98-e17c-4bcf-8b14-208bd1ac3af0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232040(v=EXCHG.150)
ms:contentKeyID: 49895623
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir a quienes llaman sin un identificador para dejar un mensaje de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede permitir que los usuarios habilitados para mensajería unificada reciban mensajes de correo de voz de personas anónimas o impedir que lo hagan. De forma predeterminada, cuando los usuarios se habilitan para mensajería unificada (MU) o correo de voz, pueden recibir llamadas anónimas que no contengan información de identificación del usuario.

En la mayoría de los casos, las llamadas que recibe un servidor de mensajería unificada contienen un identificador de usuario que se puede usar para determinar el origen de la llamada entrante. Sin embargo, es posible que las llamadas entrantes no incluyan información del Id. de la persona que llama por los siguientes motivos:

  - El equipo de telefonía de la organización está configurado para no incluir información del Id. de la persona que llama.

  - La llamada entrante proviene de un teléfono móvil o externo.

  - La persona que llama ha deshabilitado el Id. de la persona que llama en su teléfono.

Como el parámetro *AnonymousCallersCanLeaveMessages* está habilitado de forma predeterminada, un usuario habilitado para mensajería unificada puede recibir un mensaje de voz aunque no se incluya la información de identificación del autor de la llamada. Si la opción *AnonymousCallersCanLeaveMessages* está deshabilitada, y el usuario habilitado para mensajería unificada recibe una llamada que no incluye ningún identificador, la llamada se identificará como anónima y el usuario no recibirá ningún mensaje de voz.

Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/voice-mail-enabled-user-procedures).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario esté habilitado para MU. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para recibir mensajes de voz de autores de llamada anónimos

En este ejemplo, se permite al usuario habilitado para mensajería unificada recibir mensajes de voz de llamadas entrantes que no contienen el identificador de autor de llamada.

    Set-UMMailbox -Identity tonysmith@contoso.com -AnonymousCallersCanLeaveMessages $true

