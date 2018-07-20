---
title: 'Crear grupos de funciones vinculadas que reflejan grupos de funciones integradas: Exchange 2013 Help'
TOCTitle: Crear grupos de funciones vinculadas que reflejan grupos de funciones integradas
ms:assetid: 89dfcbb3-0568-4bbf-a885-746b91ba307e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876918(v=EXCHG.150)
ms:contentKeyID: 49895758
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear grupos de funciones vinculadas que reflejan grupos de funciones integradas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Al usar grupos de funciones vinculados de administración en Microsoft Exchange Server 2013, puede vincular un grupo de funciones en un bosque de recursos de Exchange 2013 con un grupo de seguridad universal (USG) en un bosque de usuarios externo. Esto resulta útil cuando desea que los administradores con cuentas en el bosque de usuarios administren los servidores que ejecutan Exchange en el bosque de recursos. Para obtener más información acerca de los grupos de funciones vinculados, consulte [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md).

De forma predeterminada, Exchange 2013 incluye una cantidad de grupos de funciones integrados que le otorgan permisos para administrar diversas características y funciones de trabajo. Cada grupo de funciones está adaptado para proporcionar permisos específicos para cada característica y función de trabajo. No obstante, estos grupos de funciones no se pueden vincular con el USG en un bosque externo. Solo pueden contener usuarios y USG del bosque de recursos local. Afortunadamente, es posible replicar estos grupos de funciones integrados que usan grupos de funciones vinculados.

Puede volver a crear cada grupo de funciones integrado como un grupo de funciones vinculado. Todas las funciones y todos los ámbitos de administración asignados a cada grupo de funciones se agregan al nuevo grupo de funciones vinculado. Para obtener más información acerca de las funciones y los ámbitos de administración, consulte los siguientes temas:

  - [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

¿Está buscando otras tareas de administración relacionadas con los grupos de funciones? Consulte [Permisos](permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Grupos de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - La configuración de un grupo de funciones vinculado requiere de confianza unidireccional entre el bosque de recursos Active Directory, en el que residirá el grupo de funciones vinculado, y el bosque externo Active Directory, en el que residen los usuarios o los USG. El bosque de recursos debe confiar en el bosque externo.

  - Debe tener la siguiente información sobre el bosque externo Active Directory:
    
      - **Credenciales**   Debe tener un nombre de usuario y una contraseña con los que se pueda tener acceso al bosque externo Active Directory. Esta información se usa con el parámetro *LinkedCredential* en el cmdlet **New-RoleGroup**. Esta información se obtiene mediante la ejecución del cmdlet **Get-Credential**. El formato del nombre de usuario es *dominio*\\*nombre de usuario*.
    
      - **Controlador de dominio**   Debe tener el nombre de dominio completo (FQDN) de un controlador de dominio de Active Directory en el bosque externo Active Directory. Esta información se usa con el parámetro *LinkedDomainController* en el cmdlet **New-RoleGroup**.
    
      - **USG externo**   Debe tener el nombre completo de USG en el bosque externo Active Directory que contenga a los miembros que desee asociar con el grupo de funciones vinculado. Esta información se usa con el parámetro *LinkedForeignGroup* en el cmdlet **New-RoleGroup**.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para crear grupos de funciones vinculados que repliquen grupos de funciones integrados

Cada una de las siguientes secciones muestra cómo volver a crear cada grupo de funciones como un grupo de funciones vinculado. Complete los procedimientos en cada sección para volver a crear todos los grupos de funciones integrados como grupos de funciones vinculados.

## Crear el grupo de funciones vinculado Administración de organizaciones

Para volver a crear el grupo de funciones Administración de la organización como un grupo de funciones vinculado, se realiza un procedimiento distinto al que se realiza para volver a crear otros grupos de funciones integrados. Esto se debe a que el grupo de funciones Administración de la organización tiene asignaciones de funciones de delegación entre él y todas las funciones de administración. Volver a crear las asignaciones de funciones de delegación requiere un paso adicional.

1.  Cree un USG en el bosque externo que se vinculará con el grupo de funciones Administración de la organización.

2.  Almacene las credenciales del bosque externo Active Directory en una variable.
    
        $ForeignCredential = Get-Credential

3.  Almacene todas las funciones asignadas al grupo de funciones Administración de la organización en una variable.
    
        $OrgMgmt  = Get-RoleGroup "Organization Management"

4.  Cree el grupo de funciones vinculado Administración de la organización y agregue las funciones asignadas al grupo de funciones integrado Administración de la organización.
    
        New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles

5.  Quite todas las asignaciones normales entre el nuevo grupo de funciones vinculado Administración de la organización y las funciones de usuarios finales My\*.
    
        Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment

6.  Agregue asignaciones de funciones de delegación entre el nuevo grupo de funciones vinculado Administración de la organización y todas las funciones de administración.
    
        Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

En este ejemplo, se supone que para cada parámetro se usan los siguientes valores:

  - **LinkedForeignGroup** `Organization Management Administrators`

  - **LinkedDomainController** `DC01.users.contoso.com`

Mediante los valores anteriores, en este ejemplo se vuelve a crear el grupo de funciones Administración de la organización como un grupo de funciones vinculado.

    $ForeignCredential = Get-Credential
    $OrgMgmt  = Get-RoleGroup "Organization Management"
    New-RoleGroup "Organization Management - Linked" -LinkedForeignGroup "Organization Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $OrgMgmt.Roles
    Get-ManagementRoleAssignment -RoleAssignee "Organization Management - Linked" -Role My* | Remove-ManagementRoleAssignment
    Get-ManagementRole | New-ManagementRoleAssignment -SecurityGroup "Organization Management - Linked" -Delegating

## Crear todos los demás grupos de funciones vinculados

Para volver a crear los grupos de funciones integrados (que no sea el grupo de funciones Administración de la organización) como grupos de funciones vinculados, use el siguiente procedimiento para cada grupo.

1.  Cree un USG en el bosque externo para cada grupo de funciones que se vinculará con cada nuevo grupo de funciones.

2.  Almacene las credenciales del bosque externo Active Directory en una variable. Deberá realizar este procedimiento una sola vez.
    
        $ForeignCredential = Get-Credential

3.  Recupere una lista de los grupos de funciones mediante el siguiente cmdlet.
    
        Get-RoleGroup

4.  Para cada grupo de funciones, que no sea el grupo de funciones Administración de la organización, realice las siguientes acciones.
    
        $RoleGroup = Get-RoleGroup <name of role group to re-create>
        New-RoleGroup "<role group name> - Linked" -LinkedForeignGroup <name of foreign USG> -LinkedDomainController <FQDN of foreign Active Directory domain controller> -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

5.  Repita el paso anterior para cada grupo de funciones integrado que desee volver a crear como un grupo de funciones vinculado.

En este ejemplo, se supone que para cada parámetro se usan los siguientes valores:

  - **LinkedDomainController** `DC01.users.contoso.com`

  - **Grupos de funciones integrados que se volverán a crear como grupos de funciones vinculados** `Recipient Management, Server Management`

  - **Grupo externo para el grupo de funciones vinculado Administración de destinatarios** `Recipient Management Administrators`

  - **Grupo externo para el grupo de funciones vinculado Administración de servidores** `Server Management Administrators`

Mediante los valores anteriores, en este ejemplo se vuelve a crear Recipient Management y los grupos de funciones Administración de servidores como grupos de funciones vinculados.

    $ForeignCredential = Get-Credential
    Get-RoleGroup
    $RoleGroup = Get-RoleGroup "Recipient Management"
    New-RoleGroup "Recipient Management - Linked" -LinkedForeignGroup "Recipient Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles
    $RoleGroup = Get-RoleGroup "Server Management"
    New-RoleGroup "Server Management - Linked" -LinkedForeignGroup "Server Management Administrators" -LinkedDomainController DC01.users.contoso.com -LinkedCredential $ForeignCredential -Roles $RoleGroup.Roles

## Otras tareas

Después de crear grupos de funciones vinculados, es posible que también desee realizar las siguientes tareas:

Agregar miembros a los USG externos mediante usuarios y equipos de Active Directory en el bosque externo.

Quitar miembros de grupos de funciones integrados. Para obtener más información, consulte [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

Agregue, quite o cambie el ámbito de roles en los nuevos grupos de roles vinculados. Para obtener más información, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

Crear grupos adicionales de funciones vinculados. Para obtener más información, consulte [Administrar grupos de funciones vinculadas](manage-linked-role-groups-exchange-2013-help.md).

