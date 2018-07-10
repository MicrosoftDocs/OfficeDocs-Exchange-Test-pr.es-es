---
title: 'Especificación de unidad del grupo de almacenamiento es missing_MailboxLogDriveDoesNotExist: Exchange 2013 Help'
TOCTitle: Especificación de unidad del grupo de almacenamiento es missing_MailboxLogDriveDoesNotExist
ms:assetid: fe210f29-60cb-4d34-877e-1356a21dc02a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.mailboxlogdrivedoesnotexist(v=EXCHG.150)
ms:contentKeyID: 48268917
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Especificación de unidad del grupo de almacenamiento es missing\_MailboxLogDriveDoesNotExist

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 Disaster Recovery no puede continuar porque la instalación de Disaster Recovery no tiene acceso a la especificación de la unidad de grupo de almacenamiento de bases de datos usada en la instalación anterior de este servidor.

La instalación de Microsoft Exchange Disaster Recovery requiere que las mismas especificaciones de la unidad de grupo de almacenamiento de bases de datos usadas por este servidor estén disponibles durante la restauración.

Para resolver esta situación, configure las unidades para que coincidan con la configuración de la unidad lógica original y vuelva a ejecutar la instalación de Microsoft Exchange Disaster Recovery.

Asignar o cambiar la letra de una unidad

1.  Abra **Administración de equipos(Local)**.

2.  En el árbol de la consola, haga clic en **Administración de equipos (Local)**, haga clic en **Almacenamiento** y, a continuación, en **Administración de discos**.

3.  Con el botón secundario, haga clic en una partición, unidad lógica o volumen y, a continuación, haga clic en **Cambiar la letra y rutas de acceso de unidad**.

4.  Utilice uno de los procedimientos siguientes:
    
      - Para asignar una letra de unidad, haga clic en **Agregar**, haga clic en la letra de unidad que desee usar y, a continuación, en **Aceptar**.
    
      - Para modificar una letra de unidad, haga clic en **Cambiar**, haga clic en la letra de unidad que desee usar y, a continuación, en **Aceptar**.

Para obtener más información acerca de cómo asignar letras de unidad, vea "Asignar, cambiar o quitar una letra de unidad" ([https://go.microsoft.com/fwlink/?LinkId=66764](https://go.microsoft.com/fwlink/?linkid=66764)).

