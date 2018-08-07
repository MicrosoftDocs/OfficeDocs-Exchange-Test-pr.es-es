---
title: 'El servicio de publicación World Wide Web está deshabilitado o falta'
TOCTitle: El servicio de publicación World Wide Web está deshabilitado o missing_ShouldReRunSetupForW3SVC
ms:assetid: f1815a6d-d16b-4271-9fab-84087465529e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.shouldrerunsetupforw3svc(v=EXCHG.150)
ms:contentKeyID: 48268869
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El servicio de publicación World Wide Web está deshabilitado o missing\_ShouldReRunSetupForW3SVC

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque al intentar instalar el servidor de buzones o la función de acceso de cliente encontró que el servicio de publicación World Wide Web o está deshabilitado o bien no está instalado en este equipo.

La instalación de Exchange 2007 requiere que el equipo en el que está instalando Microsoft Exchange tenga instalado el servicio de publicación World Wide Web y se establezca en un valor distinto a deshabilitado.

Para solucionar este problema, compruebe que el servicio de publicación World Wide Web está instalado y no está deshabilitado en el equipo local y, a continuación, vuelva a ejecutar la instalación de Microsoft Exchange.

Para comprobar que el servicio de publicación World Wide Web está instalado y no está deshabilitado

1.  Haga clic con el botón secundario en **Mi PC** y, a continuación, haga clic en **Administrar**.

2.  Expanda el nodo **Servicios y aplicaciones** y, a continuación, haga clic en el nodo **Servicios**.

3.  En el panel derecho, localice **Servicio de publicación World Wide Web**.
    
    Si no se muestra el **Servicio de publicación World Wide Web** en la lista de servicios instalados, siga los pasos que se muestran en el procedimiento siguiente para instalarlo.

4.  Si se muestra el **Servicio de publicación World Wide Web** pero tiene un estado distinto de **Iniciado**, siga los pasos que se muestran a continuación para iniciarlo.

5.  Haga clic con el botón secundario en **Servicio de publicación World Wide Web** y, a continuación, en **Propiedades**.

6.  Compruebe que el **Tipo de inicio** es **Automático** y que el **Estado de servicio** está establecido en **Iniciado**.

7.  Haga clic en **Aplicar** y, después, en **Aceptar**.

Para instalar el servicio de publicación World Wide Web

1.  En el menú **Inicio**, seleccione **Configuración**, **Panel de control** y, a continuación, haga clic en **Agregar o quitar programas**.

2.  Haga clic en **Agregar o eliminar componentes de Windows**.

3.  En la lista **Componentes**, active la casilla de verificación **Servidor de aplicaciones** y, a continuación, haga clic en **Detalles**.

4.  Seleccione **Administrador de servicios de Internet Information Server** y, a continuación, haga clic en **Detalles**.

5.  Seleccione **Servicio World Wide Web** y active la casilla de verificación.

6.  Haga clic en **Aceptar** dos veces para volver a la lista **Componentes** y haga clic en **Siguiente**.

7.  Haga clic en **Finalizar** cuando esté instalado el servicio IIS.

