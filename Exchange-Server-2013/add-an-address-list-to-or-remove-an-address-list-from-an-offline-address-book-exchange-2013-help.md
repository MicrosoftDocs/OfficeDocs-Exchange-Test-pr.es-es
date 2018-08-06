---
title: 'Agregar o quitar listas de direcciones en libretas de direcciones sin conexión | Microsoft Docs'
TOCTitle: Agregar una lista de direcciones o quitar una lista de direcciones de la libretas de direcciones sin conexión
ms:assetid: 86bd5651-ad41-4516-bf23-6579f4e4da03
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123563(v=EXCHG.150)
ms:contentKeyID: 49895754
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agregar una lista de direcciones o quitar una lista de direcciones de la libretas de direcciones sin conexión

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

Puede usar el Shell para agregar o quitar una lista de direcciones de una libreta de direcciones sin conexión (OAB). De forma predeterminada, existe una libreta de direcciones sin conexión denominada Libreta de direcciones sin conexión predeterminada que contiene la lista global de direcciones (GAL). Las OAB se generan según las listas de direcciones que contienen. Para crear OAB personalizadas que puedan ser descargadas por los usuarios, puede agregar o quitar listas de direcciones en las OAB.

Para otras tareas de administración relacionadas con las OAB, consulte [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - Las modificaciones en la lista de direcciones no estarán disponibles para que el cliente las descargue hasta que se haya generado la OAB donde se encuentra la lista de direcciones. Para obtener más información, consulte [Actualizar la libreta de direcciones sin conexión](update-an-offline-address-book-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para agregar una lista de direcciones a una OAB

Si usa el parámetro *AddressLists*, se sobrescribirán las listas de direcciones que existan en ese momento. Incluya las listas de direcciones existentes cuando use el parámetro *AddressLists* para seguir generando esas listas de direcciones en su OAB. En este ejemplo, donde usted tiene AddressList1 y AddressList2, se agrega AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2,AddressList3

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/es-es/library/aa996330\(v=exchg.150\)).

## Usar el Shell para quitar una lista de direcciones de una OAB

Para quitar una lista de direcciones de una OAB, omita la lista de direcciones en cuestión de la lista de listas de direcciones. En este ejemplo, donde usted tiene AddressList1, AddressList2 y AddressList3, se quita AddressList3.

    Set-OfflineAddressBook -Identity "My OAB" -AddressLists AddressList1,AddressList2

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/es-es/library/aa996330\(v=exchg.150\)).

