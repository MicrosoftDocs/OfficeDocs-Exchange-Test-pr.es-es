---
title: 'Incluir el texto con el mensaje de correo electrónico que se envía cuando se recibe un mensaje de voz: Exchange 2013 Help'
TOCTitle: Incluir el texto con el mensaje de correo electrónico que se envía cuando se recibe un mensaje de voz
ms:assetid: b2eec29c-e5eb-4263-80d8-0b9813dd56dc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201718(v=EXCHG.150)
ms:contentKeyID: 51406540
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir el texto con el mensaje de correo electrónico que se envía cuando se recibe un mensaje de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-12-16_

Se puede incluir texto adicional en el mensaje de correo electrónico que se envía cuando un usuario habilitado para mensajería unificada recibe un mensaje de correo de voz. El texto de un mensaje de voz solamente indica de manera predeterminada que el usuario ha recibido un mensaje de voz. No obstante, se puede crear un mensaje personalizado escribiendo texto en el cuadro de texto **Cuando un usuario recibe un mensaje de voz** en una directiva de buzones de correo de mensajería unificada. Por ejemplo, el texto puede incluir información acerca de las directivas de seguridad del sistema y describir el modo correcto de controlar los mensajes de voz en la organización. Tras escribirlo, se incluirá en cada mensaje de correo electrónico que se envíe cuando los usuarios habilitados para mensajería unificada asociados a la directiva de buzones de correo de mensajería unificada reciban un mensaje de voz.


> [!NOTE]
> El contenido del texto personalizado que acompaña a un mensaje de voz está limitado a 512&nbsp;caracteres y puede incluir texto HTML simple.



Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para cambiar el texto incluido en un mensaje de voz

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Directivas de buzón de correo de MU**, seleccione la directiva de buzones de correo de mensajería unificada que quiera administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de MU** \> **Texto del mensaje**, en el cuadro de texto **Cuando un usuario recibe un mensaje de voz**, escriba el texto que desea incluir en el mensaje de correo electrónico que se envía a los usuarios cuando reciben un mensaje de voz.

4.  Haga clic en **Guardar**.

## Uso del Shell para cambiar el texto incluido con un mensaje de voz

En este ejemplo, se incluye el texto adicional "No reenviar mensajes de voz a usuarios ajenos a esta organización", con mensajes de voz que se envían a usuarios asociados con la directiva de buzones de correo de mensajería unificada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailText "Do not forward voice messages to users outside this organization."

