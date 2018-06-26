---
title: 'No se detectaron servidores Exchange 2010 o Exchange 2007: Exchange 2013 Help'
TOCTitle: No se detectaron servidores Exchange 2010 o Exchange 2007
ms:assetid: 789cabab-c769-4a16-a6c8-3db82cff8861
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.noe14serverwarning(v=EXCHG.150)
ms:contentKeyID: 48268306
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se detectaron servidores Exchange 2010 o Exchange 2007

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2012-11-08_

El programa de instalación de Microsoft Exchange Server 2013 mostró esta advertencia porque no existen roles de servidor de Exchange Server 2010 o Exchange Server 2007 en la organización.


> [!WARNING]
> Si continúa con la instalación de Exchange Server 2013, no podrá agregar servidores Exchange 2010 o Exchange 2007 a la organización en el futuro.



Antes de implementar Exchange 2013, tenga en cuenta los siguientes factores que pueden requerir la implementación de servidores Exchange 2010 o Exchange 2007 antes de implementar Exchange 2013:

  - **Aplicaciones de terceros o desarrolladas internamente**   Puede que las aplicaciones desarrolladas para versiones anteriores de Exchange no sean compatibles con Exchange 2013. Debe mantener servidores de Exchange 2010 o Exchange 2007 para admitir estas aplicaciones.

  - **Requisitos de migración o coexistencia**   Si piensa migrar buzones en la organización, puede que algunas soluciones requieran el uso de servidores Exchange 2010 o Exchange 2007.

Si opta por implementar servidores Exchange 2010 o Exchange 2007, deberá hacerlo antes de implementar Exchange 2013. Se debe preparar Active Directory para cada versión de Exchange en el siguiente orden:

1.  Exchange 2007

2.  Exchange 2010

3.  Exchange 2013

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

