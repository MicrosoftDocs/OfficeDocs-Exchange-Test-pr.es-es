---
title: 'Este servidor es el origen de un conector de envío_ServerIsSourceForSendConnector: Exchange 2013 Help'
TOCTitle: Este servidor es el origen de un conector de envío_ServerIsSourceForSendConnector
ms:assetid: 151c0014-c90c-4c52-8e74-4b3f1bc7aaf1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.serverissourceforsendconnector(v=EXCHG.150)
ms:contentKeyID: 48267834
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Este servidor es el origen de un conector de envío\_ServerIsSourceForSendConnector

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar quitar la función del servidor Transporte de concentradores. El equipo local es el origen de uno o varios conectores de envío en la organización de Exchange.

Un conector de envío representa una puerta de enlace lógica por la que se envían los mensajes salientes.

El programa de instalación de Exchange 2007 requiere que todos los conectores de envío de una organización de Exchange se muevan o eliminen del equipo del servidor de transporte de concentradores para que se pueda eliminar la función del servidor.

Para resolver este problema, mueva o elimine todos los conectores de envío del equipo local y después vuelva a ejecutar el programa de instalación.

Para obtener más información acerca de cómo modificar o quitar los conectores de envío, consulte los siguientes temas en la documentación del producto de Exchange Server 2007:

  - "Cómo quitar un conector de envío" ([https://go.microsoft.com/fwlink/?LinkId=86655](https://go.microsoft.com/fwlink/?linkid=86655)).

  - "Cómo modificar la configuración de un conector de envío" ([https://go.microsoft.com/fwlink/?LinkId=86656](https://go.microsoft.com/fwlink/?linkid=86656)).

