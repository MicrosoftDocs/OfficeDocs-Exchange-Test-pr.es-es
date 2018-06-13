---
title: 'Administración híbrida en las implementaciones híbridas de Exchange 2013/Exchange 2007: Exchange 2013 Help'
TOCTitle: Administración híbrida en las implementaciones híbridas de Exchange 2013/Exchange 2007
ms:assetid: 4b4370d5-1645-4b44-b4e0-c585fcaf970f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn151299(v=EXCHG.150)
ms:contentKeyID: 54652471
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración híbrida en las implementaciones híbridas de Exchange 2013/Exchange 2007

Este tema se está redactando.  

_**Se aplica a:**Exchange Online, Exchange Server, Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Cuando instala un servidor que ejecuta Microsoft Exchange Server 2013 en su organización local de Exchange 2007, las herramientas de administración de Exchange 2013 se instalan automáticamente en el servidor. Use las siguientes herramientas para configurar y administrar la funcionalidad híbrida para las organizaciones de Exchange locales y de Exchange Online:

  - **Centro de Administración Exchange**   El EAC es una consola de administración basada en web incluida con Exchange 2013 que permite un fácil uso y está optimizada para implementaciones locales, en línea o híbridas de Exchange. El EAC complementa las interfaces de la Consola de administración de Exchange (EMC) y el Panel de control de Exchange (ECP) que se usan para administrar Exchange Server 2007.

  - **Shell de administración de Exchange**   El Shell de administración de Exchange es una interfaz de línea de comandos basada en Windows PowerShell.

## El Centro de administración de Exchange

El EAC le permite realizar varias tareas de implementación y muchas tareas administrativas diarias tanto en los servidores Exchange locales como en la organización Exchange Online. Está instalado de forma predeterminada en cada servidor Exchange 2013. Como es una consola de administración basada en web, también puede acceder a ella usando un explorador web en otros equipos de su red o por Internet usando la URL del directorio virtual ECP.


> [!IMPORTANT]
> Si desea acceder al EAC usando una cuenta con un buzón localizado en un servidor de buzones de Exchange 2007 (como una cuenta de administrador de dominio), debe insertar la dirección siguiente en el explorador:<BR>https://<EM>&lt;FQDN of Exchange 2013 Client Access server&gt;</EM>/ECP? ExchClientVer=15



Puede acceder a la organización de Exchange Online desde el EAC seleccionando la pestaña de navegación de Office 365 entre empresas. La navegación entre empresas le permite intercambiar fácilmente entre su organización de Exchange Online y su organización de Exchange local. Si ha configurado una implementación híbrida, seleccionar la pestaña Office 365 le permitirá administrar la organización de Exchange Online y los objetos destinatarios. Si no tiene una organización de Exchange Online, al seleccionar el enlace de Office 365 será redirigido a la página de inicio de sesión de Office 365.

Para obtener más información acerca de EAC, consulte [Centro de administración de Exchange en Exchange 2013](https://technet.microsoft.com/es-es/library/jj150562\(v=exchg.150\)).

## El Shell de administración de Exchange

El Shell de administración de Exchange permite llevar a cabo cualquier tarea que pueda efectuarse con el EAC, más algunas tareas adicionales que solo se pueden llevar a cabo en el Shell de administración de Exchange. El Shell de administración de Exchange es una colección de scripts y cmdlets de Windows PowerShell que se instalan en el equipo cuando se instalan las herramientas de administración de Exchange 2013. Esos scripts y cmdlets solo se cargan cuando se abre el Shell de administración de Exchange mediante el icono del Shell de administración de Exchange. Si Windows PowerShell se abre directamente, los scripts y los cmdlets de Exchange no se cargarán y no podrá administrar la organización local.


> [!NOTE]
> Puede crear una conexión manual de Windows PowerShell a la organización local, de un modo similar a como se conecta manualmente a la organización de Exchange Online que se indica a continuación. Sin embargo, se recomienda usar el icono del Shell de administración de Exchange para abrir el Shell de administración de Exchange y administrar los servidores Exchange locales.



Si abre el Shell de administración de Exchange mediante el icono del Shell de administración de Exchange en un equipo que tenga instaladas las herramientas de administración, podrá administrar la organización local. No obstante, no podrá administrar la organización de Exchange Online si abre el Shell de administración de Exchange con este icono. Esto se debe a que al abrir el Shell de administración de Exchange mediante el icono del Shell de administración de Exchange, se conecta automáticamente al servidor Exchange local.

Si desea administrar la organización de Exchange Online mediante Windows PowerShell, deberá abrir Windows PowerShell directamente y no mediante el icono del Shell de administración de Exchange. Cuando abra Windows PowerShell, puede especificar manualmente dónde desea conectarse. Al crear una conexión manual, especifique una cuenta de administrador en la organización inquilina de Office 365 y, a continuación, ejecute el comando para crear una conexión. Cuando se establezca esa conexión, los cmdlets de Exchange para los que tenga permisos de ejecución estarán disponibles. Obtengas más información en [Uso de Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=209660).

Si no había trabajado antes con el Shell de administración de Exchange y desea aprender los conceptos básicos sobre su funcionamiento, la sintaxis de los comandos, etc., consulte [Usar Powershell con Exchange 2013 (Shell de administración de Exchange)](https://technet.microsoft.com/es-es/library/bb123778\(v=exchg.150\)).

