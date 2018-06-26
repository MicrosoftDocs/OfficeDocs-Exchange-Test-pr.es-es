---
title: 'Ver agentes de transporte en la canalización de transporte: Exchange 2013 Help'
TOCTitle: Ver agentes de transporte en la canalización de transporte
ms:assetid: bd715d8e-7b21-48de-8f68-d425d8506e4c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124395(v=EXCHG.150)
ms:contentKeyID: 51406547
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver agentes de transporte en la canalización de transporte

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-04-08_

Puede usar el Shell de administración de Exchange para ver una lista de los agentes de transporte en la canalización de transporte de los servidores de buzones de correo y servidores de acceso de cliente de Microsoft Exchange Server 2013. De manera específica, el cmdlet **Get-TransportPipeline** muestra información sobre los siguientes tipos de agente de transporte en la canalización de transporte:

  - Agentes basados en las clases **SmtpReceiveAgent**, **RoutingAgent**, **DeliveryAgent** y **StorageAgent** en el servicio de transporte en los servidores de buzones de correo.

  - Agentes basados en **SmtpReceiveAgentClass** en el servicio de entrega de transporte de buzones de correo en los servidores de buzones de correo.

  - Agentes basados en **SmtpReceiveAgentClass** en el servicio de transporte front-end en los servidores de acceso de cliente.

Puede ver una lista de todos los agentes de transporte habilitados que han encontrado mensajes en la ruta de transporte y los eventos SMTP que han registrado. Para obtener más información acerca de los agentes de transporte, vea [Agentes de transporte](transport-agents-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Agentes de transporte" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para ver una lista de agentes de transporte en la ruta de transporte

Ejecute el siguiente comando para usar el Shell con el propósito de ver una lista de agentes de transporte en la canalización de transporte en un servidor Exchange:

    Get-TransportPipeline | Format-List

Ejecute el siguiente comando para exportar los resultados a un archivo de texto denominado C:\\My Documents\\Transport Agents.txt:

    Get-TransportPipeline | Format-List > "C:\My Documents\Transport Agents.txt"

## ¿Cómo saber si el proceso se ha completado correctamente?

Solo los agentes de transporte que detectan mensajes en la canalización de transporte entre el momento en que se inicia el servicio de transporte y el momento en que se ejecuta el cmdlet **Get-TransportPipeline** se muestran mediante el cmdlet. Si un agente de transporte no detecta ningún mensaje en la ruta de transporte, no aparece en los resultados que se muestran mediante el cmdlet **Get-TransportPipeline** incluso si el agente de transporte está habilitado.

