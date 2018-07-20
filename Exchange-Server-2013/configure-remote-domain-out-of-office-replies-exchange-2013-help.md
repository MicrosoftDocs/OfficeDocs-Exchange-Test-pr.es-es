---
title: 'Configurar las respuestas “fuera de la oficina” desde dominios remotos: Exchange 2013 Help'
TOCTitle: Configurar las respuestas “fuera de la oficina” desde dominios remotos
ms:assetid: 0c1e56be-7a29-4294-9762-600f9f788741
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657713(v=EXCHG.150)
ms:contentKeyID: 49895451
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar las respuestas “fuera de la oficina” desde dominios remotos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

Se puede utilizar Exchange Management Shell para configurar los modos de envío y recepción de los mensajes de correo electrónico desde dominios remotos. A continuación se demuestra cómo usar el Shell de administración de Exchange para configurar la forma en que Exchange gestiona las respuestas de oficina.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 10 minutos

  - Solo puede usar el Shell para realizar este procedimiento.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Dominios remotos" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para configurar las respuestas de fuera de la oficina

Puede usar el cmdlet **Set-RemoteDomain** para configurar las propiedades de un dominio remoto.

Este ejemplo deshabilita mensajes de fuera de la oficina para el dominio remoto llamado Contoso.

    Set-RemoteDomain Contoso -AllowedOOFType None

En este ejemplo sólo se permiten mensajes de fuera de la oficina externos.

    Set-RemoteDomain Contoso -AllowedOOFType External

