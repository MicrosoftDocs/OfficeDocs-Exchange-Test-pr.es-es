---
title: 'Habilitar notificaciones de llamadas perdidas para usuario: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Habilitar notificaciones de llamadas perdidas para un usuario
ms:assetid: aa0cbb60-5422-474f-af16-621aade31c1f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232159(v=EXCHG.150)
ms:contentKeyID: 52061862
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar notificaciones de llamadas perdidas para un usuario

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-12-09_

Puede habilitar o deshabilitar las notificaciones de llamadas perdidas en una directiva de buzones de correo de mensajería unificada usando el Shell o el EAC. Una notificación de llamada perdida es un mensaje de correo electrónico que se envía a un usuario cuando éste no responde a una llamada entrante y el autor de la llamada no deja un mensaje de correo de voz. Se trata de un mensaje de correo electrónico diferente al mensaje que contiene el mensaje de voz que se deja para un usuario.

Al deshabilitar las notificaciones de llamadas perdidas en una directiva de buzones de correo de mensajería unificada, se evita que los usuarios asociados a una directiva de buzones de correo de mensajería unificada reciban un mensaje de correo electrónico cuando no respondan a una llamada entrante y el autor de la llamada no deja ningún mensaje de voz. De manera predeterminada, las notificaciones de llamadas perdidas están habilitadas cuando se crea una directiva de buzones de correo de mensajería unificada. También de manera predeterminada, se crea una directiva de buzones de correo de mensajería unificada cada vez que cree un plan de marcado de mensajería unificada.


> [!NOTE]
> Si integra la mensajería unificada y Microsoft Lync Server, las notificaciones de llamadas perdidas no estarán disponibles para los usuarios que tengan un buzón de correo ubicado en un servidor de correo de voz de Exchange 2007 o Exchange 2010 cuando un usuario desconecte antes de que la llamada se envíe a un servidor de buzones de correo que ejecute el servicio de mensajería unificada de Microsoft Exchange.



Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Administrar una directiva de buzones de correo de mensajería unificada](manage-a-um-mailbox-policy-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para habilitar notificaciones de llamadas perdidas para una directiva de buzones de correo de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Directivas de buzón de correo de mensajería unificada**, seleccione la directiva de buzones de correo de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Directivas de buzón de mensajería unificada** \> **General**, marque la casilla al lado de **Permitir notificaciones de llamadas perdidas**.

4.  Haga clic en **Guardar**.

## Uso del Shell para habilitar notificaciones de llamadas perdidas para una directiva de buzones de correo de mensajería unificada

En este ejemplo, se habilitan notificaciones de llamadas perdidas para una directiva de buzón de mensajería unificada denominada `MyUMMailboxPolicy`.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -AllowMissedCallNotifications $true

