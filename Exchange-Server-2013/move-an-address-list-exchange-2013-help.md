---
title: 'Mover una lista de direcciones: Exchange 2013 Help'
TOCTitle: Mover una lista de direcciones
ms:assetid: c843bbd5-6c0e-41e1-b749-7ae87c1beb25
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124534(v=EXCHG.150)
ms:contentKeyID: 49895905
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Mover una lista de direcciones

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-14_

En este tema se explica cómo mover una lista de direcciones existente a un contenedor nuevo bajo la lista de direcciones raíz.

Para otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Listas de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para realizar este procedimiento. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para mover una lista de direcciones

En este ejemplo se utiliza la lista de direcciones del GUID (identificador único global) para mover la lista de direcciones al contenedor "Building 4", que está ubicado en Todos los usuarios/Ventas.

    Move-AddressList -Identity c3fffd8e-026b-41b9-88c4-8c21697ac8ac -Target "\All Users\Sales\Building4"

Escriba **Y** para confirmar que desea mover esta lista de direcciones y, a continuación, pulse ENTRAR.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Move-AddressList](https://technet.microsoft.com/es-es/library/bb124520\(v=exchg.150\)).

