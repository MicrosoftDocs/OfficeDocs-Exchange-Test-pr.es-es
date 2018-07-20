---
title: 'Permisos de uso compartido y colaboración: Exchange 2013 Help'
TOCTitle: Permisos de uso compartido y colaboración
ms:assetid: b7fa4b7c-1266-45bd-a14b-f66be0459cc5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ150556(v=EXCHG.150)
ms:contentKeyID: 48268592
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de uso compartido y colaboración

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Los permisos necesarios para configurar las funciones de uso compartido y colaboración varían según el procedimiento que se efectúe o el cmdlet que se vaya a ejecutar. Para obtener más información acerca del uso compartido y la colaboración, vea [Colaboración](collaboration-exchange-2013-help.md) y [Uso compartido](sharing-exchange-2013-help.md).

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).

## Permisos de función de intercambio y colaboración

Puede usar las características que aparecen en la tabla siguiente para configurar las características de uso compartido y colaboración. Se enumeran los grupos de características necesarias para configurar cada característica.

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
<td><p>Aplicaciones de socios - configurar</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Carpetas públicas, con correo habilitado</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="odd">
<td><p>Carpetas públicas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="public-folder-management-exchange-2013-help.md">Administración de carpetas públicas</a></p></td>
</tr>
<tr class="even">
<td><p>Buzones de correo del sitio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="odd">
<td><p>Directiva de aprovisionamiento de buzones de correo del sitio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
</tbody>
</table>

