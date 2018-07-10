---
title: 'Eliminar una puerta de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Eliminar una puerta de enlace IP de mensajería unificada
ms:assetid: 569d3741-67dd-4597-8d28-010011be0c12
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998214(v=EXCHG.150)
ms:contentKeyID: 49895640
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Eliminar una puerta de enlace IP de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Cuando elimina una puerta de enlace IP de mensajería unificada, los servidores Exchange ya no pueden aceptar llamadas entrantes de la puerta de enlace de Voz sobre IP (VoIP), de la central de conmutación (PBX) habilitada para protocolo de inicio de sesión (SIP), de IP PBX ni del controlador de borde de sesión (SBC) asociado con la puerta de enlace IP de mensajería unificada.


> [!IMPORTANT]
> Elimine una puerta de enlace IP de mensajería unificada solo si es totalmente consciente de las implicaciones que conlleva deshabilitar la comunicación con una puerta de enlace VoIP, una PBX IP o un SBC.



Para consultar otras tareas relacionadas con las puertas de enlace IP de mensajería unificada, vea [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada. Para conocer los pasos detallados, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para eliminar una puerta de enlace IP de mensajería unificada

1.  En el Centro de Administración de Exchange, navegue hasta **Mensajería unificada** \> **Puertas de enlace IP de MU**, seleccione la puerta de enlace IP de MU que desea eliminar y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

2.  En la página **Advertencia**, haga clic en **Sí**.

## Usar el Shell para eliminar una puerta de enlace IP de MU

En este ejemplo, se elimina la puerta de enlace IP de MU denominada `MyUMIPGateway`.

    Remove-UMIPGateway -Identity MyUMIPGateway

