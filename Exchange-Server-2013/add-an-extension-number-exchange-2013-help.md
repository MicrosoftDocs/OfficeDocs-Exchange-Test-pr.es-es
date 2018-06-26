---
title: 'Agregar un número de extensión: Exchange 2013 Help'
TOCTitle: Agregar un número de extensión
ms:assetid: 1a73c9c8-cb50-4bd7-a101-dadd20e28031
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335124(v=EXCHG.150)
ms:contentKeyID: 50556757
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregar un número de extensión

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-14_

Cuando se habilita a un usuario para la mensajería unificada y se lo vincula a un plan de marcado de extensión telefónica, se crea una dirección proxy de EUM para el usuario que tiene el número de extensión del usuario. Debe definir, al menos, un número de extensión para que la mensajería unificada use, de manera que se pueda enviar correo de voz al buzón de correo del usuario. El número de extensión también se usa cuando el usuario llama a un número de Outlook Voice Access.

El número de extensión principal que se agregó cuando se habilitó a un usuario para la mensajería unificada será la dirección proxy de EUM principal. Si el número de extensión principal se eliminó, la primera dirección proxy de EUM que se agregue que contenga el número de extensión del usuario se convertirá en la dirección proxy de EUM principal. Los números de extensión adicionales que se agreguen serán direcciones proxy de EUM secundarias. Si se agregan números de extensión adicionales, los autores de las llamadas podrán dejar un correo de voz para el usuario en todos los números de extensión establecidos. Todos los mensajes de voz se entregarán al mismo buzón de correo del usuario.

Puede usar el Centro de Administración de Exchange o el Shell para agregar un número de extensión principal o secundario para un usuario. Puede usar la página **Dirección de correo electrónico** en el buzón de correo del usuario en el Centro de Administración de Exchange para agregar un número de extensión principal o secundario. No puede usar la página **Buzón de correo de mensajería unificada** en el Centro de Administración de Exchange para agregar un número de extensión principal, pero no para agregar un número de extensión secundario.

Puede ver los números de extensión principales o secundarios para un usuario con el cmdlet **Get-UMMailbox** o el cmdlet **Get-Mailbox** en el Shell.

Para conocer tareas de administración adicionales relacionadas con los usuarios habilitados para el correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU de extensión telefónica. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya habilitado el buzón de correo del usuario para la mensajería unificada y se lo haya vinculado a un plan de marcado de extensión telefónica. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el número de extensión que se asignará al usuario contenga la cantidad correcta de dígitos establecidos en el plan de marcado de MU.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para agregar un número de extensión secundaria

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón al que desea agregar un número de extensión.

3.  En el panel de detalles, en **Características de voz y teléfono**, en **Mensajería unificada**, haga clic en **Ver detalles**.

4.  En la página **Buzón de mensajería unificada**, haga clic en **Otras extensiones** y, luego, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

5.  En la página **Otras extensiones**, al lado del cuadro **Plan de marcado de MU**, haga clic en **Examinar** y ubique el plan de marcado para el usuario.

6.  En la página **Otras extensiones**, en el cuadro **Número de extensión**, escriba el número de extensión y, luego, haga clic en **Aceptar**.

7.  Haga clic en **Guardar**.

## Uso del Centro de Administración de Exchange para agregar un número de extensión principal o secundario

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón de correo al que desea agregar un número de extensión y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Buzón de correo de usuario**, en **Dirección de correo electrónico**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En la página **Nueva dirección de correo electrónico**, seleccione **EUM** y, en el cuadro **Dirección/Extensión**, especifique el número de extensión para el usuario.

5.  En la página **Nueva dirección de correo electrónico**, en **Plan de marcado**, haga clic en **Examinar** para seleccionar el plan de marcado de extensión telefónica y, luego, haga clic en **Aceptar**.

6.  Haga clic en **Guardar**.

## Uso del Shell para agregar un número de extensión

En este ejemplo, se agrega un número de extensión 22222 para Antonio Bermejo, un usuario habilitado para la mensajería unificada.


> [!NOTE]
> Antes de agregar un número de extensión con el Shell, debe determinar la ubicación de la dirección proxy de EUM que desea agregar. Para hacerlo, use el comando <STRONG>$mbx.EmailAddresses</STRONG>. La primera dirección proxy de la lista será 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses +="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

