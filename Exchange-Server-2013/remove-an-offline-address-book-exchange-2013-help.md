---
title: 'Quitar una libreta de direcciones sin conexión: Exchange 2013 Help'
TOCTitle: Quitar una libreta de direcciones sin conexión
ms:assetid: d69f1e8a-b3cb-4739-90cd-85ea450d06f3
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124744(v=EXCHG.150)
ms:contentKeyID: 49895943
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quitar una libreta de direcciones sin conexión

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

En este tema, se explica cómo quitar una libreta de direcciones sin conexión (OAB).

Para otras tareas de administración relacionadas con las OAB, vea [Procedimientos de libretas de direcciones sin conexión](offline-address-book-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Libreta de direcciones sin conexión" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - Después de quitar una OAB vinculada a un usuario o a una base de datos de buzones, el destinatario descargará la OAB predeterminada hasta que se asigne una nueva OAB a dicho usuario. Si quita la OAB predeterminada, deberá asignar otra OAB como OAB predeterminada. Para obtener más información acerca de cómo cambiar la OAB predeterminada, consulte [Cambiar la libreta de direcciones sin conexión predeterminada](change-the-default-offline-address-book-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para quitar una OAB

En este ejemplo se quita una OAB denominada Mi OAB.

    Remove-OfflineAddressBook -Identity "My OAB"

Escriba **Y** para confirmar que desea quitar esta OAB y, a continuación, pulse INTRO.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Remove-OfflineAddressBook](https://technet.microsoft.com/es-es/library/bb123594\(v=exchg.150\)).

