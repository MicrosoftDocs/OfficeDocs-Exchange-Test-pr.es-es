---
title: 'Deshabilitar las llamadas salientes de puertas de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Deshabilitar las llamadas salientes de puertas de enlace IP de mensajería unificada
ms:assetid: a3777cc6-37e4-4359-ada3-a962ac0ef0c3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232153(v=EXCHG.150)
ms:contentKeyID: 49895809
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar las llamadas salientes de puertas de enlace IP de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-13_

Las llamadas salientes para una puerta de enlace IP de mensajería unificada se pueden habilitar y deshabilitar. Cuando desmarca la casilla **Permitir llamadas salientes a través de esta puerta de enlace IP de UM** en las propiedades de la puerta de enlace IP de mensajería unificada, configure la puerta de enlace IP de mensajería unificada para no aceptar ni enviar llamadas salientes a una puerta de enlace IP (VoIP), PBX IP, o Controlador de borde de sesión (SBC). Aunque la opción **Permitir llamadas salientes a través de esta puerta de enlace IP de mensajería unificada** controla si la puerta de enlace IP puede iniciar llamadas salientes para los usuarios, esta no afecta a las transferencias de llamada ni a las llamadas entrantes de una puerta de enlace IP, PBX IP, o SBC.

Para otras tareas de administración relacionadas con puertas de enlace IP de mensajería unificada, consulte [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Use el EAC para deshabilitar las llamadas salientes de una puerta de enlace IP de mensajería unificada

1.  En el CEF, navegue hasta **Mensajería unificada** \> **Puertas de enlace IP de la mensajería unificada**, seleccione la puerta de enlace IP de la mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Puerta de enlace IP de mensajería instantánea**, desmarque la casilla que hay al lado de **Permitir llamadas salientes a través de esta puerta de enlace IP de mensajería unificada**.

3.  Haga clic en **Guardar**.

## Use el Shell para deshabilitar las llamadas salientes de una puerta de enlace IP de mensajería unificada

En este ejemplo, se deshabilitan las llamadas salientes en una puerta de enlace IP de mensajería unificada llamada `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $false

