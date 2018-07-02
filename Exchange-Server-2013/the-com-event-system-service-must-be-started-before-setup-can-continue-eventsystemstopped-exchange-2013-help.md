---
title: 'El servicio del sistema de sucesos COM + debe iniciarse antes de que el programa de instalación pueda continue_EventSystemStopped: Exchange 2013 Help'
TOCTitle: El servicio del sistema de sucesos COM + debe iniciarse antes de que el programa de instalación pueda continue_EventSystemStopped
ms:assetid: 3b8d2ba3-87fb-4749-b4d1-5dfec97e1ca4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.eventsystemstopped(v=EXCHG.150)
ms:contentKeyID: 48268010
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El servicio del sistema de sucesos COM + debe iniciarse antes de que el programa de instalación pueda continue\_EventSystemStopped

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

El programa de instalación de Microsoft Exchange Server 2007 no puede continuar porque se produjo un error al intentar instalar las funciones del servidor Acceso de cliente o Transporte perimetral porque el servicio Sistema de eventos COM+ no está iniciado en el equipo de destino.

El programa de instalación de Exchange 2007 requiere que el estado del servicio Sistema de eventos COM+ del equipo donde esté instalando Microsoft Exchange esté establecido en **Iniciado**.

El servicio Sistema de eventos COM+ permite la notificación de eventos del sistema para componentes COM+, lo que proporciona la distribución automática de eventos a los componentes COM suscritos.

Las funciones del servidor Acceso de cliente y Transporte perimetral tienen dependencias de componentes COM+ que se suscriben al servicio Sistema de eventos COM+.

Para resolver este problema, compruebe que el estado del servicio Sistema de eventos COM+ esté establecido en **Iniciado** en el equipo local y, a continuación, vuelva a ejecutar el programa de instalación de Microsoft Exchange.

Para establecer el estado del servicio Sistema de eventos COM+ en 'Iniciado'

1.  Haga clic con el botón secundario en **Mi PC** y, a continuación, haga clic en **Administrar**.

2.  Expanda el nodo **Servicios y aplicaciones** y, a continuación, haga clic en el nodo **Servicios**.

3.  En el panel derecho, ubique el **Sistema de eventos COM+**.

4.  Haga clic con el botón secundario en **Sistema de eventos COM+** y, a continuación, haga clic en **Propiedades**.

5.  Establezca el **Tipo de inicio** en **Automático** y el **Estado del servicio** en **Iniciado**.

6.  Haga clic en **Aplicar** y, después, en **Aceptar**.

