---
title: 'El dominio local debe ser updated_LocalDomainPrep: Exchange 2013 Help'
TOCTitle: El dominio local debe ser updated_LocalDomainPrep
ms:assetid: f33e6785-e85a-495e-a124-ebcb2b763e75
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.localdomainprep(v=EXCHG.150)
ms:contentKeyID: 48268875
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El dominio local debe ser updated\_LocalDomainPrep

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque el usuario que ha iniciado la sesión carece de los permisos de cuenta necesarios para la preparación de dominios.

El programa de instalación de Exchange requiere que el usuario que haya iniciado sesión cuando se ejecute **Setup /PrepareDomain** forme parte de los grupos Administradores de dominio y Administradores de la organización de Exchange, o del grupo Administradores de la empresa.

Para resolver este problema, conceda al usuario que ha iniciado sesión los permisos de Administrador de organización de Exchange y Admins. del dominio, inscríbalos en el grupo Administradores de la empresa, o bien inicie sesión con una cuenta que tenga dichos permisos y vuelva a ejecutar el programa de instalación de Exchange 2007.

Para obtener más información acerca de los permisos de Active Directory necesarios con Microsoft Exchange, consulte "Trabajar con Active Directory permisos en Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

