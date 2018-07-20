---
title: 'Incluir el texto con el mensaje de correo electrónico que se envía cuando un usuario está habilitado para correo de voz: Exchange 2013 Help'
TOCTitle: Incluir el texto con el mensaje de correo electrónico que se envía cuando un usuario está habilitado para correo de voz
ms:assetid: 3e8292fb-0cdb-445d-8048-a59af7c38d63
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201679(v=EXCHG.150)
ms:contentKeyID: 51406492
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Incluir el texto con el mensaje de correo electrónico que se envía cuando un usuario está habilitado para correo de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-12-16_

Cuando el buzón de un usuario se habilita para el correo de voz de mensajería unificada, se envía al usuario un mensaje de correo electrónico que le da la bienvenida a la mensajería unificada. Este mensaje contiene la información del PIN que el usuario necesita para acceder por primera vez al sistema de correo de voz.

Dicho mensaje de correo electrónico de bienvenida se puede personalizar agregando texto en el cuadro **Cuando un usuario está habilitado para la mensajería unificada** en una directiva de buzón de mensajería unificada. Puede incluir información como los números de teléfono de asistencia técnica de mensajería unificada o números adicionales de Outlook Voice Access. Una vez agregado el texto, este se incluirá en cada mensaje de correo electrónico que se envíe cuando los usuarios asociados a la directiva de buzón de mensajería unificada estén habilitados para mensajería unificada.


> [!NOTE]
> El texto personalizado que agregue al mensaje de bienvenida se limita a 512 caracteres y puede incluir texto HTML plano.



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

## Usar el EAC para personalizar el texto que se envía cuando se habilita un buzón para mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de correo de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directiva de buzón de mensajería unificada** \> **Texto del mensaje**, en el cuadro de texto **Cuando un usuario está habilitado para mensajería unificada**, escriba el texto que desea incluir en el mensaje de correo electrónico que se envía cuando los usuarios están habilitados para el correo de voz de la mensajería unificada.

4.  Haga clic en **Guardar**.

## Usar el Shell para personalizar el texto que se envía cuando se habilita un buzón para mensajería unificada

En este ejemplo, se les permite a los usuarios habilitados para MU, que están asociados a la directiva de buzones de MU, recibir instrucciones adicionales sobre MU y el  número de Outlook Voice Access que pueden usar para tener acceso al buzón por medio de un teléfono.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -UMEnabledText "You've been enabled for Unified Messaging voice mail. To access your Exchange mailbox, call your internal telephone extension number. From outside your office, call 425-555-1234."

