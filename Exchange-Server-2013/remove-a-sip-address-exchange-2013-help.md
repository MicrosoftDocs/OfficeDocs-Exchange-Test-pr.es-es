---
title: 'Quitar una dirección SIP: Exchange 2013 Help'
TOCTitle: Quitar una dirección SIP
ms:assetid: eaaff0b0-7d85-4845-a7b8-ac22b42bc415
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ662761(v=EXCHG.150)
ms:contentKeyID: 50556903
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una dirección SIP

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-14_

Cuando se habilita a un usuario para la mensajería unificada y se lo vincula a un plan de marcado de URI de SIP, se crean dos direcciones proxy de EUM. Uno contiene el número de extensión del usuario y el otro contiene la dirección SIP para el usuario. El número de extensión se usa cuando el usuario llama a un número de Outlook Voice Access.

Los planes de marcado URI de SIP y las direcciones SIP se usan al integrar la mensajería unificada y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. Communications Server o Lync Server usan la dirección SIP para enrutar las llamadas entrantes y enviar correos de voz al usuario. De manera predeterminada, la dirección SIP que usa la mensajería unificada será la dirección SIP que usen Communications Server o Lync Server.

Puede quitar la dirección principal de SIP que se agregó cuando el usuario se ha habilitado para mensajería unificada o una dirección secundaria de SIP que se ha agregado más adelante, junto con la dirección de proxy EUM para el usuario. La dirección SIP principal que agrega cuando el usuario se ha habilitado para mensajería unificada se mostrarán como la dirección de proxy principal de EUM. Se mostrarán las direcciones SIP adicionales agregadas como direcciones de proxy EUM secundarias. Cuando se quita una dirección SIP, los llamadores ya no pueden dejar el correo de voz para el usuario en la dirección SIP que se ha quitado incluso si el usuario ha iniciado sesión con la dirección SIP asignada al usuario en el servidor de comunicaciones o Lync Server.

Si quita la dirección SIP principal, mensajería unificada no podrá enviar correo de voz a los buzones y llamada reglas de respuesta no se procesará el usuario. Después de que se ha quitado la dirección SIP principal, aparecerá la dirección de proxy EUM para el usuario como **Null** en el buzón del usuario en el CEF y al ejecutar el cmdlet **Get-Mailbox** en el Shell. Además, al ejecutar el cmdlet **Get-UMMailbox** , los parámetros *Extensions*, *PhoneNumber*y *CallAnsweringRulesExtensions* será en blanco o null.

Puede utilizar el CEF o el Shell para quitar principal o una secundaria dirección SIP. Puede utilizar la página de la **Dirección de correo electrónico** en el buzón del usuario en el CEF para quitar principal o una secundaria dirección SIP. No puede utilizar la página de **Buzón de mensajería unificada** en el CEF para quitar una dirección SIP primaria o secundaria.

Puede ver las direcciones SIP principales o secundarias para un usuario con el cmdlet **Get-UMMailbox** o el cmdlet **Get-Mailbox** en el Shell.

Para conocer tareas de administración adicionales relacionadas con los usuarios habilitados para el correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el buzón del usuario ha sido habilitado para mensajería unificada y vinculada a un plan de marcado de URI de SIP. Para ver pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que las direcciones SIP principales y secundarias están configuradas para el usuario.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilice el CEF para quitar la principal o una dirección SIP secundaria

1.  En el EAC, vaya a **Destinatarios** \> **Buzones**.

2.  En la vista de lista, seleccione el buzón que desea quitar una dirección SIP y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Buzón de usuario**, bajo la **dirección de correo electrónico**, seleccione la dirección SIP que desee quitar de la lista y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono"). La dirección de proxy principal de EUM o SIP aparece en números y letras en negrita.

4.  Haga clic en **Guardar**.

## Usar el Shell para quitar la principal o una dirección SIP secundaria

Este ejemplo quita el tsmith@contoso.com dirección SIP desde el buzón de Tony Smith, un usuario habilitado para mensajería unificada.


> [!NOTE]
> Antes de quitar una dirección SIP con el Shell, debe determinar la posición de la dirección de proxy EUM que desea modificar. Para determinar la posición, utilice el comando <STRONG>$mbx.EmailAddresses</STRONG> . La primera dirección de proxy EUM en la lista será 0.



    $mbx = Get-Mailbox tony.smith
    $mbx.EmailAddresses.Item(1) -="eum:tsmith@contoso.com;phone-context=MyDialPlan.contoso.com"
    Set-Mailbox tony.smith -EmailAddresses $mbx.EmailAddresses

