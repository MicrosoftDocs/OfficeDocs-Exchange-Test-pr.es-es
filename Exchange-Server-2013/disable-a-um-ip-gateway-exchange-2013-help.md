---
title: 'Deshabilitar una puerta de enlace IP de MU: Exchange 2013 Help'
TOCTitle: Deshabilitar una puerta de enlace IP de MU
ms:assetid: fe3a8797-1230-49cb-a839-ccec238266b6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb125257(v=EXCHG.150)
ms:contentKeyID: 49896040
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar una puerta de enlace IP de MU

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-13_

De forma predeterminada, cuando se crea una puerta de enlace IP de mensajería unificada (MU), su estado es habilitado. Una vez creada, el estado se puede establecer en deshabilitado para deshabilitar su funcionamiento. Después de deshabilitar la puerta de enlace IP de mensajería unificada, la puerta de enlace de dispositivos de voz sobre IP (VoIP), la central de conmutación (PBX) o el controlador de borde de sesión (SBC) que estén configurados para el uso no podrán procesar llamadas entrantes de mensajería unificada.

Para otras tareas de administración relacionadas con puertas de enlace IP de mensajería unificada, consulte [Procedimientos de puerta de enlace IP de mensajería unificada](um-ip-gateway-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Puertas de enlace IP de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una puerta de enlace IP de mensajería unificada y que esté habilitada. Para obtener instrucciones detalladas, consulte [Cree una puerta de enlace IP de mensajería unificada](create-a-um-ip-gateway-exchange-2013-help.md) y [Habilitar una puerta de enlace IP de mensajería unificada](enable-a-um-ip-gateway-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para deshabilitar una puerta de enlace IP de mensajería unificada

1.  En el EAC, desplácese hasta **Mensajería unificada** \> **Puertas de enlace IP de mensajería unificada**, seleccione la puerta de enlace de mensajería unificada que desea deshabilitar y, luego, haga clic en la **Flecha abajo**![Icono flecha abajo](images/JJ150576.ef5ca57d-a033-457b-bd92-6361877c33d0(EXCHG.150).gif "Icono flecha abajo").

2.  En la página **Advertencia**, haga clic en **Sí**.

## Uso del Shell para deshabilitar una puerta de enlace IP de mensajería unificada

En este ejemplo, se deshabilita una puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway` e se impide que acepte llamadas entrantes de una puerta de enlace VoIP, IP PBX o SBC.

    Disable-UMIPGateway -Identity MyUMIPGateway

En este ejemplo, se deshabilita una puerta de enlace IP de UM denominada `MyUMIPGateway` y desconecta todas las llamadas actuales inmediatamente.

    Disable-UMIPGateway -Identity MyUMIPGateway -Immediate $true

