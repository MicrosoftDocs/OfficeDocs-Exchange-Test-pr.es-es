---
title: 'Visor de cola: Exchange 2013 Help'
TOCTitle: Visor de cola
ms:assetid: db892f88-5c13-4607-a38c-8845b35ab8b2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124789(v=EXCHG.150)
ms:contentKeyID: 49895954
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visor de cola

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-09-25_

El visor de cola es un complemento de la Microsoft Management Console que se instala en un servidor de buzones de correo o en el servidor de transporte perimetral. El visor de cola se encuentra en la sección **Herramientas de flujo de correo** de la consola Cuadro de herramientas de Exchange. Esta herramienta se usa no sólo para ver información sobre las colas de un servidor de transporte y sus mensajes, sino también para realizar acciones de administración en dichas colas y en los elementos de correo. El Visor de cola es también útil para solucionar problemas del flujo de correo e identificar correo electrónico no deseado.

Cuando use el Visor de cola para administrar las colas, considere lo siguiente:

  - Debe estar conectado a un servidor de transporte. De manera predeterminada, el visor de cola abre la base de datos de colas en el servidor donde abrió el visor de cola. Sin embargo, también se puede conectar a diferentes servidores. Para obtener más información, consulte [Conectar a un servidor en el visor de cola](connect-to-a-server-in-queue-viewer-exchange-2013-help.md).

  - En función del flujo de correo, la lista de colas y mensajes puede ser muy extensa; esta lista cambia cuando los mensajes entran y salen del servidor. Las opciones del Visor de cola se pueden configurar para controlar el intervalo de actualización de colas y mensajes, y el número de elementos que se muestran en cada página. Para obtener más información, consulte [Establecer las opciones del visor de colas](set-queue-viewer-options-exchange-2013-help.md).

  - Se puede crear un filtro para mostrar un determinado conjunto de colas y mensajes que se deseen supervisar. Una vez ubicadas las colas y mensajes que se desean supervisar, será posible ver la información sobre las propiedades de dichas colas y mensajes. Esta información es útil para solucionar problemas relacionados con el flujo de correo. Para obtener más información, consulte [Filtros de cola](queue-filters-exchange-2013-help.md) y [Filtros de mensajes](message-filters-exchange-2013-help.md).

  - Puede usar el vínculo **Exportar lista** en el panel de acciones para exportar la lista de colas o una lista de mensajes. Para obtener más información, consulte [Exportar listas del visor de cola](export-lists-from-queue-viewer-exchange-2013-help.md).

