---
title: 'No se puede instalar Exchange para un controlador de dominio de solo lectura_ComputerRODC: Exchange 2013 Help'
TOCTitle: No se puede instalar Exchange para un controlador de dominio de solo lectura_ComputerRODC
ms:assetid: 4934d755-65be-47e2-86b0-6ea1ab148a96
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.computerrodc(v=EXCHG.150)
ms:contentKeyID: 48268082
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# No se puede instalar Exchange para un controlador de dominio de solo lectura\_ComputerRODC

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar con la instalación porque el equipo de destino es un controlador de dominio de sólo lectura (RODC).

Los controladores de dominio de sólo lectura son una función de Active Directory de Windows Server 2008. El RODC es un tipo de opción de instalación de controlador de dominio que puede instalarse en sitios remotos que pueden tener niveles inferiores de seguridad física.

El programa de instalación de Exchange requiere acceso de escritura al equipo de instalación de destino.

Para solucionar este problema, seleccione un equipo de destino que no esté designado como RODC y ejecute de nuevo el programa de instalación.

