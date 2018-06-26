---
title: 'Permisos de administración de roles: Exchange 2013 Help'
TOCTitle: Permisos de administración de roles
ms:assetid: cb9591c4-fbb3-4199-8007-6bbfdfd5a2e9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638186(v=EXCHG.150)
ms:contentKeyID: 48268695
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de administración de roles

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

Los permisos necesarios para llevar a cabo tareas de configuración de funciones de administración pueden variar en función del procedimiento que se esté realizado o del cmdlet que se quiera ejecutar. Para obtener más información acerca de las funciones de administración, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).

## Permisos de administración de roles

Puede usar las características que aparecen en la tabla siguiente para administrar los grupos de roles, los roles, las directivas de asignación, las asignaciones y los ámbitos que definen los permisos que puede aplicar a los administradores y usuarios finales. Los usuarios a los que se les asigna el grupo de roles Administración con permiso de vista pueden ver la configuración de las características en la siguiente tabla. Para obtener más información, consulte Ver solamente la administración de la organización[Administración de organización de solo lectura](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Función</th>
<th>Permisos necesarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Funciones de administración</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Funciones de administración sin ámbito</p></td>
<td><p>Función de administración <a href="unscoped-role-management-role-exchange-2013-help.md">Rol Administración de roles sin ámbito</a></p></td>
</tr>
<tr class="odd">
<td><p>Grupos de funciones</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Directivas de asignación</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Asignaciones de funciones</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Ámbitos de administración</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Entradas de funciones de administración</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Permisos heredados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Permisos divididos de Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>

> [!IMPORTANT]
> Para ejecutar el comando <CODE>setup.exe</CODE> con los parámetros <EM>PrepareAD</EM> y <EM>ActiveDirectorySplitPermissions</EM>, la cuenta que utilice debe formar parte de los grupos Administradores de esquema y Administradores de empresa.


</td>
</tr>
</tbody>
</table>

