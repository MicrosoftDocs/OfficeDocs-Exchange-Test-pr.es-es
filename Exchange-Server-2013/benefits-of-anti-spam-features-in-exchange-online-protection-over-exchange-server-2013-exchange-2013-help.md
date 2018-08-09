---
title: 'Ventajas antispam de Exchange Online Protection frente a Exchange Server 2013'
TOCTitle: Ventajas de las características contra correo no deseado de Exchange Online Protection en Exchange Server 2013
ms:assetid: 00e37a3c-3fbc-488f-bdad-d52a3c80fd72
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673032(v=EXCHG.150)
ms:contentKeyID: 49895433
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Ventajas de las características contra correo no deseado de Exchange Online Protection en Exchange Server 2013

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2016-05-26_

A continuación se indican las ventajas de usar la protección contra correo no deseado de Exchange en la nube (Microsoft Exchange Online o Microsoft Exchange Online Protection) en lugar de Microsoft Exchange Server 2013, que tiene la mayor parte de las mismas capacidades integradas contra correo no deseado que Microsoft Exchange Server 2010:

  - **Más control y configuración más sencilla**: los administradores pueden usar la consola de administración basada en web de Centro de administración de Exchange (EAC) para personalizar la configuración de los filtros de correo no deseado de modo que satisfagan mejor las necesidades de la organización. No existe una interfaz de usuario contra el correo no deseado en Exchange Server 2013. Las características de protección EOP contra correo no deseado están incluidas en Exchange Online

  - **Filtrado de conexiones más potente**: en Exchange 2013, las listas de direcciones IP permitidas y bloqueadas del filtrado de conexiones solo están disponibles al instalar un servidor de transporte perimetral en la red perimetral. Para más información, consulte [Servidores de transporte perimetral](edge-transport-servers-exchange-2013-help.md). En la nube, puede elegir omitir el filtrado de correo no deseado en los mensajes de correo procedentes de remitentes de confianza (recopilados de distintos orígenes de terceros) para garantizar que estos mensajes no se confundan por error con correo no deseado. Además, el servicio de filtrado hospedado usa las propias listas de bloqueo de Microsoft y listas agregadas de varios proveedores para ofrecer un filtrado mejor a nivel de IP.

  - **Filtrado de contenido más potente**: puede configurar fácilmente la directiva de filtrado para:
    
      - Filtrar mensajes escritos en idiomas concretos.
    
      - Filtrar los mensajes enviados desde ciertos países o regiones.
    
      - Marcar mensajes de correo masivo (como anuncios y correos de marketing) como correo no deseado.
    
      - Buscar atributos en un mensaje y actuar en el mensaje si coincide con determinado atributo de opción de correo no deseado avanzado. Si le preocupa la suplantación de identidad (phishing), algunas de estas opciones ofrecen una combinación de identificador de remitente y tecnologías SPF para autenticar y comprobar que los mensajes no están falsificados.
    
    Además de las opciones de filtrado de contenido anteriores que puede configurar en el EAC, el servicio de filtrado hospedado usa listas de URL adicionales para bloquear mensajes sospechosos que contengan URL concretas en el cuerpo del mensaje.

  - **Actualizaciones más rápidas**: las actualizaciones de correo no deseado se propagan más rápidamente a través de la red. En Exchange Server 2013 las actualizaciones se hacen dos veces al mes, mientras que el servicio se actualiza varias veces cada hora.

  - **Filtrado saliente**: el filtrado de correo no deseado saliente siempre está habilitado si usa el servicio hospedado para enviar mensajes de correo, lo que protege a las organizaciones que usan el servicio y a sus destinatarios.

