---
title: 'Crear una directiva de libreta de direcciones: Exchange 2013 Help'
TOCTitle: Crear una directiva de libreta de direcciones
ms:assetid: 6359abaf-e6f6-4667-8c2b-3860728b39a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529931(v=EXCHG.150)
ms:contentKeyID: 49895670
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear una directiva de libreta de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2014-12-16_

Las directivas de libreta de direcciones (ABP) permiten clasificar a los usuarios en grupos específicos para proporcionar vistas personalizadas de la lista global de direcciones (LGD) de una organización. Al crear una ABP, asigna una GAL, una libreta de direcciones sin conexión (OAB), una lista de sala y una o varias listas de direcciones a la directiva. A continuación, puede asignar la ABP a usuarios de los buzones y proporcionarles acceso a una GAL personalizada en Outlook y Outlook Web App. El objetivo es proporcionar un mecanismo más sencillo para cumplir la segmentación de GAL para organizaciones locales que necesiten varias GAL. Para obtener más información acerca de las ABP, consulte [Directivas de la libreta de direcciones](address-book-policies-exchange-2013-help.md).

Para consultar otras tareas de administración relacionadas con las directivas de libretas de direcciones (ABP), vea [Procedimientos de directivas de la libreta de direcciones](address-book-policy-procedures-exchange-2013-help.md).

¿Interesado en escenarios que utilizan este procedimiento? Consulte [Caso: implementación de directivas de libretas de direcciones](scenario-deploying-address-book-policies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de libreta de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - De manera predeterminada, en Exchange Online, el rol Lista de direcciones no se asigna a ningún grupo de roles. Para usar algún cmdlet que requiera el rol Lista de direcciones, es necesario agregar el rol a un grupo de roles. Para obtener más información, consulte la sección "Agregar un rol a un grupo de roles" del tema [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

  - La creación de una directiva de libretas de direcciones (ABP) para una organización es un proceso que consta de varios pasos y que se debe planificar. Para obtener más información, consulte [Caso: implementación de directivas de libretas de direcciones](scenario-deploying-address-book-policies-exchange-2013-help.md).

  - No puede usar el Centro de administración de Exchange (EAC) para crear una ABP. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## Uso del Shell para crear una ABP

En este ejemplo se crea una ABP con la siguiente configuración:

  - **Nombre:**  Todas las ABP Fabrikam

  - **LGD:**  Todo Fabrikam

  - **OAB:**  Todas las OAB Fabrikam

  - **Lista de salas:**  Todas las salas Fabrikam

  - **Listas de direcciones:**  Todo Fabrikam, Todos los buzones Fabrikam, Todas las DL Fabrikam y Todos los contactos Fabrikam

<!-- end list -->

    New-AddressBookPolicy -Name "All Fabrikam ABP" -AddressLists "\All Fabrikam","\All Fabrikam Mailboxes","\All Fabrikam DLs","\All Fabrikam Contacts" -OfflineAddressBook \Fabrikam-All-OAB -GlobalAddressList "\All Fabrikam" -RoomList "\All Fabrikam Rooms"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-AddressBookPolicy](https://technet.microsoft.com/es-es/library/hh529913\(v=exchg.150\)).

## Más información

[Asignar una directiva de libreta de direcciones a usuarios de correo](assign-an-address-book-policy-to-mail-users-exchange-2013-help.md)

