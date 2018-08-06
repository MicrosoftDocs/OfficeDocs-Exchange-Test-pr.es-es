---
title: 'Cambiar libreta de direcciones sin conexión predeterminada: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Cambiar la libreta de direcciones sin conexión predeterminada
ms:assetid: 61abf78e-2543-4431-acc8-839e3c7a4548
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998569(v=EXCHG.150)
ms:contentKeyID: 49895666
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cambiar la libreta de direcciones sin conexión predeterminada

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

De manera predeterminada, al instalar la función de servidor Buzón, se crea una libreta de direcciones sin conexión predeterminada basada en Web (OAB) llamada Libreta de direcciones sin conexión predeterminada. Puede establecer cualquier OAB en su organización de Exchange como la OAB predeterminada. Esta nueva OAB predeterminada se asocia con todas las bases de datos de buzón recién creadas. Solamente puede tener una OAB predeterminada en la organización. Si elimina la Libreta de direcciones sin conexión predeterminada, MicrosoftExchange asigna automáticamente otra Libreta de direcciones sin conexión como predeterminada. Debe designar manualmente otra Libreta de direcciones sin conexión como predeterminada.

Para otras tareas de administración relacionadas con las OAB, consulte [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de destinatarios](recipients-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para cambiar la OAB predeterminada

En este ejemplo, se establece la OAB denominada My OAB como la OAB predeterminada.

    Set-OfflineAddressBook -Identity "My OAB" -IsDefault $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OfflineAddressBook](https://technet.microsoft.com/es-es/library/aa996330\(v=exchg.150\)).

