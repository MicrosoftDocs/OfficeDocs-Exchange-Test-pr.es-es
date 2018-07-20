---
title: 'Rol Destinatarios de correo: Exchange 2013 Help'
TOCTitle: Rol Destinatarios de correo
ms:assetid: 7cf1f1c7-4f32-4446-ac04-99a7f9df2059
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876911(v=EXCHG.150)
ms:contentKeyID: 49895737
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Rol Destinatarios de correo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

La función de administración `Mail Recipients` permite que los administradores administren buzones de correo, usuarios de correo y contactos de correo existentes en una organización. Esta función no puede crear a estos destinatarios. Use el rol `Mail Recipient Creation` para crearlos.

Este tipo de función no lo habilita a administrar carpetas públicas habilitadas para correo o grupos de distribución. Use las siguientes funciones para administrar estos objetos:

  - [Rol Carpetas públicas habilitadas para correo](mail-enabled-public-folders-role-exchange-2013-help.md)

  - [Rol de grupos de distribución](distribution-groups-role-exchange-2013-help.md)

Si la organización tiene el modelo de permisos divididos en el que grupos distintos realizan la creación y la administración de los destinatarios, asigne la función `Mail Recipient Creation` al grupo que realiza la creación de destinatarios y la función `Mail Recipients` al grupo que realiza la administración de destinatarios. Para obtener más información al respecto, consulte los temas siguientes:

  - [Rol Creación de destinatarios de correo](mail-recipient-creation-role-exchange-2013-help.md)

  - [Rol Destinatarios de correo](mail-recipients-role-exchange-2013-help.md)

  - [Descripción de los permisos divididos](understanding-split-permissions-exchange-2013-help.md)

Este rol de administración es uno de los varios roles integrados del modelo de permisos de control de acceso basado en roles (RBAC) de Microsoft Exchange Server 2013. Los roles de administración, que se asignan a uno o más grupos de roles de administración, directivas de asignación de roles de administración, usuarios o grupos de seguridad universal, actúan como la agrupación lógica de cmdlets o scripts que se combinan para proporcionar acceso a fin de ver o modificar la configuración de los componentes de Exchange 2013, como bases de datos de buzones, reglas de transporte y destinatarios. Si un cmdlet o un script y sus parámetros (que, en conjunto, se denominan entrada de rol de administración), se incluyen en un rol, el cmdlet o el script y sus parámetros pueden ser ejecutados por aquellos a los que se les asignó el rol. Para obtener más información acerca de los roles de administración y las entradas de roles de administración, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

Para obtener más información acerca de los roles de administración, los grupos de roles de administración y otros componentes RBAC, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

## Asignaciones de roles de administración

Para que este rol conceda permisos, se le debe asignar un usuario, que puede ser un grupo de roles, un usuario o un grupo de seguridad universal (USG). Esta asignación se realiza mediante asignaciones de roles de administración. Las asignaciones de roles vinculan los roles y los usuarios a los que se les asignan los roles. Si se le asigna más de un rol a un usuario, este recibe la combinación de todos los permisos concedidos por todos los roles asignados.

Además de vincular usuarios a los que se les asignan roles, las asignaciones de roles pueden aplicar ámbitos de administración integrados o personalizados. Los ámbitos de administración controlan qué objetos de servidor, base de datos y destinatario pueden ser modificados por los usuarios a los que se les asignan roles. Si este rol se asigna a un usuario, pero el ámbito de administración permite al usuario administrar solamente ciertos objetos basados en un ámbito definido, el usuario solamente puede usar los permisos concedidos por este rol en esos objetos específicos. Los permisos suministrados por este rol no pueden aplicarse a los objetos fuera del ámbito definido en la asignación de roles. Para obtener más información acerca de las asignaciones de roles y los ámbitos, consulte los siguientes temas:

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

Este rol se asigna a uno o más grupos de roles de forma predeterminada. Para obtener más información, consulte la sección "Asignaciones de roles de administración predeterminadas" más adelante en este tema.

Si desea ver una lista de grupos de roles, usuarios o USG a los que se les asignaron este rol, use el siguiente comando.

    Get-ManagementRoleAssignment -Role "<role name>"

## Asignaciones de roles normales y de delegación

Este rol puede asignarse a usuarios mediante asignaciones normales o de delegación. Las asignaciones de roles normales otorgan los permisos proporcionados por el rol al usuario al que se asigna un rol. Las asignaciones de roles otorgan al usuario al que se asigna un rol la capacidad de asignar roles a otros usuarios. Para obtener más información acerca de las asignaciones de roles normales y de delegación, consulte Descripción de las asignaciones de roles de administración[Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

## Agregar o quitar asignaciones de roles

Puede cambiar los usuarios a los que se asigna este rol. Al cambiar los usuarios a los que se asigna el rol, cambiarán los usuarios que tienen los permisos. Puede asignar este rol a otros grupos de roles integrados o puede crear grupos de roles y asignarles este rol. También puede asignar este rol a usuarios o grupos de seguridad universal. Sin embargo, recomendamos que limite la asignación de roles a los usuarios y grupos de seguridad universal, ya que este tipo de asignaciones puede aumentar significativamente la complejidad del modelo de permisos.

Para asignar este rol a usuarios, el rol debe estar asignado a un grupo de roles del que usted es miembro, directamente a usted o a un grupo de seguridad universal del que es miembro, mediante la asignación de roles de delegación. Para obtener más información sobre asignaciones de roles de delegación, consulte la sección "Asignaciones de roles normales y de delegación".

Puede quitar este rol de grupos de roles integrados, grupos de roles que haya creado, usuarios y grupos de seguridad universal. Sin embargo, siempre debe haber por lo menos una asignación de roles de delegación entre este rol y un grupo de roles o un grupo de seguridad universal. No es posible eliminar la última asignación de roles de delegación. Esta limitación ayuda a evitar que se bloquee su propio acceso al sistema.


> [!IMPORTANT]
> Debe haber por lo menos una asignación de roles de delegación entre este rol y un grupo de roles o un grupo de seguridad universal. Si la última asignación es para un usuario, no es posible quitar la última asignación de roles de delegación asociada con este rol.



Para obtener más información sobre cómo agregar o quitar asignaciones entre este rol y grupos de roles, usuarios y grupos de seguridad universal, consulte los siguientes temas:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - [Quitar una función de un usuario o un grupo de seguridad universal](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

## Modificación de ámbitos de administración en las asignaciones de roles

Además, se puede cambiar los ámbitos de administración de asignaciones de roles existentes de este rol y los usuarios a los que se les asignan roles. Mediante el cambio de los ámbitos de asignaciones de roles, es posible controlar qué objetos pueden administrarse usando los permisos suministrados por este rol. Hay varias opciones disponibles al cambiar el ámbito en una asignación de roles. Puede hacer uno de los pasos siguientes:

  - Agregar un nuevo ámbito personalizado mediante el cmdlet **Set-ManagementRoleAssignment**. Para obtener más información al respecto, consulte los temas siguientes:
    
      - [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md)
    
      - [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md)

  - Agregar o cambiar un ámbito de unidad organizativa mediante el cmdlet **Set-ManagementRoleAssignment**. Para más información, consulte [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

  - Agregar o cambiar un ámbito predefinido mediante el cmdlet **Set-ManagementRoleAssignment**. Para más información, consulte [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

  - Cambiar el ámbito de la base de datos, el servidor o el destinatario en un ámbito personalizado asociado a una asignación de roles, mediante el cmdlet **Set-ManagementScope**. Para más información, consulte [Cambiar el ámbito de una función](change-a-role-scope-exchange-2013-help.md).

## Habilitación y deshabilitación de asignaciones de roles

Al habilitar o deshabilitar una asignación de roles, puede controlar si una asignación de roles debe tener vigencia. Si una asignación de roles está deshabilitada, los permisos otorgados por el rol asociado no se aplican al usuario al que se asigna el rol. Esto es útil si quiere quitar temporalmente los permisos sin eliminar una asignación de roles. Para obtener más información, consulte Cambiar una asignación de rol[Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

## Consideraciones adicionales sobre ámbitos

Además de los ámbitos de destinatario, los cmdlets **Connect-Mailbox** y **Enable-Mailbox**, que se incluyen en este rol, también pertenecen a ámbitos mediante los ámbitos de configuración de base de datos. Los ámbitos de configuración de base de datos controlan en qué bases de datos los cmdlets pueden crear nuevos buzones. La base de datos en la que desea crear un buzón debe estar dentro del ámbito de la base de datos. Esta condición se aplica cuando se especifica la base de datos mediante el parámetro *Database* en cualquier cmdlet o si permite la distribución automática de buzones para que seleccione la base de datos por usted. Para obtener más información, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

## Asignaciones de roles de administración predeterminados

Este rol tiene asignaciones de roles para uno o más usuarios a los que se asigna el rol. La siguiente tabla indica si una asignación de roles es normal o de delegación y, además, indica los ámbitos de administración aplicados a cada asignación. La siguiente lista describe cada columna:

  - **Asignación normal**   Las asignaciones normales habilitan al usuario al que se le asigna un rol para que acceda a los permisos proporcionados por las entradas de roles de administración de este rol.

  - **Asignación de delegación**   Las asignaciones de roles de delegación le proporcionan al usuario al que se asigna un rol la capacidad de asignar el rol a grupos de roles, usuarios o grupos de seguridad universal.

  - **Ámbito de lectura de destinatario**   El ámbito de lectura de destinatario determina qué objetos de destinatario tiene permitido leer desde Active Directory el usuario al que se le asigna un rol.

  - **Ámbito de escritura de destinatario**   El ámbito de escritura de destinatario determina qué objetos de destinatario tiene permitido modificar en Active Directory el usuario al que se le asigna un rol.

  - **Ámbito de lectura de configuración**   El ámbito de lectura de configuración determina qué objetos de configuración y servidor tiene permitido leer desde Active Directory el usuario al que se le asigna un rol.

  - **Ámbito de escritura de configuración**   El ámbito de escritura de configuración determina qué objetos organizativos y de servidor tiene permitido modificar en Active Directory el usuario al que se le asigna un rol.

### Asignaciones de funciones de administración predeterminadas para esta función

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
<th>Grupo de funciones</th>
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
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Personalización de roles de administración

Este rol se ha configurado para proporcionar a un usuario al que se le asignan roles todos los cmdlets necesarios, junto con sus parámetros, para administrar las características y los componentes enumerados al comienzo de este tema. También se han proporcionado otros roles para habilitar la administración de otras características. Al agregar y quitar roles de los grupos de roles, es posible crear un modelo de permisos personalizado sin necesidad de personalizar roles de administración individuales. Para obtener una lista completa de los roles, consulte [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md). Para obtener más información acerca de la creación de grupos de roles, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

Si decide que es necesario crear una versión personalizada de este rol, debe crear un rol secundario para este rol y personalizar el nuevo rol.


> [!WARNING]
> La siguiente información permite administrar los permisos de manera avanzada. La personalización de los roles de administración puede aumentar significativamente la complejidad de su modelo de permisos. Si reemplaza un rol de administración integrado por un rol personalizado configurado incorrectamente, es posible que ciertas características detengan su funcionamiento.



A continuación, se detallan los pasos más comunes para crear un rol personalizado y asignarlo a un usuario específico:

1.  Crear una copia de este rol. Para obtener más información, consulte [Crear un rol](create-a-role-exchange-2013-help.md).

2.  Cambiar o quitar las entradas de rol en el nuevo rol mediante los cmdlets **Set-ManagementRoleEntry** y **Remove-ManagementRoleEntry**. No es posible agregar otras entradas de rol al nuevo rol porque solamente puede contener las entradas de rol en el rol integrado principal. Para obtener más información al respecto, consulte los temas siguientes:
    
      - [Cambiar una entrada de función](change-a-role-entry-exchange-2013-help.md)
    
      - [Quitar una entrada de función de una función](remove-a-role-entry-from-a-role-exchange-2013-help.md)

3.  Si desea reemplazar el rol integrado por este nuevo rol personalizado, quite todas las asignaciones de roles asociadas con el rol integrado. Para obtener más información al respecto, consulte los temas siguientes:
    
      - Sección "Agregar o quitar un rol a o de un grupo de roles" en [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)
    
      - [Quitar una función de un usuario o un grupo de seguridad universal](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

4.  Añadir el nuevo rol personalizado a los encargados del rol requerido. Para obtener más información al respecto, consulte los temas siguientes:
    
      - Sección "Agregar o quitar un rol a o de un grupo de roles" en [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)
    
      - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
        

        > [!IMPORTANT]
        > Si desea que otros usuarios, además del usuario que creó el rol, puedan asignar el nuevo rol personalizado, asegúrese de agregar al menos una asignación de roles de delegación a un usuario al que se asigna un rol. Para obtener más información, consulte <A href="delegate-role-assignments-exchange-2013-help.md">Delegar asignaciones de funciones</A>.


