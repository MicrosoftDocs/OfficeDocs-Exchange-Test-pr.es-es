---
title: 'Permisos de rendimiento y estado del servidor: Exchange 2013 Help'
TOCTitle: Permisos de rendimiento y estado del servidor
ms:assetid: 00b23fd3-6679-4b06-a3d4-51df3112b9cd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150479(v=EXCHG.150)
ms:contentKeyID: 48267748
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permisos de rendimiento y estado del servidor

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los permisos requeridos para realizar las tareas de configuración de varios componentes de Microsoft Exchange Server 2013 dependen del procedimiento que se realice o del cmdlet que se desee ejecutar. Vea cada una de las secciones de este tema para obtener más información acerca de sus características respectivas.

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> Es posible que algunas funciones requieran que posea permisos de administrador local para el servidor que quiere administrar. Para administrar estas funciones, debe ser miembro del grupo de administradores locales del servidor en cuestión.



## Permisos de administración de carga de trabajo de Exchange

En la siguiente tabla aparece una lista de los permisos necesarios para realizar tareas que gestionan el estado y el rendimiento de su organización de Exchange 2013. Para obtener más información, vea [Administración de carga de trabajo de Exchange](exchange-workload-management-exchange-2013-help.md).

Los usuarios a los que se les asigna el grupo de roles Administración con permiso de vista pueden ver la configuración de las características en la siguiente tabla. Para obtener más información, consulte Ver solamente la administración de la organización[Administración de organización de solo lectura](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Permisos necesarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Limitación de peticiones de usuarios</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="even">
<td><p>Limitación de la carga de trabajo de Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
</tbody>
</table>


## Permisos de registro de eventos de Exchange

En la siguiente tabla se enumeran los permisos requeridos para realizar las tareas que administran la configuración del registro de eventos de Exchange.

Los usuarios a los que se les asigna el grupo de roles Administración con permiso de vista pueden ver la configuración de las características en la siguiente tabla. Para obtener más información, consulte Ver solamente la administración de la organización[Administración de organización de solo lectura](view-only-organization-management-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Característica</th>
<th>Permisos necesarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración del registro de eventos de Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
</tbody>
</table>

