---
title: 'Permisos de alta disponibilidad y resistencia de sitios: Exchange 2013 Help'
TOCTitle: Permisos de alta disponibilidad y resistencia de sitios
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 48268224
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de alta disponibilidad y resistencia de sitios

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-11-12_

Los permisos pertinentes para configurar alta disponibilidad varían según el procedimiento que se efectúa o el cmdlet que se quiera ejecutar. Para obtener más información acerca de alta disponibilidad, consulte [Alta disponibilidad y resistencia de sitios](high-availability-and-site-resilience-exchange-2013-help.md).

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).

## Permisos de grupo de disponibilidad de base de datos

Las funciones de la tabla siguiente son válidas para agregar, quitar y configurar parámetros para grupos de disponibilidad de base de datos (DAG).

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
<td><p>Pertenencia a grupos de disponibilidad de base de datos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rol Grupos de disponibilidad de base de datos</a></p></td>
</tr>
<tr class="even">
<td><p>Propiedades de grupos de disponibilidad de base de datos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rol Grupos de disponibilidad de base de datos</a></p></td>
</tr>
<tr class="odd">
<td><p>Grupos de disponibilidad de base de datos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rol Grupos de disponibilidad de base de datos</a></p></td>
</tr>
<tr class="even">
<td><p>Redes de disponibilidad de base de datos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="database-availability-groups-role-exchange-2013-help.md">Rol Grupos de disponibilidad de base de datos</a></p></td>
</tr>
</tbody>
</table>


## Permisos de copia de base de datos de buzones de correo

Puede usar las características de la siguiente tabla para agregar, quitar, actualizar y activar copias de bases de datos de buzones de correo.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Feature</th>
<th>Permisos necesarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cambio de conexión de base de datos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="databases-role-exchange-2013-help.md">Rol Bases de datos</a></p></td>
</tr>
<tr class="even">
<td><p>Copias de bases de datos de buzones</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Rol Copias de base de datos</a></p></td>
</tr>
<tr class="odd">
<td><p>Cambio de conexión de servidor</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="databases-role-exchange-2013-help.md">Rol Bases de datos</a></p></td>
</tr>
<tr class="even">
<td><p>Actualización de una copia de la base de datos de buzones</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="database-copies-role-exchange-2013-help.md">Rol Copias de base de datos</a></p></td>
</tr>
</tbody>
</table>

