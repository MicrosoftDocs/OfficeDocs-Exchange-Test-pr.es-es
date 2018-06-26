---
title: 'Configurar invalidaciones de disponibilidad administrada: Exchange 2013 Help'
TOCTitle: Configurar invalidaciones de disponibilidad administrada
ms:assetid: c8f315b3-1d5e-4ad9-8bea-9c3a4a13ebfc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn482055(v=EXCHG.150)
ms:contentKeyID: 59890415
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar invalidaciones de disponibilidad administrada

 

_**Se aplica a:**Exchange Online, Exchange Server 2013 SP1_

_**Última modificación del tema:**2015-11-30_

La disponibilidad administrada realiza sondeos continuos para detectar posibles problemas con los componentes de Exchange o sus dependencias, además de realizar acciones de recuperación para garantizar que la experiencia del usuario final no se vea afectada debido a un problema con cualquiera de estos componentes. Sin embargo, puede haber situaciones donde la configuración de fábrica no sea adecuada para el entorno. Los sondeos, monitores y respondedores de disponibilidad administrada se pueden personalizar mediante la creación de un reemplazo.

Hay dos tipos de reemplazos: local y global. Como sus nombres sugieren, un reemplazo local está disponible solamente en el servidor en el que se creó y un reemplazo global se usa para aplicar un reemplazo en varios servidores. Cualquier tipo de reemplazo puede crearse con una duración determinada o para una versión específica de Exchange, pero no ambos a la vez.


> [!NOTE]
> Al crear un reemplazo, este no surte efecto inmediatamente. El servicio de administración de mantenimiento de Microsoft Exchange comprueba si hay cambios de configuración cada 10 minutos y carga los cambios de configuración detectados. Como alternativa, puede reiniciar el servicio para que los cambios surtan efecto inmediatamente.



Para otras tareas de administración relacionadas con la disponibilidad administrada, consulte [Administrar conjuntos de salud y el estado del servidor](manage-health-sets-and-server-health-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Solo puede usar el Shell para realizar este procedimiento. Para obtener información sobre cómo abrir el Shell de administración de Exchange en su organización local Exchange, vea [Abrir el Shell](https://technet.microsoft.com/es-es/library/dd638134\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar Shell de administración de Exchange para crear reemplazos locales

Para crear un reemplazo local con una duración específica, utilice la sintaxis siguiente.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Duration <dd.hh:mm:ss>

Para crear un reemplazo local para una versión concreta de Exchange, utilice la sintaxis siguiente.

    Add-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertyName> -PropertyValue <Value> -Version <15.01.xxxx.xxx>


> [!NOTE]
> Al crear el reemplazo, se distinguen mayúsculas de minúsculas en los valores utilizados en el parámetro <EM>Identity</EM>.



En este ejemplo, se agrega un reemplazo local que deshabilita el respondedor `ActiveDirectoryConnectivityConfigDCServerReboot` en el servidor llamado EXCH03 durante 20 días.

    Add-ServerMonitoringOverride -Server EXCH03 -Identity "AD\ActiveDirectoryConnectivityConfigDCServerReboot" -ItemType Responder -PropertyName Enabled -PropertyValue 0 -Duration 20.00:00:00

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya creado correctamente un reemplazo local, use el cmdlet **Get-ServerMonitoringOverride** para ver la lista de reemplazos locales:

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

El reemplazo debe aparecer en la lista.

## Usar Shell de administración de Exchange para quitar reemplazos locales

Para quitar un reemplazo local, utilice la siguiente sintaxis.

    Remove-ServerMonitoringOverride -Server <ServerName> -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <PropertytoRemove>

En este ejemplo, se quita el reemplazo local existente del respondedor `ActiveDirectoryConnectivityConfigDCServerReboot` en el conjunto de mantenimiento Exchange del servidor EXCH01.

    Remove-ServerMonitoringOverride -Server EXCH01 -Identity Exchange\ActiveDirectoryConnectivityConfigDCServerReboot -ItemType Responder -PropertyName Enabled

## ¿Cómo puede saber si funcionó?

Para comprobar que haya quitado correctamente un reemplazo local, use el cmdlet **Get-ServerMonitoringOverride** para ver la lista de reemplazos locales:

    Get-ServerMonitoringOverride  -Server <ServerIdentity> | Format-List

El reemplazo eliminado no debe aparecer en la lista.

## Usar Shell de administración de Exchange para crear reemplazos globales

Para crear un reemplazo global con una duración específica, utilice la sintaxis siguiente.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -Duration <dd.hh:mm:ss>

Para crear un reemplazo global para una versión concreta de Exchange, utilice la sintaxis siguiente.

    Add-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <Probe | Monitor | Responder | Maintenance> -PropertyName <PropertytoOverride> -PropertyValue <NewPropertyValue> -ApplyVersion <15.01.xxxx.xxx>


> [!NOTE]
> Al crear el reemplazo, se distinguen mayúsculas de minúsculas en los valores utilizados en el parámetro <EM>Identity</EM>.



En este ejemplo, se agrega un reemplazo global que deshabilita el sondeo `OnPremisesInboundProxy` durante 30 días.

    Add-GlobalMonitoringOverride -Identity "FrontendTransport\OnPremisesInboundProxy" -ItemType Probe -PropertyName Enabled -PropertyValue 0 -Duration 30.00:00:00

En este ejemplo se agrega un reemplazo global que deshabilita el respondedor `StorageLogicalDriveSpaceEscalate` para todos los servidores que ejecutan la versión 15.01.0225.042 de Exchange.

    Add-GlobalMonitoringOverride -Identity "MailboxSpace\StorageLogicalDriveSpaceEscalate" -PropertyName Enabled -PropertyValue 0 -ItemType Responder -ApplyVersion "15.01.0225.042"

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que haya creado correctamente un reemplazo global, use el cmdlet **Get-GlobalMonitoringOverride** para ver la lista de reemplazos globales:

    Get-GlobalMonitoringOverride

El reemplazo debe aparecer en la lista.

## Usar Shell de administración de Exchange para quitar reemplazos globales

Para quitar un reemplazo global, utilice la siguiente sintaxis.

    Remove-GlobalMonitoringOverride -Identity <HealthSetName>\<MonitoringItemName>[\<TargetResource>] -ItemType <ExistingItemTypeValue> -PropertyName <OverriddenProperty>

Este ejemplo, se quita el reemplazo global existente de la propiedad `ExtensionAttributes` del sondeo `OnPremisesInboundProxy` en el conjunto de mantenimiento `FrontEndTransport`.

    Remove-GlobalMonitoringOverride -Identity FrontEndTransport\OnPremisesInboundProxy -ItemType Probe -PropertyName ExtensionAttributes

## ¿Cómo puede saber si funcionó?

Para comprobar que haya quitado correctamente un reemplazo global, use el cmdlet **Get-GlobalMonitoringOverride** para ver la lista de reemplazos globales:

    Get-GlobalMonitoringOverride

El reemplazo eliminado no debe aparecer en la lista.

