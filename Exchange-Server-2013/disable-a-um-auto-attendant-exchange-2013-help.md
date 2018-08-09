---
title: 'Deshabilitar a operador automático de mensajería unificada: Exchange 2013 Help'
TOCTitle: Deshabilitar a un operador automático de mensajería unificada
ms:assetid: ad79f374-f68f-430b-8b9c-2c841e1c55ae
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124228(v=EXCHG.150)
ms:contentKeyID: 49895833
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar a un operador automático de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-05_

De forma predeterminada, cuando se crea un operador automático de mensajería unificada (UM), su estado se establece en deshabilitado. Después de crear al operador automático de mensajería unificada, puede cambiar su estado a control si puede responder las llamadas entrantes. Por ejemplo, que desea deshabilitar al operador automático de mensajería unificada cuando está grabando o grabando mensajes personalizados y entradas.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de realizar estos procedimientos, confirme que se ha creado un operador automático de mensajería unificada. Para ver pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md). Confirme también que el estado del operador automático de mensajería unificada se establece en habilitado.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Utilice el CEF para deshabilitar a un operador automático de mensajería unificada

1.  En el CEF, desplácese a la **Mensajería unificada** \> **planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado que desea cambiar y, en la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione al operador automático de mensajería unificada que desea deshabilitar. En la barra de herramientas, haga clic en **flecha abajo**![Icono flecha abajo](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icono flecha abajo")

3.  En la página **Advertencia**, haga clic en **Sí**.

## Usar el Shell para deshabilitar a un operador automático de mensajería unificada

Este ejemplo deshabilita a un operador automático de mensajería unificada denominado `MyUMAutoAttendant`.

    Disable-UMAutoAttendant -Identity MyUMAutoAttendant

