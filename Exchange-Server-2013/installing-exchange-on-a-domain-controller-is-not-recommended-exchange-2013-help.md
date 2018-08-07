---
title: 'No se recomienda instalar Exchange en un controlador de dominio'
TOCTitle: No se recomienda instalar Exchange en un controlador de dominio
ms:assetid: 48922de2-a68c-4092-96a5-d38c8e5f49f5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.warninginstallexchangerolesondomaincontroller(v=EXCHG.150)
ms:contentKeyID: 48268076
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se recomienda instalar Exchange en un controlador de dominio

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2013-03-22_

El programa de instalación de Microsoft Exchange Server 2013 detectó que el equipo en el que intenta instalar Exchange 2013 es un controlador de dominio de Active Directory. No se recomienda instalar Exchange 2013 en un controlador de dominio.

Si instala Exchange 2013 en un controlador de dominio, tenga en cuenta lo siguiente:

  - No se admite la configuración de Exchange 2013 para permisos divididos de Active Directory.

  - El grupo de seguridad universal (USG) del subsistema de confianza de Exchange se agrega al grupo de administradores de dominio cuando Exchange se instala en un controlador de dominio. Cuando esto ocurre, se concede derechos de administrador de dominio a los servidores Exchange de ese dominio.

  - Exchange Server y Active Directory son aplicaciones que consumen muchos recursos. Cuando ambas se ejecutan en el mismo equipo, hay que tener en cuenta los efectos sobre el rendimiento.

  - Debe asegurarse de que el controlador de dominio en el que se instale Exchange 2013 sea un servidor de catálogo global.

  - Puede que los servicios de Exchange no se inicien correctamente cuando el controlador de dominio sea también un servidor de catálogo global.

  - El apagado del sistema tardará más si los servicios de Exchange no se detienen antes de apagar o reiniciar el servidor.

  - No se puede disminuir un controlador de dominio a un servidor miembro.

  - No se admite la ejecución de Exchange 2013 en un nodo en clúster que también sea un controlador de dominio de Active Directory.

Se recomienda instalar Exchange 2013 en un servidor miembro.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

