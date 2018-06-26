---
title: 'Configurar informes de mensajes de dominio remoto: Exchange 2013 Help'
TOCTitle: Configurar informes de mensajes de dominio remoto
ms:assetid: 73dc686a-e7a3-44c7-b82f-f52ff9273199
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ649325(v=EXCHG.150)
ms:contentKeyID: 49895712
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar informes de mensajes de dominio remoto

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

Se puede utilizar Exchange Management Shell para configurar los modos de envío y recepción de los mensajes de correo electrónico desde dominios remotos. Lo siguiente demuestra cómo utilizar el Shell de administración de Exchange para configurar la forma en que Exchange gestiona los informes de entrega y de no entrega.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Solo puede usar el Shell para realizar este procedimiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Dominios remotos" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para configurar los informes de mensajes

Utilice el cmdlet **Set-RemoteDomain** para configurar las propiedades de un dominio remoto.

En este ejemplo se deshabilitan los informes de entrega al dominio remoto Contoso. Esta opción está habilitada de manera predeterminada.

    Set-RemoteDomain Contoso -DeliveryReportEnabled $false

En este ejemplo se deshabilita la no entrega de informes al dominio remoto. Esta opción está habilitada de manera predeterminada.

    Set-RemoteDomain Contoso -NDREnabled $false

