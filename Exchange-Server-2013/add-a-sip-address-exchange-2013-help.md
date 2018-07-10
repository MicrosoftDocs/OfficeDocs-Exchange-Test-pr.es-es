---
title: 'Agregar una dirección SIP: Exchange 2013 Help'
TOCTitle: Agregar una dirección SIP
ms:assetid: 40295bcf-c62b-4f26-95ca-a8c4bd210fb3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ662760(v=EXCHG.150)
ms:contentKeyID: 50556769
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agregar una dirección SIP

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-14_

Cuando se habilita a un usuario para la mensajería unificada y se lo vincula a un plan de marcado de URI de SIP, se crean dos direcciones proxy de EUM. Uno contiene el número de extensión del usuario y el otro contiene la dirección SIP para el usuario. El número de extensión se usa cuando el usuario llama a un número de Outlook Voice Access.

Los planes de marcado URI de SIP y las direcciones SIP se usan al integrar la mensajería unificada y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. Communications Server o Lync Server usan la dirección SIP para enrutar las llamadas entrantes y enviar correos de voz al usuario. De manera predeterminada, la dirección SIP que usa la mensajería unificada será la dirección SIP que usen Communications Server o Lync Server.

La dirección principal de SIP que se agregó cuando se habilitó a un usuario para la mensajería unificada será la dirección proxy de EUM principal. Si la dirección principal de SIP se eliminó, la primera dirección proxy de EUM que se agregue que contenga la dirección SIP del usuario será la dirección proxy de EUM principal. Las direcciones SIP adicionales que se agreguen serán direcciones proxy de EUM secundarias. Cuando se agreguen direcciones secundarias de SIP, los autores de llamadas pueden dejar correo de voz para el usuario en los extremos de SIP en los que el usuario haya iniciado sesión con las direcciones SIP. Todos los mensajes de voz se entregarán al mismo buzón de correo del usuario.

Puede usar el Centro de Administración de Exchange o el Shell para agregar una dirección SIP principal o secundaria para un usuario. Puede usar la página **Dirección de correo electrónico** en el buzón de correo del usuario en el Centro de Administración de Exchange para agregar una dirección SIP principal o secundaria. No puede usar la página **Buzón de correo de mensajería unificada** en el Centro de Administración de Exchange para agregar una dirección SIP principal o secundaria.

Puede ver las direcciones SIP principales o secundarias para un usuario con el cmdlet **Get-UMMailbox** o el cmdlet **Get-Mailbox** en el Shell.

Para conocer tareas de administración adicionales relacionadas con los usuarios habilitados para el correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU de URI de SIP. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya habilitado el usuario existente para la mensajería unificada y se lo haya vinculado a un plan de marcado de URI de SIP. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que la dirección SIP que se asignará al usuario sea válido y tenga el formato correcto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para agregar una dirección SIP principal o secundaria

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón de correo al que desea agregar una dirección SIP y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Buzón de correo de usuario**, en **Dirección de correo electrónico**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En la página **Nueva dirección de correo electrónico**, seleccione **EUM** y, en el cuadro **Dirección/Extensión**, especifique la nueva dirección SIP para el usuario.

5.  En la página **Nueva dirección de correo electrónico**, en **Plan de marcado**, haga clic en **Examinar** para seleccionar el plan de marcado de URI de SIP y, luego, haga clic en **Aceptar**.

6.  Haga clic en **Guardar**.

## Uso del Shell para añadir una dirección SIP

En este ejemplo, se agrega una dirección SIP para Antonio Bermejo, un usuario habilitado para MU.


> [!NOTE]
> Antes de agregar una dirección SIP con el Shell, debe determinar la ubicación de la dirección proxy de EUM que desea agregar. Para hacerlo, use el comando <STRONG>$mbx.EmailAddresses</STRONG>. La primera dirección proxy de la lista será 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:tsmit@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

