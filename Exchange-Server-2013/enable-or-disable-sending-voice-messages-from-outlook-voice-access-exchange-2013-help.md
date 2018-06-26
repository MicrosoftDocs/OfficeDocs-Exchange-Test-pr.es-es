---
title: 'Habilitar o deshabilitar el envío de mensajes de voz de Outlook Voice Access: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el envío de mensajes de voz de Outlook Voice Access
ms:assetid: 63544ae2-6a28-40b2-82fc-3df83e93ee56
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423546(v=EXCHG.150)
ms:contentKeyID: 52061836
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar el envío de mensajes de voz de Outlook Voice Access

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-12-13_

Puede habilitar o deshabilitar a los usuarios de Outlook Voice Access para que envíen mensajes de correo de voz a otros usuarios habilitados para mensajería unificada que estén asociados al mismo plan de marcado.

Esta opción está habilitada de forma predeterminada. Si deshabilita esta opción, los usuarios de Outlook Voice Access que llamen a un número de Outlook Voice Access no podrán enviar mensajes de voz a los usuarios dentro del mismo plan de marcado.

Para obtener más información acerca de otras tareas relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para permitir o impedir que los usuarios de Outlook Voice Access envíen mensajes de voz a otros usuarios del mismo plan de marcado

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de mensajería unificada**, haga clic en **Configurar**.

4.  En **Transferencia y búsqueda**, en **Permitir a quienes llaman**, seleccione **Dejar mensajes de voz sin llamar al teléfono del usuario** para permitir que se envíen mensajes de voz. Si quiere impedir que los usuarios envíen mensajes de voz, desactive esta opción.

5.  Haga clic en **Guardar**.

## Usar el Shell para permitir o impedir que los usuarios de Outlook Voice Access envíen mensajes de voz a otros usuarios del mismo plan de marcado

Este ejemplo permite que los usuarios de Outlook Voice Access asociados con el plan de marcado denominado `MyUMDialPlan` envíen mensajes de voz a los usuarios asociados con el mismo plan de marcado.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $true

En este ejemplo se impide que los usuarios de Outlook Voice Access asociados con el plan de marcado de mensajería unificada denominado `MyUMDialPlan` envíen mensajes de voz a los usuarios asociados con el mismo plan de marcado.

    Set-UMDialPlan -identity MyUMDialPlan -SendVoiceMsgEnabled $false

