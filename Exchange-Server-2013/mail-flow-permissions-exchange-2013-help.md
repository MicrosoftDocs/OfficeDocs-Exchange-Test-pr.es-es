---
title: 'Permisos de flujo del correo: Exchange 2013 Help'
TOCTitle: Permisos de flujo del correo
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 48268873
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de flujo del correo

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2016-12-09_

Los permisos necesarios para llevar a cabo tareas relacionadas con el flujo de correo varían en función del procedimiento que se esté realizado o del cmdlet que se desee ejecutar. Para obtener más información acerca de las características de transporte, vea [Flujo de correo](mail-flow-exchange-2013-help.md).

En este tema se enumeran los permisos necesarios para administrar las características de flujo de correo en Microsoft Exchange Server 2013. Para obtener información sobre cómo se relacionan los permisos de Office 365 con los permisos de Exchange, vea [Permisos en Office 365](https://go.microsoft.com/fwlink/p/?linkid=335814).

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> Es posible que algunas características que desea administrar existan en los servidores de transporte perimetral. Para administrar características en los servidores de transporte perimetral, debe convertirse en miembro del grupo local de administradores del servidor de transporte perimetral que desea administrar. Los servidores de transporte perimetral no usan el control de acceso basado en roles (RBAC). Las características que pueden administrarse en los servidores de transporte perimetral tienen la opción Administrador local de transporte perimetral en la columna "Permisos necesarios", en la tabla de abajo.




> [!NOTE]
> Es posible que algunas funciones requieran que posea permisos de administrador local para el servidor que quiere administrar. Para administrar estas funciones, debe ser miembro del grupo de administradores locales del servidor en cuestión.



## Permisos de flujo de correo

Puede utilizar las características de las siguientes tablas para configurar valores de flujo de correo en el servicio de transporte front-end en servidores de acceso de cliente, en el servicio de transporte en servidores de buzones de correo, en el servicio de transporte de buzones de correo en servidores de buzones de correo y en servidores de transporte perimetral. Se enumeran los permisos necesarios para configurar cada característica.

Los usuarios a los que se les asigna el grupo de roles de administración con permiso de solo vista pueden ver la configuración de las características de la siguiente tabla. Para obtener más información, vea [Administración de organización de solo lectura](view-only-organization-management-exchange-2013-help.md).

**Servidores de buzones de correo y servidores de acceso de cliente**


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
<td><p>Dominios aceptados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Sitio de Active Directory y administración del vínculo de sitio</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Características contra correo electrónico no deseado</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="even">
<td><p>Actualizaciones contra correo electrónico no deseado</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="odd">
<td><p>Administración de certificados</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Conectores de agente de entrega</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>DSN</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>EdgeSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectores externos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Servicio de transporte de front-end</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="odd">
<td><p>Registro en diario</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="even">
<td><p>Acceso al buzón</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración de correo electrónico no deseado del buzón de correo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p>
<p><a href="help-desk-exchange-2013-help.md">Servicio de asistencia</a></p></td>
</tr>
<tr class="even">
<td><p>Servicio de transporte de buzón de correo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="odd">
<td><p>MailTips</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Clasificaciones de mensajes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Seguimiento de mensajes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="even">
<td><p>Transporte moderado</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="odd">
<td><p>Colas</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Conectores de recepción</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="odd">
<td><p>Dominios remotos</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Agregación de listas seguras</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Conectores de envío</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Redundancia de instantánea</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Flujo de comprobación de correo</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Prueba de procesamiento de reglas de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Agentes de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="odd">
<td><p>Registros de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Reglas de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
</tr>
<tr class="odd">
<td><p>Servicio de transporte</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="even">
<td><p>Dominios X.400</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
</tbody>
</table>


**Servidores de transporte perimetral**


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
<td><p>Dominios aceptados - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>Reconfiguración de direcciones - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Servidor de transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>EdgeSync - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Colas - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>Conectores de recepción - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Conectores de envío - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>Configuración de transporte - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="odd">
<td><p>Registros de transporte - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
<tr class="even">
<td><p>Reglas de transporte - Transporte perimetral</p></td>
<td><p>Administrador local de transporte perimetral</p></td>
</tr>
</tbody>
</table>

