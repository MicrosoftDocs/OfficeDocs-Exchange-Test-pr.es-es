---
title: 'Evitar que el indicador de espera de mensaje (MWI) en una puerta de enlace IP de mensajería unificada: Exchange 2013 Help'
TOCTitle: Evitar que el indicador de espera de mensaje (MWI) en una puerta de enlace IP de mensajería unificada
ms:assetid: 7af6d094-199f-4134-a25d-9fc7e9c05fe1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673536(v=EXCHG.150)
ms:contentKeyID: 49895732
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Evitar que el indicador de espera de mensaje (MWI) en una puerta de enlace IP de mensajería unificada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-21_

Puede evitar las notificaciones de correo de voz a los usuarios con respecto a las llamadas recibidas por la puerta de enlace IP de mensajería unificada (MU). Si habilita este ajuste, la puerta de enlace IP de MU puede recibir y enviar mensajes de notificación de SIP para los usuarios. El indicador de mensaje en espera (MWI) está habilitado de forma predeterminada y permite que se envíen notificaciones de mensaje en espera a los usuarios, pero puede apagarlo de acuerdo con sus necesidades.

Un indicador de mensaje en espera notifica al usuario acerca de un mensaje de voz nuevo o sin escuchar. Aparecerá en la Bandeja de entrada en clientes como Outlook y Outlook Web App. También puede ser un mensaje de texto (SMS) enviado a un teléfono móvil registrado, una llamada saliente hecha desde un servidor Exchange a un número que fue configurado para reproducir los mensajes nuevos o una lámpara encendida en el teléfono de escritorio del usuario.


> [!TIP]
> Las notificaciones del MWI también se puede habilitar o deshabilitar en una directiva de buzón de mensajería unificada para un grupo de usuarios.



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

## Usar el EAC para evitar el indicador de mensaje en espera

1.  En el CEF, navegue hasta **Mensajería unificada** \> **Puertas de enlace IP de la mensajería unificada**, seleccione la puerta de enlace IP de la mensajería unificada que desea modificar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Puerta de enlace IP de la mensajería instantánea**, desmarque la casilla que hay al lado de **Permitir indicador de mensaje en espera**.

3.  Haga clic en **Guardar**.

## Usar el Shell para evitar el indicador de mensaje en espera

Este ejemplo impide que el indicador de mensaje en espera se muestre a los usuarios asociados a la puerta de enlace IP de mensajería unificada denominada `MyUMIPGateway` con una dirección IP de 10.10.10.1.

    Set-UMIPGateway -Identity MyUMIPGateway -Address 10.10.10.1 -MessageWaitingIndicatorAllowed $false

