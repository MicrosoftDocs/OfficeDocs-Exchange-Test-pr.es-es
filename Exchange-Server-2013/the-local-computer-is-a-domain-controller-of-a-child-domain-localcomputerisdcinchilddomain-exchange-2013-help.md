---
title: 'El equipo local es un controlador de dominio de un dominio secundario'
TOCTitle: El equipo local es un controlador de dominio de un dominio secundario_LocalComputerIsDCInChildDomain
ms:assetid: 7db1dcc0-d953-41b8-b081-2a47a70950c4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.localcomputerisdcinchilddomain(v=EXCHG.150)
ms:contentKeyID: 48268334
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El equipo local es un controlador de dominio de un dominio secundario\_LocalComputerIsDCInChildDomain

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque el equipo local es un controlador de dominio de un dominio secundario.

La instalación de Exchange 2007 no se instalará en un controlador de dominio de un dominio secundario a menos que el controlador de dominio sea un servidor de catálogo global.

Para resolver este problema, aumente el nivel del controlador de dominio a servidor de catálogo global o instale Exchange 2007 en un controlador que no sea de dominio, en un servidor miembro, o en el dominio secundario, y luego vuelva a ejecutar la instalación de Microsoft Exchange.

Para corregir esta advertencia al convertir el servidor de Exchange en un servidor de catálogo global

1.  En el controlador de dominio, haga clic en **Inicio**, seleccione **Programas**, haga clic en **Herramientas administrativas** y, a continuación, haga clic en **Sitios y servicios de Active Directory**.

2.  En el árbol de la consola, haga doble clic en **Sitios**, haga doble clic en el nombre del sitio y, después, haga doble clic en **Servidores**.

3.  Haga doble clic en el controlador de dominio de destino.

4.  En el panel de resultados, haga clic con el botón secundario en **Configuración NTDS** y, a continuación, en **Propiedades**.

5.  En la ficha **General**, active la casilla de verificación **Catálogo global**.

6.  Reinicie el controlador de dominio.

