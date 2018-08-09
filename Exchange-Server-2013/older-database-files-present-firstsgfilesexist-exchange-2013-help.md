---
title: 'Present_FirstSGFilesExist de archivos base datos antiguos: Exchange 2013 Help'
TOCTitle: Present_FirstSGFilesExist de archivos de base de datos antiguos
ms:assetid: 907faeb8-1c6d-49fc-95a1-417f415a9d79
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.firstsgfilesexist(v=EXCHG.150)
ms:contentKeyID: 48268415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Present\_FirstSGFilesExist de archivos de base de datos antiguos

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque detectó archivos de base de datos de Microsoft Exchange existentes en la ruta de instalación de destino.

La instalación de Exchange 2007 requiere que se vacíe la ruta de instalación de destino de los archivos de base de datos de Microsoft Exchange.

Para resolver este problema, quite todos los archivos existentes de las rutas de instalación de destino y vuelva a ejecutar la instalación.

Para eliminar archivos de base de datos de Exchange Server existentes de la ruta de instalación de destino

1.  En Mi PC o Explorador de Windows, busque la ruta de instalación de destino.
    

    > [!NOTE]
    > De manera predeterminada, los archivos de base de datos están ubicados en:<BR>&lt;systemDrive&gt;:\Archivos de programa\Microsoft\Exchange Server\Mailbox\First Storage Group.



2.  Haga clic con el botón secundario en los archivos que se van a quitar y, a continuación, seleccione **Eliminar**.

3.  En el cuadro de diálogo **Confirmar eliminación de archivos**, haga clic en **Sí**.

4.  Repita los pasos 2 y 3 para todos los archivos de la ruta de instalación de destino.

