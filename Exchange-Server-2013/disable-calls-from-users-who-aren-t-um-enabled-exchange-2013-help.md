---
title: 'Deshabilitar las llamadas de los usuarios que no están habilitados para mensajería unificada: Exchange 2013 Help'
TOCTitle: Deshabilitar las llamadas de los usuarios que no están habilitados para mensajería unificada
ms:assetid: 272ff4ab-b4d9-4647-98e2-7c171f9dfc3f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673516(v=EXCHG.150)
ms:contentKeyID: 49895530
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar las llamadas de los usuarios que no están habilitados para mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Puede habilitar o deshabilitar las llamadas de los usuarios que no están habilitados para mensajería unificada (MU). De forma predeterminada, la mensajería unificada hace posible que las llamadas entrantes de personas no autenticadas realizadas por medio de un operador automático se transfieran a usuarios habilitados para MU. Cuando esta configuración está habilitada, los usuarios que se encuentran fuera de la organización pueden transferir llamadas a usuarios habilitados para mensajería unificada.

Si para un usuario habilitado para MU esta configuración ha sido deshabilitada, de todas formas, el buzón del usuario se puede encontrar mediante una búsqueda de directorios. No obstante, si el autor de una llamada externa intenta transferir la llamada al usuario, el sistema emitirá el mensaje: "Lo sentimos. No es posible transferir la llamada a este usuario." Luego, si se ha configurado un operador en el operador automático, la persona que llama será transferida al dicho operador. Si no se ha configurado ningún operador en el operador automático, la llamada será transferida a un operador de plan de marcado, si este ha sido configurado. Si no se ha configurado ninguna extensión de operador en el operador automático habilitado para voz, en el operador automático de reserva DTMF (multifrecuencia de tono dual) o en el plan de marcado, el sistema dará la siguiente respuesta: "Lo sentimos. No están disponibles ni el operador ni el servicio de marcación por tono."

Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario esté habilitado para MU. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para deshabilitar las llamadas de los usuarios que no tienen mensajería unificada habilitada

En este ejemplo, se impide que Tony Smith reciba llamadas de voz de los usuarios que no están habilitados para mensajería unificada.

    Set UMMailbox -Identity tony@contoso.com -AllowUMCallsFromNonUsers None

