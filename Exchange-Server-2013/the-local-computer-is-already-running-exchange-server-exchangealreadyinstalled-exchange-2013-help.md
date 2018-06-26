---
title: 'El equipo local está ejecutando Exchange Server_ExchangeAlreadyInstalled: Exchange 2013 Help'
TOCTitle: El equipo local está ejecutando Exchange Server_ExchangeAlreadyInstalled
ms:assetid: 3f168b5d-9910-418f-86fb-e99d852dcb5e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.exchangealreadyinstalled(v=EXCHG.150)
ms:contentKeyID: 48268031
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El equipo local está ejecutando Exchange Server\_ExchangeAlreadyInstalled

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque el equipo local tiene instalados componentes anteriores de Microsoft Exchange.

La instalación de Exchange 2007 requiere que el equipo local no tenga instalados otros componentes existentes de Microsoft Exchange.

Para resolver este problema, elimine cualquier componente de Microsoft Exchange 2000 Server o de Microsoft Exchange Server 2003, y después vuelva a ejecutar la instalación de Microsoft Exchange.

Para eliminar los componentes de Microsoft Exchange

1.  Haga clic en**Inicio**, seleccione **Configuración** y, a continuación, haga clic en **Panel de control**.

2.  Haga doble clic en **Agregar o quitar programas**.

3.  En la lista **Programas actualmente instalados**, haga clic en **Microsoft Exchange** y, a continuación, haga clic en **Cambiar o quitar**.

4.  En el Asistente de instalación de Microsoft Exchange, haga clic en **Siguiente**.

5.  En la lista de acciones de la página Selección de componentes, haga clic en la flecha hacia abajo que está junto a cada componente instalado y, a continuación, haga clic en **Quitar**.
    

    > [!NOTE]
    > Los componentes instalados tienen una marca de verificación en la lista de acciones. Al hacer clic en <STRONG>Quitar</STRONG>, la marca de verificación se sustituye por la palabra <STRONG>Quitar</STRONG>.



6.  Haga clic dos veces en **Siguiente**.

7.  Haga clic en **Finalizar**.

