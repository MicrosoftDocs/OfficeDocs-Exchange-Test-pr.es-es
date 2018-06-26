---
title: 'El sistema operativo es de depuración mode_OSCheckedBuild: Exchange 2013 Help'
TOCTitle: El sistema operativo es de depuración mode_OSCheckedBuild
ms:assetid: 93a1380f-1388-494d-8f78-92dfefd069bd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.oscheckedbuild(v=EXCHG.150)
ms:contentKeyID: 48268427
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El sistema operativo es de depuración mode\_OSCheckedBuild

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2016-12-15_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La Herramienta Microsoft® Exchange Server Analyzer consulta la clase de Instrumental de administración de Microsoft Windows® (WMI) **Win32\_OperatingSystem** para determinar si hay un valor configurado para la propiedad **Debug**. Si el valor para esta clave en un equipo con Exchange Server es **True**, se muestra un error.

Para cambiar al modo depuración de Windows, agregue el parámetro **/debug** en el archivo Boot.ini. Cuando **/debug** se especifica en el archivo Boot.ini de un equipo con Windows Server, el depurador de núcleo se carga durante el inicio y se mantiene en memoria en todo momento. Esto permite a los profesionales de soporte conectarse al sistema que se esta depurando y llegar hasta el depurador, incluso cuando el sistema no está suspendido en una pantalla de Parada del núcleo. A diferencia del modificador **/crashdebug**, el modificador **/debug** utiliza el puerto COM, tanto si está depurando como si no. Este modificador se utiliza para depurar problemas que pueden reproducirse con regularidad. Es probable que el modificador **/debug** se estableciera como una forma de solucionar un problema y por accidente se dejase así.

Debido a los procesos adicionales que se ejecutan, el rendimiento se resiente considerablemente. Por tanto, no se recomienda ejecutar Exchange Server en un equipo en el que Windows se esté ejecutando en modo depuración.

Para eliminar este error, edite el archivo Boot.ini y elimine el parámetro **/debug**.

## Para solucionar este error

1.  En el Explorador de Windows, vaya a la partición del sistema. Esta es la partición que contiene los archivos específicos del hardware como Boot.ini y NTLDR.

2.  Si no puede ver el archivo Boot.ini, podría ser porque las **Opciones de carpeta** están establecidas en **Ocultar archivos protegidos del sistema operativo**. Si éste es el caso, en la ventana del Explorador de Windows, haga clic en **Herramientas**, **Opciones de carpeta** y, a continuación, haga clic en **Ver**. Borre la casilla de verificación **Ocultar archivos de sistemas operativos protegidos (Recomendado)**. Cuando aparezca, haga clic en **Sí**.

3.  Una vez que el archivo Boot.ini se puede ver en el Explorador de Windows, haga clic con el botón secundario en él, haga clic en **Abrir con** y, a continuación, seleccione **Bloc de notas** para abrir el archivo.

4.  En la sección **\[Sistemas Operativos\]**, elimine el parámetro **/debug**.

5.  Guarde y cierre el archivo y reinicie el equipo con Exchange Server para que el cambio surta efecto.

Para obtener más información acerca de los parámetros que pueden utilizarse en el archivo Boot.ini, consulte el artículo 833721 de Microsoft Knowledge Base, "opciones de modificador disponibles para los archivos de Boot.ini de Windows Server 2003 y Windows XP" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=833721](https://go.microsoft.com/fwlink/?linkid=3052%26kbid=833721)).

