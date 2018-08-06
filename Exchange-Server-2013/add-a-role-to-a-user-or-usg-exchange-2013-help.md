---
title: 'Agregar función a usuario o grupo de seguridad universal: Exchange 2013 Help | Microsoft Docs'
TOCTitle: Agregar una función a un usuario o grupo de seguridad universal
ms:assetid: ae5608de-a141-4714-8876-bce7d2a22cb5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351056(v=EXCHG.150)
ms:contentKeyID: 49895836
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Agregar una función a un usuario o grupo de seguridad universal

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Las asignaciones de funciones de administración pueden asignar una función a un usuario o un grupo de seguridad universal. Al asignar una función a un usuario o un grupo de seguridad universal, esos usuarios pueden efectuar tareas conforme a los cmdlets o las secuencias de comandos y sus parámetros que estén definidos en la función de administración.

Si desea asignar funciones a un grupo de funciones de administración o a una directiva de asignación de funciones de administración, consulte los temas siguientes:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md)

Si desea agregar miembros a un grupo de funciones de administración o asignar una directiva de asignación de funciones a un usuario final, consulte los temas siguientes:

  - [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md)

  - [Cambiar la directiva de asignación en un buzón](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

Para obtener más información, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Asignaciones de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Si bien se puede asignar roles directamente a usuarios y a grupos de seguridad universal, el método recomendado de otorgar permisos a administradores y usuarios finales es emplear grupos de roles de administración y directivas de asignación de roles de administración. Si usa grupos de roles y directivas de asignación, el modelo de permisos se simplifica.

  - Las asignaciones de funciones son de adición. Esto significa que todas las funciones se agregan juntas cuando se evalúan. Si se asignan dos roles a un usuario y uno contiene un cmdlet pero el otro no, el cmdlet seguirá estando disponible para el usuario.
    
    De forma predeterminada, las asignaciones de funciones no otorgan la capacidad de asignar funciones a otros usuarios. Para que un usuario pueda asignar funciones a otros usuarios o grupos de seguridad universal, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).

  - Si crea una asignación con un ámbito, el ámbito anula el ámbito de escritura implícito del rol. Sin embargo, el ámbito de lectura implícito de la función sigue vigente. El nuevo ámbito no puede devolver objetos fuera del ámbito de lectura implícito del rol. Para obtener más información, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

  - Todos los procedimientos de este tema usan el parámetro *SecurityGroup* para asignar funciones a un grupo de seguridad universal. Si desea asignar el rol a un determinado usuario, use el parámetro*User* en lugar del parámetro *SecurityGroup*. El resto de la sintaxis para cada comando es el mismo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Creación una asignación de función sin ámbito

Puede crear una asignación de función sin ámbito. Al hacer esto, se aplican los ámbitos implícitos de lectura y escritura de la función.

Use la sintaxis siguiente para asignar un rol sin ámbito a un grupo de seguridad universal.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name>

En este ejemplo se asigna el rol Servidores de Exchange al grupo de seguridad universal SeattleAdmins.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Crear una asignación de roles con un ámbito predefinido relativo

Si un ámbito relativo predefinido se adecua a los requisitos empresariales, puede aplicarlo a la asignación de roles en vez de crear un ámbito personalizado. Para obtener una lista con los ámbitos predefinidos y sus descripciones, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Use la sintaxis siguiente para asignar un rol a un grupo de seguridad universal (USG) con un ámbito predefinido.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -RecipientRelativeWriteScope < MyDistributionGroups | Organization | Self >

En este ejemplo se asigna el rol Servidores de Exchange al USG SeattleAdmins y se aplica el ámbito predefinido Organización.

    New-ManagementRoleAssignment -Name "Exchange Servers_SeattleAdmins" -SecurityGroup SeattleAdmins -Role "Exchange Servers" -RecipientRelativeWriteScope Organization

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Creación una asignación de función con un ámbito basado en filtro

Si crea un ámbito basado en filtro de destinatarios y lo va a usar con una asignación de roles, debe incluir el ámbito en el comando que se aplica para asignar el rol a un grupo de seguridad universal mediante el parámetro *CustomRecipientWriteScope*. Si usa el parámetro *CustomRecipientWriteScope*, no puede usar el parámetro *RecipientOrganizationalUnitScope*.

Antes de poder agregar un ámbito a una asignación de funciones, debe crear uno. Para obtener más información, consulte [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Use la sintaxis siguiente para asignar un rol a un grupo de seguridad universal con un ámbito basado en el filtro de destinatarios.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup < USG> -Role <role name> -CustomRecipientWriteScope <role scope name>

En este ejemplo se asigna el rol Destinatarios de correo al USG Administradores de destinatarios de Seattle y aplica el ámbito Destinatarios de Seattle.

    New-ManagementRoleAssignment -Name "Mail Recipients_Seattle Recipient Admins" -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -CustomRecipientWriteScope "Seattle Recipients"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Creación de una asignación de roles con un ámbito de configuración de servidor o base de datos basado en filtros o listas

Si crea un ámbito de configuración de servidor basado en listas o filtros base de datos y lo va a usar con una asignación de roles, debe incluir el ámbito en el comando que se aplica para asignar el rol a un grupo de seguridad universal mediante el parámetro *CustomConfigWriteScope*.

Antes de poder agregar un ámbito a una asignación de funciones, debe crear uno. Para obtener más información, consulte [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Use la sintaxis siguiente para asignar un rol a un grupo de seguridad universal con un ámbito de configuración.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -CustomConfigWriteScope <role scope name>

En este ejemplo se asigna el rol Servidores de Exchange al USG MailboxAdmins y se aplica el ámbito Servidores de buzones.

    New-ManagementRoleAssignment -Name "Exchange Servers_MailboxAdmins" -SecurityGroup MailboxAdmins -Role "Exchange Servers" -CustomConfigWriteScope "Mailbox Servers"

En el ejemplo anterior se muestra cómo agregar una asignación de funciones con un ámbito de configuración de servidor. La sintaxis para agregar un ámbito de configuración de base de datos es la misma. Solo tiene que indicar el nombre del ámbito de base de datos en vez del ámbito de servidor.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Creación una asignación de función con un ámbito de unidad organizativa

Si desea asignar un ámbito de escritura de una función a una unidad organizativa, puede especificar la unidad organizativa directamente en el parámetro *RecipientOrganizationalUnitScope*. Si usa el parámetro *RecipientOrganizationalUnitScope*, no puede usar el parámetro *CustomRecipientWriteScope*.

Use la sintaxis siguiente para asignar un rol a un grupo de seguridad universal y restringir el ámbito de escritura de un rol a una determinada unidad organizativa.

    New-ManagementRoleAssignment -Name <assignment name> -SecurityGroup <USG> -Role <role name> -RecipientOrganizationalUnitScope <OU>

Este ejemplo asigna el rol de destinatarios de correo al grupo de seguridad universal SalesRecipientAdmins y aplica el ámbito de asignación a la OU Ventas/Usuarios del dominio contoso.com.

    New-ManagementRoleAssignment -Name "Mail Recipients_SalesRecipientAdmins" -SecurityGroup SalesRecipientAdmins -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Creación una asignación de función con un ámbito de configuración o de destinatario exclusivo

Para crear una asignación de rol con un ámbito de configuración o de destinatario exclusivo, puede usar los mismos procedimientos indicados en las secciones Creación una asignación de función con un ámbito basado en filtro y Creación de una asignación de roles con un ámbito de configuración de servidor o base de datos basado en filtros o listas. La única diferencia estriba en que, al crear una función con un ámbito exclusivo, debe especificar los parámetros exclusivos siguientes en función de si se usa un parámetro de configuración exclusivo o uno de destinatario exclusivo:

  - **Ámbitos exclusivos de destinatarios**   Use el parámetro *ExclusiveRecipientWriteScope* en lugar del parámetro *CustomRecipientWriteScope*.

  - **Ámbitos exclusivos de configuración**   Use el parámetro *ExclusiveConfigWriteScope* en lugar del parámetro *CustomConfigWriteScope*.

Al efectuar este procedimiento, los usuarios a los que se asigna el rol pueden realizar acciones respecto a los objetos que se incluyen en el ámbito exclusivo. Para obtener más información sobre los ámbitos exclusivos, consulte [Descripción de ámbitos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

No se puede crear una asignación de función con ámbitos exclusivos y normales.

En este ejemplo se asigna el rol Destinatarios de correo al USG Protected User Admins y se aplica el ámbito exclusivo Usuarios protegidos.

    New-ManagementRoleAssignment -Name "Mail Recipients_Protected User Admins" -SecurityGroup "Protected User Admins" -Role "Mail Recipients" -ExclusiveRecipientWriteScope "Protected Users"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

