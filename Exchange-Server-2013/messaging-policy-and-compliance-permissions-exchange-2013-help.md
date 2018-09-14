---
title: 'Permisos de directivas de mensajería y conformidad: Exchange 2013 Help'
TOCTitle: Permisos de directivas de mensajería y conformidad
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 48268834
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de directivas de mensajería y conformidad

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2016-12-09_

Los permisos necesarios para configurar la directiva y conformidad de mensajería varían según el procedimiento que se efectúe o el cmdlet que se vaya a ejecutar. Para obtener más información acerca de la directiva y conformidad de mensajería, vea [Directiva de mensajería y conformidad](messaging-policy-and-compliance-exchange-2013-help.md).

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> Es posible que algunas características que desea administrar existan en los servidores de transporte perimetral. Para administrar características en los servidores de transporte perimetral, debe convertirse en miembro del grupo local de administradores del servidor de transporte perimetral que desea administrar. Los servidores de transporte perimetral no usan el control de acceso basado en roles (RBAC). Las características que pueden administrarse en los servidores de transporte perimetral tienen la opción Administrador local de transporte perimetral en la columna "Permisos necesarios", en la tabla de abajo.



## Permisos de directivas de mensajería y cumplimiento

Puede usar las características que aparecen en la tabla siguiente para configurar las características de directiva y conformidad de mensajería. Se enumeran los grupos de características necesarias para configurar cada característica.

Los usuarios a los que se les asigna el grupo de características de administración con permiso de solo vista pueden ver la configuración de las características de la siguiente tabla. Para obtener más información, vea [Administración de organización de solo lectura](view-only-organization-management-exchange-2013-help.md).


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
<td><p>Prevención de pérdida de datos (DLP)</p></td>
<td><p>Si usa Office 365:</p>
<ul>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">El administrador global de Office 365</a>, que automáticamente incluye Exchange <a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">El administrador de servicios de Office 365</a>, además del <a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a> grupo de roles de administrador en Exchange</p></li>
<li><p><a href="https://go.microsoft.com/fwlink/p/?linkid=335814">Administrador de contraseñas de Office 365</a></p></li>
</ul>
<p>Si usa Exchange Server 2013 o Exchange Online solamente:</p>
<ul>
<li><p><a href="compliance-management-exchange-2013-help.md">Administración de cumplimiento</a></p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Eliminar el contenido del buzón (utilizando el cmdlet <a href="https://technet.microsoft.com/es-es/library/dd298173(v=exchg.150)">Search-Mailbox</a> con el modificador <em>DeleteContent</em>)</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Administración de la detección</a> <strong>y</strong></p>
<p><a href="mailbox-import-export-role-exchange-2013-help.md">Rol Importar/Exportar buzón</a></p>

> [!NOTE]
> De forma predeterminada, el rol Importar o exportar buzones no está asignado a ningún grupo de roles. Puede asignar un rol de administración a un grupo de roles integrado o personalizado, a un usuario o a un grupo de seguridad universal. Se recomienda asignar un rol a un grupo de roles. Para obtener más información, vea <A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Agregar una función a un usuario o grupo de seguridad universal</A>.


</td>
</tr>
<tr class="odd">
<td><p>Crear buzones de detección</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="even">
<td><p>Registro en diario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro de auditoría de buzones de correo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="even">
<td><p>Clasificaciones de mensajes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Administración de registros de mensajes</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Administración de cumplimiento</a></p>
<p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="even">
<td><p>Exhibición de documentos electrónicos en contexto</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Administración de la detección</a></p>

> [!NOTE]
> De forma predeterminada, el rol Administración de detección no tiene ningún miembro. Ningún usuario, incluidos los administradores, tiene permisos necesarios para buscar en los buzones. Para obtener más información, vea <A href="https://docs.microsoft.com/es-es/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions">Asignar permisos de exhibición de documentos electrónicos en Exchange</A>.


</td>
</tr>
<tr class="odd">
<td><p>Retención en contexto</p></td>
<td><p><a href="discovery-management-exchange-2013-help.md">Administración de la detección</a></p>
<p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>

> [!IMPORTANT]
> Para crear una retención local basada en consulta, un usuario requiere que se asignen los roles Búsqueda en buzones y Retención por juicio directamente o mediante la pertenencia a un grupo de roles que tiene ambos roles asignados. Para crear una retención local sin usar una consulta, la cual retiene todos los elementos del buzón de correo, debe tener asignado el rol Retención por juicio. El grupo de roles Administración de la detección tiene asignados ambos roles.<BR>El grupo de roles Administración de la organización tiene asignado el rol Retención por juicio. Los miembros del grupo de roles Administración de la organización pueden aplicar una retención local en todos los elementos de un buzón de correo, pero no pueden crear una retención local basada en consulta.


</td>
</tr>
<tr class="even">
<td><p>Archivo en contexto</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="odd">
<td><p>Archivo local – Conectividad de prueba</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de Information Rights Management (IRM)</p></td>
<td><p><a href="compliance-management-exchange-2013-help.md">Administración de cumplimiento</a></p>
<p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Aplicar directivas de retención</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="even">
<td><p>Directivas de retención - Crear</p></td>
<td><p>Vea la entrada Administración de registros de mensajes</p></td>
</tr>
<tr class="odd">
<td><p>Reglas de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
</tbody>
</table>

