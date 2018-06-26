---
title: 'Quitar una carpeta pública: Exchange 2013 Help'
TOCTitle: Quitar una carpeta pública
ms:assetid: 334b831d-e372-4d85-a407-5c8a5d0e78de
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997202(v=EXCHG.150)
ms:contentKeyID: 49895560
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quitar una carpeta pública

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2016-11-16_

Es posible que deba eliminar carpetas públicas que ya no se utilicen en la organización. Para determinar qué carpetas públicas se deben quitar, consulte [Ver estadísticas de carpetas públicas y elementos de carpetas públicas](view-statistics-for-public-folders-and-public-folder-items-exchange-2013-help.md).

Para otras tareas de administración relacionadas con la administración de carpetas públicas, consulte [Procedimientos de carpetas públicas](public-folder-procedures-exchange-2013-help.md).

Para otras tareas de administración relacionadas con las carpetas públicas, consulte [Procedimientos de carpetas públicas en Office 365 y Exchange Online](https://technet.microsoft.com/es-es/library/jj966272\(v=exchg.150\)).

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Carpetas públicas" en el tema [Permisos de uso compartido y colaboración](sharing-and-collaboration-permissions-exchange-2013-help.md).

  - No puede eliminar una carpeta pública habilitada para correo. Primero, debe deshabilitar el correo electrónico de la carpeta pública antes de eliminarla. Para obtener más información, consulte [Habilitar o deshabilitar el correo para una carpeta pública](mail-enable-or-mail-disable-a-public-folder-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Uso del Centro de Administración de Exchange para eliminar una carpeta pública

1.  Vaya a **Carpetas públicas** \> **Carpetas públicas**.

2.  En la vista de lista, seleccione la carpeta pública que quiera eliminar. Tenga en cuenta que, al hacer clic en el nombre de la carpeta, se mostrarán las subcarpetas de esa carpeta (si existen). Después, puede hacer clic para seleccionar una subcarpeta específica que quiera quitar.
    
    Para eliminar una carpeta o subcarpeta, haga clic en cualquiera de sus filas excepto en el nombre subrayado de la carpeta y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono"). Si hace clic en el nombre subrayado de la carpeta, la opción **Eliminar** no estará disponible para seleccionarse.
    
    ![Seleccionar una carpeta pública para quitarla](images/Aa997202.8666290d-3f19-4c70-afe3-45569762718b(EXCHG.150).png "Seleccionar una carpeta pública para quitarla")  

3.  Se mostrará un cuadro de advertencia preguntando si está seguro de que quiere eliminar la carpeta pública. Haga clic en **Sí** para continuar.

## Uso del Shell para eliminar una carpeta pública

Este ejemplo elimina la carpeta pública de ayuda Desk\\Resolved. Este comando supone que la carpeta pública Resuelto no tiene ninguna subcarpeta.

    Remove-PublicFolder -Identity "\Help Desk\Resolved"

En este ejemplo, se prueba el comando anterior sin realizar modificaciones.

    Remove-PublicFolder -Identity "\HelpDesk\Resolved" -WhatIf

En este ejemplo, se quita la carpeta pública Marketing y todas sus subcarpetas, porque el comando se ejecuta de manera recursiva.

    Remove-PublicFolder -Identity "\Marketing" -Recurse:$True

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-PublicFolder](https://technet.microsoft.com/es-es/library/bb124894\(v=exchg.150\)).

