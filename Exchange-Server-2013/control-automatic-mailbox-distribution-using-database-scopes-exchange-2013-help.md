---
title: 'Controlar distribución automática buzones mediante ámbitos base datos'
TOCTitle: Controlar la distribución automática de buzones mediante los ámbitos de base de datos
ms:assetid: 8eaff177-2251-4c8b-8570-c91a77d0a6fc
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff628332(v=EXCHG.150)
ms:contentKeyID: 49895772
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Controlar la distribución automática de buzones mediante los ámbitos de base de datos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

La distribución automática de buzones es una característica en Exchange Server 2013 de Microsoft que selecciona aleatoriamente un base de dato del buzón para almacenar un buzón nuevo o movido cuando no especifica una base de datos de forma específica. Esta característica puede ser útil cuando desea permitir que administradores junior o el personal de la asistencia técnica creen buzones sin necesidad de saber qué buzones de las bases de datos deben crearse.

Puede usar los ámbitos de administración de la base de datos para controlar qué bases de datos del buzón pueden ser seleccionadas por la distribución automática de buzones. Cuando aplica los ámbitos de la base de datos a un administrador, solamente las bases de datos que coinciden con el ámbito de la base de datos definido están disponibles para el administrador. Como la distribución automática de buzones utiliza el contexto del usuario actual, también está restringida por los ámbitos de la base de datos aplicados al administrador.

Para obtener más información acerca de la distribución automática de buzones, los ámbitos de la base datos y asignaciones de roles, consulte los siguientes temas:

  - [Distribución automática de buzones](automatic-mailbox-distribution-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

¿Está buscando otras tareas de administración relacionadas con ámbitos? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Ámbitos de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Crear un ámbito de base de datos

En este paso, decida qué bases de datos desea incluir en el ámbito de base de datos. También, decida si desea especificar una lista estática de bases de datos o si desea crear un filtro de base de dato que incluye solamente las bases de datos que coinciden con el criterio que especifica.


> [!IMPORTANT]
> Las asignaciones de roles asociadas a ámbitos de base de datos se aplican únicamente a los usuarios que se conectan a servidores que utilizan Microsoft Exchange Server 2010 Service Pack 1 (SP1) o una versión posterior, o bien Exchange&nbsp;2013. Si un usuario con una asignación de roles asociada a un ámbito de base de datos se conecta a una versión anterior a Exchange 2010 SP1, la asignación de roles no se aplicará al usuario y este no gozará de ninguno de los permisos concedidos por la asignación de roles.



## Usar un ámbito de la lista de base de dato

Use una lista de base de datos si desea definir una lista estática de las bases de datos del buzón que se deben incluir en este ámbito. Use la sintaxis siguiente para crear un ámbito basado en listas de bases de datos.

    New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>

En este ejemplo se crea un ámbito que se aplica solo a las bases de datos Database 1, Database 2 y Database 3.

    New-ManagementScope -Name "Accounting databases" -DatabaseList "Database 1", "Database 2", "Database 3"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Usar un ámbito del filtro de base de dato

Use un filtro de base de datos si desea crear un ámbito de base de datos dinámico que incluye solamente las bases de datos que coinciden con el criterio que especifica. Esto puede ser útil si no desea administrar el ámbito de la base de datos después de que se creó y definió los valores estándar para su organización que pueden identificar conjuntos específicos de bases de datos del buzón.

Para obtener una lista de propiedades de base de datos que se pueden filtrar, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

Use la sintaxis siguiente para crear un ámbito del filtro de bases de datos.

    New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>

En este ejemplo se crea un ámbito que incluye todas las bases de datos que contienen la cadena "ACCT" en la propiedad **Name** de la base de datos.

    New-ManagementScope -Name "Accounting Databases" -DatabaseRestrictionFilter { Name -Like '*ACCT*' }

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Paso 2: Agregar el ámbito de la base de datos a una asignación de roles de administración

Una vez creado el ámbito, debe agregarlo a una asignación de roles de administración nueva o existente. Recomendamos que use grupos de roles de administración para controlar los permisos administrativos, por lo tanto los ejemplos en este paso usan un grupo de roles de ejemplo llamado Administradores contables. Si desea obtener más información sobre cómo crear un grupo de roles, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

Después de asignar el rol a un grupo de roles con el ámbito de base de datos, los miembros del grupo de roles solamente podrán crear buzones y mudar buzones a las bases de datos incluidas en el ámbito.

Para obtener una lista de los roles integrados que puede asignar a un grupo de roles, consulte [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md).

## Agregar una nueva asignación de roles

Use este procedimiento si recién creó un grupo de roles y necesita agregarle roles.

Use la siguiente sintaxis para crear una asignación de roles entre el rol de administración que desea asignar y el nuevo grupo de roles con el nuevo ámbito de base de datos.

    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <database scope name>

Este ejemplo crea una asignación de roles entre los roles destinatarios de correo y creación del destinatario de correo y el grupo de roles administradores contables, usando el ámbito de base de datos Bases de datos contables.

    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipients" -CustomConfigWriteScope "Accounting Databases"
    New-ManagementRoleAssignment -SecurityGroup "Accounting Administrators" -Role "Mail Recipient Creation" -CustomConfigWriteScope "Accounting Databases"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Modificar una asignación del rol existente

Use este procedimiento si tiene un grupo de roles existentes que ya tiene asignaciones de roles entre él y los roles en las que desea aplicar el nuevo ámbito de base de dato.

Este procedimiento utiliza la canalización. Para obtener más información, consulte [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\)).

Use la siguiente sintaxis para modificar una asignación de roles entre el rol de administración en la que desea aplicar el ámbito de base de datos y el grupo de roles existentes.

    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> | Set-ManagementRoleAssignment -CustomConfigWriteScope <database scope name>

Este ejemplo agrega el ámbito de base de datos Bases de datos contables a los roles destinatarios de correo y creación de destinatario de correo asignadas al grupo de roles administradores contables.

    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipients" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"
    Get-ManagementRoleAssignment -RoleAssignee "Accounting Administrators" -Role "Mail Recipient Creation" | Set-ManagementRoleAssignment -CustomConfigWriteScope "Accounting Databases"

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)) o [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## Paso 3: Agregar miembros a un grupo de roles (si corresponde)

Si desea agregar miembros a un grupo de roles, consulte [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).


> [!IMPORTANT]
> Si agrega miembros a este grupo de roles para restringir qué bases de datos pueden crear los usuarios, o mover los buzones, asegúrese de que no son miembros de otros grupos de roles que podrían otorgar permisos adicionales.



## Paso 4: Quitar miembros a un grupo de roles (si corresponde)

Si agregó miembros a un nuevo grupo de roles que limita en qué bases de datos se puede crear un buzón, o se pueden mover buzones, y son miembros de otro grupo de roles que tiene permisos adicionales, quítelos del viejo grupo de roles. Para obtener más información, consulte [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

