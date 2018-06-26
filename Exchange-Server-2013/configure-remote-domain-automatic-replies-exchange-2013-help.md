---
title: 'Configurar respuestas automáticas de dominio remoto: Exchange 2013 Help'
TOCTitle: Configurar respuestas automáticas de dominio remoto
ms:assetid: 3d88a1fb-4b62-419a-a50d-ffd868e229d0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657720(v=EXCHG.150)
ms:contentKeyID: 49895585
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar respuestas automáticas de dominio remoto

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

Se puede utilizar Exchange Management Shell para configurar los modos de envío y recepción de los mensajes de correo electrónico desde dominios remotos. A continuación se demuestra cómo usar el Shell de administración de Exchange para configurar la forma en que Exchange gestiona las respuestas automáticas.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Solo puede usar el Shell para realizar este procedimiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Dominio remoto" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para configurar respuestas automáticas

Puede usar el cmdlet **Set-RemoteDomain** para configurar las propiedades de un dominio remoto.

En este ejemplo se permiten respuestas automáticas al dominio remoto denominado Contoso. Esta opción está deshabilitada de forma predeterminada.

    Set-RemoteDomain Contoso -AutoReplyEnabled $true

En este ejemplo se permiten reenvíos automáticos al dominio remoto. Esta opción está deshabilitada de forma predeterminada.

    Set-RemoteDomain Contoso -AutoForwardEnabled $true

