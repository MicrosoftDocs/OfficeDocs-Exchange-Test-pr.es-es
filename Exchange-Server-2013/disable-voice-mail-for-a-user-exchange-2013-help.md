---
title: 'Deshabilitar el correo de voz para un usuario: Exchange 2013 Help'
TOCTitle: Deshabilitar el correo de voz para un usuario
ms:assetid: cecc9c0d-377d-489e-9db4-d487e9c0b552
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124691(v=EXCHG.150)
ms:contentKeyID: 49895923
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar el correo de voz para un usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

Puede deshabilitar mensajería unificada (UM) para un usuario habilitado para mensajería unificada. Al hacerlo, el usuario ya no puede utilizar las características de correo de voz de mensajería unificada. Si lo prefiere, al deshabilitar mensajería unificada para un usuario, puede mantener la configuración de mensajería unificada para el usuario.

Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva para los buzones de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el usuario existente actualmente tenga la mensajería unificada habilitada. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para deshabilitar la mensajería unificada y el correo de voz para un usuario

1.  En el EAC, haga clic en **Destinatarios**.

2.  El la vista de lista, seleccione el usuario cuyo buzón desea deshabilitar para la mensajería unificada.

3.  En el panel Detalles, en **Características de voz y teléfono**, en **Mensajería unificada**, haga clic en **Deshabilitar**.

4.  En el cuadro **Advertencia**, haga clic en **Sí** para deshabilitar la mensajería unificada para el usuario.

## Usar el Shell para deshabilitar la mensajería unificada y el correo de voz para un usuario

En este ejemplo se deshabilita la mensajería unificada y el correo de voz para el usuario tonysmith@contoso.com, pero se conserva la configuración de buzón de mensajería unificada.

    Disable-UMMailbox -Identity tonysmith@contoso.com -KeepProperties $True

