---
title: 'Actualizar la libreta de direcciones sin conexión: Exchange 2013 Help'
TOCTitle: Actualizar la libreta de direcciones sin conexión
ms:assetid: 448a207e-41b4-4cef-9fe9-a68b81e2ec4e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997684(v=EXCHG.150)
ms:contentKeyID: 49895599
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Actualizar la libreta de direcciones sin conexión

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2013-11-15_

Después de crear una OAB o modificar la configuración de una OAB, los cambios no estarán disponibles para los usuarios hasta que se complete el proceso de generación de OAB (OABGen).

Para otras tareas de administración relacionadas con las OAB, consulte [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para actualizar una libreta de direcciones sin conexión

En este ejemplo, se actualiza la OAB denominada My OAB.

    Update-OfflineAddressBook -Identity "My OAB"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Update-OfflineAddressBook](https://technet.microsoft.com/es-es/library/aa995979\(v=exchg.150\)).

