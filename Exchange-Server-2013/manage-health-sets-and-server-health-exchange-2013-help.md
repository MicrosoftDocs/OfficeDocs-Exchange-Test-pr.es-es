---
title: 'Administrar conjuntos de salud y el estado del servidor: Exchange 2013 Help'
TOCTitle: Administrar conjuntos de salud y el estado del servidor
ms:assetid: a4f84312-6cfa-4f17-9707-676aadab1143
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dn482054(v=EXCHG.150)
ms:contentKeyID: 59890414
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar conjuntos de salud y el estado del servidor

 

_**Se aplica a:**Exchange Online, Exchange Server 2013 SP1_

_**Última modificación del tema:**2013-12-02_

Puede utilizar cmdlets de informes de mantenimiento integrados para realizar diversas tareas relacionadas con la disponibilidad administrada, tales como:

  - Ver el mantenimiento de un servidor o grupo de servidores

  - Ver una lista de conjuntos de mantenimiento

  - Ver una lista de sondeos, monitores y respondedores asociados a un conjunto particular de mantenimiento

  - Ver una lista de monitores y su mantenimiento actual

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 2 minutos

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Ver el mantenimiento del servidor

Puede usar el Shell para obtener un resumen del mantenimiento de un servidor que ejecuta Exchange 2013.

## Usar el Shell para ver el mantenimiento del servidor

Ejecute cualquiera de los siguientes comandos para ver los conjuntos de mantenimiento y la información de mantenimiento en un servidor que ejecuta Exchange 2013.

    Get-HealthReport -Identity <ServerName>

    Get-ServerHealth -Identity <ServerName> | Format-Table Server,CurrentHealthSetState,Name,HealthSetName,AlertValue,HealthGroupName -Auto

Ejecute cualquiera de los siguientes comandos para ver conjuntos de mantenimiento en un servidor o grupo de disponibilidad de bases de datos que ejecuta Exchange 2013.

    Get-ExchangeServer | Get-HealthReport -RollupGroup

    Get-ExchangeServer | Get-HealthReport -RollupGroup -HealthSetName <HealthSet>

    (Get-DatabaseAvailabiltyGroup <DAGName>).Servers | Get-HealthReport -RollupGroup

## Ver una lista de conjuntos de mantenimiento

Un conjunto de mantenimiento es un grupo de monitores, sondeos y respondedores de un componente que determinan si el componente está en buen estado o en mal estado. Puede usar el Shell para ver la lista de conjuntos de mantenimiento en un servidor que ejecuta Exchange 2013.

## Usar el Shell para ver una lista de conjuntos de mantenimiento

Ejecute el siguiente comando para ver los conjuntos de mantenimiento en un servidor que ejecuta Exchange 2013.

    Get-HealthReport -Server <ServerName>

## Ver los sondeos, monitores y respondedores para un conjunto de mantenimiento

Un conjunto de mantenimiento es un grupo de monitores, sondeos y respondedores de un componente que determinan si el componente está en buen estado o en mal estado. Puede usar el Shell para ver una lista de sondeos, monitores y respondedores asociados con un conjunto de mantenimiento en un servidor que ejecuta Exchange 2013.

## Usar el Shell para ver los sondeos, monitores y respondedores de un conjunto de mantenimiento

Ejecute el siguiente comando para ver los sondeos, monitores y respondedores asociados con un conjunto de mantenimiento en un servidor que ejecuta Exchange 2013.

    Get-MonitoringItemIdentity -Server <ServerName> -Identity <HealthSetName> | Format-Table Identity,ItemType,Name -Auto

## Ver una lista de monitores y su mantenimiento actual

El mantenimiento de un monitor se notifica mediante los "peores" monitores en el conjunto de mantenimiento. Puede ver los detalles de un conjunto de mantenimiento para ver los monitores que están en buen estado y los que están en mal estado.

## Usar el Shell para ver una lista de monitores y su mantenimiento actual

Ejecute el siguiente comando para ver una lista de monitores y su mantenimiento actual en un servidor que ejecuta Exchange 2013.

    Get-ServerHealth -HealthSet <HealthSetName> -Server <ServerName> | Format-Table Name, AlertValue -Auto

