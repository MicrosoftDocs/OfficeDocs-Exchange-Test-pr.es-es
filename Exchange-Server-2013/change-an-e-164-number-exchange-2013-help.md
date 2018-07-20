---
title: 'Cambiar un número E.164: Exchange 2013 Help'
TOCTitle: Cambiar un número E.164
ms:assetid: 2a3da11b-bb9b-4d4d-9238-6a1a47ef63f2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335162(v=EXCHG.150)
ms:contentKeyID: 50556752
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambiar un número E.164

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-14_

Cuando se habilita a un usuario para la mensajería unificada y se lo vincula a un plan de marcado de E.164, se crean dos direcciones proxy de EUM. Uno contiene el número de extensión del usuario y el otro contiene el número de E.164 para el usuario. El número de extensión se usa cuando el usuario llama a un número de Outlook Voice Access.

Es posible modificar el número principal de E.164 que se agregó cuando se habilitó la mensajería unificada del usuario o un número secundario de E.164 que se haya agregado posteriormente, junto con las direcciones proxy de EUM del usuario. El número principal de E.164 que se agregó cuando se habilitó a un usuario para la mensajería unificada será la dirección proxy de EUM principal. Los números secundarios de E.164 adicionales que se agreguen aparecerán como direcciones proxy de EUM secundarias. Cuando los números de E.164 se hayan cambiado, los autores de llamadas pueden dejar correos de voz al usuario en todos los números de E.164 nuevos que se hayan configurado. Todos los mensajes de voz se entregarán al mismo buzón de correo del usuario.

Puede usar el Centro de Administración de Exchange o el Shell para cambiar los números principales o secundarios de E.164 para un usuario. Puede usar la página **Dirección de correo electrónico** en el buzón de correo del usuario para cambiar un número principal o secundario de E.164. Sin embargo, no puede usar la página **Buzón de correo de mensajería unificada** en el Centro de Administración de Exchange para cambiar un número principal o secundario de E.164.

Puede ver los números principales o secundarios de E.164 para un usuario con el cmdlet **Get-UMMailbox** o el cmdlet **Get-Mailbox** en el Shell.

Para conocer tareas de administración adicionales relacionadas con los usuarios habilitados para el correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU de E.164. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya habilitado el buzón de correo del usuario para la mensajería unificada y se haya vinculado a un plan de marcado de E.164. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el número de E.164 que se asignará al usuario habilitado para mensajería unificada sea válido.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para cambiar el número principal o secundario de E.164

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón de correo cuyo número de E.164 desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Buzón de usuario**, en **Dirección de correo electrónico**, seleccione el número de E.164 que desea cambiar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar"). El número principal de E.164 aparece en números y letras en negrita.

4.  En la página **Dirección de correo electrónico**, en el cuadro **Dirección/Extensión**, escriba el nuevo número de E.164 del usuario y, luego, haga clic en **Aceptar**. Si necesita seleccionar un nuevo plan de marcado de MU, puede hacer clic en **Examinar**.

5.  Haga clic en **Guardar**.

## Uso del Shell para cambiar el número principal o secundario de E.164

En este ejemplo, se cambia un número de E.164 para Antonio Bermejo, un usuario habilitado para MU.


> [!NOTE]
> Antes de cambiar un número de E.164 con el Shell, debe determinar la ubicación de la dirección proxy de EUM que desea cambiar. Para hacerlo, use el comando <STRONG>$mbx.EmailAddresses</STRONG>. La primera dirección proxy de EUM es el número de E.164 predeterminado (principal) y será 0 en la lista.



    $mbx=Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1)="eum:+14255550123;phone-context=MyE.164DialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

