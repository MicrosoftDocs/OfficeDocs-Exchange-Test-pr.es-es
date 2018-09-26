---
title: 'Administración de carpetas públicas: Exchange 2013 Help'
TOCTitle: Administración de carpetas públicas
ms:assetid: e167d95e-bb39-43fd-b960-204ab0de27da
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876947(v=EXCHG.150)
ms:contentKeyID: 49895972
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Administración de carpetas públicas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Administración de carpetas públicas Un grupo de administración de roles es uno de varios grupos de roles integrados que constituye el modelo de permisos de control de acceso basado en roles (RBAC) de Microsoft Exchange Server 2013. Los grupos de roles se asignan a uno o más roles de administración que contienen los permisos requeridos para realizar un determinado conjunto de tareas. Los miembros de un grupo de roles obtienen acceso a los roles de administración asignados a un grupo de roles. Para obtener más información acerca de los grupos de roles, consulte [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md).

Los administradores que son miembros del grupo de roles de administración de carpetas públicas pueden administrar carpetas públicas en servidores que ejecutan Exchange 2013.

Para obtener más información acerca de las carpetas públicas, consulte [Carpetas públicas](public-folders-exchange-2013-help.md). Para obtener más información acerca RBAC, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

## Pertenencia a un grupo de roles

Si desea agregar o quitar miembros de este grupo de roles, consulte [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

De manera predeterminada, solo los miembros del grupo de roles Administración de la organización pueden agregar o quitar miembros de este grupo de roles. Para obtener más información sobre cómo agregar delegados a los grupos de roles, consulte la sección "Agregar o quitar un delegado del grupo de roles" en [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

El siguiente comando se puede usar para ver una lista de usuarios o Grupos de seguridad universal (USG) que son miembros de este grupo de funciones.

```powershell
Get-RoleGroupMember "Public Folder Management"
```

Para obtener más información acerca de los miembros de un grupo de roles, consulte [View the members of a role group](manage-role-group-members-exchange-2013-help.md) en [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

## Personalización de un grupo de roles

Este grupo de roles tiene asignado roles de administración de forma predeterminada. Los roles incluidos están enumerados en la sección "Roles de administración asignados a este grupo de roles". Puede agregar o quitar asignaciones de roles de este grupo de roles de acuerdo con las necesidades de su organización.

Los grupos de roles proporcionados con Exchange 2013 están diseñados de modo que coincidan con las tareas más granulares. Mediante la asignación de roles a un grupo de roles, se permite a los miembros de ese grupo de roles realizar tareas vinculadas con el rol. Por ejemplo, el rol de registro en diario permite la administración del agente de registro en diario y las reglas de registro en diario. Para obtener más información acerca de cómo los roles se asignan a grupos de roles, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Los roles asignados a este grupo de roles reciben ámbitos de administración predeterminados. Los ámbitos de administración determinan qué objetos de Exchange pueden ser vistos o modificados por los miembros de un grupo de roles. Es posible cambiar los ámbitos asociados con las asignaciones de roles y grupos de roles. Por ejemplo, es posible que desee hacerlo si desea que solamente los miembros de un grupo de roles puedan cambiar los destinatarios de una unidad organizativa específica o de una ubicación específica. Para obtener más información sobre cómo crear los ámbitos de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Para obtener más información sobre cómo personalizar este grupo de roles, consulte los siguientes temas:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md)

Si desea crear un grupo de roles y asignar algunos de los roles asignados a este grupo de roles al nuevo grupo de roles, consulte la sección “Crear un grupo de roles” en [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

## Funciones de administración asignadas a este grupo de funciones

La siguiente tabla enumera todos los roles de administración que se asignan a este grupo de roles y los atributos de cada asignación de roles:

  - **Asignación normal**   Habilita a los miembros de cada grupo de roles para que accedan a las entradas de roles de administración disponibles por el rol de administración asociado.

  - **Asignación de delegación**   Proporciona a los miembros del grupo de roles la capacidad para asignar el rol especificado a los otros grupos de roles, directivas de asignación de roles de administración, usuarios o grupos de seguridad universal.

  - **Ámbito de lectura de destinatario**   Determina qué miembros de objetos de destinatario del grupo de roles pueden leerse desde Active Directory.

  - **Ámbito de escritura de destinatario**   Determina qué miembros de objetos de destinatario del grupo de roles pueden modificarse en Active Directory.

  - **Ámbito de lectura de configuración**   Determina qué miembros de objetos de configuración del grupo de roles pueden leerse desde Active Directory.

  - **Ámbito de escritura de configuración**   Determina qué miembros de objetos organizativos y de servidor del grupo de roles pueden modificarse en Active Directory.

Para obtener más información acerca de las asignaciones de funciones y los ámbitos de administración, consulte los siguientes temas:

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

### Funciones de administración asignadas a este grupo de funciones

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Función de administración</th>
<th>Asignación normal</th>
<th>Asignación de delegación</th>
<th>Ámbito de lectura de destinatario</th>
<th>Ámbito de escritura de destinatario</th>
<th>Ámbito de lectura de configuración</th>
<th>Ámbito de escritura de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">Rol Carpetas públicas habilitadas para correo</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="public-folders-role-exchange-2013-help.md">Rol Carpetas públicas</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>

