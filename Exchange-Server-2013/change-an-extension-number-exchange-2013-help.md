---
title: 'Cambiar un número de extensión: Exchange 2013 Help'
TOCTitle: Cambiar un número de extensión
ms:assetid: ff22b366-3bfb-4bf7-9f11-62fba48f1caf
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232208(v=EXCHG.150)
ms:contentKeyID: 50556866
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambiar un número de extensión

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-14_

Cuando se habilita a un usuario para mensajería unificada y se vincula a un plan de marcado de extensiones telefónicas, se crea una dirección de proxy EUM para el usuario que contenga el número de extensión del usuario antes citado. Debe definir al menos un número de extensión para usarlo con la mensajería unificada, de modo que se pueda enviar correo de voz al buzón del usuario. El número de extensión también se usa cuando el usuario llame a un número de Outlook Voice Access.

Puede cambiar el número de extensión principal que se agregó cuando el usuario se habilitó para mensajería unificada o un número de extensión secundaria que se agregara después, junto con las direcciones de proxy EUM relacionadas para el usuario. El número de extensión principal que agregó cuando el usuario se habilitó para mensajería unificada aparece como la dirección de proxy EUM principal. Cualquier número de extensión secundaria adicional que agregara después aparece como la dirección de proxy EUM secundaria. Cuando los números de extensión se cambian, los autores de la llamada pueden dejar correo de voz para el usuario en todos los números de extensión nuevos establecidos. Todos los mensajes de voz se entregarán en el mismo buzón del usuario.

Puede usar la EAC o el Shell para cambiar un número de extensión principal o secundaria para un usuario. Utilice la página **Dirección de correo electrónico** del buzón del usuario en la EAC para cambiar un número de extensión principal o secundaria. No se puede usar la página **Buzón de mensajería unificada** en la EAC para cambiar un número de extensión principal, pero sí para una extensión secundaria. Si desea cambiar un número de extensión secundaria, primero debe quitar el número de extensión secundaria existente y, a continuación, agregar el número de extensión secundaria correcto para el usuario.

Para ver los números de extensión principal y secundaria de un usuario, utilice el cmdlet **Get-UMMailbox** o el cmdlet **Get-Mailbox** en el Shell.

Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de mensajería unificada de extensiones telefónicas. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario se habilitó para mensajería unificada y está vinculado a un plan de marcado de extensiones telefónicas. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el número de extensión que se asignará al usuario contiene el número correcto de dígitos establecidos en el plan de marcado de mensajería unificada.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para cambiar el número de extensión principal o secundaria

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón para el que desea cambiar un número de extensión y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Buzón de usuario**, en **Dirección de correo electrónico**, seleccione el número de extensión que desea cambiar y, a continuación, haga clic en **Eliminar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). El número de extensión principal aparece con letras y números en negrita.

4.  En la página **Dirección de correo electrónico**, en el cuadro **Dirección/extensión**, escriba el nuevo número de extensión para el usuario. Si desea seleccionar un nuevo plan de marcado de mensajería unificada, haga clic en **Examinar**.

5.  Haga clic en **Guardar**.

## Uso del Shell para cambiar el número de extensión principal o secundaria

En este ejemplo, se cambia el número de extensión a 22222 para Tony Smith, un usuario habilitado para mensajería unificada.


> [!NOTE]
> Para poder cambiar un número de extensión a través del Shell, primero debe determinar la posición de la dirección de proxy EUM que desea cambiar. Para determinar la posición, use el comando <STRONG>$mbx.EmailAddresses</STRONG>. La primera dirección de proxy EUM es el número de extensión predeterminado (principal) y será 0 en la lista.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(0)="eum:22222;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

