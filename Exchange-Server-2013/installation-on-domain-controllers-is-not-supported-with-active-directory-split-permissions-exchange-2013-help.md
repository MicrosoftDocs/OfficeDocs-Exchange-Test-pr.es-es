---
title: 'No se admite la instalación en controladores de dominio con permisos divididos de Active Directory: Exchange 2013 Help'
TOCTitle: No se admite la instalación en controladores de dominio con permisos divididos de Active Directory
ms:assetid: 977e3758-5e09-40a2-80c1-fe344b1d8a2a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.installondcinadsplitpermissionmode(v=EXCHG.150)
ms:contentKeyID: 48268471
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se admite la instalación en controladores de dominio con permisos divididos de Active Directory

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2012-11-12_

El programa de instalación de Microsoft Exchange Server 2013 detectó que está intentando ejecutar el programa de instalación en un controlador de dominio de Active Directory y se cumple una de las siguientes condiciones:

  - La organización de Exchange ya está configurada para el modo de permisos divididos de Active Directory.

  - Se seleccionó la opción de permisos divididos de Active Directory en el programa de instalación de Exchange 2013.

No se admite la instalación de Exchange 2013 en controladores de dominio cuando la organización de Exchange está configurada para permisos divididos de Active Directory.

Si desea instalar Exchange 2013 en un controlador de dominio, debe configurar la organización de Exchange para permisos divididos de control de acceso basado en roles (RBAC) o permisos compartidos.


> [!IMPORTANT]
> No se recomienda instalar Exchange&nbsp;2013 en controladores de dominio de Active Directory. Para obtener más información, consulte <A href="installing-exchange-on-a-domain-controller-is-not-recommended-exchange-2013-help.md">No se recomienda instalar Exchange en un controlador de dominio</A>.



Si desea seguir usando los permisos divididos de Active Directory, debe instalar Exchange 2013 en un servidor miembro.

Para obtener más información acerca de los permisos compartidos y divididos en Exchange 2013, vea los siguientes temas:

[Descripción de los permisos divididos](understanding-split-permissions-exchange-2013-help.md)

[Configurar Exchange 2013 para permisos divididos](configure-exchange-2013-for-split-permissions-exchange-2013-help.md)

[Configurar Exchange 2013 para permisos compartidos](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md)

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

