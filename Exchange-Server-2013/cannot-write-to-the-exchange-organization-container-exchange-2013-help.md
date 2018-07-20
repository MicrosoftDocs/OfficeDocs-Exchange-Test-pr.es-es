---
title: 'No se puede escribir en el contenedor de la organización de Exchange: Exchange 2013 Help'
TOCTitle: No se puede escribir en el contenedor de la organización de Exchange
ms:assetid: 17c4667b-7db1-4e0a-b824-1f6d51d980a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.globalserverinstall(v=EXCHG.150)
ms:contentKeyID: 48267845
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se puede escribir en el contenedor de la organización de Exchange

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2014-11-05_

El programa de instalación de Microsoft Exchange Server 2013 no puede continuar porque el usuario que ha iniciado sesión no tiene los permisos de cuenta requeridos para escribir en el contenedor de la organización del servicio de directorio Active Directory.

El programa de instalación requiere que el usuario que inició sesión cuando se instaló Exchange 2013 tenga permisos para crear y modificar objetos en Active Directory. Si va a ejecutar el programa de instalación de Exchange 2013 por primera vez, la cuenta que use debe ser miembro de los grupos de administradores de esquema y administradores de organización. Estos permisos son necesarios porque Active Directory se prepara para Exchange 2013 la primera vez que se ejecuta el programa de instalación. Una vez que Active Directory esté configurado, la cuenta que use para instalar servidores Exchange 2013 adicionales debe ser miembro del grupo de roles de administración de "administración de organización".

Para solucionar este problema, conceda los permisos adecuados al usuario que inició sesión, o bien inicie sesión con una cuenta que tenga dichos permisos y vuelva a ejecutar el programa de instalación de Exchange 2013.


> [!IMPORTANT]
> No se admite la instalación de Exchange&nbsp;2013 entre bosques. Use una cuenta que forme parte del bosque de Active Directory donde vaya a instalar Exchange&nbsp;2013.



¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

