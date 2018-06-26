---
title: 'Habilitar las llamadas salientes de puertas de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Habilitar las llamadas salientes de puertas de enlace IP de mensajería unificada
ms:assetid: c3ad8e53-d37e-499e-b1f1-defb0ba1bd12
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673562(v=EXCHG.150)
ms:contentKeyID: 49895894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar las llamadas salientes de puertas de enlace IP de mensajería unificada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-13_

Puede habilitar llamadas salientes para una puerta de enlace IP de mensajería unificada (UM) si las llamadas salientes se han deshabilitado. Cuando selecciona la opción **Permitir llamadas salientes mediante esta puerta de enlace IP de mensajería unificada** en las propiedades de la puerta de enlace IP de mensajería unificada, configura esta puerta de enlace para que acepte y envíe llamadas salientes a la puerta de enlace de voz sobre IP (VoIP), la central de conmutación (PBX) habilitada para el protocolo de inicio de sesión (SIP), el IP PBX o los controladores de borde de sesión (SBC). Aunque la opción **Permitir llamadas salientes mediante esta puerta de enlace IP de mensajería unificada** controla si la puerta de enlace IP puede iniciar llamadas salientes para los usuarios, no afecta a las transferencias de llamada ni a las llamadas entrantes de una puerta de enlace de voz sobre IP, una central de conmutación (PBX) habilitada para SIP, IP PBX o SBC.

*Llamada externa* es el concepto que se usa para describir una situación en la que un plan de marcado de mensajería unificada inicia una llamada a un usuario habilitado para mensajería unificada de otro plan de marcado o a un número de teléfono externo.

Para permitir la llamada externa a usuarios habilitados para mensajería, debe:

  - Comprobar que las puertas de enlace IP de mensajería unificada permitan llamadas salientes.

  - Crear grupos de reglas de marcado mediante la creación de entradas de regla de marcado en el plan de marcado de mensajería unificada asociado a la puerta de enlace IP de mensajería unificada.

  - Agregar los grupos de reglas de marcado correctos a la lista de restricciones de marcado en **Autorización de marcado** del plan de marcado de mensajería unificada, operador automático o directiva de buzones de correo de mensajería unificada.

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

## Uso del Centro de Administración de Exchange para habilitar llamadas salientes de una puerta de enlace IP de mensajería unificada

1.  En el CEF, navegue hasta **Mensajería unificada** \> **Puertas de enlace IP de la mensajería unificada**, seleccione la puerta de enlace IP de la mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Puerta de enlace IP de mensajería unificada**, active la casilla de la opción **Permitir llamadas salientes mediante esta puerta de enlace IP de mensajería unificada**.

3.  Haga clic en **Guardar**.

## Uso del Shell para habilitar llamadas salientes de una puerta de enlace IP de mensajería unificada

En este ejemplo, se habilitan las llamadas salientes en una puerta de enlace IP de mensajería unificada, conocida como `MyUMIPGateway`.

    Set-UMIPGateway -Identity MyUMIPGateway -OutcallsAllowed $true

