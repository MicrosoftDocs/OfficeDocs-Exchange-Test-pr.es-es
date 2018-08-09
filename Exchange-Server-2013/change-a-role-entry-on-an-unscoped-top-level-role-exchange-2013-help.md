---
title: 'Cambiar entrada función función nivel superior sin ámbito: Exchange 2013 Help'
TOCTitle: Cambiar una entrada de función en una función de nivel superior sin ámbito
ms:assetid: 65c0bfb3-aafd-4c64-8429-7616c57adf1c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876896(v=EXCHG.150)
ms:contentKeyID: 49895675
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambiar una entrada de función en una función de nivel superior sin ámbito

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Las entradas de función de administración en funciones de administración de nivel superior sin ámbito hacen referencia a los scripts y a los cmdlets que no son Exchange, los cuales se desea que estén disponibles para su asignación por función. Al cambiar los parámetros disponibles en una entrada de función, se controlan las acciones con el script o el cmdlet que no es Exchange de quienes tienen la función asignada. Para obtener más información acerca de las entradas de funciones sin ámbito, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> Si desea cambiar una entrada de función en una función de administración que contenga cmdlets de Exchange, consulte <A href="change-a-role-entry-exchange-2013-help.md">Cambiar una entrada de función</A>.



¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - La capacidad de cambiar una entrada de función en una función de nivel superior sin ámbito no se incluye en cualquier grupo de función de administración de manera predeterminada. Para que el usuario pueda agregar o cambiar una entrada de función de nivel superior sin ámbito, debe asignar primero la función Administración de funciones sin ámbito a un usuario, o a un grupo de seguridad universal (USG) o un grupo de función del cual el usuario es miembro. Para obtener más información acerca de la adición de una función a un usuario, grupo de seguridad universal o grupo de funciones, consulte los siguientes temas:
    
      - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)
    
      - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para agregar uno o más parámetros a una entrada de función

Para agregar parámetros a una entrada de función de nivel superior sin ámbito, debe realizar las siguientes acciones:

  - Especifique los parámetros que desea agregar con el parámetro *Parameters*.

  - Especifique el parámetro *AddParameter* para indicar que desea realizar una operación de agregado.

  - Especifique el parámetro *UnscopedTopLevel* para indicar que está cambiando una entrada de función en una función de nivel superior sin ámbito. Si no especifica este parámetro al cambiar una entrada de función en una función sin ámbito, se produce un error.

Para agregar parámetros a una entrada de función, use la siguiente sintaxis.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter -UnscopedTopLevel

En este ejemplo, se agregan los parámetros *EmailAddress* y *City* al script **CreateUsers.ps1** en la función sin ámbito Administradores de destinatarios.

    Set-ManagementRoleEntry "Recipient Administrators\CreateUsers.ps1" -Parameters EmailAddress, City -AddParameter -UnscopedTopLevel

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

## Use el Shell para quitar uno o más parámetros de una entrada de función

Para quitar parámetros de una entrada de función, debe realizar las siguientes acciones:

  - Especifique los parámetros que desea quitar con el parámetro *Parameters*.

  - Especifique el parámetro *RemoveParameter* para indicar que desea realizar una operación de eliminación.

  - Especifique el parámetro *UnscopedTopLevel* para indicar que está cambiando una entrada de función en una función de nivel superior sin ámbito. Si no especifica este parámetro al cambiar una entrada de función en una función sin ámbito, se produce un error.


> [!WARNING]
> No puede deshacer las operaciones en las que se quitan elementos. Si, por error, quita un parámetro de una entrada de función, debe agregarlo nuevamente de forma manual.



Para quitar parámetros de una entrada de función, use la siguiente sintaxis.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter -UnscopedTopLevel

En este ejemplo, se quitan los parámetros *Delay*, *Force* y *Credential* del cmdlet **Start-Widget** que no es Exchange en la función Administrador de servidores de nivel 1.

    Set-ManagementRoleEntry "Tier 1 Server Administrators\Start-Widget" -Parameters Delay, Force, Credential -RemoveParameter -UnscopedTopLevel

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

## Usar el Shell para quitar todos los parámetros de una entrada de función

Para quitar todos los parámetros de una entrada de función, debe realizar las siguientes acciones:

  - Especifique el valor `$Null` en el parámetro *Parameters*. No es necesario incluir el parámetro *RemoveParameter*.

  - Especifique el parámetro *UnscopedTopLevel* para indicar que está cambiando una entrada de función en una función de nivel superior sin ámbito. Si no especifica este parámetro al cambiar una entrada de función en una función sin ámbito, se produce un error.

Quitar todos los parámetros de una entrada de función resulta muy útil cuando desea que solo algunos parámetros estén disponibles en un script o un cmdlet que no es Exchange y que todos los demás se excluyan.

Si no desea que la función tenga acceso a un script o un cmdlet que no es Exchange, quite la entrada de función asociada por completo de la función en lugar de quitar solamente los parámetros. Para obtener más información acerca de cómo quitar una entrada de función de una función, consulte [Quitar una entrada de función de una función](remove-a-role-entry-from-a-role-exchange-2013-help.md).


> [!WARNING]
> No puede deshacer las operaciones en las que se quitan elementos. Si, por error, quita todos los parámetros de una entrada de función, debe agregarlos nuevamente de forma manual.



Para quitar todos los parámetros de una entrada de función, use la siguiente sintaxis.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters $Null -UnscopedTopLevel

En este ejemplo, se quitan todos los parámetros del script FindMailboxesOverQuota.ps1 en la función Administradores de destinatarios.

    Set-ManagementRoleEntry "Recipient Administrators\FindMailboxesOverQuota.ps1" -Parameters $Null -UnscopedTopLevel

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

## Usar el Shell para aplicar un conjunto específico de parámetros

Si desea que se incluya solamente un conjunto de parámetros específico en una entrada de función, debe realizar las siguientes acciones:

  - Especifique solamente el parámetro *Parameters*. No incluya los parámetros *AddParameter* ni *RemoveParameter*.

  - Especifique el parámetro *UnscopedTopLevel* para indicar que está cambiando una entrada de función en una función sin ámbito. Si no especifica este parámetro al cambiar una entrada de función en una función de nivel superior sin ámbito, se produce un error.


> [!WARNING]
> Cuando solamente especifica el parámetro <EM>Parameters</EM>, solo los parámetros que especifique en el comando se incluirán en la entrada de función. El resto de parámetros se quitan.



Para especificar un conjunto de parámetros, use la siguiente sintaxis.

    Set-ManagementRoleEntry <role name>\<script or non-Exchange cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -UnscopedTopLevel

En este ejemplo, se incluyen solo los parámetros *Alias*, *DisplayName*, *WidgetConfig* y *Enabled* en el cmdlet **Set-Widget** en la función Administradores de destinatarios de correo de Seattle.

    Set-ManagementRoleEntry "Seattle Mail Recipient Admins\Set-UMMailbox" -Parameters Alias, DisplayName, WidgetConfig, Enabled -UnscopedTopLevel

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

## Otras tareas

Después de cambiar una entrada de función o una función de nivel superior sin ámbito, es posible que también desee realizar las siguientes tareas:

[Agregar una entrada de función a una función](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

[Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md)

[Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Quitar una función de un usuario o un grupo de seguridad universal](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

