---
title: 'Componentes de compatibilidad con IIS 6 no instalados_LonghornIIS6MgmtConsoleNotInstalled: Exchange 2013 Help'
TOCTitle: Componentes de compatibilidad con IIS 6 no instalados_LonghornIIS6MgmtConsoleNotInstalled
ms:assetid: 8358eafb-def7-4b8d-8fe1-623bc5a0e20e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.longhorniis6mgmtconsolenotinstalled(v=EXCHG.150)
ms:contentKeyID: 48268355
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componentes de compatibilidad con IIS 6 no instalados\_LonghornIIS6MgmtConsoleNotInstalled

 

_**Se aplica a:**Exchange Server_

_**Última modificación del tema:**2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft®Exchange Server 2007 Setup no puede continuar su intento de instalar el rol de servidor Acceso de clientes, el rol de servidor Buzón de correo ni las herramientas administrativas de Exchange 2007 en los siguientes sistemas operativos Windows:

  - Windows Server 2008 R2

  - Windows Server 2008

  - Windows 7 (sólo herramientas administrativas)

  - Windows Vista (sólo herramientas administrativas)

Este problema se produce debido a que el componente Compatibilidad con metabase IIS 6 de Internet Information Server y el componente de la Consola de administración IIS 6 no están instalados.

El programa de instalación de Exchange 2007 requiere que el equipo donde esté instalando el rol de servidor Acceso de cliente de Exchange 2007, el rol de servidor Buzón de correo o las Herramientas administrativas de Exchange 2007 tenga instalado el componente Compatibilidad con metabase IIS 6 y Consola de administración IIS 6.

Para solucionar este problema, instale el componente Compatibilidad con metabase IIS 6 en el equipo de destino y vuelva a ejecutar el Microsoft Exchange Setup.

Instale los componentes Compatibilidad con la administración de IIS 6.0 en Windows Server 2008 R2 o en Windows Server usando la herramienta Administrador de servidores

1.  Haga clic en **Inicio**, seleccione **Herramientas administrativas** y, a continuación, haga clic en **Administrador de servidores**.

2.  En el panel de navegación izquierdo, expanda **Roles** y, a continuación, haga clic con el botón secundario en **Servidor web (IIS)** y, a continuación, haga clic en **Agregar servicios de rol**.

3.  En el panel **Seleccionar servicios de rol**, desplácese hasta **Compatibilidad con la administración de IIS 6**.

4.  Haga clic para seleccionar las casillas de verificación **Compatibilidad con metabase IIS 6** , **Compatibilidad con WMI de IIS 6** y **Consola de administración IIS 6**.

5.  En el panel **Seleccionar servicios de rol**, haga clic en **Siguiente**.

6.  En la página **Confirmar selecciones de instalación**, haga clic en **Instalar**.

7.  Haga clic en **Cerrar** para salir del Asistente para agregar servicios de rol.

Instale los componentes Compatibilidad con la administración de IIS 6.0 en Windows 7 o en el Windows Vista desde el Panel de control

1.  Haga clic en **Inicio**, en **Panel de control**, **Programas y características** y, a continuación, haga clic en **Activar o desactivar características de Windows**.

2.  Abra **Internet Information Services**.

3.  Abra **Herramientas de administración web**.

4.  Abra **Compatibilidad con la administración de IIS 6.0**.

5.  Haga clic para seleccionar las casillas de verificación **Compatibilidad con metabase IIS 6 y configuración IIS 6** , **Compatibilidad con WMI de IIS 6** y **Consola de administración IIS 6**.

6.  Haga clic en **Aceptar**.

