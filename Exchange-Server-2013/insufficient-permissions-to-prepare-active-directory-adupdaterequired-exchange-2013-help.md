---
title: 'Permisos insuficientes para preparar Active Directory_ADUpdateRequired: Exchange 2013 Help'
TOCTitle: Permisos insuficientes para preparar Active Directory_ADUpdateRequired
ms:assetid: 1412d8a1-605a-4b1e-bee3-0c97f2cc9e65
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.adupdaterequired(v=EXCHG.150)
ms:contentKeyID: 48267822
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permisos insuficientes para preparar Active Directory\_ADUpdateRequired

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar preparar el dominio.

El programa de instalación de Exchange requiere que el servicio de directorio Active Directorio se modifique para Exchange Server 2007 para que puedan prepararse los dominios en Active Directory.

La cuenta que se usa para ejecutar el comando **setup /PrepareAD** tiene permisos insuficientes para ejecutar este comando incluso si parece pertenecer al grupo Administradores de la empresa. Puede que la cuenta haya expirado.

Para resolver este problema, compruebe que la cuenta del usuario que ha iniciado sesión sea válida y pertenezca al grupo Administradores de la empresa o inicie sesión con una cuenta con esos permisos y vuelva a ejecutar **setup /PrepareAD**.

Para obtener más información acerca de cómo realizar el proceso PrepareAD, consulte "Cómo preparar Active Directory y los dominios" ([https://go.microsoft.com/fwlink/?LinkId=78453](https://go.microsoft.com/fwlink/?linkid=78453)).

Para obtener más información acerca de los permisos de Active Directory necesarios con Microsoft Exchange, consulte "Trabajar con Active Directory permisos en Exchange Server" ([https://go.microsoft.com/fwlink/?LinkId=47592](https://go.microsoft.com/fwlink/?linkid=47592)).

