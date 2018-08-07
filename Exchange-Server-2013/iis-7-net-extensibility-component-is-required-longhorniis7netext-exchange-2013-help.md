---
title: 'El componente Extensibilidad de .NET de IIS 7 es necesario'
TOCTitle: El componente Extensibilidad de .NET de IIS 7 es necesario_LonghornIIS7NetExt
ms:assetid: 8b481626-b68a-4fba-b66e-a02c03856bfd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.longhorniis7netext(v=EXCHG.150)
ms:contentKeyID: 48268391
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El componente Extensibilidad de .NET de IIS 7 es necesario\_LonghornIIS7NetExt

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2012-06-05_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft®Exchange Server 2010 Setup no puede continuar porque el componente Extensibilidad de .NET de Microsoft Internet Information Server (IIS) 7 no está instalado en el servidor de destino.

Para que Exchange 2010 pueda usar Windows PowerShell Remoting, el componente Extensibilidad de .NET de IIS 7 debe estar instalado en el servidor de destino.

Para solucionar este error, use el Administrador de servidores para instalar el componente Extensibilidad de .NET de IIS 7 en este servidor y, a continuación, vuelva a ejecutar el programa de instalación de Exchange 2010.

Instale el componente de Extensibilidad de .NET de IIS 7 en Windows Server 2008 o en Windows Server 2008 R2 usando la herramienta Administrador de servidores

1.  Haga clic en **Inicio**, en **Herramientas administrativas** y, a continuación, en **Administrador de servidores**.

2.  En el panel de navegación izquierdo, expanda **Funciones** y, a continuación, haga clic con el botón secundario en **Servidor web (IIS)** y seleccione **Agregar servicios de función**.

3.  En el panel **Seleccionar servicios de función**, desplácese hasta **Desarrollo de aplicaciones**.

4.  Active la casilla situada bajo **Extensibilidad de .NET**.

5.  Haga clic en **Siguiente** en el panel **Seleccionar servicios de función** y, a continuación, haga clic en **Instalar** en el panel **Confirmar selecciones de instalación**.

6.  Haga clic en **Cerrar** para salir del Asistente para agregar servicios de rol.

