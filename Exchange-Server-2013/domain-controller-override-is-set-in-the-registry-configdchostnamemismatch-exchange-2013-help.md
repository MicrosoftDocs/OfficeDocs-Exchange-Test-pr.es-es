---
title: 'Reemplazar de controlador de dominio está establecido en el Registry_ConfigDCHostNameMismatch: Exchange 2013 Help'
TOCTitle: Reemplazar de controlador de dominio está establecido en el Registry_ConfigDCHostNameMismatch
ms:assetid: 3aef5470-d510-4b59-a4b6-36d274a984ae
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.configdchostnamemismatch(v=EXCHG.150)
ms:contentKeyID: 48268019
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Reemplazar de controlador de dominio está establecido en el Registry\_ConfigDCHostNameMismatch

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-15_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar usar el controlador de dominio especificado. Se ha asignado un controlador de dominio de forma estática en el Registro.

El programa de instalación de Exchange 2007 requiere que el controlador de dominio especificado en el comando de instalación coincida con el asignado de forma estática mediante una invalidación del Registro.

Para resolver este problema, vuelva a ejecutar la configuración, especificando el controlador de dominio asignado estáticamente para el parámetro **/DomainController: Parámetro \<***FQDN del* *controlador de dominio asignado estáticamente***\>** .

Para obtener más información acerca de DSAccess y la detección de servicios de directorio, consulte Microsoft Knowledge Base el artículo 250570, "Directory Service Server Detection and DSAccess Usage" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=250570](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=250570)).

