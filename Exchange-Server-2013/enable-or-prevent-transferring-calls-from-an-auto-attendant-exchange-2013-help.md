---
title: 'Permitir o impedir la transferencia de llamadas de un operador automático'
TOCTitle: Permitir o impedir la transferencia de llamadas de un operador automático
ms:assetid: ca961cc8-cc24-4e05-b72d-79979c155cf9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ee423558(v=EXCHG.150)
ms:contentKeyID: 52061937
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir o impedir la transferencia de llamadas de un operador automático

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede permitir o impedir que los autores de llamadas transfieran llamadas a usuarios a través de un operador automático. Esta opción está habilitada de manera predeterminada y permite que los autores de llamadas transfieran llamadas a usuarios con mensajería unificada habilitada en el plan de marcado de mensajería unificada asociado al operador automático de mensajería unificada.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para permitir o impedir las transferencias de llamadas a usuarios desde un operador automático de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de la mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada en el que quiera configurar la transferencia de llamadas y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **Libreta de direcciones y acceso de operador**, en **Opciones para ponerse en contacto con los usuarios**, active la casilla al lado de **Permitir que los autores de llamadas marquen a usuarios** para permitir que se transfieran llamadas. Para impedir las transferencias de llamadas, desactive esta casilla.

4.  Haga clic en **Guardar**.


> [!NOTE]
> Si desactiva esta casilla y, también, la casilla <STRONG>Permitir que los autores de llamadas dejen mensajes de voz para los usuarios</STRONG>, se deshabilitarán las <STRONG>Opciones para las búsquedas en la libreta de direcciones</STRONG>.



## Usar el Shell para permitir o impedir las transferencias de llamadas a usuarios desde un operador automático de mensajería unificada

En este ejemplo, se impiden las transferencias de llamadas en un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $false

En este ejemplo, se permiten las transferencias de llamadas en un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -AllowDialPlanSubscribers $true

