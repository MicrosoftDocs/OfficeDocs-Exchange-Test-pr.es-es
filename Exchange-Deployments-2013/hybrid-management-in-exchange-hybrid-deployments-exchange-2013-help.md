---
title: 'Administración híbrida en las implementaciones híbridas de Exchange: Exchange 2013 Help'
TOCTitle: Administración híbrida en las implementaciones híbridas de Exchange
ms:assetid: 233f9f34-3ff5-47e1-a9e8-3244ee868d6e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659048(v=EXCHG.150)
ms:contentKeyID: 49895002
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración híbrida en las implementaciones híbridas de Exchange

 

_<strong>Se aplica a:</strong>Exchange Server 2013, Exchange Server 2016_

_<strong>Última modificación del tema:</strong>2016-12-09_

Cuando instala un servidor de Exchange, las herramientas de administración de Exchange se instalan automáticamente en el servidor. Use las siguientes herramientas para configurar y administrar las organizaciones de Exchange locales y de Exchange Online:

  - **Centro de Administración Exchange** El EAC es una consola de administración basada en web que permite un fácil uso y está optimizada para implementaciones de Exchange locales, en línea e híbridas. La EAC reemplaza a la Consola de Administración de Exchange (EMC) y al Panel de Control de Exchange (ECP), que eran las interfaces que se usaban para administrar Exchange Server 2010.

  - **Shell de administración de Exchange**   El Shell de administración de Exchange es una interfaz de línea de comandos basada en Windows PowerShell.

## El Centro de administración de Exchange

El EAC le permite realizar varias tareas de implementación y muchas tareas administrativas diarias tanto en los servidores de Exchange locales como en la organización de Exchange Online. Está instalado de forma predeterminada en cada servidor nuevo o de Exchange 2013. Asimismo, y dado que es una consola de administración basada en web, también puede acceder a él usando un navegador web en otros equipos de su red o a través de Internet usando la URL del directorio virtual ECP.

Puede acceder a la organización Exchange Online desde la EAC seleccionando la ficha de navegación Office 365 entre empresas. La navegación entre empresas le permite intercambiar fácilmente entre su organización Exchange Online y su organización Exchange local. Si ha configurado una implementación híbrida, seleccionar la ficha Office 365 le permitirá administrar la organización Exchange Online y los objetos destinatarios. Si no tiene una organización de Exchange Online, al seleccionar el vínculo de Office 365 será redirigido a la página de inicio de sesión de Office 365.

Para obtener más información acerca de EAC, consulte [Centro de administración de Exchange en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150562\(v=exchg.150\)).

## El Shell de administración de Exchange

El Shell de administración de Exchange permite llevar a cabo cualquier tarea que pueda efectuarse con el EAC, más algunas tareas adicionales que solo se pueden llevar a cabo en el Shell de administración de Exchange. El Shell de administración de Exchange es una colección de scripts y cmdlets de Windows PowerShell que se instalan en el equipo cuando se instalan las herramientas de administración de Exchange. Esos scripts y cmdlets solo se cargan cuando se abre el Shell de administración de Exchange mediante el icono del Shell de administración de Exchange. Si Windows PowerShell se abre directamente, los scripts y los cmdlets de Exchange no se cargarán y no podrá administrar la organización local.


> [!NOTE]
> Puede crear una conexión manual de Windows PowerShell a la organización local, de un modo similar a como se conecta manualmente a la organización de Exchange Online que se indica a continuación. Sin embargo, se recomienda usar el icono del Shell de administración de Exchange para abrir el Shell de administración de Exchange y administrar los servidores Exchange locales.



Si abre el Shell de administración de Exchange mediante el icono del Shell de administración de Exchange en un equipo que tenga instaladas las herramientas de administración, podrá administrar la organización local. No obstante, no podrá administrar la organización de Exchange Online si abre el Shell de administración de Exchange con este icono. Esto se debe a que al abrir el Shell de administración de Exchange mediante el icono del Shell de administración de Exchange, se conecta automáticamente al servidor Exchange local.

Si desea administrar la organización de Exchange Online mediante Windows PowerShell, deberá abrir Windows PowerShell directamente y no mediante el icono del Shell de administración de Exchange. Cuando abra Windows PowerShell, puede especificar manualmente dónde desea conectarse. Al crear una conexión manual, especifique una cuenta de administrador en la organización inquilina de Office 365 y, a continuación, ejecute el comando para crear una conexión. Cuando se establezca esa conexión, los cmdlets de Exchange para los que tenga permisos de ejecución estarán disponibles. Obtengas más información en [Uso de Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660).

Si no había trabajado antes con el Shell de administración de Exchange y desea aprender los conceptos básicos sobre su funcionamiento, la sintaxis de los comandos, etc., consulte [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)).

