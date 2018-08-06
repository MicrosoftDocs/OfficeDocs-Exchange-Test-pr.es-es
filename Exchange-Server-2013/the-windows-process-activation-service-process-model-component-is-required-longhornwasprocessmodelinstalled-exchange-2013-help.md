---
title: 'Servicio activación procesos Windows: se necesita componente modelo procesos | Microsoft Docs'
TOCTitle: El Servicio de activación de procesos de Windows - componente de modelo de procesos es necesario_LonghornWASProcessModelInstalled
ms:assetid: 8cc13dbb-4921-4c07-8602-d26613d7730a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.longhornwasprocessmodelinstalled(v=EXCHG.150)
ms:contentKeyID: 48268398
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# El Servicio de activación de procesos de Windows - componente de modelo de procesos es necesario\_LonghornWASProcessModelInstalled

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2015-04-07_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

La instalación de Exchange Server 2010 no puede continuar en el equipo con Windows Server 2008 o Windows Server 2008 basado en R2 porque la característica "Windows Process Activation Service: modelo de procesos" no está instalada en el servidor.

El servicio WAS generaliza el modelo de procesos de Internet Information Services (IIS) y elimina la dependencia de HTTP. Todas las características de IIS que estaban disponibles sólo para aplicaciones HTTP se encuentran ahora a disposición de las aplicaciones que hospedan los servicios WCF (Windows Communication Foundation) a través de los protocolos no-HTTP. IIS 7.0 también usa el servicio Windows Process Activation para la activación basada en mensajes a través de HTTP.

El modelo de procesos hospeda los servicios web y WCF. Incluido en IIS 6.0, el modelo de procesos es una arquitectura nueva que ofrece protección rápida frente a errores, seguimiento de estado y reciclado.

Para resolver este problema, instale en este servidor el servicio WAS (Windows Process Activation Service): modelo de procesos y, a continuación, vuelva a ejecutar el programa de instalación de Exchange 2010.

Instale la característica "Windows Process Activation Service: modelo de procesos" con la herramienta Administrador de servidores

1.  Haga clic en **Inicio**, en **Herramientas administrativas** y, a continuación, en **Administrador de servidores**.

2.  En el panel de navegación izquierdo, haga clic con el botón secundario en **Características** y, a continuación, haga clic en **Agregar características**.

3.  En el panel **Seleccionar características**, desplácese hasta **Servicio WAS (Windows Process Activation Service)**.

4.  Active las casillas situadas bajo **Modelo de procesos**.

5.  Haga clic en **Siguiente** en el panel **Seleccionar características** y, a continuación, haga clic en **Instalar** en el panel **Confirmar selecciones de instalación**.

6.  Haga clic en **Cerrar** para salir del Asistente para agregar servicios de función.

