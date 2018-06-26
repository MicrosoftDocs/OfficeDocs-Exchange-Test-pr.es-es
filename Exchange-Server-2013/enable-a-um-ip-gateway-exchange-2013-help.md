---
title: 'Habilitar una puerta de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Habilitar una puerta de enlace IP de mensajería unificada
ms:assetid: 2706ae06-c45d-41b7-abbe-378a9fca104a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa996857(v=EXCHG.150)
ms:contentKeyID: 49895529
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar una puerta de enlace IP de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-05_

De forma predeterminada, cuando se crea una puerta de enlace IP de mensajería unificada (MU), su estado se establece en habilitado. Sin embargo, puede que tenga que deshabilitar la puerta de enlace IP de mensajería unificada para que esté fuera de línea y no permitir que administre llamadas entrantes y salientes. Después de crear una puerta de enlace IP de mensajería unificada, puede controlar su funcionamiento y funcionalidad estableciendo su variable de estado en habilitada o deshabilitada.

Para otras tareas de administración relacionadas con puertas de enlace IP de mensajería unificada, consulte [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada y que se haya deshabilitado. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar una puerta de enlace IP de mensajería unificada

1.  En el EAC, vaya a \> **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada**, seleccione la puerta de enlace IP de mensajería unificada que desee habilitar y, a continuación, haga clic en **Flecha hacia arriba**![Icono flecha arriba](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif "Icono flecha arriba").

2.  En la página **Advertencia**, haga clic en **Sí**.

## Usar el Shell para habilitar una puerta de enlace IP de MU

El siguiente ejemplo habilita la puerta de enlace IP de MU denominada `MyUMIPGateway`.

    Enable-UMIPGateway -Identity MyUMIPGateway

