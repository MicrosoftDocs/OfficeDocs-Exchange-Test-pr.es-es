---
title: 'Incluir el texto con el mensaje de correo electrónico que se envía cuando un restablecimiento de PIN es: Exchange 2013 Help'
TOCTitle: Incluir el texto con el mensaje de correo electrónico que se envía cuando un restablecimiento de PIN es
ms:assetid: f7a4d775-a588-412f-ac2c-11ab1a5c67eb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201750(v=EXCHG.150)
ms:contentKeyID: 51406572
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir el texto con el mensaje de correo electrónico que se envía cuando un restablecimiento de PIN es

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede incluir texto adicional en el mensaje de correo electrónico que se envía a los usuarios después de restablecer su PIN de mensajería unificada o de correo de voz. Para hacerlo, escriba el texto personalizado en el cuadro **Cuando se restablezca el PIN de Outlook Voice Access de un usuario** en una directiva de buzón de mensajería unificada. El texto personalizado puede incluir, por ejemplo, información relacionada con la seguridad para los usuarios habilitados para mensajería unificada.

De manera predeterminada, el sistema de mensajería unificada o de correo de voz restablece los PIN que se usan para Outlook Voice Access si el número de intentos con error supera los 5. Los usuarios también pueden restablecer sus PIN usando las características de mensajería unificada incluidas con Outlook Web App o Outlook 2010, o versiones posteriores, o usando Outlook Voice Access desde un teléfono.


> [!NOTE]
> El texto que escriba en este cuadro se limita a 512&nbsp;caracteres, y es posible incluir texto HTML simple.



Para tareas adicionales relacionadas con la seguridad del PIN de Outlook Voice Access, consulte [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para agregar texto al mensaje de correo electrónico que se envía a los usuarios cuando se restablece su PIN

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzón de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de correo de mensajería unificada** \> **Texto del mensaje**, en el cuadro de texto **Cuando se restablezca el PIN de Outlook Voice Access de un usuario**, escriba el texto que desee incluir en el mensaje de correo electrónico que se envía cuando se restablece el PIN de un usuario.

4.  Haga clic en **Guardar**.

## Usar el Shell para agregar texto al mensaje de correo electrónico que se envía a los usuarios cuando se restablece su PIN

En este ejemplo, se incluye el texto adicional, "Do not share your PIN with other users. Doing so may result in disciplinary action", en el mensaje de correo electrónico que se envía a los usuarios asociados con la directiva de buzón de mensajería unificada `MyUMMailboxPolicy` cuando se restablece su PIN.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ResetPINText "Do not share your PIN with other users. Doing so may result in disciplinary action."

