---
title: 'Desinstalar los paquetes de idioma de la mensajería unificada_AdditionalUMLangPackExists: Exchange 2013 Help'
TOCTitle: Desinstalar los paquetes de idioma de la mensajería unificada_AdditionalUMLangPackExists
ms:assetid: 3a7e2621-0553-44f5-8029-c72fea25af3c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.additionalumlangpackexists(v=EXCHG.150)
ms:contentKeyID: 48268017
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Desinstalar los paquetes de idioma de la mensajería unificada\_AdditionalUMLangPackExists

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al actualizar la función del servidor Mensajería unificada.

El programa de instalación de Exchange requiere que todos los paquetes de idioma de la función del servidor Mensajería unificada, excepto el de inglés de EE.UU., se desinstalen para que pueda continuar la actualización de la función del servidor Mensajería unificada.

Los paquetes de idioma de mensajería unificada que se incluyen con Exchange 2007 contienen mensajes pregrabados y compatibilidad con conversión de texto a voz (TTS) para un idioma determinado.

Los paquetes de idioma de mensajería unificada de Exchange 2007 permiten a los autores de llamadas y a los usuarios de Outlook Voice Access interactuar con el sistema de mensajería unificada en varios idiomas.

Los paquetes de idioma existentes que no estén en inglés de EE.UU. deben desinstalarse para poder instalar los nuevos paquetes de idioma.

Para resolver este problema, desinstale todos los paquetes de idioma de la función del servidor Mensajería unificada, excepto el que está en inglés de EE.UU., y después vuelva a ejecutar el programa de instalación de Exchange 2007.

Para obtener más información acerca de cómo desinstalar los paquetes de idioma de rol de servidor de mensajería unificada, consulte [cómo quitar un idioma paquete de mensajería unificada desde un servidor de mensajería unificada](https://go.microsoft.com/fwlink/?linkid=85973) en la documentación del producto Exchange 2007.

