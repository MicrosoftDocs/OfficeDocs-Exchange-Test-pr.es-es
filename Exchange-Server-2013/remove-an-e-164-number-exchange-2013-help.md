---
title: 'Quitar un número E.164: Exchange 2013 Help'
TOCTitle: Quitar un número E.164
ms:assetid: 17941918-7dc5-41a0-b540-09f2f907362b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ662759(v=EXCHG.150)
ms:contentKeyID: 50556750
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar un número E.164

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-14_

Cuando se habilita a un usuario para la mensajería unificada y se lo vincula a un plan de marcado de E.164, se crean dos direcciones proxy de EUM. Uno contiene el número de extensión del usuario y el otro contiene el número de E.164 para el usuario. El número de extensión se usa cuando el usuario llama a un número de Outlook Voice Access.

Es posible eliminar el número principal de E.164 que se agregó cuando se habilitó la mensajería unificada del usuario o un número secundario de E.164 que se haya agregado posteriormente, junto con las direcciones proxy de EUM del usuario. El número principal de E.164 que se agregó cuando se habilitó a un usuario para la mensajería unificada será la dirección proxy de EUM principal. Los números de E.164 adicionales que se agreguen serán direcciones proxy de EUM secundarias. Cuando se elimina un número de E.164, los autores de llamadas no pueden dejar correos de voz al usuario en el número de E.164 eliminado.

Si elimina el número de E.164 principal, la mensajería automática no podrá enviar correos de voz al buzón del usuario ni se procesarán las reglas de respuesta a llamada. Después de eliminar el número de E.164 principal, la dirección proxy de EUM para el usuario aparecerá como **Nula** en el buzón del correo del usuario en el Centro de Administración de Exchange y cuando ejecute el cmdlet **Get-Mailbox** en el Shell. Asimismo, cuando ejecute el cmdlet **Get-UMMailbox**, los parámetros *Extensions*, *PhoneNumber* y *CallAnsweringRulesExtensions* estarán en blanco o serán nulos.

Puede usar el Centro de Administración de Exchange o el Shell para eliminar un número de E.164 principal o secundario para un usuario. Puede usar la página **Dirección de correo electrónico** en el buzón de correo del usuario en el Centro de Administración de Exchange para eliminar un número de E.164 principal o secundario. No puede usar la página **Buzón de correo de mensajería unificada** en el Centro de Administración de Exchange para eliminar un número de E.164 principal o secundario.

Puede ver los números principales o secundarios de E.164 para un usuario con el cmdlet **Get-UMMailbox** o el cmdlet **Get-Mailbox** en el Shell.

Para conocer tareas de administración adicionales relacionadas con los usuarios habilitados para el correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo este procedimiento, confirme que se haya creado un plan de marcado de MU de E.164. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya habilitado el buzón de correo del usuario para la mensajería unificada y se haya vinculado a un plan de marcado de E.164. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que los números de E.164 principales o secundarios se hayan configurado para el usuario.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para eliminar el número principal o secundario de E.164

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón de correo cuyo número de E.164 desea eliminar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Buzón de usuario**, en **Dirección de correo electrónico**, seleccione el número de E.164 que desea eliminar de la lista y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono"). La dirección proxy de EUM o número de E.164 principal aparece en números y letras en negrita.

4.  Haga clic en **Guardar**.

## Uso del Shell para eliminar el número de E.164 principal o secundario

En este ejemplo, se quita el número de E.164 a +14255551010 para Tony Smith, un usuario habilitado para mensajería unificada.


> [!NOTE]
> Antes de eliminar un número de E.164 con el Shell, debe determinar la ubicación de la dirección proxy de EUM que desea modificar. Para hacerlo, use el comando <STRONG>$mbx.EmailAddresses</STRONG>. La primera dirección proxy de EUM de la lista será 0.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:+14255551010;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

