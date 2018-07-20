---
title: 'El equipo local es responsable de ampliar la pertenencia a grupos_ServerIsGroupExpansionServer: Exchange 2013 Help'
TOCTitle: El equipo local es responsable de ampliar la pertenencia a grupos_ServerIsGroupExpansionServer
ms:assetid: 52872561-60e6-4f3d-bbc6-6de0edf74b09
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.serverisgroupexpansionserver(v=EXCHG.150)
ms:contentKeyID: 48268127
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El equipo local es responsable de ampliar la pertenencia a grupos\_ServerIsGroupExpansionServer

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque se produjo un error al intentar desinstalar una función de transporte de concentradores responsable de expandir la pertenencia a grupos.

La instalación de Exchange 2007 requiere que la expansión de la lista de distribución se quite del servidor cabeza de puente actual antes de que se pueda desinstalar la función de transporte de concentradores.

La expansión de las listas de distribución permite la identificación de destinatarios individuales que pertenecen a la lista de distribución que se va a identificar, o la identificación de listas de distribución adicionales para su expansión. Una lista de distribución expandida puede devolver la ruta de cualquier notificación de estado de entrega (DSN) requerida. Las DSN notifican al administrador de Microsoft Exchange o al remitente del correo electrónico del estado de un mensaje de correo electrónico determinado. Además, la expansión de la lista de distribución identifica si se deben enviar los mensajes de Fuera de la oficina o las respuestas generadas automáticamente al remitente del mensaje original.

Para resolver este problema, desplace la expansión del grupo de distribución a otro servidor y vuelva a ejecutar la instalación de Microsoft Exchange.

Para cambiar el servidor de expansión para un grupo de distribución o grupo de distribución dinámico

1.  Abra la Consola de administración de Exchange.

2.  En el árbol de la consola, expanda **Configuración de destinatarios**.

3.  En el árbol de la consola, haga clic en **Grupo de distribución**.

4.  Cree un filtro para ver todos los grupos de distribución y grupos de distribución dinámica que usan el servidor cabeza de puente actual como un servidor de expansión.
    
    1.  En el panel de acciones, haga clic en **Crear filtro**.
    
    2.  En la lista desplegable de propiedades, haga clic en **Servidor de expansión**.
    
    3.  En la lista desplegable de operadores, haga clic en **Es igual a**.
    
    4.  En el cuadro Valor, haga clic en el botón **Examinar** para seleccionar el servidor cabeza de puente que está actuando actualmente como servidor de expansión.


> [!NOTE]
> El siguiente paso es opcional.



1.  Haga clic en **Agregar expresión** para especificar criterios de filtro adicionales. Únicamente se muestran los mensajes que cumplen todos los criterios de filtro.

2.  Haga clic en **Aplicar filtro**. Se muestran los resultados que cumplen con los criterios de filtro.

<!-- end list -->

1.  En el panel de resultados, haga clic en el grupo de distribución para el que desea cambiar el servidor de expansión y, a continuación, haga clic en **Propiedades** en el panel de acciones.

2.  En **Propiedades**, haga clic en la ficha **Avanzadas**.

3.  En la lista desplegable del servidor de expansión, seleccione un servidor específico en la lista o seleccione **Cualquier servidor en la organización**.

4.  Repita los pasos 5 a 7 para todos los grupos de distribución o para los grupos de distribución dinámica que están usando el servidor cabeza de puente como servidor de expansión.

