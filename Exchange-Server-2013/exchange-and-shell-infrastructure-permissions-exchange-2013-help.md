---
title: 'Permisos de infraestructura de la Shell y de Exchange: Exchange 2013 Help'
TOCTitle: Permisos de infraestructura de la Shell y de Exchange
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 48267989
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de infraestructura de la Shell y de Exchange

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2015-03-09_

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



## Permisos de infraestructura de Exchange

En la siguiente tabla se enumeran los permisos requeridos para realizar las tareas que configuran los parámetros generales de Exchange 2013.

Los usuarios a los que se les asigna el grupo de roles Administración con permiso de vista pueden ver la configuración de las características en la siguiente tabla. Para obtener más información, consulte Ver solamente la administración de la organización[Administración de organización de solo lectura](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Registro de auditoría de administrador</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="even">
<td><p>Ajustes de la configuración del Centro de administración de Exchange</p></td>
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectividad del Centro de administración de Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Opciones de configuración del servidor de Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración de la Ayuda de Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Categorías de mensajes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p>
<p><a href="help-desk-exchange-2013-help.md">Servicio de asistencia</a></p></td>
</tr>
<tr class="odd">
<td><p>Clave de producto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Estado del sistema de prueba</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro de auditoría de administrador con permiso de vista</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p>

> [!NOTE]
> También puede asignar manualmente el rol de administración Registros de auditoría con permiso de vista a un grupo de roles de administración. Para obtener más información, vea <A href="view-only-audit-logs-role-exchange-2013-help.md">Rol Registros de auditoría con permiso de vista</A>.


</td>
</tr>
<tr class="even">
<td><p>Escribir en el registro de auditoría</p></td>
<td><p>Los usuarios que son miembros de cualquier grupo de roles o a los que se les asignó cualquier rol de administración pueden escribir en el registro de auditoría de administrador.</p></td>
</tr>
</tbody>
</table>


## Permisos de infraestructura de Shell

En la siguiente tabla, se enumeran los permisos requeridos para realizar las tareas que configuran las características que controlan la forma en que se ejecuta el Shell de administración de Exchange.

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
<td><p>Configuración del servidor de Servicios de dominio de Active Directory</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p>
<p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
</tr>
<tr class="even">
<td><p>Agentes de extensión de cmdlet</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Directorios virtuales de PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Instalación de WinRM y PowerShell</p></td>
<td><p>Administrador de servidor local</p></td>
</tr>
<tr class="odd">
<td><p>Shell remoto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
</tbody>
</table>


## Permisos de certificados y federación

En la tabla siguiente, se enumeran los permisos necesarios para realizar las tareas relacionadas con las confianzas de federación, la configuración de OAuth, la administración de certificados y la configuración de implementaciones híbridas.

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
<td><p>Administración de certificados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Confianzas de federación, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Confianzas de federación de prueba, OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de implementación híbrida</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectores internos de la organización</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
</tbody>
</table>

