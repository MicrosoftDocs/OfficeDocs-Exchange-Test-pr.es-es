---
title: 'Existe un contenedor Objetos de sistema de Microsoft Exchange duplicado en Active Directory: Exchange 2013 Help'
TOCTitle: Existe un contenedor Objetos de sistema de Microsoft Exchange duplicado en Active Directory
ms:assetid: cd0f45ab-89de-4653-b50d-c1157c2329d5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.adiniterrorrule(v=EXCHG.150)
ms:contentKeyID: 48268709
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Existe un contenedor Objetos de sistema de Microsoft Exchange duplicado en Active Directory

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2013-02-18_

La instalación de Microsoft Exchange Server 2013 no puede continuar porque encontró un contenedor Objetos de sistema de Microsoft Exchange duplicado en el contexto de nomenclatura del dominio de Active Directory. Cuando el programa de instalación encuentra un contenedor Objetos de sistema de Microsoft Exchange duplicado, es necesario eliminar el contenedor duplicado para que se reanude la instalación. Cuando existe un duplicado del contenedor Objetos de sistema de Microsoft Exchange, el problema no puede solucionarse volviendo a ejecutar **DomainPrep**. Deberá identificar y eliminar el contenedor Objetos de sistema de Microsoft Exchange duplicado.

Para resolver este problema, realice los siguientes pasos:

1.  Inicie la sesión en el controlador de dominio con credenciales de administrador.

2.  En **Herramientas administrativas**, haga clic en **Usuarios y equipos de Active Directory**.

3.  En el panel de la consola de administración **Usuarios y equipos de Active Directory**, haga clic en **Ver** en el menú de la barra de herramientas y, a continuación, seleccione **Características avanzadas**.

4.  Busque el contenedor Objetos de sistema de Microsoft Exchange duplicado.

5.  Compruebe que el contenedor Objetos de sistema de Microsoft Exchange duplicado no contenga objetos válidos de Active Directory.

6.  Haga clic con el botón secundario en el contenedor Objetos de sistema de Microsoft Exchange duplicado y, a continuación, haga clic en **Eliminar**.

7.  Confirme la eliminación haciendo clic en **Sí** en el cuadro de diálogo de Active Directory.


> [!NOTE]
> Si desea que el cambio se replique inmediatamente, debe iniciar manualmente la replicación entre controladores de dominio.



¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

