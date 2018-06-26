---
title: 'No tiene permisos suficientes para eliminar todos los roles_CannotUninstallDelegatedServer: Exchange 2013 Help'
TOCTitle: No tiene permisos suficientes para eliminar todos los roles_CannotUninstallDelegatedServer
ms:assetid: 214ae6f3-15e7-4337-99e8-40f9547c8e0c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.cannotuninstalldelegatedserver(v=EXCHG.150)
ms:contentKeyID: 48267891
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# No tiene permisos suficientes para eliminar todos los roles\_CannotUninstallDelegatedServer

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar desinstalar todas las funciones del servidor.

El programa de instalación de Exchange 2007 requiere que el usuario que haya iniciado sesión cuando se desinstalen todas las funciones del servidor forme parte del grupo Administradores de la organización de Exchange o el grupo Administradores de la empresa.

Para resolver este problema, conceda al usuario que ha iniciado sesión los permisos de Administrador de organización de Exchange o inscríbalos en el grupo Administradores de la empresa, o bien inicie sesión con una cuenta que tenga dichos permisos y vuelva a ejecutar el programa de instalación de Exchange 2007.

Para obtener más información acerca de los permisos de Active Directory con Microsoft Exchange, consulte "Trabajar con Active Directory permisos en Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

