---
title: 'Required_DomainPrepRequired de preparación de dominio: Exchange 2013 Help'
TOCTitle: Required_DomainPrepRequired de preparación de dominio
ms:assetid: f6feae6f-7404-4b1f-887f-ed63c26a6bcd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.domainpreprequired(v=EXCHG.150)
ms:contentKeyID: 48268889
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Required\_DomainPrepRequired de preparación de dominio

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar instalar la función del servidor.

El programa de instalación de Microsoft Exchange requiere que el dominio local esté preparado para Exchange Server 2007 para poder instalar determinadas funciones del servidor.

La preparación del dominio para Exchange Server 2007 consta de las siguientes tareas:

  - Establecer permisos en el contenedor Dominio para Servidores de Exchange, Administradores de la organización de Exchange, Usuarios autenticados y Administradores de buzones de Exchange.

  - Crear el contenedor Objetos de sistema de Microsoft Exchange si no existe y establecer permisos en este contenedor para Servidores de Exchange, Administradores de la organización de Exchange y Usuarios autenticados.

  - Crear un nuevo grupo global de dominios en el dominio actual llamado Servidores de dominio de instalación de Exchange.

  - Agregar el grupo Servidores de dominio de instalación de Exchange al grupo de seguridad universal Servidores de Exchange en el dominio raíz.

Para resolver este problema, ejecute **setup /PrepareDomain** para preparar el dominio local y vuelva a intentar la instalación de la función del servidor.

Para obtener más información acerca de cómo realizar el proceso PrepareDomain, consulte "Cómo preparar Active Directory y los dominios" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

