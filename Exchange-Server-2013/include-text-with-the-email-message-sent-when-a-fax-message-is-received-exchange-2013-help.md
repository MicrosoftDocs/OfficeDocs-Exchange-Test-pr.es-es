---
title: 'Incluir el texto con el mensaje de correo electrónico que se envía cuando se recibe un mensaje de fax: Exchange 2013 Help'
TOCTitle: Incluir el texto con el mensaje de correo electrónico que se envía cuando se recibe un mensaje de fax
ms:assetid: 48244e58-b7d6-4f0e-bbae-d22bf0fc11ff
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201684(v=EXCHG.150)
ms:contentKeyID: 51406504
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir el texto con el mensaje de correo electrónico que se envía cuando se recibe un mensaje de fax

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-12-09_

Puede incluir un texto adicional en el mensaje de correo electrónico que se envía cuando un usuario habilitado para el correo de voz de mensajería unificada recibe un mensaje de fax y está habilitado para fax, así como también cuando la directiva de buzones de la mensajería unificada se ha configurado correctamente para usar un proveedor socio de fax. De forma predeterminada, el texto que se incluye cuando un usuario habilitado para MU recibe un mensaje de fax indica solamente que el usuario ha recibido el mensaje de fax. No obstante, puede crear un mensaje personalizado agregando texto en el cuadro **Cuando un usuario recibe un mensaje de fax** en una directiva de correo de mensajería unificada. Por ejemplo, el texto puede incluir información acerca de las directivas de seguridad del sistema y describir la forma correcta en que se deben tratar los mensajes de fax en su organización. Después de agregar el texto, este se incluirá en cada mensaje de correo electrónico enviado cuando los usuarios habilitados para MU asociados a la directiva de buzón de MU reciban un mensaje de fax.


> [!NOTE]
> El texto personalizado que acompaña a un mensaje de fax está limitado a 512 caracteres y puede incluir texto plano HTML.



Para obtener más información acerca de los partners de fax, consulte [Microsoft PinPoint para asociados de negocios de Fax](https://go.microsoft.com/fwlink/?linkid=190238).

Para otras tareas de administración relacionadas con los faxes, consulte [Procedimientos de envío de faxes](faxing-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para cambiar el texto incluido en un mensaje de fax

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzón de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzones de mensajería unificada** \> **Texto del mensaje**, en el cuadro de texto **Cuando un usuario recibe un mensaje de fax**, escriba el texto que quiere incluir en el mensaje de correo electrónico que se envía cuando un usuario recibe un mensaje de fax en su buzón.

4.  Haga clic en **Guardar**.

## Usar Shell para cambiar el texto incluido con un mensaje de fax

En este ejemplo, se permite a los usuarios habilitados para MU asociados con una directiva de buzón de MU recibir instrucciones adicionales acerca de cómo abrir un mensaje de fax recibido en su buzón.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -FaxMessageText "To open this fax message, double-click the file attachment."

