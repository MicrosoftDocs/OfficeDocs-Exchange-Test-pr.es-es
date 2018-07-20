---
title: 'Actualmente, el protocolo Simple de transferencia de correo es installed_SMTPSvcInstalled: Exchange 2013 Help'
TOCTitle: Actualmente, el protocolo Simple de transferencia de correo es installed_SMTPSvcInstalled
ms:assetid: f786a93c-876d-4f4e-adb6-4dfea3d820d1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.smtpsvcinstalled(v=EXCHG.150)
ms:contentKeyID: 48268893
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Actualmente, el protocolo Simple de transferencia de correo es installed\_SMTPSvcInstalled

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Microsoft® Exchange Server 2007 no puede continuar porque el servicio de Protocolo simple de transferencia de correo (SMTP) de Microsoft Windows® Server™ 2003 está instalado en este equipo.

La instalación de Microsoft Exchange requiere que el servicio SMTP no esté instalado en los servidores que se usan para Exchange 2007.

Para resolver este problema, desinstale el servicio SMTP y vuelva a ejecutar la instalación de Microsoft Exchange.

Para desinstalar el servicio SMTP usando Agregar o quitar componentes de Windows en el Panel de control

1.  En el menú **Inicio**, haga clic en **Panel de control**.

2.  Haga doble clic en **Agregar o quitar programas**.

3.  Haga clic en **Agregar o eliminar componentes de Windows**.

4.  En la lista **Componentes**, active la casilla de verificación **Servidor de aplicaciones** y, a continuación, haga clic en **Detalles**.

5.  Seleccione **Administrador de servicios de Internet Information Server** y, a continuación, haga clic en **Detalles**.

6.  Seleccione **Servicio SMTP** y, a continuación, haga clic para desactivar la casilla de verificación.

7.  Haga clic en **Aceptar** dos veces para volver a la lista **Componentes** y, a continuación, haga clic en **Siguiente**.

8.  Haga clic en **Finalizar** cuando esté desinstalado el servicio SMTP.

