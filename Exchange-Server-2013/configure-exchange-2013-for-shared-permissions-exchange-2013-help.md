---
title: 'Configurar Exchange 2013 para permisos compartidos: Exchange 2013 Help'
TOCTitle: Configurar Exchange 2013 para permisos compartidos
ms:assetid: 7d119977-b420-4b66-acf0-0a978b188cdd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638146(v=EXCHG.150)
ms:contentKeyID: 49895738
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar Exchange 2013 para permisos compartidos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Los permisos compartidos le permiten, como administrador de Microsoft Exchange Server 2013, crear entidades de seguridad de Active Directory, tales como usuarios y, luego, configurarlos como destinatarios de Exchange. A diferencia de los permisos divididos, que dividen las tareas de administración entre grupos de administradores de Exchange y administradores de Active Directory, no existe la división de tareas con los permisos compartidos.

Para obtener más información acerca de los permisos compartidos y divididos, consulte [Descripción de los permisos divididos](understanding-split-permissions-exchange-2013-help.md).

Puede configurar la organización de Exchange 2013 para permisos compartidos si ya estableció los permisos divididos en la organización. El procedimiento para cambiar los permisos compartidos es diferente según si está usando los permisos divididos del Control de acceso basado en roles (RBAC) o de Active Directory. Seleccione el procedimiento siguiente que se aplica a la configuración actual. Si se cumplen las siguientes condiciones, la organización usa permisos divididos de Active Directory:

  - La unidad de organización (OU) de grupos protegidos de Microsoft Exchange existe.

  - El grupo de seguridad de permisos de Exchange Windows se encuentra en la OU de los grupos protegidos de Microsoft Exchange.

  - El grupo de seguridad del subsistema de confianza de Exchange es miembro del grupo de permisos de Exchange Windows.

  - No hay asignaciones de funciones de administración regulares para la función Creación de destinatario de correo o la función Pertenencia y creación del grupo de seguridad.

Si nunca ha configurado los permisos divididos en la organización, no es necesario que realice este procedimiento. Exchange 2013 está configurado para permisos compartidos de forma predeterminada.

Para obtener más información acerca de grupos de funciones de administración, funciones de administración y asignaciones de funciones de administraciones regulares y delegadas, consulte los siguientes temas:

  - [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md)

  - [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md)

  - [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

¿Está buscando otras tareas de administración relacionadas con permisos? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Los procedimientos descritos en este tema requieren permisos específicos. Vea cada procedimiento para ver la información de permisos.

  - Debe utilizar Windows PowerShell, el Shell de comandos de Windows o bien ambos para realizar estos procedimientos. Para obtener más información, consulte todos los procedimientos.

  - La organización de Exchange 2013 debe estar configurada para permisos divididos de RBAC o de Active Directory.

  - Si dispone de servidores Microsoft Exchange Server 2010 en su organización, el modelo de permisos que seleccione también se aplicará a dichos servidores.

  - Debe tener permisos para delegar la función de administración Creación de destinatarios de correo y la función de administración Pertenencia y creación de grupos de seguridad en el grupo de funciones de administración de Administración de la organización o en otro grupo de funciones que tenga asignada la función Destinatarios de correo.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Cambie de los permisos divididos de RBAC a los permisos compartidos

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

Para cambiar de los permisos divididos de RBAC a los permisos compartidos de Exchange 2013, debe asignar la función Creación de destinatarios de correo y la función Pertenencia y creación de grupos de seguridad a un grupo de funciones que tenga asignada además la función Destinatarios de correo y cuente con administradores de Exchange 2013 como miembros. En la configuración predeterminada de permisos compartidos, el grupo de funciones Administración de la organización incluye cada una de estas funciones. Es por ello que el grupo de funciones Administración de la organización figura en este procedimiento.

## Configure permisos compartidos

Para configurar permisos compartidos en el grupo de funciones Administración de la organización, realice las siguientes acciones con una cuenta que tenga permisos para delegar asignaciones de funciones para la función Creación de destinatarios de correo y la función Pertenencia y creación de grupos de seguridad:

1.  Use los siguientes comandos para agregar asignaciones de funciones de delegación para la función Creación de destinatario de correo y Pertenencia y creación de grupos de seguridad al grupo de funciones de Administración de la organización.
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management" -Delegating
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management" -Delegating
    

    > [!NOTE]
    > El grupo de funciones (en este procedimiento, grupo de funciones de administradores de Active Directory) que tiene asignaciones de funciones delegadas para la función Creación de destinatario de correo y para la función Pertenencia y creación de grupo de seguridad debe tener asignada la función Administración de funciones para ejecutar el cmdlet <STRONG>New-ManagementRoleAssignment</STRONG>. Este usuario al que se le asignan funciones y que puede delegar la función Administración de funciones debe asignar dicha función al grupo de funciones Administradores de Active Directory.



2.  Con los siguientes comandos, agregue asignaciones de funciones regulares a la función Creación de destinatarios de correo a los grupos de funciones Administración de la organización y Recipient Management.
    
        New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Recipient Management"

3.  Agregue una asignación de función regular a la función Pertenencia y creación de grupos de seguridad al grupo de funciones Administración de la organización con el comando siguiente.
    
        New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

## Quite permisos de administradores de Active Directory (opcional)

Como opción, puede quitar los permisos concedidos a los administradores de Active Directory si ya no desea que puedan crear o administrar objetos de Active Directory con las herramientas de administración de Exchange. Si desea quitar los permisos de los administradores de Active Directory, lleve a cabo este procedimiento.


> [!NOTE]
> Aunque puede quitarle a los administradores de Active Directory los permisos para administrar objetos de Active Directory con herramientas de administración de Exchange, los administradores de Active Directory pueden continuar administrando objetos de Active Directory con herramientas de administración de Active Directory si sus permisos de Active Directory así lo permiten. No obstante, no podrán administrar atributos específicos de Exchange en objetos de Active Directory. Para obtener más información, consulte <A href="understanding-split-permissions-exchange-2013-help.md">Descripción de los permisos divididos</A>.



Para quitar permisos divididos relacionados con Exchange a los administradores de Active Directory, realice las siguientes acciones:

1.  Quite las asignaciones de funciones regulares y de delegación que asignan la función Creación de destinatarios de correo al grupo de funciones o al grupo de seguridad universal (USG) que incluye a los administradores de Active Directory como usuarios con el siguiente comando. Este comando usa el grupo de funciones Administradores de Active Directory como un ejemplo. El conmutador *WhatIf* permite ver cuáles asignaciones de roles se quitarán. Quite el conmutador *WhatIf* y ejecute nuevamente el comando para quitar las asignaciones de roles.
    
        Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

2.  Elimine las asignaciones de roles habituales y de delegación que asignan al rol Pertenencia y creación de grupos de seguridad al grupo de roles o bien el USG que incluye a los administradores de Active Directory como usuarios con el siguiente comando. Este comando usa el grupo de funciones Administradores de Active Directory como un ejemplo. El conmutador *WhatIf* permite ver cuáles asignaciones de roles se quitarán. Quite el conmutador *WhatIf* y ejecute nuevamente el comando para quitar las asignaciones de roles.
    
        Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -EQ "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

3.  Opcional. Si desea quitarles todos los permisos de Exchange a los administradores de Active Directory, puede quitar el grupo de funciones o el USG del cual son miembros. Si desea obtener más información acerca de cómo eliminar un grupo de funciones, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)) o [Remove-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351205\(v=exchg.150\)).

## Cambie de los permisos divididos de Active Directory a los permisos compartidos

Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el La entrada "Permisos divididos de Active Directory" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

Para cambiar de los permisos divididos de Active Directory a los permisos compartidos de Exchange 2013, debe volver a ejecutar el Asistente de instalación de Exchange para deshabilitar los permisos divididos de Active Directory en la organización de Exchange y, luego, crear asignaciones de funciones entre un grupo de funciones y la función Creación de destinatario de correo y la función Pertenencia y creación de un grupo de seguridad. En la configuración predeterminada de permisos compartidos, el grupo de funciones Administración de la organización incluye cada una de estas funciones. Es por ello que el grupo de funciones Administración de la organización figura en este procedimiento.


> [!IMPORTANT]
> El comando setup.com en este procedimiento realiza cambios en Active Directory. Debe usar una cuenta que disponga de los permisos requeridos para realizar estos cambios. Es posible que esta cuenta no sea la misma cuenta que tiene permisos para crear asignaciones de roles con el cmdlet <STRONG>New-ManagementRoleAssignment</STRONG>. Use la cuenta o las cuentas con los permisos necesarios para completar de manera satisfactoria cada paso de este procedimiento.



Para cambiar de permisos divididos de Active Directory a permisos compartidos, realice lo siguiente:

1.  Desde un shell de comandos de Windows, ejecute el siguiente comando desde los medios de instalación de Exchange 2013 para deshabilitar los permisos divididos de Active Directory.
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false

2.  Desde el Shell de administración de Exchange, ejecute los siguientes comandos para agregar asignaciones de funciones regulares entre la función Creación de destinatario de correo y la función Administración y creación de grupos de seguridad y los grupos de funciones Administración de la organización y Recipient Management.
    
        New-ManagementRoleAssignment "Mail Recipient Creation_Organization Management" -Role "Mail Recipient Creation" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Security Group Creation and Membership_Org Management" -Role "Security Group Creation and Membership" -SecurityGroup "Organization Management"
        New-ManagementRoleAssignment "Mail Recipient Creation_Recipient Management" -Role "Mail Recipient Creation" -SecurityGroup "Recipient Management"

3.  Reinicie los servidores Exchange 2013 en la organización.
    

    > [!NOTE]
    > Si dispone de servidores Exchange 2010 en su organización, también deberá reiniciar dichos servidores.



Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

