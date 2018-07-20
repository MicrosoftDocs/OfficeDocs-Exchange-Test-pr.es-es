---
title: 'Quitar una función de un usuario o un grupo de seguridad universal: Exchange 2013 Help'
TOCTitle: Quitar una función de un usuario o un grupo de seguridad universal
ms:assetid: df3510ef-e0c2-4d3c-81b0-7dc3e70c01a0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351196(v=EXCHG.150)
ms:contentKeyID: 49895965
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una función de un usuario o un grupo de seguridad universal

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-02_

Asignaciones de funciones de administración asignan una función de administración a un usuario o un grupo de seguridad universal (USG). Si quita una asignación de función, los usuarios asignados a la función ya no tendrán acceso a los cmdlets disponibles en dicha función. Para obtener más información acerca de las asignaciones de funciones de administración en Microsoft Exchange Server 2013, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Asignaciones de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Quitar una asignación de funciones de administración

Si conoce el nombre del que desea quitar la asignación de funciones, utilice la sintaxis siguiente.

    Remove-ManagementRoleAssignment <assignment name>

Por ejemplo, para quitar la asignación de roles de "Nivel 2 ayuda escritorio asignación", utilice el siguiente comando.

    Remove-ManagementRoleAssignment "Tier 2 Help Desk Assignment"

Si no conoce el nombre de la asignación de funciones, puede utilizar la siguiente sintaxis.

    Get-ManagementRoleAssignment -RoleAssignee <user or USG> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment 

Por ejemplo, si desea quitar la asignación de función normal de los destinatarios de correo del usuario davids, utilice el siguiente comando.

    Get-ManagementRoleAssignment -RoleAssignee davids -Role "Mail Recipients" -Delegating $false | Remove-ManagementRoleAssignment

