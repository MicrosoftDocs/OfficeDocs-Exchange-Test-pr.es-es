---
title: 'Habilitar o deshabilitar una regla de contestador automático para un usuario: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar una regla de contestador automático para un usuario
ms:assetid: f9e40ac3-117f-44f6-9ab1-dc9f4c72e8ac
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn140252(v=EXCHG.150)
ms:contentKeyID: 54652420
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar una regla de contestador automático para un usuario

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2015-04-08_

Puede usar el Shell para habilitar o deshabilitar una o más reglas de contestador automático para un usuario. También puede usar los cmdlets **Enable-UMCallAnsweringRule** o **Disable-UMCallAnsweringRule** en un script del Shell de administración de Exchange para habilitar o deshabilitar una o más reglas de contestador automático para varios usuarios.

Las reglas de contestador automático se aplican a las llamadas entrantes de modo similar a la forma en que las reglas de bandeja de entrada se aplican a los mensajes de correo electrónico entrantes. De manera predeterminada, cuando un usuario está habilitado para mensajería unificada (UM), no se configuran reglas de contestador automático. A pesar de ello, el sistema de correo contesta las llamadas entrantes y se pide a las personas que llaman que dejen un mensaje de voz.

Para otras tareas de administración relacionadas con reglas de contestador automático, consulte [Reenvío de llamadas a procedimientos](forwarding-calls-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Reglas de contestador automático de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario esté habilitado para mensajería unificada. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)). Para obtener información sobre cómo usar Windows PowerShell para conectarse a Exchange Online, vea [Conexión a Exchange Online PowerShell](https://go.microsoft.com/fwlink/p/?linkid=396554).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para habilitar una regla de contestador automático

Cuando se crea una regla de contestador automático, esta se encuentra habilitada. Puede usar el Shell para habilitar una regla de contestador automático que se deshabilitó previamente. Al habilitar una regla de contestador automático, se permite al cmdlet **Enable-UMCallAnsweringRule** recuperar la regla, incluidas las condiciones y acciones para una regla de contestador automático especificada.

En este ejemplo se habilita la regla de contestador automático `MyUMCallAnsweringRule` en el buzón de Tony Smith.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

El ejemplo utiliza el modificador *WhatIf* para probar si la regla de contestador automático `MyUMCallAnsweringRule` en el buzón de Tony Smith está lista para habilitarse y si no hay errores en el comando.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

Este ejemplo habilita la regla de contestador automático `MyUMCallAnsweringRule` en el buzón de Tony Smith y solicita al usuario conectado que confirme que se debe habilitar la regla de contestador automático.

    Enable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

## Usar el Shell para deshabilitar una regla de contestador automático

La deshabilitación de una regla de contestador automático evita que esta se recupere y se procese al recibir una llamada entrante. Cuando crea una regla de contestador automático, debería deshabilitarla mientras configura sus condiciones y acciones. Esto impide que la regla se procese al recibir una llamada entrante antes de que se la haya configurado correctamente.

En este ejemplo se deshabilita la regla de contestador automático `MyUMCallAnsweringRule` en el buzón de Tony Smith.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith

En este ejemplo se utiliza el modificador *WhatIf* para probar si la regla de contestador automático `MyUMCallAnsweringRule` en el buzón de Tony Smith está lista para deshabilitarse y si no hay errores en el comando.

    Disable -UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -WhatIf

En este ejemplo se deshabilita la regla de contestador automático `MyUMCallAnsweringRule` en el buzón de Tony Smith y se solicita al usuario conectado que confirme que está deshabilitando la regla de contestador automático.

    Disable-UMCallAnsweringRule -Identity MyUMCallAnsweringRule -Mailbox tonysmith -Confirm

