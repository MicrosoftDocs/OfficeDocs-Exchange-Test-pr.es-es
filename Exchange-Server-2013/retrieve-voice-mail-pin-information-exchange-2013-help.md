---
title: 'Recuperar información de PIN del correo de voz: Exchange 2013 Help'
TOCTitle: Recuperar información de PIN del correo de voz
ms:assetid: 01517cca-99fe-46b2-b586-19e8d2707728
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa995900(v=EXCHG.150)
ms:contentKeyID: 54652399
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Recuperar información de PIN del correo de voz

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-03_

Puede recuperar la información de PIN de un usuario que está habilitado para mensajería unificada (UM). Cuando se habilita a un usuario para UM y se crea o genera un PIN, este se cifra y se almacena en el buzón del usuario.

Al recuperar información de PIN de un usuario habilitado para UM, la información que se devuelve se calcula usando los datos de PIN cifrados almacenados en el buzón del usuario. Esta tarea le permite ver información del buzón del usuario y también indica si se ha bloqueado el buzón y el usuario no puede acceder.

Para consultar otras tareas relacionadas con la seguridad de PIN, vea [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesito saber antes de empezar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estas tareas, confirme que se haya creado un plan de marcado de UM. Puede ver los pasos detallados en [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estas tareas, confirme que se haya creado una directiva de buzón de mensajería unificada. Puede ver los pasos detallados en [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estas tareas, confirme que el buzón del usuario esté habilitado para la UM. Puede ver los pasos detallados en [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué quiere hacer?

## Usar el EAC para recuperar información de PIN de un usuario habilitado para UM

1.  En la EAC, vaya a **Destinatarios** . En la vista de lista, seleccione el buzón del usuario que quiera ver.

2.  En el panel de detalles, en **Características de voz y teléfono**, haga clic en **Ver detalles**.

3.  En la página **Buzón de mensajería unificada** \> **Configuración de buzón de mensajería unificada**, consulte el **Estado de PIN** del usuario. En esta página también se puede restablecer el PIN del correo de voz del usuario.

## Usar el Shell para recuperar información de PIN de un usuario habilitado para UM

En este ejemplo, se muestra el identificador de usuario, si un PIN ha expirado, si el buzón de UM está bloqueado o si Tony es un usuario nuevo.

    Get-UMMailboxPIN -identity tony@contoso.com

