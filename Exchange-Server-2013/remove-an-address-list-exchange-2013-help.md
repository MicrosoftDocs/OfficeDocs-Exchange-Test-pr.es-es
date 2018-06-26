---
title: 'Quitar una lista de direcciones: Exchange 2013 Help'
TOCTitle: Quitar una lista de direcciones
ms:assetid: 39a313f3-41d4-4c8f-af67-df2316f3687f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997294(v=EXCHG.150)
ms:contentKeyID: 49895574
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una lista de direcciones

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-14_

En este tema se explica cómo quitar una lista de direcciones. No puede quitar la lista global de direcciones (GAL) predeterminada.

Para otras tareas de administración relacionadas con las listas de direcciones, consulte [Procedimientos de la lista de direcciones](address-list-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Lista de direcciones" en el tema [Permisos de libreta de direcciones y dirección de correo electrónico](email-address-and-address-book-permissions-exchange-2013-help.md).

  - No puede quitar una lista de direcciones principal que contiene listas de direcciones secundarias. Sin embargo, puede quitar las listas de direcciones principal y secundaria pulsando la tecla CONTROL y seleccionando las listas deseadas. Si intenta quitar una lista de direcciones principal sin quitar las listas secundarias, se mostrará un error.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el EAC para quitar una lista de direcciones

1.  Vaya a **Organización** \> **Lista de direcciones**.

2.  En la vista de lista, seleccione la lista de direcciones que desee quitar y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  En la advertencia haga clic en **Sí** para quitar la lista de direcciones.

## Usar el Shell para quitar una lista de direcciones

En este ejemplo, se quita la lista de direcciones Departamento de ventas que no contiene ninguna lista de direcciones secundaria.

    Remove-AddressList -Identity "Sales Department"

Introduzca **S** para confirmar que desea eliminar esta lista de direcciones y, a continuación, presione INTRO.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-AddressList](https://technet.microsoft.com/es-es/library/bb124342\(v=exchg.150\)).

## Usar el Shell para quitar una lista de direcciones que contiene listas de direcciones secundarias

Este ejemplo quita los departamentos de la lista de direcciones primarias y todas sus listas de direcciones secundarias.

    Remove-AddressList -Identity Departments -Recursive

Introduzca **S** para confirmar que desea quitar la lista de direcciones principales y sus listas de direcciones secundarias y, a continuación, presione INTRO.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-AddressList](https://technet.microsoft.com/es-es/library/bb124342\(v=exchg.150\)).

