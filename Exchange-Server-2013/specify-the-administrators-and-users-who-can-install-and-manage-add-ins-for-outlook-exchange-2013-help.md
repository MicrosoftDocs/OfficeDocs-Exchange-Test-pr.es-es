---
title: 'Especifique los administradores y los usuarios que pueden instalar y administrar complementos para Outlook: Exchange 2013 Help'
TOCTitle: Especifique los administradores y los usuarios que pueden instalar y administrar complementos para Outlook
ms:assetid: 7ee4302d-b8bb-40a0-9810-10d3a0271bcb
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ943754(v=EXCHG.150)
ms:contentKeyID: 52062038
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Especifique los administradores y los usuarios que pueden instalar y administrar complementos para Outlook

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2017-02-08_

Puede especificar que los administradores de la organización tienen permisos para instalar y administrar complementos para Outlook. También puede especificar qué usuarios de la organización tienen permiso para instalar y administrar complementos para su propio uso.

Para ello, asignar o quitar funciones de administración específicas de los complementos. Hay cinco funciones integradas que puede utilizar.

Roles administrativos

  - **Aplicaciones de mercado org**   Permite a un administrador instalar y administrar los complementos que están disponibles en el almacén de Office para su organización.

  - **Aplicaciones personalizadas de org**   Permite a un administrador instalar y administrar complementos personalizados para su organización.

Roles de usuario

  - **Mis aplicaciones de Marketplace**   Permite al usuario instalar y administrar complementos de Office Store para su propio uso.

  - **Mis aplicaciones personalizadas**   Permite al usuario instalar y administrar complementos personalizados para su propio uso.

  - **Mis aplicaciones ReadWriteMailbox**   Permite al usuario instalar y administrar complementos que solicitan el nivel de permiso de ReadWriteMailbox en su manifiesto.

De forma predeterminada, todos los administradores con el grupo de funciones de **Administración de la organización** tienen dos de las funciones administrativas anteriores habilitadas. También de forma predeterminada, los usuarios finales tienen habilitadas las funciones de usuario anteriores.

Para obtener información acerca de cada una de estas funciones, consulte [Rol de aplicaciones del mercado de la organización](org-marketplace-apps-role-exchange-2013-help.md), [Rol Aplicaciones personalizadas de la organización](org-custom-apps-role-exchange-2013-help.md), [Rol My Marketplace Apps](my-marketplace-apps-role-exchange-2013-help.md), [Rol Mis aplicaciones personalizadas](my-custom-apps-role-exchange-2013-help.md)y [El rol de mis aplicaciones ReadWriteMailbox](my-readwritemailbox-apps-role-exchange-2013-help.md).

Para obtener información sobre los complementos, consulte [Aplicaciones para Outlook](add-ins-for-outlook-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder ejecutar este cmdlet. Aunque todos los parámetros correspondientes a este cmdlet se describen en este tema, tal vez no tenga acceso a algunos parámetros si no están incluidos en los permisos que se le han asignado. Para ver qué permisos necesita, consulte el Entrada de "Asignaciones de funciones" en el tema de [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md) .

  - El acceso a la Tienda Office no se admite para buzones y organizaciones de ciertas regiones. Si no puede ver la opción **Agregar desde la Tienda Office** en el **Centro de administración de Exchange**, que encontrará en **Organización** \> **Complementos** \> ![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono"), es posible que no pueda instalar un complemento de Outlook desde una URL o una ubicación de archivo. Para obtener más información, póngase en contacto con su proveedor de servicios.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Asignar a los administradores los permisos necesarios para instalar y administrar complementos para su organización

## Usar el EAC para asignar permisos a los administradores

Puede utilizar el CEF para asignar a los administradores los permisos necesarios para instalar y administrar complementos que está disponible desde el almacén de Office para su organización. Para obtener información detallada acerca de cómo hacerlo, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

## Asignar a los usuarios los permisos necesarios para instalar y administrar complementos para su propio uso

## Usar el EAC para asignar permisos a usuarios

Puede utilizar el CEF para asignar a los usuarios los permisos necesarios para ver y modificar los complementos personalizados para su propio uso. Para obtener información detallada acerca de cómo hacerlo, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar si ha asignado los permisos para un usuario correctamente, ejecute un comando del Shell usando el formato `Get-ManagementRoleAssignment -Role <Role Name> -GetEffectiveUsers`, donde `Role Name` es el rol para el que quiere comprobar los permisos asignados.

En este ejemplo se muestra cómo comprobar que se ha asignado permisos para instalar complementos desde el almacén de la oficina para la organización.

1.  Ejecute `Get-ManagementRoleAssignment -Role "Org Marketplace Apps" -GetEffectiveUsers`.

2.  En los resultados, revise las entradas de la columna **Usuarios eficaces**.

Para obtener más información sobre sintaxis y parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

