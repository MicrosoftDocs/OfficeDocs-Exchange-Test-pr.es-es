---
title: 'Eliminar un plan de marcado de mensajería unificada: Exchange 2013 Help'
TOCTitle: Eliminar un plan de marcado de mensajería unificada
ms:assetid: c9b32ef6-432c-45ca-b94c-31bbcc973128
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124546(v=EXCHG.150)
ms:contentKeyID: 49895907
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminar un plan de marcado de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-11_

Puede eliminar a un plan de marcado de mensajería unificada (UM) existente. Al eliminar el plan de marcado de mensajería unificada, este ya no estará disponible para puertas de acceso de enlace IP de mensajería unificada, directivas de buzón de correo de mensajería unificada y grupos de extensiones de mensajería unificada. No puede eliminar un plan de marcado de mensajería unificada al que hace referencia o al que está asociado con directivas de buzón de correo de mensajería unificada, operadores automáticos de mensajería unificada, puertas de enlace IP de mensajería unificada o grupos de extensiones de mensajería unificada.

Para otras tareas de administración relacionadas con los planes de marcado de mensajería unificada, consulte [Procedimientos de plan de marcado de mensajería unificada](um-dial-plan-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Planes de marcado de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del EAC para eliminar un plan de marcado existente

1.  En la EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**.

2.  En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea eliminar y haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  En la página de advertencia, haga clic en **Sí**.

## Uso de Shell para eliminar un plan de marcado existente

En este ejemplo se elimina un plan de marcado de Mensajería unificada denominado `MyUMDialPlan`.

    RemoveUMDialplan -identity MyUMDialPlan

