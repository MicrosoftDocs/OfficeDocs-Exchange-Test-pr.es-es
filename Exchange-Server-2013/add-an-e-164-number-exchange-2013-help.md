---
title: 'Agregar un número E.164: Exchange 2013 Help'
TOCTitle: Agregar un número E.164
ms:assetid: fab86207-be03-40ef-9fea-045a50f3d122
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ662762(v=EXCHG.150)
ms:contentKeyID: 50556913
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregar un número E.164

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-14_

Cuando se habilita a un usuario para mensajería unificada y se vincula a un plan de marcado E.164, se crean dos direcciones de proxy EUM. Una que contiene el número de extensión del usuario y otra con un número E.164 para el usuario. El número de extensión se usa cuando el usuario llame a un número de Outlook Voice Access.

El número E.164 principal que agregó cuando el usuario se habilitó para mensajería unificada aparece como la dirección de proxy EUM principal. Si se eliminó el número E.164 principal, la primera dirección de proxy EUM que agregue que contenga el número E.164 del usuario aparecerá como la dirección principal de proxy EUM. Cualquier número E.164 adicional que agregue después aparece como la dirección de proxy EUM secundaria. Cuando se agregan números E.164 adicionales, los autores de la llamada pueden dejar correo de voz para el usuario en todos los números E.164 establecidos. Todos los mensajes de voz se entregarán en el mismo buzón del usuario.

Puede usar la EAC o el Shell para agregar un número E.164 principal o secundario para un usuario. Utilice la página **Dirección de correo electrónico** del buzón del usuario en la EAC para agregar un número E.164 principal o secundario. En la página **Buzón de mensajería unificada** no se pueden agregar números E.164 principales o secundarios.

Para ver los números E.164 principales y secundarios de un usuario, utilice el cmdlet **Get-UMMailbox** o el cmdlet **Get-Mailbox** en el Shell.

Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada E.164. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario se habilitó para mensajería unificada y está vinculado a un plan de marcado E.164. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el número E.164 que se asignará al usuario es válido y tiene un formato correcto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para agregar un número E.164 principal o secundario

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón para el que desea agregar un número E.164 y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Buzón de usuario**, en **Dirección de correo electrónico**, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

4.  En la página **Nueva dirección de correo electrónico**, seleccione **EUM** y, en el cuadro **Dirección/extensión**, escriba el nuevo número E.164 para el usuario.

5.  En la página **Nueva dirección de correo electrónico**, en **Plan de marcado**, haga clic en **Examinar** para seleccionar el plan de marcado E.164 y, a continuación, haga clic en **Aceptar**.

6.  Haga clic en **Guardar**.

## Uso del Shell para agregar un número E.164

En este ejemplo, se agrega un número E.164 para Tony Smith, un usuario habilitado para mensajería unificada.


> [!NOTE]
> Para poder agregar un número E.164 mediante el Shell, debe determinar la posición de la dirección de proxy EUM que desea agregar. Para ello, use el comando <STRONG>$mbx.EmailAddresses</STRONG>. La primera dirección proxy de la lista será 0.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(2)="eum:+14255550123;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

