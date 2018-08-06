---
title: 'Maestro de esquema no ejecuta Windows Server 2003 Service Pack 1 o posterior | Microsoft Docs'
TOCTitle: El maestro de esquema no ejecuta Windows Server 2003 Service Pack 1 o posterior_DomainControllerIsOutOfSite
ms:assetid: 5edbe0b8-7610-4a52-aaaa-38c6a99e7e53
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.domaincontrollerisoutofsite(v=EXCHG.150)
ms:contentKeyID: 48268191
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El maestro de esquema no ejecuta Windows Server 2003 Service Pack 1 o posterior\_DomainControllerIsOutOfSite

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque el controlador de dominio asignado a la función de maestro de esquema del servicio de directorio Active Directory, también conocido como FSMO (del inglés, Flexible Single Master Operations), no está ejecutando Microsoft Windows Server 2003 Service Pack 1 (SP1) o una versión posterior.

La instalación de Exchange 2007 requiere que el controlador de dominio que sirve como FSMO de esquema ejecute el SP1 de Windows Server o una versión posterior.

El FSMO controla todas las actualizaciones y modificaciones que se realizan en el esquema de Active Directory.

Para resolver este problema, realice al menos una de las operaciones siguientes:

  - Actualice el controlador de dominio FSMO a Windows Server 2003 SP1 o una versión posterior y vuelva a ejecutar el programa de instalación de Microsoft Exchange.

  - Si un controlador de dominio FSMO está ejecutando Microsoft Windows Server 2003 Service Pack 1 (SP1) o una versión posterior en la organización de Exchange, ejecute el programa de instalación de Exchange 2007 con el parámetro /domaincontroller señalando a ese controlador de dominio FSMO:
    
    \[*/DomainController*, o */dc\<FQDN of domain controller\>*\]
    
    Use el parámetro */DomainController* para especificar el controlador de dominio que se usará para leer y escribir en Active Directory durante la instalación. Puede usar el nombre NetBIOS o el nombre de dominio completo (FQDN).

Para obtener el service pack más reciente para Windows Server 2003, consulte "Windows Server TechCenter" ([https://go.microsoft.com/fwlink/?LinkId=45315](https://go.microsoft.com/fwlink/?linkid=45315)).

Para obtener más información acerca de los parámetros de instalación de Exchange Server 2007, consulte "Cómo para instalar Exchange 2007 en modo desatendido" ([https://go.microsoft.com/fwlink/?LinkId=86476](https://go.microsoft.com/fwlink/?linkid=86476)) en la documentación del producto Exchange Server 2007.

