---
title: 'Permisos de dispositivos móviles y clientes: Exchange 2013 Help'
TOCTitle: Permisos de dispositivos móviles y clientes
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 48268152
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Permisos de dispositivos móviles y clientes

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-11-10_

Los permisos necesarios para realizar tareas para clientes y dispositivos móviles pueden variar en función del procedimiento que se esté llevando a cabo o del cmdlet que se desee ejecutar. Para obtener más información acerca de las características de dispositivos móviles y clientes, vea [Clientes y móvil](clients-and-mobile-exchange-2013-help.md).

Para obtener más información sobre qué permisos requiere para realizar el procedimiento o ejecutar el cmdlet, realice las siguientes acciones:

1.  En la siguiente tabla, busque la característica que está más relacionada con el procedimiento que desea realizar o el cmdlet que desea ejecutar.

2.  A continuación, examine los permisos necesarios para la característica. Debe tener asignado uno de estos grupos de roles, un grupo de roles personalizados equivalente o un rol de administración equivalente. Además, puede hacer clic en un grupo de roles para ver los roles de administración. Si una característica enumera más de un grupo de roles, solo tiene que estar asignado a uno de los grupos de roles para usarla. Para obtener más información acerca de grupos de roles y roles de administración, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

3.  Ejecute el cmdlet de **Get-ManagementRoleAssignment** para ver los grupos de roles o los roles de administración que se le asignaron, a fin de consultar si tiene los permisos necesarios para administrar este rol.
    

    > [!NOTE]
    > Debe tener asignado el rol de administración Administración de rol para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>. Si no posee los permisos para ejecutar el cmdlet <STRONG>Get-ManagementRoleAssignment</STRONG>, pídale a su administrador de Exchange que recupere los grupos de rol o los roles de administración que le asignaron.



Si desea delegar la capacidad de administrar una característica a otro usuario, consulte [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md).


> [!NOTE]
> Es posible que algunas funciones requieran que posea permisos de administrador local para el servidor que quiere administrar. Para administrar estas funciones, debe ser miembro del grupo de administradores locales del servidor en cuestión.



## Permisos de servidor de acceso de clientes

Para el servidor de acceso de clientes, puede configurar cualquiera de las siguientes opciones.

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
<td><p>Configuración de matriz del servidor de acceso de cliente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración del servidor de acceso de cliente</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración del canal de correo electrónico del servicio de acceso de clientes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de usuario de acceso de clientes</p></td>
<td><p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración del directorio virtual de acceso de cliente</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de acceso de cliente RPC</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración del proxy de notificaciones de inserción</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de redirección de autenticación OAuth</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
</tbody>
</table>


## Permisos de Exchange ActiveSync

Para Exchange ActiveSync se puede configurar cualquiera de las siguientes opciones.

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
<td><p>Configuración de bloqueo automático de Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de directivas de buzón de correo de Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración de servidor de Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración de usuario de Exchange ActiveSync</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de directorio virtual de Exchange ActiveSync</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración de directivas de buzón de dispositivo móvil</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de usuarios de dispositivo móvil</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
</tbody>
</table>


## Permisos de Detección automática

Para el servicio Detección automática se pueden configurar las opciones siguientes.

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
<td><p>Parámetros de configuración del servicio Detección automática</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Configuración delegada</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración del directorio virtual Detección automática</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
</tbody>
</table>


## Permisos del servicio de disponibilidad

Para el servicio de disponibilidad se pueden configurar las opciones siguientes.

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
<td><p>Configuración del espacio de direcciones del servicio de disponibilidad</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="even">
<td><p>Parámetros de configuración del servicio de disponibilidad</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
</tbody>
</table>


## Permisos de limitación de clientes

Puede configurar las siguientes opciones para la limitación de clientes.

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
<td><p>Configuración de limitación de clientes</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
</tbody>
</table>


## Permisos de servicios Web Exchange

Para los directorios virtuales de los servicios web es posible configurar las siguientes opciones.

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
<td><p>Configuración de directorio virtual de servicios Web Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Probar de servicios Web Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="odd">
<td><p>Prueba de servicios Web Exchange</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
</tbody>
</table>


## Permisos de Outlook Anywhere

Puede configurar y administrar los siguientes valores de configuración para Outlook en cualquier lugar.

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
<td><p>Configuración de Outlook en cualquier lugar (habilitar, deshabilitar, modificar, ver)</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Configuración delegada</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
<tr class="even">
<td><p>Componente RPC sobre proxy HTTP</p></td>
<td><p>Administrador de servidor local</p></td>
</tr>
<tr class="odd">
<td><p>Prueba de conectividad de Outlook en cualquier lugar</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
</tbody>
</table>


## Permisos de Outlook Web App

Puede usar las siguientes características para ver la configuración de Outlook Web App, el control de la seguridad y el acceso de usuarios de Outlook Web App, y para comprobar la conectividad de Outlook Web App.

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
<td><p>Editor de gráficos</p></td>
<td><p>Administrador de servidor local</p></td>
</tr>
<tr class="even">
<td><p>Administrador de IIS</p></td>
<td><p>Administrador de servidor local</p></td>
</tr>
<tr class="odd">
<td><p>ISA Server 2006</p></td>
<td><p>Administrador de empresa de ISA Server</p></td>
</tr>
<tr class="even">
<td><p>Directivas de buzones de Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="odd">
<td><p>Directorios virtuales de Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
</tr>
<tr class="even">
<td><p>Editor del Registro</p></td>
<td><p>Administrador de servidor local</p></td>
</tr>
<tr class="odd">
<td><p>Configuración S/MIME</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Editor de texto</p></td>
<td><p>Administrador de servidor local</p></td>
</tr>
<tr class="odd">
<td><p>Vista de directivas de buzones de correo de Outlook Web App</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p>
<p><a href="delegated-setup-exchange-2013-help.md">Configuración delegada</a></p>
<p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
</tr>
</tbody>
</table>


## Permisos de POP3 e IMAP4

Puede configurar las opciones siguientes para POP3 e IMAP4.

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
<td><p>Configuración de IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="odd">
<td><p>Prueba de configuración de IMAP4</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="even">
<td><p>Prueba de configuración de POP3</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p>
<p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
</tbody>
</table>


## Permisos del directorio virtual de Windows PowerShell

Puede configurar las opciones siguientes para Windows PowerShell.

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
<td><p>Probar Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de Windows PowerShell</p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
</tbody>
</table>


## Permisos de mensajería de texto

Puede configurar las siguientes opciones para la mensajería de texto.

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
<td><p>Configuración de notificaciones de mensajería de texto</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="even">
<td><p>Configuración de la mensajería de texto</p></td>
<td><p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="odd">
<td><p>Configuración de usuario de mensajería de texto</p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Rol MyTextMessaging</a></p>
<p>Los usuarios pueden configurar las opciones para la mensajería de texto en su propio buzón. Los administradores no pueden configurar las opciones para la mensajería de texto en el buzón de otro usuario.</p></td>
</tr>
</tbody>
</table>

