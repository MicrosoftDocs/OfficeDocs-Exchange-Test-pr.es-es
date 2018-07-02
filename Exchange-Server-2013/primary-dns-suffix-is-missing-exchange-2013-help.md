---
title: 'Falta el sufijo DNS principal: Exchange 2013 Help'
TOCTitle: Falta el sufijo DNS principal
ms:assetid: 310765bf-a650-4a3d-a5e4-6173b559d4f6
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.fqdnmissing(v=EXCHG.150)
ms:contentKeyID: 61204105
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Falta el sufijo DNS principal

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2014-01-15_

El programa de instalación de Microsoft Exchange Server 2013 no puede continuar porque el sufijo del sistema de nombres de dominio (DNS) del equipo donde va a instalar Exchange no se ha configurado.

Para resolver este problema, agregue un sufijo DNS principal al equipo mediante los pasos siguientes y, después, vuelva a ejecutar el programa de instalación.


> [!IMPORTANT]
> No se permite cambiar el nombre de equipo o el sufijo DNS principal después de instalar Exchange 2013.



1.  Inicie sesión en el equipo donde desea instalar el rol Transporte perimetral como un usuario que sea miembro del grupo Administradores local.

2.  Abra el **Panel de control** y haga doble clic en **Sistema**.

3.  En la sección **Configuración de nombre, dominio y grupo de trabajo del equipo**, haga clic en **Cambiar configuración**.

4.  En la ventana **Propiedades del sistema**, asegúrese de que la pestaña **Nombre de equipo** está seleccionada y, a continuación, haga clic en **Cambiar...**.

5.  En **Cambios en el dominio o en el nombre del equipo**, haga clic en **Más...**.

6.  En **Sufijo DNS principal de este equipo**, escriba el nombre de dominio DNS del servidor de transporte perimetral. Por ejemplo, contoso.com.

7.  Haga clic en **Aceptar** para cerrar cada ventana.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

