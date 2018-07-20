---
title: 'Asignar una directiva de buzón de mensajería unificada: Exchange 2013 Help'
TOCTitle: Asignar una directiva de buzón de mensajería unificada
ms:assetid: c8da6cbe-3d22-4fff-8b5a-416b1c8adb6c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201728(v=EXCHG.150)
ms:contentKeyID: 49895906
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Asignar una directiva de buzón de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-30_

Cuando habilita a un usuario para utilizar la mensajería unificada (MU) y el correo de voz, debe seleccionar la directiva del buzón de mensajería unificada que se asociará al buzón del usuario. Puede modificar la directiva del buzón de mensajería unificada asociada con el buzón del usuario después de haberlo habilitado para mensajería unificada.

Las directivas de buzón de mensajería unificada se crean para aplicar un conjunto común de directivas u opciones de seguridad a una serie de buzones de usuarios habilitados para mensajería unificada. Puede utilizar las directivas de buzón de mensajería unificada para aplicar ajustes como los siguientes:

  - Directivas de PIN

  - Restricciones de marcado

  - Otras propiedades generales de directivas de buzón de mensajería unificada


> [!NOTE]
> Se crea una directiva de buzón de mensajería unificada estándar cada vez que crea un plan de marcado de mensajería unificada. Puede eliminar las directivas predeterminadas del buzón de mensajería unificada o crear otras nuevas en función de las necesidades de la organización.



Para conocer tareas de administración adicionales relacionadas con los usuarios que están habilitados para correo de voz, consulte [Procedimientos de usuario habilitado para correo de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  2 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que el usuario tiene habilitada la mensajería unificada. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para modificar la directiva del buzón de mensajería unificada asignada a un usuario habilitado para mensajería unificada

1.  En el EAC, vaya a **Destinatarios** \> **Buzones de correo**.

2.  En la vista de lista, seleccione el buzón de correo para el que desee cambiar la directiva de buzón de mensajería unificada.

3.  En el panel de detalles, en **Características de voz y teléfono** \> **Mensajería unificada**, haga clic en **Ver detalles**.

4.  En la página **Buzón de mensajería unificada**, haga clic en **Configuración del buzón de mensajería unificada** y luego, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

5.  En la página **Buzón de mensajería unificada** \>junto a **Directiva del buzón de mensajería unificada**, haga clic en **Examinar** para ubicar la directiva del buzón de mensajería unificada para el usuario.

6.  Haga clic en **Guardar**.

## Uso del Shell para cambiar la directiva de buzón de mensajería unificada asignada a un usuario habilitado para mensajería unificada

En este ejemplo se asocia un usuario habilitado para Mensajería unificada llamado "Tony Smith" con una directiva de buzón de Mensajería unificada denominada `MyUMMailboxPolicy`.

    Set-UMMailbox -Identity tonysmith@contoso.com -UMMailboxPolicy MyUMMailboxPolicy

