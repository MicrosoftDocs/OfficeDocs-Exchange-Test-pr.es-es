---
title: 'Permisos insuficientes para ejecutar /PrepareDomain_PrepareDomainNotAdmin: Exchange 2013 Help'
TOCTitle: Permisos insuficientes para ejecutar /PrepareDomain_PrepareDomainNotAdmin
ms:assetid: c33a2bc0-5b07-49b8-a1c1-53baa4933d44
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.preparedomainnotadmin(v=EXCHG.150)
ms:contentKeyID: 48268641
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permisos insuficientes para ejecutar /PrepareDomain\_PrepareDomainNotAdmin

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar ejecutar el proceso **/PrepareDomain**. El usuario que ha iniciado sesión carece de permisos suficientes para realizar el proceso **/PrepareDomain**.

El programa de instalación de Exchange 2007 requiere que el usuario que tenga la sesión iniciada al ejecutar el proceso **/PrepareDomain** sea miembro del grupo Administradores del dominio que se va a preparar, así como miembro del grupo Administradores de la empresa.

Para resolver este problema, conceda al usuario que ha iniciado sesión los permisos del grupo Administradores del dominio para el dominio correspondiente e inscríbalo en los grupos de Administradores de la empresa, o bien, inicie sesión con una cuenta que tenga dichos permisos y vuelva a ejecutar el programa de instalación de Exchange 2007.

Para obtener más información acerca de los permisos de Active Directory necesarios con Microsoft Exchange, consulte "Trabajar con Active Directory permisos en Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

