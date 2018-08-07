---
title: 'Cambiar configuración de directiva de libreta direcciones: Exchange 2013 Help'
TOCTitle: Cambiar la configuración de una directiva de libreta de direcciones
ms:assetid: ba1ca350-71c2-4c60-a612-33bfa9320b5e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Hh529941(v=EXCHG.150)
ms:contentKeyID: 49895867
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Cambiar la configuración de una directiva de libreta de direcciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-03-30_

Después de crear una directiva de libreta de direcciones (ABP), puede ver o modificar el nombre y la lista global de direcciones (LGD), la libreta de direcciones sin conexión (OAB), la lista de salas y las listas de direcciones asignadas.

Para otras tareas de administración relacionadas con las directivas de libretas de direcciones (ABP), consulte [Procedimientos de directivas de la libreta de direcciones](address-book-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de libreta de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - La creación de una directiva de libretas de direcciones (ABP) para una organización es un proceso que consta de varios pasos y que se debe planificar. Para obtener más información, consulte [Caso: implementación de directivas de libretas de direcciones](scenario-deploying-address-book-policies-exchange-2013-help.md)

  - No puede usar el Centro de Administración de Exchange (EAC) para configurar una ABP. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).

  - ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

## ¿Qué desea hacer?

## Cambiar la OAB, la lista de salas y la LGD para una ABP

En este ejemplo se cambia la OAB, la lista de salas y la LGD que utilizarán los usuarios de buzones asignados a la ABP llamada Todas las ABP Fabrikam.

    Set-AddressBookPolicy -Identity "All Fabrikam ABP" -OfflineAddressBook \Fabrikam-OAB-2 -GlobalAddressList "\All Fabrikam GAL" -RoomList "\All Fabrikam Rooms"

## Reemplazar listas de direcciones en una ABP

Las listas de direcciones que especifique para una ABP existente reemplazan todas las listas de direcciones de la ABP.

En este ejemplo se reemplazan las listas de direcciones existentes denominadas GovernmentAgencyA-Atlanta y GovernmentAgencyA-Moscow por la ABP denominada Government Agency A.

    Set-AddressBookPolicy -Identity "Government Agency A" -AddressLists "GovernmentAgencyA-Atlanta","GovernmentAgencyA-Moscow"

## Agregar listas de direcciones a una ABP

Para conservar las listas de direcciones que ya están definidas en una ABP, debe especificar dichas listas al agregar otras nuevas a la ABP.

En este ejemplo se agrega la lista de direcciones denominada Contoso-Chicago a la ABP denominada ABP Contoso, que ya está configurada para usar la lista de direcciones denominada Contoso-Seattle.

    Set-AddressBookPolicy -Identity "ABP Contoso" -AddressLists "Contoso-Chicago","Contoso-Seattle"

## Quitar listas de direcciones de una ABP

Para quitar listas de direcciones existentes que ya están definidas en una ABP, debe especificar las listas que quiere conservar.

Por ejemplo, la ABP denominada ABP Fabrikam usa las listas de direcciones Fabrikam-HR y Fabrikam-Finance. Para quitar de la ABP la lista de direcciones Fabrikam-HR, especifique la lista de direcciones Fabrikam-Finance que quiere conservar.

    Set-AddressBookPolicy -Identity "ABP Fabrikam" -AddressLists Fabrikam-Finance

## Más información

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-AddressBookPolicy](https://technet.microsoft.com/es-es/library/hh529945\(v=exchg.150\)).

