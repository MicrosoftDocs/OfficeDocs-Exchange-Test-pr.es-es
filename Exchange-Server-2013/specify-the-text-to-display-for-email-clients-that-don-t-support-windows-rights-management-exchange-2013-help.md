---
title: 'Indicar texto mostrar cliente correo incompatible Windows Rights Management'
TOCTitle: Especificar el texto que se muestra para los clientes de correo electrónico que no son compatibles con Windows Rights Management
ms:assetid: a9b2238a-b534-469c-a0c3-2768bc3d005b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423552(v=EXCHG.150)
ms:contentKeyID: 52061861
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Especificar el texto que se muestra para los clientes de correo electrónico que no son compatibles con Windows Rights Management

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede especificar el texto que se enviará a un usuario cuando reciba un mensaje de voz protegido pero no sea compatible con Information Rights Management (IRM) o Windows Rights Management.

Solo se puede acceder al correo de voz protegido a través de clientes de correo electrónico compatibles con Windows Rights Management o cuando un usuario con mensajería unificada habilitada usa Outlook Voice Access para acceder a un mensaje de voz protegido.

El correo de voz protegido está cifrado. Cuando un mensaje de voz está protegido:

  - El mensaje se marca como privado en Microsoft Outlook y Outlook Web App.

  - El mensaje de voz solo lo puede abrir el destinatario deseado del mensaje de voz.

  - El destinatario puede contestar el mensaje de voz, pero no lo puede reenviar a una persona que no esté incluida en el mensaje de voz original.

Si un mensaje de voz protegido se envía a alguien cuyo cliente de correo electrónico no es compatible con Windows Rights Management y no accede al mensaje con Outlook Voice Access, se le enviará un correo electrónico con el texto que especifique. Este texto debe incluir instrucciones acerca de las acciones que debe realizar el receptor de la llamada para recibir el mensaje de voz protegido.

Para otras tareas de administración relacionadas con los procedimientos de correo de voz protegido, consulte [Procedimientos de correo de voz protegidos](protected-voice-mail-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para obtener instrucciones detalladas, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para especificar el texto que se mostrará a los clientes de correo electrónico no compatibles con Windows Rights Management

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de correo de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de mensajería unificada** \> **Correo de voz protegido** , en **Mensaje para enviar a los usuarios no compatibles con Windows Rights Management**, escriba el texto del mensaje en el cuadro de texto.

4.  Haga clic en **Guardar**.

## Uso del Shell para especificar el texto que se mostrará a los clientes de correo electrónico no compatibles con Windows Rights Management

Este ejemplo especifica el texto que se mostrará a los usuarios asociados con la directiva de buzones de correo de mensajería unificada denominada`MyUMMailboxPolicy` que tiene clientes de correo electrónico no compatibles con Windows Rights Management.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -ProtectedVoiceMailText "Your email client software does not support Protected Voice Mail. Please contact the Help Desk."

