---
title: 'Configurar Exchange 2013 para permisos divididos: Exchange 2013 Help'
TOCTitle: Configurar Exchange 2013 para permisos divididos
ms:assetid: 8c74f893-a6f3-4869-8571-3bc0f662cc87
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638155(v=EXCHG.150)
ms:contentKeyID: 49895765
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar Exchange 2013 para permisos divididos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Los permisos divididos habilitan a dos grupos distintos, como administradores de Active Directory y administradores de Microsoft Exchange Server 2013, para administrar sus respectivos servicios, objetos y atributos. Los administradores de Active Directory administran entidades de seguridad, como usuarios que proporcionan permisos de acceso a un bosque Active Directory. Los administradores de Exchange administran los atributos relacionados con Exchange en objetos de Active Directory, y la creación y administración de objetos específicos de Exchange.

Microsoft Exchange Server 2013 ofrece los siguientes tipos de modelos de permisos divididos:

  - **Permisos divididos de RBAC**   Los permisos para crear entidades de seguridad en las particiones del dominio de Active Directory son controlados por el Control de acceso basado en roles (RBAC). Solo aquellas personas que son miembros de los grupos de funciones apropiados pueden crear entidades de seguridad.

  - **Permisos divididos de Active Directory**   Los permisos para crear entidades de seguridad en la partición de dominio de Active Directory se quitan completamente de cualquier usuario, servicio o servidor de Exchange. En el RBAC, no se brinda ninguna opción para crear entidades de seguridad. La creación de entidades de seguridad en Active Directory se debe realizar mediante el uso de las herramientas de administración de Active Directory.
    

    > [!NOTE]
    > Los permisos divididos de Active Directory están disponibles en las organizaciones que ejecuten Exchange Server 2010 Service Pack 1 (SP1) o una versión posterior, Exchange&nbsp;2013, o bien ambas versiones de Exchange.



El modelo que usted elija dependerá de la estructura y las necesidades de su organización. A continuación, elija el procedimiento que sea aplicable al modelo que desea configurar. Recomendamos que use el modelo de permisos divididos de RBAC. El modelo de permisos divididos de RBAC brinda mucho más flexibilidad y, al mismo tiempo, brinda la misma separación de administración que los permisos divididos de Active Directory.

Para obtener más información acerca de los permisos compartidos y divididos, consulte [Descripción de los permisos divididos](understanding-split-permissions-exchange-2013-help.md).

Para obtener más información acerca de grupos de funciones de administración, funciones de administración y asignaciones de funciones de administraciones regulares y delegadas, consulte los siguientes temas:

  - [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md)

  - [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md)

  - [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

¿Está buscando otras tareas de administración relacionadas con permisos? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el La entrada "Permisos divididos de Active Directory" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe utilizar Windows PowerShell, el Shell de comandos de Windows o bien ambos para realizar estos procedimientos. Para obtener más información, consulte todos los procedimientos.

  - Si dispone de servidores Exchange 2010 en su organización, el modelo de permisos que seleccione también se aplicará a dichos servidores.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Cambie a permisos divididos de RBAC

Puede configurar la organización de Exchange 2013 para los permisos divididos de RBAC. Al finalizar, solo los administradores de Active Directory podrán crear entidades de seguridad de Active Directory. Esto significa que los administradores de Exchange no podrán usar los siguientes cmdlets:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Los administradores de Exchange solo podrán administrar los atributos de Exchange en entidades de seguridad de Active Directory existentes. No obstante, podrán crear y administrar objetos específicos de Exchange, como reglas de transporte y grupos de distribución. Para obtener más información, consulte la sección "Permisos divididos de RBAC" en [Descripción de los permisos divididos](understanding-split-permissions-exchange-2013-help.md).

Para configurar Exchange 2013 para permisos divididos, debe asignar las funciones Creación de destinatarios de correo y Pertenencia y creación de grupos de seguridad a un grupo de funciones que contiene miembros que son administradores de Active Directory. Luego, debe eliminar las asignaciones entre estas funciones y cualquier grupo de funciones o grupo de seguridad universal (USG) que contenga administradores de Exchange.

Para configurar los permisos divididos de RBAC, realice lo siguiente:

1.  Si su organización se encuentra actualmente configurada para permisos divididos de Active Directory, realice lo siguiente desde un símbolo del sistema del shell de comandos de Windows.
    
    1.  Deshabilite los permisos divididos de Active Directory mediante la ejecución del siguiente comando desde los medios de instalación de Exchange 2013.
        
            setup.exe /PrepareAD /ActiveDirectorySplitPermissions:false
    
    2.  Reinicie los servidores de Exchange 2013 en su organización o espere a que el token de acceso de Active Directory se replique en todos los servidores de Exchange 2013.
        

        > [!NOTE]
        > Si dispone de servidores Exchange 2010 en su organización, también deberá reiniciar dichos servidores.



2.  Realice lo siguiente desde el Shell de administración de Exchange:
    
    1.  Cree un grupo de funciones para los administradores de Active Directory. Además de crear el grupo de funciones, el comando crea asignaciones de funciones normales entre el nuevo grupo de funciones y las funciones Creación de destinatarios de correo y Pertenencia y creación de grupos de seguridad.
        
            New-RoleGroup "Active Directory Administrators" -Roles "Mail Recipient Creation", "Security Group Creation and Membership"
        

        > [!NOTE]
        > Si desea que los miembros de este grupo de funciones pueda crear asignaciones de funciones, incluya la función Administración de función. No es necesario agregar este rol ahora. Sin embargo, si desea asignar la función Creación de destinatarios de correo o la función Pertenencia y creación de grupos de seguridad a otros usuarios a los que se les asignan funciones, la función Administración de funciones debe asignarse a este nuevo grupo de funciones. Los siguientes pasos configuran el grupo de funciones Administradores de Active Directory como el único grupo que puede delegar estas funciones.

    
    2.  Use los siguientes comandos para crear asignaciones de funciones de delegación entre el grupo de funciones nuevo y la funciones Creación de destinatario de correo y Pertenencia y creación de grupos de seguridad.
        
            New-ManagementRoleAssignment -Role "Mail Recipient Creation" -SecurityGroup "Active Directory Administrators" -Delegating
            New-ManagementRoleAssignment -Role "Security Group Creation and Membership" -SecurityGroup "Active Directory Administrators" -Delegating
    
    3.  Agregue miembros al grupo de funciones nuevo utilizando el siguiente comando.
        
            Add-RoleGroupMember "Active Directory Administrators" -Member <user to add>
    
    4.  Reemplace la lista de delegaciones en el nuevo grupo de funciones para que solamente los miembros del grupo de funciones puedan agregar o quitar miembros.
        
            Set-RoleGroup "Active Directory Administrators" -ManagedBy "Active Directory Administrators"
        

        > [!IMPORTANT]
        > Los miembros del grupo de roles Administración de la organización, o quienes tengan asignada el rol Administración de roles, ya sea&nbsp;de forma directa o mediante otro grupo de roles o grupo de seguridad universal, pueden pasar por alto esta comprobación de seguridad de delegación. Si desea impedir que cualquier administrador de Exchange se agregue a un nuevo grupo de funciones, debe quitar la asignación de funciones entre la función Administrador de funciones y cualquier administrador de Exchange, y asignarla a otro grupo de funciones.

    
    5.  Utilice el siguiente comando para buscar todas las asignaciones de funciones normales y de delegación que correspondan a la función Creación de destinatarios de correo. El comando solo muestra las propiedades **Name**, **Role** y **RoleAssigneeName**.
        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    6.  Utilice el siguiente comando para trasladar a la función Creación de destinatarios de correo todas las asignaciones de funciones normales y de delegación que no estén asociadas con el nuevo grupo de funciones u otro grupo de funciones, USG o asignaciones directas que desea mantener.
        
            Remove-ManagementRoleAssignment <Mail Recipient Creation role assignment to remove>
        

        > [!NOTE]
        > Use el siguiente comando si desea quitar todas las asignaciones de funciones normales y de delegación de la función Creación de destinatario de correo o de cualquier usuario al que se le asignan funciones que no sea el grupo de funciones Administradores de Active Directory. El conmutador <EM>WhatIf</EM> permite ver cuáles asignaciones de roles se quitarán. Quite el conmutador <EM>WhatIf</EM> y ejecute nuevamente el comando para quitar las asignaciones de roles.

        
            Get-ManagementRoleAssignment -Role "Mail Recipient Creation" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf
    
    7.  Use el siguiente comando para buscar todas las asignaciones de roles normales y de delegación que correspondan a la función Pertenencia y creación de grupos de seguridad. El comando solo muestra las propiedades **Name**, **Role** y **RoleAssigneeName**.
        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Format-Table Name, Role, RoleAssigneeName -Auto
    
    8.  Use el siguiente comando para quitar la función Pertenencia y creación de grupos de seguridad de todas las asignaciones de funciones normales y de delegación que no estén asociadas con el nuevo grupo de funciones u otro grupo de funciones, USG o asignaciones directas que desea mantener.
        
            Remove-ManagementRoleAssignment <Security Group Creation and Membership role assignment to remove>
        

        > [!NOTE]
        > Puede usar el mismo comando en la Nota anterior para quitar todas las asignaciones de funciones normales y de delegación correspondientes a la función Pertenencia y creación de grupos de seguridad o cualquier usuario al que se le asignan funciones que no sea el grupo de funciones Administradores de Active Directory, tal como se muestra en este ejemplo.

        
            Get-ManagementRoleAssignment -Role "Security Group Creation and Membership" | Where { $_.RoleAssigneeName -NE "Active Directory Administrators" } | Remove-ManagementRoleAssignment -WhatIf

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte los siguientes temas:

  - [New-RoleGroup](https://technet.microsoft.com/es-es/library/dd638181\(v=exchg.150\))

  - [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\))

  - [Add-RoleGroupMember](https://technet.microsoft.com/es-es/library/dd638207\(v=exchg.150\))

  - [Set-RoleGroup](https://technet.microsoft.com/es-es/library/dd638182\(v=exchg.150\))

  - [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\))

  - [Remove-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351205\(v=exchg.150\))

## Cambie a permisos divididos de Active Directory

Puede configurar su organización de Exchange 2013 para los permisos divididos de Active Directory. Los permisos divididos de Active Directory quitan, por completo, los permisos que permiten que los administradores y servidores de Exchange creen entidades de seguridad en Active Directory o modifiquen atributos que no pertenecen a Exchange en esos objetos. Al finalizar, solo los administradores de Active Directory podrán crear entidades de seguridad de Active Directory. Esto significa que los administradores de Exchange no podrán usar los siguientes cmdlets:

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

  - **Update-DistributionGroupMember**

Los administradores y servidores de Exchange solo podrán administrar los atributos de Exchange en entidades de seguridad de Active Directory existentes. No obstante, podrán crear y administrar objetos específicos de Exchange, como reglas de transporte y planes de marcado de Mensajería unificada.


> [!WARNING]
> Después de habilitar los permisos divididos de Active Directory, los administradores y servidores de Exchange no podrán crear entidades de seguridad en Active Directory y no podrán administrar la pertenencia a grupos de distribución. Estas tareas se deben realizar mediante el uso de las herramientas de administración de Active Directory con los permisos de Active Directory requeridos. Antes de realizar este cambio, debe comprender el impacto que estos cambios tendrán en sus procesos de administración y en sus aplicaciones de terceros que se integran con Exchange&nbsp;2013 y el modelo de permisos de RBAC.<BR>Para obtener más información, consulte la sección "Permisos divididos de Active Directory" en <A href="understanding-split-permissions-exchange-2013-help.md">Descripción de los permisos divididos</A>.



Para cambiar de permisos divididos de RBAC o de uso compartido a permisos divididos de Active Directory, realice lo siguiente:

1.  Desde un shell de comandos de Windows, ejecute el siguiente comando desde los medios de instalación de Exchange 2013 para habilitar los permisos divididos de Active Directory.
    
        setup.exe /PrepareAD /ActiveDirectorySplitPermissions:true

2.  Si dispone de varios dominios de Active Directory en la organización, deberá ejecutar `setup.exe /PrepareDomain` en cada dominio secundario que incluya servidores u objetos de Exchange, o bien ejecutar `setup.exe /PrepareAllDomains` desde un sitio que incluya un servidor Active Directory de cada dominio.

3.  Reinicie los servidores de Exchange 2013 en su organización o espere que el token de acceso de Active Directory se replique en todos los servidores de Exchange 2013.
    

    > [!NOTE]
    > Si dispone de servidores Exchange 2010 en su organización, también deberá reiniciar dichos servidores.


