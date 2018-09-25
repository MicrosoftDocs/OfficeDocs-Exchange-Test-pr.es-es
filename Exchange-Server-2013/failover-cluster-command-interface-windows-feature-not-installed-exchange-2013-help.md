---
title: 'Característica de Windows Interfaz de comandos de clúster de conmutación por error no instalada: Exchange 2013 Help'
TOCTitle: Característica de Windows Interfaz de comandos de clúster de conmutación por error no instalada
ms:assetid: 0d839514-5ab7-497d-8945-41392b4c3980
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.rsatclusteringcmdinterfaceinstalled(v=EXCHG.150)
ms:contentKeyID: 51406474
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Característica de Windows Interfaz de comandos de clúster de conmutación por error no instalada

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2014-12-03_

El programa de instalación de Microsoft Exchange Server 2013 no puede continuar porque el equipo local no tiene una característica de Windows necesaria. Tendrá que instalar esta característica de Windows para que Exchange 2013 pueda continuar.

El programa de instalación de Exchange 2013 requiere que la característica de Windows **Interfaz de comandos de clúster de conmutación por error** esté instalada en el equipo para poder continuar con la instalación.

Haga lo siguiente para instalar la característica de Windows en este equipo. Si la característica requiere reiniciar el equipo para completar la instalación, salga del programa de instalación de Exchange 2013, reinicie y, a continuación, inicie el programa de instalación de nuevo.


> [!NOTE]
> Es posible que deba instalar características o actualizaciones adicionales de Windows para que el programa de instalación de Exchange&nbsp;2013 pueda continuar. Para obtener una lista completa de las actualizaciones y las características de Windows necesarias, consulte <A href="exchange-2013-prerequisites-exchange-2013-help.md">Requisitos previos de Exchange 2013</A>.



1.  Abra Windows PowerShell en el equipo local.

2.  Ejecute el siguiente comando para instalar la característica necesaria de Windows.
    
```powershell
Install-WindowsFeature RSAT-Clustering-CmdInterface
```

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

¿Encontró lo que buscaba? Tómese un minuto para [enviarnos comentarios](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedbac) sobre la información que deseaba encontrar.

