---
title: 'No se puede delegar instalación del primer servidor Exchange en organización'
TOCTitle: No se puede delegar la instalación del primer servidor Exchange en la organización
ms:assetid: 4cf9f1a1-aeac-455b-a5c3-efcd4185a467
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.delegatedclientaccessfirstinstall(v=EXCHG.150)
ms:contentKeyID: 48268106
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# No se puede delegar la instalación del primer servidor Exchange en la organización

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2014-11-05_

El programa de instalación de Microsoft Exchange Server 2013 no puede continuar porque el usuario que ha iniciado sesión no tiene los permisos de cuenta requeridos para instalar el primer servidor de Exchange 2013 en la organización.

Aunque el programa de instalación de Exchange 2013 permite usar la delegación para instalar varios roles de servidor sucesivos, exige que el usuario que ha iniciado sesión sea miembro del grupo de seguridad de Windows de administradores de la organización cuando se instale el primer servidor de Exchange 2013 en la organización. El motivo es que el programa de instalación de Exchange 2013 crea y configura objetos en el contenedor de la organización de Exchange en Active Directory durante la instalación.


> [!NOTE]
> Si no ha preparado el esquema de Active Directory para Exchange&nbsp;2013, el usuario que ha iniciado sesión también debe ser miembro del grupo de seguridad de Windows de administradores de esquema. Otra opción es que otro usuario que sea miembro del grupo de Windows de administración del esquema prepare el esquema de Active Directory antes de instalar Exchange&nbsp;2013.



Para resolver este problema, añada al usuario que tiene iniciada la sesión como miembro del grupo de seguridad de administradores de la organización. O inicie sesión con una cuenta que sea miembro del grupo de seguridad de administradores de la organización. A continuación, vuelva a ejecutar el programa de instalación de Exchange 2013.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

