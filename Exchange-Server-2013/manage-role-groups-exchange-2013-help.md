---
title: 'Administrar grupos de roles: Exchange 2013 Help'
TOCTitle: Administrar grupos de roles
ms:assetid: ab9b7a3b-bf67-4ba1-bde5-8e6ac174b82c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657480(v=EXCHG.150)
ms:contentKeyID: 49895830
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar grupos de roles

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-08_

En este tema se muestra cómo agregar, quitar, copiar y ver los grupos de roles de administración en Microsoft Exchange Server 2013. También se explica cómo agregar, quitar y listar los roles de administración en grupos de roles y cómo cambiar los ámbitos y delegados de administración en los grupos de roles. Para obtener más información sobre los grupos de roles en Exchange 2013, consulte [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md).

Para otras tareas de administración relacionadas con los grupos de roles, consulte [Permisos](permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: de 5 a 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear un grupo de roles

Si desea personalizar los permisos que puede asignar a un grupo de usuarios, cree un nuevo grupo de roles de administración personalizado.

## Usar el EAC para crear un grupo de roles

1.  En el Centro de administración de Exchange (EAC), vaya a **Permisos** \> **Roles de administración** y haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la ventana **Nuevo grupo de roles**, indique un nombre para el nuevo grupo de roles.

3.  Puede seleccionar ahora los roles que quiera asignar al grupo de roles y los miembros que quiera agregar al grupo de roles o puede hacerlo en otro momento.

4.  Seleccione el ámbito de escritura que quiere aplicar al nuevo grupo de roles.

5.  Haga clic en **Guardar** para crear el grupo de roles.

## Usar el Shell para crear un grupo de roles

Ejemplos

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el grupo de roles se creó correctamente, haga lo siguiente:

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Compruebe que el nuevo grupo de roles esté incluido en la lista de grupos de roles y luego selecciónelo.

3.  Compruebe que los miembros, roles asignados y ámbito que especificó en el nuevo grupo de roles estén incluidos en el panel de detalles del grupo de roles.

## Copiar un grupo de roles

## Usar el EAC para copiar un grupo de roles

Si tiene un grupo de roles que contenga los permisos que desea otorgar a los usuarios, pero quiere aplicar un ámbito de administración distinto o quitar o agregar uno o dos roles de administración sin tener que agregar todos los otros roles de manera manual, puede copiar el grupo de roles existente.


> [!IMPORTANT]
> No puede usar el EAC para copiar un grupo de roles si usó el Shell de administración de Exchange para configurar varios ámbitos de roles de administración o ámbitos exclusivos en el grupo de roles. Si configuró varios ámbitos o ámbitos exclusivos en el grupo de roles, debe usar los procedimientos del Shell, que se explican más adelante en este tema, para copiar un grupo de roles. Para obtener más información sobre los ámbitos de roles de administración, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Descripción de los ámbitos de roles de administración</A>.



1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de roles que quiera copiar y haga clic en **Copiar**![Copiar icono](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif "Copiar icono").

3.  En la ventana **Nuevo grupo de roles**, indique un nombre para el nuevo grupo de roles.

4.  Revise los roles que se han copiado en el nuevo grupo de roles. Agregue o quite roles según sea necesario.

5.  Examine el ámbito de escritura y cámbielo si es necesario.

6.  Revise los miembros que se han copiado en el nuevo grupo de roles. Agregue o quite miembros según sea necesario.

7.  Haga clic en **Guardar** para crear el grupo de roles.

## Use el Shell para copiar un grupo de funciones sin ningún ámbito

1.  Almacene el grupo de roles que desee copiar en una variable mediante la siguiente sintaxis:
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  Cree el nuevo grupo de funciones y agregue miembros al grupo de funciones y especifique quién puede delegar el nuevo grupo de funciones a otros usuarios. Use la siguiente sintaxis:

    ```powershell
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -Members <member1, member2, member3...> -ManagedBy <user1, user2, user3...>
    ```

Por ejemplo, los siguientes comandos copian el grupo de funciones Administración organizativa y denominan al nuevo grupo de funciones "Administración organizativa limitada". Esto agrega los miembros Isabelle, Carter y Lucas y pueden ser delegados por Jenny y Katie.

```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Limited Organization Management" -Roles $RoleGroup.Roles -Members Isabelle, Carter, Lukas -ManagedBy Jenny, Katie
```

Después de haber creado el nuevo grupo de roles, puede agregar y quitar roles, cambiar el ámbito de las asignaciones de roles en un rol y otras tareas.

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-RoleGroup](https://technet.microsoft.com/es-es/library/dd638115\(v=exchg.150\)) y [New-RoleGroup](https://technet.microsoft.com/es-es/library/dd638181\(v=exchg.150\)).

## Use el Shell para copiar un grupo de funciones con un ámbito personalizado

1.  Almacene el grupo de roles que desee copiar en una variable mediante la siguiente sintaxis:
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  Cree el nuevo grupo de roles con un ámbito personalizado mediante la siguiente sintaxis:

    ```powershell
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuraiton scope name>
    ```

Por ejemplo, los siguientes comandos copian el grupo de funciones Administración organizativa y crean un nuevo grupo de funciones denominado Administración organizativa de Vancouver con el ámbito de destinatarios Usuarios de Vancouver y el ámbito de configuración Servidores de Vancouver.

```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    New-RoleGroup "Vancouver Organization Management" -Roles $RoleGroup.Roles -CustomRecipientWriteScope "Vancouver Users" -CustomConfigWriteScope "Vancouver Servers"
```

Además, puede agregar miembros al grupo de funciones cuando lo cree usando el parámetro *Members*, como se muestra anteriormente en Use the Shell to copy a role group with no scope, en este tema. Para obtener más información acerca de los ámbitos de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Después de haber creado el nuevo grupo de roles, puede agregar y quitar roles, cambiar el ámbito de las asignaciones de roles en un rol y realizar otras tareas.

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-RoleGroup](https://technet.microsoft.com/es-es/library/dd638115\(v=exchg.150\)) y [New-RoleGroup](https://technet.microsoft.com/es-es/library/dd638181\(v=exchg.150\)).

## Use el Shell para copiar un grupo de funciones con un ámbito OU

1.  Almacene el grupo de roles que desee copiar en una variable mediante la siguiente sintaxis:
    
    ```powershell
    $RoleGroup = Get-RoleGroup <name of role group to copy>
    ```

2.  Cree el nuevo grupo de roles con un ámbito personalizado mediante la siguiente sintaxis:

    ```powershell
        New-RoleGroup <name of new role group> -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope <OU name>
    ```

Por ejemplo, los siguientes comandos copian el grupo de funciones Administración de destinatarios y crean un grupo de funciones denominado Administración de destinatarios de Toronto que permite la administración de usuarios solo en la OU de usuarios de Toronto.

```powershell
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Toronto Recipient Management" -Roles $RoleGroup.Roles -RecipientOrganizationalUnitScope "contoso.com/Toronto Users"
```

Además, puede agregar miembros al grupo de funciones cuando lo cree usando el parámetro *Members*, como se muestra anteriormente en Use the Shell to copy a role group with no scope, en este tema. Para obtener más información acerca de los ámbitos de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Después de haber creado el nuevo grupo de roles, puede agregar y quitar roles, cambiar el ámbito de las asignaciones de roles en un rol y otras tareas.

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-RoleGroup](https://technet.microsoft.com/es-es/library/dd638115\(v=exchg.150\)) y [New-RoleGroup](https://technet.microsoft.com/es-es/library/dd638181\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que el grupo de roles se copió correctamente, haga lo siguiente:

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Compruebe que el grupo de roles copiado esté incluido en la lista de grupos de roles y luego selecciónelo.

3.  Compruebe que los miembros, roles asignados y ámbito que especificó en el grupo de roles copiado estén incluidos en el panel de detalles del grupo de roles.

## Quitar un grupo de roles

Si ya no necesita un grupo de roles que creó, puede quitarlo. Cuando se quita un grupo de roles, se eliminan las asignaciones de roles de administración entre el grupo de roles y los roles de administración. Los roles de administración no se eliminan. Si un usuario dependía de un grupo de roles para obtener acceso a una característica, el usuario ya no podrá tener acceso a ella. No puede quitar los grupos de roles integrados.

## Usar el EAC para quitar un grupo de roles

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de roles que quiere quitar y haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

3.  Confirme que quiere quitar el grupo de roles seleccionado y, si fuera así, responda **Sí** a la advertencia.

## Usar el Shell para quitar un grupo de funciones

Ejemplos

## Ver grupos de roles

Puede ver una lista de los grupos de roles o la información detallada de un determinado grupo de roles que existe en su organización.

## Usar el EAC para ver una lista de grupos de roles y los detalles del grupo de roles

1.  En el EAC, vaya a **Permisos** \> **Roles de administración**. Aquí aparecen todos los grupos de roles de la organización.

2.  Seleccione un grupo de roles para ver los miembros, roles asignados y ámbito que están configurados en este grupo de roles.

## Usar el Shell para ver una lista de grupos de roles y los detalles del grupo de roles

Ejemplos

## Agregar un rol a un grupo de roles

Agregar un rol de administración a un grupo de roles es el mejor modo, y el más sencillo, de revocar los permisos concedidos a un grupo de administradores o usuarios especializados. Si quiere que los usuarios que son miembros de un grupo de roles puedan administrar una característica, debe agregar el rol de administración que administra la característica al grupo de roles. Una vez agregado el rol, los miembros del grupo de roles recibirán los permisos que el rol proporciona.

## Usar el EAC para agregar un rol de administración a un grupo de roles


> [!IMPORTANT]
> No puede usar el EAC para agregar roles a un grupo de roles si usó el Shell para configurar varios ámbitos de roles de administración o ámbitos exclusivos del grupo de roles. Si configuró varios ámbitos o ámbitos exclusivos en el grupo de roles, deberá utilizar los procedimientos del Shell que se describen más adelante en este tema para agregar roles al grupo de roles. Para obtener más información sobre los ámbitos de roles de administración, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Descripción de los ámbitos de roles de administración</A>.



1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de roles al que quiere agregar un rol y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la sección **Roles**, seleccione los roles que quiere agregar al grupo de roles.

4.  Cuando termine de agregar roles al grupo de roles, haga clic en **Guardar**.

## Utilice el Shell para crear una asignación de funciones sin ámbito

Puede crear una asignación de funciones sin ámbito entre una función y un grupo de funciones. Al hacer esto, se aplican los ámbitos implícitos de lectura y escritura de la función.

Use la siguiente sintaxis para asignar una función sin ámbito a un grupo de funciones: Si no se especifica, se crea automáticamente un nombre de asignación de roles.

```powershell
New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name>
```

Este ejemplo asigna la función de administración de reglas de transporte al grupo de función Compatibilidad con Seattle.

```powershell
New-ManagementRoleAssignment -SecurityGroup "Seattle Compliance" -Role "Transport Rules"
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Utilice el Shell para crear una asignación de funciones con un ámbito predefinido

Si un ámbito predefinido cumple sus requisitos de negocio, puede aplicar dicho ámbito a la asignación de funciones en lugar de crear uno nuevo. Para obtener una lista con los ámbitos predefinidos y sus descripciones, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Para obtener más información acerca de las asignaciones de roles, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Utilice la siguiente sintaxis para asignar una función a un grupo de funciones con un ámbito predefinido. Si no se especifica, se crea automáticamente un nombre de asignación de roles.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientRelativeWriteScope < MyGAL | MyDistributionGroups | Organization | Self >
```

Este ejemplo asigna la función de seguimiento de mensajes al grupo de funciones Soporte corporativo y aplica el ámbito predefinido de organización.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Enterprise Support" -Role "Message Tracking" -RecipientRelativeWriteScope Organization
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Utilice el Shell para crear una asignación de funciones con un ámbito de destinatarios basado en filtros

Si crea un ámbito de destinatarios basado en filtros, debe incluir el ámbito en el comando que se utiliza para asignar la función a un grupo de funciones utilizando el parámetro *CustomRecipientWriteScope*.

También puede incluir un ámbito de escritura de configuración cuando crea una asignación de funciones que tiene un ámbito de escritura de destinatario.

Para obtener más información acerca de las asignaciones de funciones y los ámbitos, consulte los siguientes temas:

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

Utilice la siguiente sintaxis para asignar una función a un grupo de funciones con un ámbito de destinatarios basado en filtros. Si no se especifica, se crea automáticamente un nombre de asignación de roles.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomRecipientWriteScope <role scope name>
```

Este ejemplo asigna la función de seguimiento de mensajes al grupo de funciones Administradores de destinatarios de Seattle y aplica el ámbito Destinatarios de Seattle.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Message Tracking" -CustomRecipientWriteScope "Seattle Recipients"
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Uso del Shell para crear una asignación de roles con un ámbito de configuración

Si crea un ámbito basado en listas o filtros de configuración de un servidor o una base de datos, debe incluir el ámbito en el comando que se utiliza para asignar la función a un grupo de roles utilizando el parámetro *CustomConfigWriteScope*.

También puede incluir un ámbito de escritura de destinatario cuando crea una asignación de funciones que tiene un ámbito de escritura de configuración.

Para obtener más información acerca de las asignaciones de funciones y los ámbitos de administración, consulte los siguientes temas:

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

Utilice la siguiente sintaxis para asignar un rol a un grupo con un ámbito de configuración. Si no se especifica, se crea automáticamente un nombre de asignación de roles.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -CustomConfigWriteScope <role scope name>
```

Este ejemplo asigna la función de bases de datos al grupo de funciones Administradores de destinatarios de Seattle y aplica el ámbito Servidores de Seattle.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Seattle Server Admins" -Role "Databases" -CustomConfigWriteScope "Seattle Servers"
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Utilice el Shell para crear una asignación de funciones con un ámbito OU

Si desea asignar un ámbito de escritura de una función a una OU, puede especificar la OU directamente en el parámetro *RecipientOrganizationalUnitScope*.

Para obtener más información acerca de las asignaciones de funciones y los ámbitos de administración, consulte los siguientes temas:

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

Utilice el siguiente comando para asignar una función a un grupo de funciones y limitar el ámbito de escritura de una función a una OU específica. Si no se especifica, se crea automáticamente un nombre de asignación de roles.

```powershell
    New-ManagementRoleAssignment -SecurityGroup <role group name> -Role <role name> -RecipientOrganizationalUnitScope <OU>
```

Este ejemplo asigna la función de destinatarios de correo al grupo de funciones Administradores de destinatarios de Seattle y aplica el ámbito de asignación a la OU Ventas/Usuarios del dominio Contoso.com.

```powershell
    New-ManagementRoleAssignment -SecurityGroup "Seattle Recipient Admins" -Role "Mail Recipients" -RecipientOrganizationalUnitScope contoso.com/sales/users
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se agregaron correctamente roles al grupo de roles, haga lo siguiente:

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de roles al que agregó roles. En el panel de detalles del grupo de roles, compruebe que estén incluidos los roles que agregó.

## Quitar un rol de un grupo de roles

Quitar un rol de un grupo de roles de administración es el mejor modo, y el más sencillo, de revocar los permisos concedidos a un grupo de administradores o usuarios especializados. Si no quiere que los administradores o usuarios especializados dispongan de permiso para administrar una característica, puede quitar el rol de administración del grupo de roles de administración que administra los permisos. Después de eliminar el rol, los miembros del grupo de roles ya no tendrán permiso para administrar la característica.


> [!NOTE]
> Algunos grupos de roles, por ejemplo Administración de la organización, limitan las funciones que se pueden quitar de un grupo de roles. Para obtener más información, consulte <A href="understanding-management-role-groups-exchange-2013-help.md">Descripción de los grupos de roles de administración</A>.<BR>Si se asigna un administrador a otro grupo de roles que contenga roles de administración que permitan administrar la característica, debe quitar el administrador de los otros grupos de roles, o bien quitar el rol que permite administrar la característica desde los otros grupos de roles.



## Usar el EAC para quitar un rol de administración de un grupo de roles


> [!IMPORTANT]
> No podrá usar el EAC para eliminar roles de un grupo de roles si usó el Shell para configurar varios ámbitos o ámbitos exclusivos en el grupo de roles. Si configuró varios ámbitos o ámbitos exclusivos en el grupo de roles, deberá usar los procedimientos del Shell que se explican más adelante en este tema para eliminar roles del grupo de roles. Para obtener más información sobre los ámbitos de roles de administración, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Descripción de los ámbitos de roles de administración</A>.



1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de roles del que quiere quitar un rol y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la sección **Roles**, seleccione los roles que quiere quitar del grupo de roles.

4.  Cuando termine de quitar los roles del grupo de roles, haga clic en **Guardar**.

## Uso del Shell para quitar un rol de un grupo de roles

Puede eliminar roles de los grupos de roles recuperando la asignación de rol de administración asociada mediante el cmdlet **Get-ManagementRoleAssignment** y canalizando la asignación del rol que se devuelve al cmdlet **Remove-ManagementRoleAssignment**. A no ser que quiera eliminar las asignaciones de roles normales y por delegación al mismo tiempo, especifique el parámetro *Delegating* para indicar si quiere eliminar las asignaciones de roles normales o por delegación.

Para obtener más información acerca de las asignaciones de funciones normales o de delegación, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Este procedimiento utiliza la canalización. Para obtener más información acerca de la canalización, consulte [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\)).

Para quitar un rol de un grupo de roles, utilice la sintaxis siguiente.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <role group name> -Role <role name> -Delegating <$true | $false> | Remove-ManagementRoleAssignment
```

En este ejemplo, se quita el rol Grupos de distribución, que permite que los administradores pertenecientes al grupo de roles de administradores de destinatarios de Seattle administren grupos de distribución. Dado que queremos eliminar la asignación de roles que da permiso para administrar grupos de distribución, el parámetro *Delegating* se fija en `$False` para devolver solo las asignaciones de roles normales.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee "Seattle Recipient Administrators" -Role "Distribution Groups" -Delegating $false | Remove-ManagementRoleAssignment
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Remove-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351205\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se quitaron correctamente los roles del grupo de roles, haga lo siguiente:

1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de roles al que le quitó roles. En el panel de detalles del grupo de roles, compruebe que no estén incluidos los roles que quitó.

## Cambiar el ámbito de un grupo de roles

Las asignaciones de roles de administración entre un grupo de roles y un rol contienen ámbitos de administración que determinan qué objetos están disponibles para los miembros de cada grupo de roles. Al cambiar el ámbito de escritura en un grupo de roles, puede cambiar los objetos disponibles para que los miembros del grupo de roles puedan crear, cambiar o quitar. No se puede cambiar el ámbito de lectura en un grupo de roles.

Exchange 2013 incluye ámbitos que se aplican de forma predeterminada a asignaciones de roles cuando no se crean ámbitos personalizados. Si quiere usar un ámbito personalizado con una asignación de roles en un grupo de roles, primero debe crearlo. Para obtener más información sobre la creación de ámbitos personalizados, que es una tarea avanzada, consulte [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

Para obtener más información sobre los ámbitos y las asignaciones de roles de administración en Exchange 2013, consulte los siguientes temas:

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

## Usar el EAC para cambiar el ámbito en un grupo de roles

Al usar el EAC para cambiar el ámbito de un grupo de roles, en realidad se está cambiando el ámbito en todas las asignaciones de roles entre el grupo de roles y cada uno de los roles de administración asignados al grupo de roles. Si quiere cambiar el ámbito de asignaciones de roles específicos, debe usar los procedimientos del Shell que aparecen más adelante en este tema.


> [!IMPORTANT]
> No se puede usar el EAC para administrar los ámbitos en las asignaciones de roles entre los roles y un grupo de roles si usó el Shell para configurar varios ámbitos o ámbitos exclusivos en esas asignaciones de roles. Si configuró varios ámbitos o ámbitos exclusivos en esas asignaciones de roles, debe usar los procedimientos del Shell que aparecen más adelante en este tema para administrar ámbitos. Para obtener más información sobre los ámbitos de roles de administración, consulte <A href="understanding-management-role-scopes-exchange-2013-help.md">Descripción de los ámbitos de roles de administración</A>.



1.  En el EAC, vaya a **Permisos** \> **Funciones de administración**.

2.  Seleccione el grupo de roles en el que quiere cambiar el ámbito y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Seleccione una de las dos siguientes opciones de **Ámbito de escritura**:
    
      - Un ámbito de escritura en la casilla desplegable, donde puede seleccionar el ámbito de escritura predeterminado o un ámbito de escritura personalizado.
    
      - **Unidad organizativa**   Seleccione esta opción y proporcione una unidad organizativa (OU) si desea configurar el ámbito de este grupo de funciones a una OU.

4.  Haga clic en **Guardar** para guardar los cambios realizados en el grupo de funciones.

## Usar el Shell para cambiar el ámbito de todas las asignaciones de funciones en un grupo de funciones al mismo tiempo

Las asignaciones de roles entre el grupo de funciones y los que tiene asignados pueden usar el ámbito implícito obtenido desde los mismos roles, el mismo ámbito personalizado o distintos ámbitos personalizados. Para obtener más información acerca de las asignaciones de roles, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Los ámbitos de las asignaciones de roles se administran mediante el uso del cmdlet **Set-ManagementRoleAssignment**. No puede administrar ámbitos mediante el cmdlet **Set-RoleGroup**.

Para cambiar el ámbito de todas las asignaciones de funciones entre un grupo de funciones y un conjunto de funciones de administración al mismo tiempo, en primer lugar, debe recuperar las asignaciones de funciones del grupo de funciones y, luego, establecer el nuevo ámbito en cada una de las asignaciones. Puede hacerlo con el cmdlet **Get-ManagementRoleAssignment** para recuperar las asignaciones de funciones y, luego, canalizarlas con el cmdlet **Set-ManagementRoleAssignment**.

Este procedimiento usa los conceptos de la canalización y el modificador *WhatIf*. Para obtener más información al respecto, consulte los temas siguientes:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Modificadores WhatIf, Confirm y ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md)

Para establecer el ámbito en todas las asignaciones de funciones en un grupo de funciones al mismo tiempo, use la siguiente sintaxis.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee <name of role group> | Set-ManagementRoleAssignment -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
```

Usted usa solamente los parámetros necesarios para configurar el ámbito que desea usar. Por ejemplo, si desea cambiar el ámbito de destinatario de todas las asignaciones de funciones en el grupo de funciones Administración de destinatarios de ventas a Empleados de ventas directas, use el comando siguiente.

```powershell
    Get-ManagementRoleAssignment -RoleAssignee "Sales Recipient Management" | Set-ManagementRoleAssignment -CustomRecipientWriteScope "Direct Sales Employees"
```


> [!NOTE]
> Puede usar el conmutador <EM>WhatIf</EM> para comprobar qué solamente se cambien las asignaciones de funciones que desea cambiar. Ejecute el comando anterior con el conmutador <EM>WhatIf</EM> para comprobar los resultados y, luego, quite el conmutador <EM>WhatIf</EM> para aplicar los cambios.



Para obtener más información acerca del cambio de asignaciones de funciones de administración, consulte [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Usar el Shell para cambiar el ámbito de asignaciones de funciones individuales en un grupo de funciones

Las asignaciones de roles entre el grupo de funciones y los que tiene asignados pueden usar el ámbito implícito obtenido desde los mismos roles, el mismo ámbito personalizado o distintos ámbitos personalizados. Para obtener más información acerca de las asignaciones de roles, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Los ámbitos de las asignaciones de roles se administran mediante el uso del cmdlet **Set-ManagementRoleAssignment**. No puede administrar ámbitos mediante el cmdlet **Set-RoleGroup**.

Este procedimiento usa los conceptos de canalización y el cmdlet **Format-List**. Para obtener más información al respecto, consulte los temas siguientes:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

Para cambiar el ámbito de una asignación de funciones entre un grupo de funciones y una función de administración, en primer lugar, debe buscar el nombre de la asignación de funciones y, luego, establecer el ámbito de la asignación de funciones.

1.  Para encontrar los nombres de todas las asignaciones de funciones en un grupo de funciones, use el siguiente comando. Si canaliza las asignaciones de funciones de administración al cmdlet **Format-List**, podrá ver el nombre completo de la asignación.
    
    ```powershell
    Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-List Name
    ```

2.  Busque el nombre de la asignación de roles que quiere cambiar. Use el nombre de la asignación de rol en el paso siguiente.

3.  Para establecer el ámbito de una asignación individual, utilice la sintaxis siguiente.

    ```powershell
    
        Set-ManagementRoleAssignment <role assignment name> -CustomRecipientWriteScope <recipient scope name> -CustomConfigWriteScope <configuration scope name> -RecipientRelativeScopeWriteScope < MyDistributionGroups | Organization | Self> -ExclusiveRecipientWriteScope <exclusive recipient scope name> -ExclusiveConfigWriteScope <exclusive configuration scope name> -RecipientOrganizationalUnitScope <organizational unit>
    ```

Usted usa solamente los parámetros necesarios para configurar el ámbito que desea usar. Por ejemplo, si desea cambiar el ámbito de destinatario en la asignación de funciones de administración Destinatarios de correo\_Destinatarios de ventas a Todos los empleados de ventas, use el comando siguiente.

```powershell
    Set-ManagementRoleAssignment "Mail Recipients_Sales Recipient Management" -CustomRecipientWriteScope "All Sales Employees"
```

Para obtener más información acerca del cambio de asignaciones de funciones de administración, consulte [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que cambió correctamente el ámbito de una asignación de roles en un grupo de roles, haga lo siguiente:

  - Si usó el EAC para configurar el ámbito en el grupo de roles, haga lo siguiente:
    
    1.  En el EAC, vaya a **Permisos** \> **Roles de administración**. Aquí se incluyen todos los grupos de roles de su organización.
    
    2.  Seleccione un grupo de roles para ver el ámbito que está configurado en el grupo de roles.

  - Si usó el Shell para configurar el ámbito en el grupo de roles, haga lo siguiente:
    
    1.  Ejecute el siguiente comando en el Shell.

        ```powershell
            Get-ManagementRoleAssignment -RoleAssignee <role group name> | Format-Table *WriteScope
        ```
    
    2.  Compruebe que el ámbito de escritura en las asignaciones de roles haya cambiado al ámbito que especificó.

## Agregar o quitar un delegado de grupo de roles

Los delegados del grupo de roles son usuarios o grupos de seguridad universal (USG) que pueden agregar o quitar miembros de un grupo de roles o modificar las propiedades de un grupo de roles. Al agregar o quitar delegados de un grupo de roles, es posible controlar a quién se le permite administrar un grupo de roles.


> [!IMPORTANT]
> Después de agregar un delegado a un grupo de funciones, solamente los delegados del grupo de funciones podrán administrar el grupo; o bien, podrán administrarlo usuarios a quienes se les asignó, directa o indirectamente, la función de administración Administración de funciones.<BR>Si a un usuario se le asigna, directa o indirectamente, la función Administración de funciones y no se lo agrega como delegado del grupo de funciones, el usuario debe utilizar el conmutador <EM>BypassSecurityGroupManagerCheck</EM> de los cmdlets <STRONG>Add-RoleGroupMember</STRONG>, <STRONG>Remove-RoleGroupMember</STRONG>, <STRONG>Update-RoleGroupMember</STRONG> y <STRONG>Set-RoleGroup</STRONG> para administrar un grupo de funciones.




> [!NOTE]
> No puede usar el EAC para agregar un delegado a un grupo de roles.



## Usar el Shell para agregar un delegado a un grupo de funciones

Para cambiar la lista de delegados de un grupo de funciones, use el parámetro *ManagedBy* del cmdlet **Set-RoleGroup**. El parámetro *ManagedBy* sobrescribe la lista completa de delegados en el grupo de funciones. Si desea agregar delegados al grupo de funciones, en lugar de reemplazar la lista completa de delegados, siga estos pasos:

1.  Almacene el grupo de funciones en una variable mediante el siguiente comando.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  Agregue el delegado al grupo de funciones almacenado en la variable mediante el siguiente comando.
    ```powershell
        $RoleGroup.ManagedBy += (Get-User <user to add>).Identity
    ```
    

    > [!NOTE]
    > Use el cmdlet <STRONG>Get-Group</STRONG> si desea agregar un USG.



3.  Repita el paso 2 cada vez que desee agregar un delegado.

4.  Aplique la nueva lista de delegados al grupo de funciones actual mediante el siguiente comando.
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

En este ejemplo, se agrega el usuario David Strome como delegado del grupo de funciones Administración de la organización.

```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy += (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-RoleGroup](https://technet.microsoft.com/es-es/library/dd638182\(v=exchg.150\)).

## Usar el Shell para quitar un delegado de un grupo de funciones

Para cambiar la lista de delegados de un grupo de funciones, use el parámetro *ManagedBy* del cmdlet **Set-RoleGroup**. El parámetro *ManagedBy* sobrescribe la lista completa de delegados en el grupo de funciones. Si desea quitar delegados del grupo de funciones, en lugar de reemplazar la lista completa de delegados, siga estos pasos:

1.  Almacene el grupo de funciones en una variable mediante el siguiente comando.
    
    ```powershell
    $RoleGroup = Get-RoleGroup <role group name>
    ```

2.  Quite el delegado del grupo de funciones almacenado en la variable mediante el siguiente comando.
    ```powershell
        $RoleGroup.ManagedBy -= (Get-User <user to remove>).Identity
    ```
    

    > [!NOTE]
    > Use el cmdlet <STRONG>Get-Group</STRONG> si desea quitar un USG.



3.  Repita el paso 2 cada vez que desee quitar un delegado.

4.  Aplique la nueva lista de delegados al grupo de funciones actual mediante el siguiente comando.
    
    ```powershell
    Set-RoleGroup <role group name> -ManagedBy $RoleGroup.ManagedBy
    ```

En este ejemplo, se quita al usuario David Strome como delegado del grupo de funciones Administración de la organización.
```powershell
    $RoleGroup = Get-RoleGroup "Organization Management"
    $RoleGroup.ManagedBy -= (Get-User "David Strome").Identity
    Set-RoleGroup "Organization Management" -ManagedBy $RoleGroup.ManagedBy
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-RoleGroup](https://technet.microsoft.com/es-es/library/dd638182\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que se cambió correctamente la lista de delegados en un grupo de roles, haga lo siguiente:

1.  En el Shell, ejecute el siguiente comando.
    
    ```powershell
    Get-RoleGroup <role group name> | Format-List ManagedBy
    ```

2.  Compruebe que los delegados que aparecen en la propiedad *ManagedBy* solo sean los delegados capaces de administrar el grupo de roles.

