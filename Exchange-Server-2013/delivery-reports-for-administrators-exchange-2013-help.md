---
title: 'Informes de entrega para administradores: Exchange 2013 Help'
TOCTitle: Informes de entrega para administradores
ms:assetid: d98623d3-e0b7-4cb9-93fb-6351b4a06137
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ919241(v=EXCHG.150)
ms:contentKeyID: 51406555
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Informes de entrega para administradores

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Los informes de entrega para administradores permiten realizar el seguimiento de la información de entrega de los mensajes que se hayan enviado desde un buzón de correo específico de la organización o se hayan recibido desde dicho buzón. De manera específica, los informes de entrega para administradores usan el Centro de administración de Exchange (EAC) para realizar una búsqueda destinada de los registros de seguimiento de mensajes. La búsqueda siempre se asigna a un buzón de correo específico. Puede buscar mensajes enviados por el buzón de correo o enviados al buzón de correo y puede filtrar los resultados de la búsqueda por asunto del mensaje.

En un informe de entrega no se recupera el contenido del cuerpo del mensaje, pero la línea de asunto se muestra en los resultados. Si quiere buscar mensajes de correo electrónico específicos en los buzones de correo de la organización en función del contenido del mensaje, vea [Exhibición de documentos electrónicos en contexto](https://docs.microsoft.com/es-es/exchange/security-and-compliance/data-loss-prevention/integrate-sensitive-information-rules).

Los informes de entrega pueden resultar útiles en las situaciones siguientes:

  - Un administrador realiza un informe no favorable de un empleado porque no presentó un trabajo a tiempo. El empleado insiste en que envió el mensaje con la tarea adjunta. El administrador pide que se compruebe el estado del mensaje.

  - Se ha enviado un boletín de seguridad a los usuarios en el que se solicita una respuesta inmediata, pero nadie ha respondido. ¿Pasan por alto el mensaje o acaso no lo han recibido?

  - Los usuarios se quejan de que nadie está recibiendo mensajes. Comprueban el estado de entrega de su correo pero son incapaces de descubrir qué está pasando. Esto puede deberse a la aplicación de una regla a los mensajes en la organización.

Después de crear una búsqueda de informes de entrega, el informe de entrega resultante mostrará la siguiente información: quién envió el mensaje y a quién lo envió, la línea de asunto y cuando se envió el mensaje. El informe de entrega también muestra el estado de entrega de los mensajes y las razones que motivaron el retraso o el error en la entrega.

## Más información acerca de los informes de entrega

  - Aquí se explica cómo crear un nuevo informe de entrega: [Seguimiento de mensajes con informes de entrega](track-messages-with-delivery-reports-exchange-2013-help.md).

  - Las organizaciones de Exchange locales pueden usar el Shell de administración de Exchange para consultar directamente los registros de seguimiento de mensajes. Para obtener más información, consulte [Buscar en registros seguimiento de mensajes](search-message-tracking-logs-exchange-2013-help.md).

  - Los usuarios pueden hacer un seguimiento de sus propios mensajes. Para más información, vea el tema sobre [informes de entrega para usuarios](https://go.microsoft.com/fwlink/?linkid=279920).

  - Si su organización contiene una versión anterior de Exchange, debe plantearse cómo funciona la característica de informes de entrega en Exchange 2013 a través de las versiones de Exchange.
    
      - Los informes de entrega de Exchange 2013 pueden realizar un seguimiento de los mensajes entre los servidores de Exchange 2010 en el mismo sitio de Active Directory.
    
      - Los informes de entrega de Exchange 2013 no pueden realizar un seguimiento de los mensajes entre los servidores de Exchange 2007 en el mismo sitio de Active Directory. La característica de informes de entrega usa una llamada de procedimiento remoto y una interfaz de servicio web que no existe en Exchange 2007.

