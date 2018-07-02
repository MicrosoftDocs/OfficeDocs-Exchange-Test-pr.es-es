---
title: 'Actualizar Exchange 2013 a la actualización acumulativa o Service Pack más reciente: Exchange 2013 Help'
TOCTitle: Actualizar Exchange 2013 a la actualización acumulativa o Service Pack más reciente
ms:assetid: 928a4a0b-0082-4d50-a696-bfaf2782f42d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ983803(v=EXCHG.150)
ms:contentKeyID: 52062047
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Actualizar Exchange 2013 a la actualización acumulativa o Service Pack más reciente

 

_**Se aplica a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:** 2015-09-04_

Si tiene Microsoft Exchange Server 2013 instalado, puede actualizarlo a la última actualización acumulativa o Service Pack de Exchange 2013. Puede usar el asistente de instalación de Exchange 2013 para actualizar su versión actual de Exchange 2013. Para obtener más información sobre la última actualización acumulativa o Service Pack de Exchange 2013, consulte [Actualizaciones para Exchange 2013](updates-for-exchange-2013-exchange-2013-help.md). Para obtener más información acerca de Exchange 2013, consulte [Novedades en Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).


> [!WARNING]
> Después de actualizar Exchange&nbsp;2013 a una actualización acumulativa o Service Pack más nuevo, no podrá desinstalar la nueva versión para volver a la versión anterior. Si desinstala la nueva versión, quitará Exchange del servidor.



## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 60 minutos

  - Asegúrese de leer las notas de la versión antes de instalar Exchange 2013. Para obtener más información, consulte [Notas de la versión de Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md).

  - Asegúrese de que el servidor en el que va a instalar la actualización acumulativa o el Service Pack cumpla los requisitos del sistema y los requisitos previos. Para obtener más información, consulte [Requisitos del sistema para Exchange 2013](exchange-2013-system-requirements-exchange-2013-help.md) y [Requisitos previos de Exchange 2013](exchange-2013-prerequisites-exchange-2013-help.md).
    

    > [!WARNING]
    > Las configuraciones personalizadas referentes al servidor que lleve a cabo en los archivos de configuración de la aplicación XML de Exchange, por ejemplo, los archivos web.config en los servidores de acceso de cliente o el archivo EdgeTransport.exe.config en los servidores de buzones de correo, se sobrescribirán al instalar la actualización acumulativa o el Service Pack de Exchange. Asegúrese de guardar esta información para que pueda volver a configurar fácilmente su servidor tras la instalación. Vuelva a establecer estas configuraciones después de instalar una actualización acumulativa de Exchange.



  - Después de instalar una actualización acumulativa o un Service Pack, debe reiniciar el equipo para que puedan realizarse los cambios en el Registro y en el sistema operativo.


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Instalar la actualización acumulativa o Service Pack de Exchange 2013

Puede instalar la actualización acumulativo o Service Pack de Exchange 2013 usando el asistente de configuración mediante el modo desatendido. Para obtener instrucciones específicas, consulte los siguientes temas:

  - [Instalar Exchange 2013 utilizando el asistente de configuración](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)

  - [Instalar Exchange 2013 usando el modo desatendido](install-exchange-2013-using-unattended-mode-exchange-2013-help.md)

Si el equipo en el que ha instalado un Service Pack o una actualización acumulativa es miembro de un grupo de disponibilidad de base de datos (DAG), siga los pasos descritos en la sección [Cómo realizar el mantenimiento en los miembros de DAG](managing-database-availability-groups-exchange-2013-help.md) del tema [Administrar grupos de disponibilidad de base de datos](managing-database-availability-groups-exchange-2013-help.md).

