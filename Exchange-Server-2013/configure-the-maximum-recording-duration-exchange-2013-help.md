---
title: 'Configurar la duración máxima de grabación: Exchange 2013 Help'
TOCTitle: Configurar la duración máxima de grabación
ms:assetid: 18eeb567-1048-4c82-93cf-612cb12ec5e3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423539(v=EXCHG.150)
ms:contentKeyID: 49895496
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar la duración máxima de grabación

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-09_

Puede especificar el número máximo de minutos que se permiten para cada grabación de voz cuando una persona que llama deja un mensaje de correo de voz. Este valor puede establecerse en un número entre 1 y 100. Para la mayoría de las organizaciones, el valor debe establecerse de manera predeterminada en 20 minutos. Si el valor establecido es demasiado bajo es posible que los mensajes de voz extensos se desconecten antes de completarse. Si especifica un valor demasiado alto, los usuarios podrán guardar mensajes de voz de larga duración en su bandeja de entrada.

Esta opción es importante si ha fijado cuotas de disco muy estrictas para los usuarios. Se debe establecer en un valor inferior al establecido en **Duración máxima de llamada (minutos)**.

Para obtener más información acerca de otras tareas relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar la duración máxima de la grabación

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de MU que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Plan de marcado de la mensajería unificada**, haga clic en **Configurar**.

4.  En **Configuración**, en **Duración máxima de grabación (minutos)**, introduzca el número en minutos.

5.  Haga clic en **Guardar**.

## Usar el Shell para configurar la duración máxima de la grabación

En este ejemplo, se establece la duración máxima de grabación en 10 minutos para un plan de marcado de MU denominado `MyUMDialPlan`.

    Set-UMDialPlan -identity MyUMDialPlan -MaxRecordingDuration 10

