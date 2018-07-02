---
title: 'Permisos de mensajería unificada: Exchange 2013 Help'
TOCTitle: Permisos de mensajería unificada
ms:assetid: d326c3bc-8f33-434a-bf02-a83cc26a5498
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638193(v=EXCHG.150)
ms:contentKeyID: 48268702
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de mensajería unificada

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los permisos necesarios para realizar tareas en los servidores de acceso de cliente que ejecutan el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange y los servidores de buzones de correo que ejecutan el servicio de mensajería unificada de Microsoft Exchange varían según el procedimiento que se realiza o el cmdlet que desea ejecutar.

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).

## Permisos de componentes de mensajería unificada

Puede definir la configuración de los componentes y las características de mensajería unificada en la tabla siguiente.

Los usuarios a los que se les asigna el grupo de roles Administración con permiso de vista pueden ver la configuración de las características en la siguiente tabla. Para obtener más información, consulte Ver solamente la administración de la organización[Administración de organización de solo lectura](view-only-organization-management-exchange-2013-help.md).


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
<td><p>operadores automáticos de mensajería unificada</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="even">
<td><p>Reglas de respuesta a llamadas de mensajería unificada</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="odd">
<td><p>Informes de resumen y datos de llamadas de MU</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="even">
<td><p>Servidor de acceso de cliente (servicio de enrutador de llamadas de mensajería unificada)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="odd">
<td><p>planes de marcado de mensajería unificada</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="even">
<td><p>Grupos de búsqueda de mensajería unificada</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="odd">
<td><p>puertas de enlace IP de UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="even">
<td><p>directivas de buzón de mensajería unificada</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="odd">
<td><p>Buzones de UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="even">
<td><p>Mensajes de UM</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="odd">
<td><p>Servidor de buzones de correo (servicio de mensajería unificada)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
</tbody>
</table>

