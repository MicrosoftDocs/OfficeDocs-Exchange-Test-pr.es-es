---
title: 'El usuario que inició sesión no es un miembro del grupo de administradores de esquema: Exchange 2013 Help'
TOCTitle: El usuario que inició sesión no es un miembro del grupo de administradores de esquema
ms:assetid: a4a3f293-afb9-4c00-aa07-c438238b6a98
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.schemaupdaterequired(v=EXCHG.150)
ms:contentKeyID: 48268508
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# El usuario que inició sesión no es un miembro del grupo de administradores de esquema

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2014-12-02_

El programa de instalación de Microsoft Exchange Server 2013 no puede continuar porque la cuenta de usuario que realiza el proceso de actualización de esquema de Active Directory no es miembro de los grupos de administradores de organización o administradores de esquema.

El programa de instalación requiere que el usuario que inició sesión cuando se instaló Exchange 2013 tenga permisos para crear y modificar objetos en Active Directory. Si va a ejecutar el programa de instalación de Exchange 2013 por primera vez, la cuenta que use debe ser miembro de los grupos de administradores de esquema y administradores de organización. Estos permisos son necesarios porque Active Directory se prepara para Exchange 2013 la primera vez que se ejecuta el programa de instalación. Una vez que Active Directory esté configurado, la cuenta que use para instalar servidores Exchange 2013 adicionales debe ser miembro del grupo de roles de administración de "administración de organización".

Para solucionar este problema, conceda los permisos adecuados al usuario que inició sesión, o bien inicie sesión con una cuenta que tenga dichos permisos y vuelva a ejecutar el programa de instalación de Exchange 2013.


> [!IMPORTANT]
> No se admite la instalación de Exchange&nbsp;2013 entre bosques. Use una cuenta que forme parte del bosque de Active Directory donde vaya a instalar Exchange&nbsp;2013.



¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

