---
title: 'Administrar directivas de asignación de funciones: Exchange 2013 Help'
TOCTitle: Administrar directivas de asignación de funciones
ms:assetid: f93d502e-5df4-4ba0-b68d-01a17ccffb4d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657511(v=EXCHG.150)
ms:contentKeyID: 49896028
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administrar directivas de asignación de funciones

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-09_

Si desea personalizar los permisos que asigna a un grupo de usuarios finales, cree una nueva directiva de asignación de roles de administración. La directiva de asignación que crea se puede personalizar para adecuarla a los requisitos concretos del usuario final. Para obtener más información acerca de las directivas de asignación en Microsoft Exchange Server 2013, consulte [Descripción de las directivas de asignación de roles de administración](understanding-management-role-assignment-policies-exchange-2013-help.md).

¿Busca otras tareas de administración relacionadas con los permisos de administración? Consulte [Permisos](permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de asignación" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Agregar una directiva de asignación

Una vez creada la nueva directiva de asignación, puede asignarle usuarios. Para obtener más información, consulte [Cambiar la directiva de asignación en un buzón](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

## Uso del EAC para crear una nueva directiva de asignación


> [!NOTE]
> Únicamente puede crear directivas de asignación explícita mediante el Centro de administración de Exchange (EAC). Para crear una nueva directiva de asignación predeterminada, debe usar el Shell de administración de Exchange. Para obtener más información, consulte la sección "Uso del Shell para crear una directiva de asignación predeterminada", más adelante en este tema.



1.  En el EAC, vaya a **Permisos** \> **Roles de usuario** y, a continuación, haga clic en **Agregar**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  En la ventana de directiva de asignación de roles, especifique un nombre para la nueva directiva de asignación.

3.  Active la casilla que hay junto al rol o los roles que desea añadir a la directiva de asignación. Puede seleccionar varios roles, incluyendo los roles de usuario final que ha agregado. Si selecciona un rol con roles subordinados, estos se seleccionan automáticamente.

4.  Haga clic en **Guardar** para guardar los cambios en la directiva de asignación.

## Uso del Shell para crear una directiva de asignación explícita

Para crear una directiva de asignación explícita que se pueda asignar manualmente a buzones, use la sintaxis siguiente.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign>

En este ejemplo, se crea la directiva de asignación explícita Limited Mailbox Configuration y se le asignan los roles `MyBaseOptions`, `MyAddressInformation` y `MyDisplayName`.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638101\(v=exchg.150\)).

## Uso del Shell para crear una directiva de asignación predeterminada

Para crear una directiva de asignación predeterminada asignada a buzones nuevos, utilice la sintaxis siguiente.

    New-RoleAssignmentPolicy <assignment policy name> -Roles <roles to assign> -IsDefault

En este ejemplo, se crea la directiva de asignación predeterminada Limited Mailbox Configuration y se le asignan los roles `MyBaseOptions`, `MyAddressInformation` y `MyDisplayName`.

    New-RoleAssignmentPolicy "Limited Mailbox Configuration" -Roles MyBaseOptions, MyAddressInformation, MyDisplayName -IsDefault

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638101\(v=exchg.150\)).

## Quitar una directiva de asignación

Si ya no necesita la directiva de asignación de funciones de administración, puede quitarla.

## ¿Qué necesita saber antes de comenzar?

  - Todos los usuarios que tengan asignada la directiva de asignación deben cambiarse a otra directiva de asignación. Para obtener más información acerca de cambiar a una directiva de asignación en un buzón, consulte [Cambiar la directiva de asignación en un buzón](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).

  - Deben quitarse todas las asignaciones de funciones de administración entre la directiva de asignación y las funciones de administración asignadas. Para obtener más información sobre cómo quitar una asignación de roles de una directiva de asignación, consulte la sección Utilice el Shell para quitar una función de una directiva de asignación más adelante en este tema.

  - Si desea quitar una directiva de asignación predeterminada, debe tratarse de la última directiva de asignación de la organización de Exchange 2013.

## Uso del EAC para quitar una directiva de asignación

1.  En el EAC, vaya a **Permisos** \> **Roles de usuario**.

2.  Seleccione la directiva de asignación que desea quitar y, a continuación, haga clic en **Eliminar**![Eliminar icono](images/Dd979797.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif "Eliminar icono").

## Uso del Shell para quitar una directiva de asignación

Para quitar una directiva de asignación, use la sintaxis siguiente.

    Remove-RoleAssignmentPolicy <role assignment policy>

En este ejemplo se quita la directiva de asignación de usuarios temporales de Nueva York.

    Remove-RoleAssignmentPolicy "New York Temporary Users"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638190\(v=exchg.150\)).

## Ver una lista de las directivas de asignación o detalles de la directiva de asignación

Puede ver directivas de asignación de roles de administración de varias maneras, según la información que desea y si está usando el EAC o el Shell.

En el EAC, puede ver la lista de directivas de asignación y los roles asignados a estas directivas. En el Shell, puede visualizar todas las directivas de asignación de su organización, hacer una lista de los buzones de correo que tienen asignada una directiva específica y más.

## Uso del EAC para ver una lista de directivas de asignación

1.  En el EAC, vaya a **Permisos** \> **Roles de usuario**. Aquí se muestran todas las directivas de asignación de la organización.

2.  Para ver los detalles de una directiva de asignación específica, seleccione la directiva de asignación que desea ver. Las descripciones y los roles asignados a la directiva de asignación se muestran en el panel de detalles.

## Usar el Shell para ver una lista de las directivas de asignación

Puede ver una lista de todas las directivas de asignación de la organización sin especificar directivas de asignación cuando ejecute el cmdlet **Get-RoleAssignmentPolicy**.

Este procedimiento hace uso de la canalización y el cmdlet **Format-Table**. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

Use el siguiente comando para devolver una lista de todas las directivas de asignación en la organización.

    Get-RoleAssignmentPolicy

Para devolver una lista de propiedades específicas para todas las directivas de asignación en la organización, puede canalizar los resultados al cmdlet **Format-Table** y especificar las propiedades que desee incluir en la lista de resultados. Use la siguiente sintaxis.

    Get-RoleAssignmentPolicy | Format-Table <property 1>, <property 2...>

En este ejemplo, se devuelve una lista de todas las directivas de asignación en la organización y se incluyen las propiedades **Name** y **IsDefault**.

    Get-RoleAssignmentPolicy | Format-Table Name, IsDefault

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638195\(v=exchg.150\)).

## Usar el Shell para ver los detalles de una directiva de asignación única

Puede ver los detalles de una directiva de asignación específica utilizando el cmdlet **Get-RoleAssignmentPolicy** y canalizando el resultado al cmdlet **Format-List**.

Este procedimiento hace uso de la canalización y el cmdlet **Format-List**. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

Para ver los detalles de una directiva de asignación específica, use la sintaxis siguiente.

    Get-RoleAssignmentPolicy <assignment policy name> | Format-List

En este ejemplo, se ven los detalles sobre los usuarios de Redmond (sin directivas de asignación de mensajería de texto).

    Get-RoleAssignmentPolicy "Redmond Users - no Text Messaging" | Format-List

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638195\(v=exchg.150\)).

## Usar el Shell para encontrar la directiva de asignación predeterminada

Puede encontrar la directiva de asignación predeterminada canalizando el resultado del cmdlet **Get-RoleAssignmentPolicy** al cmdlet **Where**. Con el cmdlet **Where**, filtre los datos devueltos para ver solamente la directiva de asignación que tenga la propiedad *IsDefault* establecida en `$True`.

Este procedimiento hace uso de la canalización y del cmdlet **Where**. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

En este ejemplo se devuelve la directiva de asignación predeterminada.

    Get-RoleAssignmentPolicy | Where { $_.IsDefault -eq $True }

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638195\(v=exchg.150\)).

## Usar el Shell para ver los buzones que tienen asignada una directiva específica

Puede encontrar todos los buzones de correo asignados a una directiva de asignación específica canalizando el resultado del cmdlet **Get-Mailbox** al cmdlet **Where**. Con el cmdlet **Where**, filtre los datos devueltos para ver solamente los buzones que tengan la propiedad *RoleAssignmentPolicy* establecida en el nombre de directiva de asignación especificado.

Este procedimiento hace uso de la canalización y del cmdlet **Where**. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:

  - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))

  - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

Use la siguiente sintaxis.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "<role assignment policy>" }

En este ejemplo, se muestran todos los buzones que tienen asignada la directiva de usuarios finales de Vancouver.

    Get-Mailbox | Where { $_.RoleAssignmentPolicy -Eq "Vancouver End Users" }

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) o [Get-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638195\(v=exchg.150\)).

## Cambiar la directiva de asignación predeterminada

Puede cambiar la directiva de asignación de funciones de administración asignada a los buzones de correo que se crean. Al cambiar la directiva de asignación de roles predeterminada, no se cambia la directiva de asignación de los buzones de correo existentes. Para cambiar la directiva de asignación de los buzones de correo existentes, consulte [Cambiar la directiva de asignación en un buzón](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md).


> [!NOTE]
> No puede usar el EAC para cambiar la directiva de asignación predeterminada. Debe usar el Shell.



## Uso del Shell para cambiar la directiva de asignación predeterminada

Para cambiar la directiva de asignación predeterminada, utilice la sintaxis siguiente.

    Set-RoleAssignmentPolicy <assignment policy name> -IsDefault

En este ejemplo, Vancouver End Users se establece como directiva de asignación predeterminada.

    Set-RoleAssignmentPolicy "Vancouver End Users" -IsDefault


> [!IMPORTANT]
> Se asignan nuevos buzones de correo a la directiva de asignación predeterminada aunque ésta no tenga asignadas funciones de administración. Los buzones de correo que tienen directivas de asignación sin roles de administración no pueden acceder a ninguna característica de configuración de buzones en Microsoft Outlook Web App.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-RoleAssignmentPolicy](https://technet.microsoft.com/es-es/library/dd638090\(v=exchg.150\)).

## Agregar un rol a una directiva de asignación

## Uso del EAC para agregar un rol a una directiva de asignación

1.  En el EAC, vaya a **Permisos** \> **Roles de usuario**.

2.  Seleccione la directiva de asignación a la cual desea agregar uno o más roles y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Active la casilla que hay junto al rol o los roles que desea añadir a la directiva de asignación. Puede seleccionar varios roles, incluyendo los roles de usuario final que ha agregado. Si selecciona un rol con roles subordinados, estos se seleccionan automáticamente.

4.  Haga clic en **Guardar** para guardar los cambios en la directiva de asignación.

## Usar en Shell para agregar una función a una directiva de asignación

Para crear una asignación de funciones de administración entre una función y una directiva de asignaciones, use la sintaxis siguiente.

    New-ManagementRoleAssignment -Name <role assignment name> -Role <role name> -Policy <assignment policy name>

En este ejemplo, se crea la asignación de funciones usuarios de Seattle\_correo de voz entre la función MyVoicemail y la directiva de asignación usuarios de Seattle.

    New-ManagementRoleAssignment -Name "Seattle Users - Voicemail" -Role MyVoicemail -Policy "Seattle Users"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Quitar un rol de una directiva de asignación

Si no desea que los usuarios finales tengan permiso para administrar determinadas características del buzón de correo o grupo de distribución, puede quitar el rol de administración que concede los permisos de la directiva de asignación de roles de administración a la que está asignado el usuario. Si otros usuarios tienen asignada la misma directiva de asignación, también perderán la capacidad de administrar esa función.

## Uso del EAC para quitar un rol de una directiva de asignación

1.  En el EAC, vaya a **Permisos** \> **Roles de usuario**.

2.  Seleccione la directiva de asignación de la que desea quitar uno o más roles y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  Desactive la casilla situada junto al rol o los roles que desea quitar de la directiva de asignación. Si desactiva la casilla de un rol con roles secundarios, las casillas de los roles secundarios también se desactivarán.

4.  Haga clic en **Guardar** para guardar los cambios en la directiva de asignación.

## Utilice el Shell para quitar una función de una directiva de asignación

Puede quitar funciones de las políticas de asignación recuperando la asignación de roles de administración asociada con el cmdlet **Get-ManagementRoleAssignment** y, a continuación, canalizando la asignación de roles devuelta al cmdlet **Remove-ManagementRoleAssignment**.

Para obtener más información acerca de las asignaciones de funciones normales o de delegación, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Este procedimiento utiliza la canalización. Para obtener más información acerca de la canalización, consulte [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\)).

Para quitar un rol de una directiva de asignación, use la sintaxis siguiente.

    Get-ManagementRoleAssignment -RoleAssignee <assignment policy name> -Role <role name> | Remove-ManagementRoleAssignment

En este ejemplo se quita el rol de administración MyVoicemail que permite a los usuarios administrar las opciones de correo de voz desde la directiva de asignación Usuarios de Seattle.

    Get-ManagementRoleAssignment -RoleAssignee "Seattle Users" -Role MyVoicemail | Remove-ManagementRoleAssignment

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351205\(v=exchg.150\)).

