---
title: 'Modificar una asignación de roles: Exchange 2013 Help'
TOCTitle: Modificar una asignación de roles
ms:assetid: 0fa77efc-e393-461f-b3c0-232cc56cee85
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335096(v=EXCHG.150)
ms:contentKeyID: 49895470
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modificar una asignación de roles

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Las asignaciones de roles de administración asignan un rol de administración a un usuario al que se le asigna un rol. Al modificar la asignación de roles, puede controlar los objetos que pueden modificar los usuarios a los que se asigna un rol. Los ámbitos de los roles de administración que se aplican a las asignaciones de roles invalidan el ámbito de escritura implícito del rol. Sin embargo, el ámbito de lectura implícito del rol sigue vigente. Los ámbitos que se aplican no pueden devolver objetos que se encuentren fuera del ámbito de lectura implícito del rol.

Para obtener más información sobre los ámbitos y las asignaciones de funciones de administración en Microsoft Exchange Server 2013, consulte los siguientes temas:

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

¿Está buscando otras tareas de administración relacionadas con las asignaciones de roles? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Asignaciones de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué quiere hacer?

## Usar el Shell para habilitar o deshabilitar una asignación de roles

Las asignaciones de roles están habilitadas de forma predeterminada, lo que implica que el rol asociado se aplica al usuario al que se asigna el rol. Si una asignación de roles está deshabilitada, el rol asociado no se aplica al usuario al que se le asignan roles.

Para habilitar una asignación de roles, utilice la sintaxis siguiente.

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $true
```

Para deshabilitar una asignación de roles, utilice la sintaxis siguiente.

```powershell
Set-ManagementRoleAssignment <role assignment> -Enabled $false
```

En este ejemplo, se deshabilita la asignación de roles Asignación del Servicio de asistencia.

```powershell
Set-ManagementRoleAssignment "Help Desk Assignment" -Enabled $false
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## Usar el Shell para modificar un rol de administración o un usuario al que se asigna un rol en una asignación de roles

No puede modificar un rol de administración o un usuario al que se asigna un rol especificado en una asignación de roles. Si desea asociar una asignación de roles con otro rol o usuario al que se asigna el rol, debe crear una nueva asignación de roles y, luego, eliminar la asignación de roles anterior. Para obtener más información acerca de cómo agregar o quitar asignaciones de roles, consulte los siguientes temas:

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Quitar una función de un usuario o un grupo de seguridad universal](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

Si creó asignaciones directamente a un usuario o un grupo de seguridad universal (USG), se recomienda considerar usar grupos de roles de administración y directivas de asignación de roles de administración. Los grupos de roles y las directivas de asignación le permiten simplificar su modelo de permisos y reducir la cantidad de asignaciones de roles que se deben administrar. Para obtener más información, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

## Usar el Shell para modificar un ámbito relativo predefinido en una asignación de roles

Puede modificar o agregar un ámbito relativo predefinido en una asignación de roles. Si agrega o modifica un ámbito predefinido, todos los ámbitos de destinatarios especificados anteriormente se quitan de la asignación de roles. Para obtener una lista con los ámbitos predefinidos y sus descripciones, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Para modificar o agregar un ámbito predefinido en una asignación de roles, utilice la sintaxis siguiente.

```powershell
Set-ManagementRoleAssignment <assignment name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >
```

En este ejemplo, se modifica el ámbito predefinido en la asignación de roles Asignación de Juan a MyDistributionGroups.

```powershell
Set-ManagementRoleAssignment "John's Assignment" - RecipientRelativeWriteScope MyDistributionGroups
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## Usar el Shell para modificar un ámbito de filtro de destinatarios en una asignación de roles

Puede especificar un nuevo ámbito basado en filtro de destinatarios o modificar el ámbito ya aplicado a la asignación de roles. Si agrega un ámbito de filtro de destinatarios, todos los ámbitos de destinatarios definidos anteriormente se quitan de la asignación de roles.

Para especificar un nuevo ámbito basado en filtro de destinatarios o reemplazar uno existente, utilice la sintaxis siguiente.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomRecipientWriteScope <role scope name>
```

En este ejemplo, se agrega el ámbito basado en filtro de destinatarios a Destinatarios de Redmond o se lo modifica.

```powershell
Set-ManagementRoleAssignment "Redmond Recipient Administrators Assignment" -CustomRecipientWriteScope "Redmond Recipients"
```

Si desea conservar el mismo ámbito basado en filtro de destinatarios aplicado a la asignación de roles, pero desea modificar el filtro de destinatarios usado para que coincida con los objetos de destinatarios, debe modificar el filtro de destinatarios en el ámbito propiamente dicho. Para obtener más información acerca de cómo modificar los ámbitos, consulte [Cambiar el ámbito de una función](change-a-role-scope-exchange-2013-help.md).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## Usar el Shell para modificar el ámbito de configuración basado en lista o filtro de servidores en una asignación de roles

Puede especificar un nuevo ámbito de configuración basado en lista o filtro de servidores o modificar el ámbito ya aplicado a la asignación de roles. Si agrega o modifica un ámbito de configuración, todos los ámbitos de configuración especificados anteriormente se quitan de la asignación de roles.

Para especificar un nuevo ámbito de configuración o reemplazar uno existente, utilice la sintaxis siguiente.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

En este ejemplo, se agrega el ámbito de configuración a Servidores de Redmond o se lo modifica.

```powershell
Set-ManagementRoleAssignment "Redmond Administrators Assignment" -CustomConfigWriteScope "Redmond Servers"
```

Si desea conservar el mismo ámbito de configuración aplicado a la asignación de roles, pero desea modificar la lista de servidores o el filtro de servidores del ámbito, debe modificar el ámbito de configuración propiamente dicho. Para obtener más información acerca de cómo modificar los ámbitos, consulte [Cambiar el ámbito de una función](change-a-role-scope-exchange-2013-help.md).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## Usar el Shell para cambiar el ámbito de configuración basado en lista o filtro de base de datos en una asignación de roles

Puede especificar un nuevo ámbito de configuración basado en lista o filtro de base de datos, o cambiar el ámbito ya aplicado a la asignación de roles. Si agrega o modifica un ámbito de configuración, todos los ámbitos de configuración especificados anteriormente se quitan de la asignación de roles.

Para especificar un nuevo ámbito de configuración o reemplazar uno existente, utilice la sintaxis siguiente.

```powershell
Set-ManagementRoleAssignment <assignment name> -CustomConfigWriteScope <role scope name>
```

En este ejemplo, se agrega o se cambia el ámbito de configuración a bases de datos de Redmond.

```powershell
Set-ManagementRoleAssignment "Redmond Database Admins" -CustomConfigWriteScope "Redmond Databases"
```

Si desea conservar el mismo ámbito de configuración aplicado a la asignación de roles, pero desea cambiar la lista de servidores o el filtro de base de datos del ámbito, debe cambiar el ámbito de configuración. Para obtener más información acerca de cómo modificar los ámbitos, consulte [Cambiar el ámbito de una función](change-a-role-scope-exchange-2013-help.md).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## Usar el Shell para modificar la unidad organizativa en una asignación de roles

Puede agregar una nueva unidad organizativa (UO) o cambiar una UO ya aplicada a la asignación de roles. Si especifica una nueva OU, todos los ámbitos de destinatarios especificados anteriormente se quitan de la asignación de roles.

Para modificar o agregar una nueva OU en una asignación de roles, utilice la sintaxis siguiente.

```powershell
Set-ManagementRoleAssignment <assignment name> -RecipientOrganizationalUnitScope <OU>
```

En este ejemplo, se agrega la OU Ingeniería\\Usuarios en el dominio contoso.com a la asignación de roles Servicio de asistencia de ingeniería.

```powershell
Set-ManagementRoleAssignment "Engineering Help Desk" -RecipientOrganizationalUnitScope contoso.com/Engineering/Users
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## Usar el Shell para modificar un ámbito exclusivo de configuración o destinatarios

Para cambiar ámbitos de configuración o de destinatario exclusivos, puede usar los procedimientos que se proporcionan en las secciones anteriores de este tema "Usar el Shell para cambiar un ámbito de filtro de destinatarios en una asignación de roles" "Usar el Shell para cambiar el ámbito de configuración basado en lista o filtro de servidores en una asignación de roles" y "Usar el Shell para cambiar el ámbito de configuración basado en lista o filtro de base de datos en una asignación de roles". La única diferencia reside en que cuando se modifica un ámbito exclusivo, se deben especificar los siguientes parámetros exclusivos según si se desea modificar un ámbito exclusivo de destinatarios o un ámbito exclusivo de configuración:

  - **Ámbitos exclusivos de destinatarios**   Use el parámetro *ExclusiveRecipientWriteScope* en lugar del parámetro *CustomRecipientWriteScope*.

  - **Ámbitos exclusivos de configuración de base de datos y servidor**   Use el parámetro *ExclusiveConfigWriteScope* en lugar del parámetro *CustomConfigWriteScope*.

Al igual que ocurre con los ámbitos normales de destinatarios y configuración, si agrega o modifica un ámbito exclusivo, se reemplazan todos los ámbitos de configuración o destinatarios definidos anteriormente.

En este ejemplo, se modifica un ámbito de escritura exclusivo de destinatarios.

```powershell
Set-ManagementRoleAssignment "Exclusive Executive Users" -ExclusiveRecipientWriteScope "Exclusive Executives"
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

