---
title: 'No se puede quitar la base de datos de buzones: Exchange 2013 Help'
TOCTitle: No se puede quitar la base de datos de buzones
ms:assetid: 5881e4c0-c2e2-48db-84b4-7f9ce3cf46a7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.unwillingtoremovemailboxdatabase(v=EXCHG.150)
ms:contentKeyID: 48268161
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# No se puede quitar la base de datos de buzones

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2012-11-08_

El programa de instalación de Microsoft Exchange Server 2013 no puede continuar porque no puede quitar una base de datos de buzones de usuario del servidor local sin incurrir en una pérdida potencial de datos.

El programa de instalación de Exchange 2013 determina si se eliminaron todas las bases de datos de buzones del servidor antes de que se quite el rol de servidor Buzón de correo. Sin embargo, los buzones de usuario pemanecen en el servidor.

Para solucionar este problema, mueva los buzones del servidor a otro servidor Exchange o, si los buzones y los datos que contienen ya no se necesitan, deshabilite los buzones. A continuación, vuelva a ejecutar el programa de instalación de Exchange 2013.

  - Para obtener más información acerca de cómo identificar un buzón en la base de datos, vea [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)).

  - Para obtener más información acerca de cómo mover un buzón, vea [Movimientos de buzones de Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).

  - Para obtener más información acerca de cómo deshabilitar un buzón, vea [Disable-Mailbox](https://technet.microsoft.com/es-es/library/aa997210\(v=exchg.150\)).

  - Para obtener más información acerca de cómo quitar una base de datos de buzones, vea [Administrar bases de datos de buzones en Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

