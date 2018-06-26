---
title: 'Descripción de los ámbitos de roles de administración: Exchange 2013 Help'
TOCTitle: Descripción de los ámbitos de roles de administración
ms:assetid: 24ed4a38-438a-4223-9f9c-5d4dea4b046b
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335146(v=EXCHG.150)
ms:contentKeyID: 49895523
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de los ámbitos de roles de administración

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2015-04-07_

Los *ámbitos de rol de administración* permiten establecer el ámbito de impacto o influencia específico de un rol de administración cuando se crea una asignación de rol de administración. Cuando se aplica un ámbito, el usuario asignado a un rol solamente puede modificar los objetos contenidos en dicho ámbito. El usuario puede ser un grupo de roles de administración, un rol de administración, una directiva de rol de administración, un usuario o un grupo de seguridad universal (USG). Para obtener más información acerca de los roles de administración, vea [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).


> [!NOTE]
> Este tema se centra en las funciones avanzadas de RBAC. Si desea administrar los permisos básicos de Exchange&nbsp;2013, como usar el Panel de control de Exchange (EAC) para agregar y quitar miembros de grupos de roles, crear y modificar grupos de roles o crear y modificar directivas de asignación de roles, consulte <A href="permissions-exchange-2013-help.md">Permisos</A>.



Todo rol de administración, ya sea integrado o personalizado, tiene ámbitos de administración. Los ámbitos de administración pueden ser:

  - **Normal**   El *ámbito normal* no es exclusivo. Éste determina dónde, en Active Directory, los usuarios asignados al rol de administración pueden ver o modificar los objetos. Por lo general, un rol de administración indica qué puede crear o modificar, y un ámbito de rol de administración indica dónde puede crear o modificar. Los ámbitos normales pueden ser implícitos o explícitos, conceptos que trataremos más adelante en este tema.

  - **Exclusivo**   El *ámbito exclusivo* funciona casi de igual manera que el ámbito normal. La diferencia principal es que permite negar a los usuarios el acceso a objetos que se encuentren dentro del ámbito exclusivo si a los usuarios no se les asigna un rol asociado con el ámbito exclusivo. Todos los ámbitos exclusivos son ámbitos explícitos y se tratarán más adelante en este tema.
    
    Para obtener más información sobre los ámbitos exclusivos, vea [Descripción de ámbitos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

Los ámbitos se pueden heredar de un rol de administración, especificada como un ámbito relativo predefinido en una asignación de rol de administración, o se pueden crear mediante filtros personalizados y agregar a una asignación de rol de administración. Los ámbitos heredados de los roles de administración se llaman *ámbitos implícitos* y los ámbitos predefinidos y personalizados se llaman *ámbitos explícitos*. En las secciones siguientes se describe cada uno de los ámbitos:

  - Ámbitos implícitos

  - Ámbitos explícitos

  - Ámbitos relativos predefinidos

  - Ámbitos personalizados
    
      - Ámbitos de filtro de destinatarios
    
      - Ámbitos de configuración

Cada rol puede tener los siguientes tipos de ámbitos:

  - **Ámbito de lectura de destinatario**   El ámbito de lectura de destinatario implícito determina qué objetos de destinatario puede leer de Active Directory el usuario asignado a un rol de administración.

  - **Ámbito de escritura de destinatario**   El ámbito de escritura de destinatario implícito determina qué objetos de destinatario puede modificar de Active Directory el usuario asignado a un rol de administración.

  - **Ámbito de lectura de configuración**   El ámbito de lectura de configuración implícito determina qué objetos de configuración puede leer de Active Directory el usuario asignado a un rol de administración.

  - **Ámbito de escritura de configuración**   El ámbito de escritura de configuración implícita determina qué objetos de organización, de base de datos y de servidor tiene permitido modificar en Active Directory el usuario al que se le asigna el rol de administración.

Los objetos de destinatario pueden ser buzones de correo, grupos de distribución, usuarios habilitados para correo y otros objetos. Los objetos de configuración incluyen servidores que ejecuten Microsoft Exchange Server 2013 y bases de datos ubicadas en servidores que ejecuten Exchange. Cada tipo de ámbito puede ser o implícito o explícito.

## Ámbitos implícitos

Los ámbitos implícitos son ámbitos predeterminados que se aplican a un tipo de rol de administración. Como los ámbitos implícitos están asociados al tipo de rol de administración, todos los roles de administración principales y secundarios con mismo tipo de rol también tienen los mismos ámbitos implícitos. Los ámbitos implícitos se aplican tanto a los roles de administración integrados como a los personalizados. Para obtener más información acerca de los roles de administración y los tipos de roles de administración, vea [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

En la tabla siguiente se enumeran todos los ámbitos implícitos que se pueden definir en los roles de administración.

### Ámbitos implícitos definidos en los roles de administración

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ámbitos implícitos</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Si <code>Organization</code> está presente en el ámbito de escritura de destinatario, el rol puede crear o modificar objetos de destinatario en la organización de Exchange.</p>
<p>Si <code>Organization</code> está presente en el ámbito de lectura de destinatario, los roles pueden ver objetos de destinatario en la organización de Exchange.</p>
<p>Este ámbito se usa solamente con ámbitos de lectura y escritura de destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>MyGAL</code></p></td>
<td><p>Si <code>MyGAL</code> está presente en el ámbito de escritura de destinatario del rol, el rol puede ver las propiedades de cualquier destinatario dentro de la lista global de direcciones (GAL) actual del usuario.</p>
<p>Si <code>MyGAL</code> está presente en el ámbito de lectura del destinatario del rol, el rol puede ver las propiedades de cualquier destinatario dentro de la lista global de direcciones (GAL) actual.</p>
<p>Este ámbito se usa solo con ámbitos de lectura de destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>Self</code></p></td>
<td><p>Si <code>Self</code> está presente en el ámbito de escritura de destinatario del rol, el rol solo puede modificar las propiedades del buzón de correo del usuario actual.</p>
<p>Si <code>Self</code> está presente en el ámbito de lectura de destinatario del rol, el rol solamente puede modificar las propiedades del buzón de correo del usuario actual.</p>
<p>Este ámbito se usa solamente con ámbitos de lectura y escritura de destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Si <code>MyDistributionGroups</code> está presente en el ámbito de escritura de destinatario del rol, el rol puede crear o modificar objetos de listas de distribución que pertenezcan al usuario actual.</p>
<p>Si <code>MyDistributionGroups</code> está presente en el ámbito de lectura de destinatario del rol, el rol puede ver objetos de listas de distribución que pertenezcan al usuario actual.</p>
<p>Este ámbito se usa solamente con ámbitos de lectura y escritura de destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationConfig</code></p></td>
<td><p>Si <code>OrganizationConfig</code> está presente en el ámbito de escritura de configuración del rol, este puede crear o modificar objetos de configuración de base de datos o servidores en la organización de Exchange.</p>
<p>Si <code>OrganizationConfig</code> está presente en el ámbito de lectura de configuración del rol, este puede ver objetos de configuración de la base de datos o servidores en la organización de Exchange.</p>
<p>Este ámbito solo se usa con los ámbitos de lectura y escritura de configuración.</p></td>
</tr>
<tr class="even">
<td><p><code>None</code></p></td>
<td><p>Si <code>None</code> está en un ámbito, ese ámbito no estará disponible para el rol. Por ejemplo, un rol que tiene <code>None</code> en el ámbito de escritura de destinatario no puede modificar los objetos de destinatario en la organización de Exchange.</p></td>
</tr>
</tbody>
</table>


Si se asigna un rol a un usuario y no se especifican ámbitos predefinidos o personalizados, los ámbitos implícitos definidos en el rol se usan para controlar los objetos de destinatario o de organización que el usuario puede ver o modificar.

El ámbito de escritura implícito de un rol siempre es igual o menor que el ámbito de lectura implícito. Esto significa que un rol nunca puede modificar los objetos que el ámbito no puede ver.

No puede cambiar los ámbitos implícitos definidos en los roles de administración. Sin embargo, se pueden invalidar el ámbito de escritura implícito y el ámbito de configuración en un rol de administración. Cuando se usa un ámbito relativo predefinido o un ámbito personalizado en una asignación de rol, se invalida el ámbito de escritura implícito del rol y el nuevo ámbito adquiere prioridad. El ámbito de lectura implícito de un rol no se puede invalidar y siempre se aplica. Para obtener más información, vea Ámbitos relativos predefinidos y Ámbitos personalizados.

Expanda la siguiente tabla para consultar la lista de todos los roles de administración integrados con sus ámbitos implícitos. Para obtener más información sobre cada rol integrado, vea [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md).

## Ámbitos implícitos de los roles de administración integrados


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de administración</th>
<th>Ámbito de lectura de destinatario</th>
<th>Ámbito de escritura de destinatario</th>
<th>Ámbito de lectura de configuración</th>
<th>Ámbito de escritura de configuración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Active Directory Permissions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Address Lists</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Cmdlet Extension Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Data Loss Prevention</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Database Availability Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Database Copies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Disaster Recovery</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Distribution Groups</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Edge Subscriptions</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>E-Mail Address Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Server Certificates</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Exchange Servers</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Exchange Virtual Directories</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Federated Sharing</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Information Rights Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Legal Hold</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>LegalHoldApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Enabled Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipient Creation</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Tips</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Mailbox Import Export</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Mailbox Search</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Message Tracking</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Migration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Monitoring</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Move Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>My Custom Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>My Marketplace Apps</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyAddressInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDiagnostics</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDisplayName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>MyGAL</code></p></td>
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyMobileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyName</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyPersonalInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyTeamMailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Client Access</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Organization Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Organization Transport Settings</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>POP3 And IMAP4 Protocols</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Public Folders</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Receive Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Recipient Policies</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Remote and Accepted Domains</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Reset Password</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Retention Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Security Group Creation and Membership</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Send Connectors</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Support Diagnostics</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>Self</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Agents</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Hygiene</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Transport Queues</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>Transport Rules</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UM Mailboxes</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UM Prompts</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>Unified Messaging</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>UnScoped Role Management</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="odd">
<td><p><code>User Options</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Audit Logs</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>View-Only Configuration</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="even">
<td><p><code>View-Only Recipients</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>None</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>None</code></p></td>
</tr>
<tr class="odd">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>Organization</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
<td><p><code>OrganizationConfig</code></p></td>
</tr>
</tbody>
</table>


## Ámbitos explícitos

Los ámbitos explícitos son ámbitos que se establecen para controlar qué objetos puede modificar un rol de administración. Aunque que los ámbitos implícitos se definen en un rol de administración, los ámbitos explícitos se definen en una asignación de rol de administración. Esto permite aplicar los ámbitos implícitos de manera coherente en todos los roles de administración a menos que decida usar un ámbito de invalidación explícito. Para obtener más información acerca de asignaciones de roles de administración, vea [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Los ámbitos explícitos invalidan los ámbitos de escritura y de configuración implícitos de un rol de administración. Sin embargo, no invalidan el ámbito de lectura implícito de un rol de administración. El ámbito de lectura implícito define qué objetos puede leer el rol de administración.

Los ámbitos explícitos son útiles cuando el ámbito de escritura implícito de un rol de administración no satisface las necesidades de su empresa. Puede agregar un ámbito explícito para incluir casi cualquier cosa que desee, siempre y cuando el nuevo ámbito no sobrepase los límites del ámbito de lectura implícito. Para poder crear o modificar objetos, los cmdlets que forman parte de un rol de administración tienen que poder leer la información sobre los objetos o los contenedores que contienen objetos. Por ejemplo, si el ámbito de lectura implícito en un rol de administración está configurado en `Self`, no se puede agregar un ámbito de escritura explícito de `Organization` porque el ámbito de escritura explícito sobrepasa los límites del ámbito de lectura implícito.

Para obtener más información, vea las siguientes secciones:

  - Ámbitos relativos predefinidos

  - Ámbitos personalizados

## Ámbitos relativos predefinidos

Exchange 2013 incluye varios ámbitos de escritura relativos predefinidos que se pueden usar para modificar los ámbitos del rol de administración. Los ámbitos relativos predefinidos brindan una solución sencilla para satisfacer mejor las necesidades de su empresa sin tener que crear ámbitos personalizados en forma manual. Se llaman ámbitos relativos porque son relativos al usuario al que está asignada la asignación del rol de administración. Por ejemplo, el ámbito relativo predefinido `Self` restringe ese ámbito de escritura solo al usuario actual. El ámbito relativo predefinido `MyDistributionGroups` restringe el ámbito de escritura solo al grupo de distribución que tiene en usuario actual. Los ámbitos relativos predefinidos solo se pueden usar para objetos de ámbitos de destinatarios. Los ámbitos relativos predefinidos no se pueden usar para objetos de ámbitos de configuración. En la tabla siguiente se enumeran los ámbitos relativos predefinidos que puede usar.

### Ámbitos relativos predefinidos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ámbitos implícitos</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>Organization</code></p></td>
<td><p>Si <code>Organization</code> está presente en el ámbito de escritura de destinatario, el rol puede crear o modificar objetos de destinatario en la organización de Exchange.</p>
<p>Si <code>Organization</code> está presente en el ámbito de lectura de destinatario, los roles pueden ver objetos de destinatario en la organización de Exchange.</p>
<p>Este ámbito se usa solamente con ámbitos de lectura y escritura de destinatario.</p></td>
</tr>
<tr class="even">
<td><p><code>Self</code></p></td>
<td><p>Si <code>Self</code> está presente en el ámbito de escritura de destinatario del rol, el rol solo puede modificar las propiedades del buzón de correo del usuario actual.</p>
<p>Si <code>Self</code> está presente en el ámbito de lectura de destinatario del rol, el rol solamente puede modificar las propiedades del buzón de correo del usuario actual.</p>
<p>Este ámbito se usa solamente con ámbitos de lectura y escritura de destinatario.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p>Si <code>MyDistributionGroups</code> está presente en el ámbito de escritura de destinatario del rol, el rol puede crear o modificar objetos de listas de distribución que pertenezcan al usuario actual.</p>
<p>Si <code>MyDistributionGroups</code> está presente en el ámbito de lectura de destinatario del rol, el rol puede ver objetos de listas de distribución que pertenezcan al usuario actual.</p>
<p>Este ámbito se usa solamente con ámbitos de lectura y escritura de destinatario.</p></td>
</tr>
</tbody>
</table>


Los ámbitos relativos predefinidos se aplican cuando crea una nueva asignación de rol de administración. Durante la creación de la asignación del rol, con el cmdlet **New-ManagementRoleAssignment**, puede especificar un ámbito relativo predefinido mediante el parámetro *RecipientRelativeWriteScope*. Cuando se crea la asignación del nuevo rol, el nuevo rol predefinido invalida el ámbito de escritura implícito del rol de administración. No puede especificar un ámbito de destinatario personalizado cuando crea una asignación de rol con un ámbito relativo predefinido. Sin embargo, puede especificar un ámbito de configuración personalizado si es necesario.

Para obtener más información acerca de cómo agregar una asignación de rol de administración con un ámbito relativo predefinido, vea [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

## Ámbitos personalizados

Los ámbitos personalizados son necesarios cuando ni los ámbitos de escritura implícitos ni los ámbitos relativos predefinidos satisfacen las necesidades de su empresa. Los ámbitos personalizados le permiten definir de manera individualizada en qué ámbito se aplicará su rol de administración. Por ejemplo, aplicarla a una unidad organizacional específica (OU), un tipo de destinatario específico o ambos. O puede solamente querer permitir a un grupo de administradores tener a posibilidad de administrar un conjunto específico de bases de datos de buzones de correo.

Así como sucede con los ámbitos relativos predefinidos, los ámbitos personalizados invalidan los ámbitos de escritura y organización de configuración implícitos definidos por roles de administración. El ámbito de lectura implícito de los roles de administración se sigue aplicando; el ámbito personalizado resultante no debe superar los límites del ámbito de lectura implícito. Puede crear los siguientes tres tipos de ámbitos personalizados:

  - **Ámbito OU**   El ámbito OU, que es el ámbito personalizado más simple, se crea al utilizar el parámetro *RecipientOrganizationalUnitScope* en el cmdlet **New-ManagementRoleAssignment**. Al especificar un ámbito OU cuando se asigna un rol, el usuario asignado al rol puede modificar solamente los objetos de destinatario dentro de ese OU. Para obtener más información acerca de cómo agregar una asignación de rol de administración con un ámbito OU, vea [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

  - **Ámbito de filtros de destinatarios**   Los ámbitos de filtros de destinatarios utilizan filtros orientados a destinatarios específicos según el tipo de destinatario y otras propiedades, como departamento, gerente, ubicación, etc. Para obtener más información, vea la sección Ámbitos de filtro de destinatarios.

  - **Ámbito de configuración** Los ámbitos de configuración usan filtros o listas orientados a servidores específicos basados en listas de servidores o propiedades filtrables que se pueden definir en servidores, como un sitio Active Directory o un rol de servidor. Los ámbitos de configuración además pueden usar ámbitos de bases de datos orientados a bases de datos específicas de listas de bases de datos o propiedades de bases de datos que se pueden filtrar. Para obtener más información, vea la sección Ámbitos de configuración.

Se pueden crear ámbitos personalizados simples, amplios o complejos, con destinatarios granulares y de configuración con el cmdlet **New-ManagementScope**. Cuando crea un ámbito de destinatario o de configuración, solo devuelven los objetos de destinatarios, de servidores o de bases de datos que coinciden con sus respectivos ámbitos. Cuando estos ámbitos se aplican a una asignación de rol mediante los cmdlets **New-ManagementRoleAssignment** o **Set-ManagementRoleAssignment**, los usuarios asignados al rol solo pueden modificar los objetos que coinciden con los ámbitos. Después de que se crea un ámbito personalizado, no puede cambiar el tipo de ámbito. Un ámbito de destinatario siempre será un ámbito de destinatario y un ámbito de configuración siempre será un ámbito de configuración.

De manera predeterminada, un ámbito personalizado habilita un usuario para que tenga acceso a un conjunto de objetos que coinciden con los ámbitos establecidos. Sin embargo, estos no excluyen de manera activa a otros usuarios que no tengan asignado el mismo ámbito o alguno equivalente. Cualquier ámbito personalizado puede tener acceso a los mismos objetos si las listas o los filtros de esos ámbitos coinciden con los mismos objetos. Quizá desea que esto no ocurra con algunos objetos, por ejemplo en el caso de los ejecutivos. En ese caso, puede definir ámbitos exclusivos para dichos objetos. Los ámbitos exclusivos usan filtros o listas del mismo modo que los ámbitos normales. La diferencia radica en que los ámbitos exclusivos niegan acceso a los objetos incluidos en el ámbito a cualquiera que no forme parte de ese mismo ámbito o de uno equivalente. Para obtener más información sobre los ámbitos exclusivos, vea [Descripción de ámbitos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

## Ámbitos de filtro de destinatarios

Los ámbitos de filtro de destinatarios le permiten controlar los usuarios a los que se les asigna un rol de objetos de destinatarios mediante la evaluación de una o más propiedades de un objeto de destinatario con el valor que se especifica en la declaración de filtros. Los destinatarios incluidos en ámbitos de destinatarios son buzones de correo, usuarios habilitados para correo, grupos de distribución y contactos de correo. Los usuarios asignados a roles a quienes se les asigna esa asignación de roles pueden administrar solo a los destinatarios que coinciden con el filtro que especifica. Un ejemplo de instrucción de filtros es `{ Name -Eq "David" }` donde **Name** es la propiedad del objeto del destinatario que se está evaluando y **David** es el valor que desea evaluar con las propiedades. El operador de comparaciones de **-Eq** indica que el valor almacenado en las propiedades debe ser igual al valor especificado para que el filtro sea verdadero. Si el filtro es verdadero, ese destinatario se incluye en el ámbito.

Los ámbitos de filtros de destinatarios se crean al especificar el filtro de destinatario a utilizar con el parámetro *RecipientRestrictionFilter* en el cmdlet **New-ManagementScope**. De manera predeterminada, el cmdlet de **New-ManagementScope** crea ámbitos regulares. Si desea crear un ámbito exclusivo, incluya el conmutador *Exclusive* junto con el parámetro *RecipientRestrictionFilter*.

Cuando cree un filtro de restricción de destinatarios, Exchange evaluará el filtro proporcionado con cada objeto del destinatario en la organización de manera predeterminada. Si desea limitar los destinatarios que evalúa el ámbito, puede utilizar el parámetro *RecipientRoot* junto con el parámetro *RecipientRestrictionFilter*. El parámetro *RecipientRoot* acepta una unidad organizativa. Cuando utiliza el parámetro *RecipientRoot*, Exchangesolo evalúa los destinatarios incluidos en la unidad organizativa especificada con el filtro proporcionado.

Cuando agrega un ámbito de filtro de destinatario a una asignación de roles, especifique el nombre del ámbito del destinatario en el parámetro *CustomRecipientWriteScope* en **New-ManagementRoleAssignment** si está creando una nueva asignación de rol o el cmdlet **Set-ManagementRoleAssignment** si está actualizando una asignación de roles existente. Cada asignación de rol puede tener un ámbito de destinatario, incluidos ámbitos relativos predefinidos. Puede agregar un ámbito de configuración con la misma asignación de roles a la que agregó un ámbito de destinatario.

Para obtener más información sobre sintaxis de filtros y una lista completa de propiedades de destinatarios que se pueden filtrar en los destinatarios, vea [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

## Ámbitos de configuración

Los siguientes son los dos tipos de ámbitos de la configuración que se ofrecen en Exchange 2013:

  - **Ámbitos de servidores**   Existen dos tipos de ámbitos de servidores, ámbitos de filtros de servidores y ámbitos de listas de servidores. La configuración de servidores, que incluye los conectores de recepción, colas de transporte, certificados de servidores, directorios virtuales, entre otros, sólo se puede administrar si se incluye un objeto de servidor en un ámbito de servidor.
    
      - **Ámbitos de filtros de servidores**   Los ámbitos de filtro de servidores le permiten controlar los usuarios a los que se les asigna un rol de objetos de destinatarios mediante la evaluación de una o más propiedades de un objeto de servidores con el valor que se especifica en la declaración de filtros. Para crear un ámbito de filtro de servidores, utilice el parámetro *ServerRestrictionFilter* en el cmdlet **New-ManagementScope**.
    
      - **Ámbitos de listas de servidores**   Los ámbitos de listas de servidores le permiten controlar qué usuarios a los que se les asigna roles de objetos pueden administrar mediante la definición de una lista de servidores al que puede tener acceso el usuario al que se le asigna roles. Para crear un ámbito de listas de servidores, utilice el parámetro *ServerList* en el cmdlet **New-ManagementScope**.

  - **Ámbitos de bases de datos**   Existen dos tipos de ámbitos de bases de datos, ámbitos de filtros de bases de datos y ámbitos de listas de bases de datos. La configuración de la base de datos que se puede administrar si el objeto de la base de datos está incluido en un ámbito de base de datos comprende límites de cuota de base de datos, mantenimiento de base de datos, replicación de carpetas públicas, si la base de datos está montada, etc. Además de la configuración de la base de datos, los ámbitos de base de datos también se pueden usar para controlar los destinatarios de bases de datos que se pueden crear. Si tiene servidores anteriores a Exchange 2010 SP1 en la organización, vea la sección Ámbitos de bases de datos y versiones anteriores de Exchange más adelante en este tema.
    
      - **Ámbitos de filtros de bases de datos**   Los ámbitos de filtro de bases de datos le permiten controlar los usuarios a los que se les asigna un rol de objetos de destinatarios mediante la evaluación de una o más propiedades de un objeto de bases de datos con el valor que se especifica en la declaración de filtros. Para crear un ámbito de filtro de base de datos, utilice el parámetro *DatabaseRestrictionFilter* en el cmdlet **New-ManagementScope**.
    
      - **Ámbitos de listas de bases de datos**   Los ámbitos de listas de bases de datos le permiten controlar qué usuarios a los que se les asigna roles de objetos pueden administrar mediante la definición de una lista de bases de datos a la que puede tener acceso el usuario al que se le asigna roles. Para crear un ámbito de lista de base de datos, utilice el parámetro *DatabaseList* en el cmdlet **New-ManagementScope**.

Para obtener más información sobre sintaxis de filtros y una lista completa de propiedades de bases de datos y servidores que se pueden filtrar, vea [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

Se pueden definir listas de bases de datos y servidores al especificar cada servidor y base de datos que desea incluir en sus respectivos ámbitos. Se pueden especificar varias bases de datos o varios servidores múltiples en sus ámbitos respectivos al separar los nombres de la base de datos y el servidor con comas.

Cuando agrega un ámbito de configuración de base de datos o servidor a una asignación de roles, especifique el nombre del ámbito de configuración de base de datos o servidor en el parámetro *CustomConfigWriteScope* en el cmdlet **New-ManagementRoleAssignment** si está creando una nueva asignación de rol o en el cmdlet **Set-ManagementRoleAssignment** si está actualizando una asignación de roles existente. Cada asignación de rol solo puede tener un ámbito de configuración.

Además de controlar los usuarios a los que se les asigna un rol de base de datos que pueden administrar, los ámbitos de bases de datos además lo habilitan para controlar qué usuarios a los que se les asigna un rol de base de datos pueden crear buzones de correo. Esto es independiente del control de los destinatarios que puede administrar un usuario al que se le asigna un rol. Si el usuario al que se le asigna un rol tiene permiso para crear un nuevo buzón de correo, habilitar para correo un usuario existente o mover buzones de correo, podrá refinar aún más los permisos si utiliza ámbitos de bases de datos para controlar la base de datos en la que se ha creado el buzón de correo o la base de datos a la que se moverá el buzón de correo. El control de los destinatarios que puede administrar un usuario al que se le asigna un rol se realiza mediante el ámbito del destinatario especificado en el parámetro *CustomRecipientWriteScope* en **New-ManagementRoleAssignment** o el cmdlet **Set-ManagementRoleAssignment**. El control de las bases de datos que puede crear o mover un buzón de correo se controla mediante el ámbito de la base de datos especificado en el parámetro *CustomConfigurationWriteScope* en los mismos cmdlets.


> [!NOTE]
> La distribución automática de buzón se puede controlar mediante el uso de ámbitos de la base de datos.



Las características de Exchange pueden que necesiten ámbitos de servidor, ámbitos de bases de datos, o ambos, para ser administrados. Si la función necesita que se administren los ámbitos de bases de datos y servidores, se deberán crear dos asignaciones de roles y se deberán asignar al usuario al que se le asigna un rol que debería tener acceso para administrar la función. Se debería asociar una asignación de roles con el ámbito de servidores y se debería asociar una asignación de roles con el ámbito de la base de datos.

Algunos cmdlets pueden utilizar ámbitos de configuración que no son inmediatamente obvios. La siguiente tabla contiene una lista de cmdlets y los ámbitos de configuración que puede utilizar para controlar su uso. En el caso de los cmdlets incluidos en el área de funciones de destinatarios, los ámbitos de configuración le permiten controlar las bases de datos en las que se pueden crear destinatarios. No controlan los destinatarios que pueden administrar. La columna **ámbitos necesarios** puede contener lo siguiente:

  - **Base de datos**  Para ejecutar el cmdlet, se le debe asignar al usuario al que se asigna un rol una asignación de roles con un ámbito de base de datos que comprenda la base de datos a administrar o el ámbito de escritura de configuración implícito del rol debe incluir la base de datos que se administrará.

  - **Servidor**  Para ejecutar el cmdlet, se le debe asignar al usuario al que se asigna un rol una asignación de roles con un ámbito de servidores que comprenda el servidor a administrar o el ámbito de escritura de configuración implícito del rol debe incluir el servidor que se administrará.

  - **Servidor o base de datos**   Para ejecutar el cmdlet, se le debe asignar al usuario al que se asigna un rol una asignación de roles con un ámbito de base de datos que incluya la base de datos a administrar o donde el ámbito de servidores incluya el servidor donde se ubica la base de datos. O el ámbito de escritura de configuración implícita del rol debe contener una base de datos a administrar o contener al servidor en donde se ubica la base de datos y la asignación de rol no puede tener un ámbito de escritura personalizado.

  - **Servidor y base de datos**   Para ejecutar este cmdlet, se le debe asignar al usuario al que se asigna un rol dos asignaciones de roles. La primera asignación de roles debe incluir un ámbito de base de datos que incluya la base de datos que se administrará. La segunda asignación de roles debe incluir un ámbito de servidores que incluya al servidor donde se ubica la base de datos. Las asignaciones de roles pueden tener ámbitos de configuración personalizados definidos o las asignaciones de roles pueden heredar ámbitos de escritura de configuración implícita del rol. Para heredar el ámbito de escritura implícita del rol, la asignación de roles no puede tener un ámbito de escritura personalizado.

### Ámbitos de servidores, base de datos aplicable y áreas de funciones

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Área de funciones</th>
<th>Cmdlet</th>
<th>Ámbitos necesarios</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Bases de datos</p></td>
<td><p><strong>Dismount-Database</strong></p></td>
<td><p>base de datos</p></td>
</tr>
<tr class="even">
<td><p>Bases de datos</p></td>
<td><p><strong>Mount-Database</strong></p></td>
<td><p>base de datos</p></td>
</tr>
<tr class="odd">
<td><p>Bases de datos</p></td>
<td><p><strong>Move-DatabasePath</strong></p></td>
<td><p>Servidor y base de datos</p></td>
</tr>
<tr class="even">
<td><p>Bases de datos</p></td>
<td><p><strong>Remove-MailboxDatabase</strong></p></td>
<td><p>Servidor o base de datos</p></td>
</tr>
<tr class="odd">
<td><p>Bases de datos</p></td>
<td><p><strong>Set-MailboxDatabase</strong></p></td>
<td><p>base de datos</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Add-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Add-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Move-ActiveMailboxDatabase</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Remove-DatabaseAvailabilityGroupServer</strong></p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Remove-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor o base de datos</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Resume-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor o base de datos</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Set-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor o base de datos</p></td>
</tr>
<tr class="odd">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Suspend-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor o base de datos</p></td>
</tr>
<tr class="even">
<td><p>Alta disponibilidad</p></td>
<td><p><strong>Update-MailboxDatabaseCopy</strong></p></td>
<td><p>Servidor o base de datos</p></td>
</tr>
<tr class="odd">
<td><p>Destinatarios</p></td>
<td><p><strong>Connect-Mailbox</strong></p></td>
<td><p>base de datos</p></td>
</tr>
<tr class="even">
<td><p>Destinatarios</p></td>
<td><p><strong>Enable-Mailbox</strong></p></td>
<td><p>base de datos</p></td>
</tr>
<tr class="odd">
<td><p>Destinatarios</p></td>
<td><p><strong>New-Mailbox</strong></p></td>
<td><p>base de datos</p></td>
</tr>
<tr class="even">
<td><p>Destinatarios</p></td>
<td><p><strong>New-MoveRequest</strong></p></td>
<td><p>base de datos</p></td>
</tr>
<tr class="odd">
<td><p>Solución de problemas</p></td>
<td><p><strong>Test-MapiConnectivity</strong></p></td>
<td><p>base de datos</p></td>
</tr>
</tbody>
</table>


## Ámbitos de bases de datos y versiones anteriores de Exchange

Los ámbitos de bases de datos se introdujeron por primera vez en Microsoft Exchange 2010 Service Pack 1 (SP1) y continúan siendo compatibles con Exchange 2013. Las versiones de Exchange anteriores a Exchange 2010 SP1 solo son compatibles con los ámbitos de destinatarios y los ámbitos de configuración de servidores. Cuando cree un nuevo ámbito de base de datos en un servidor Exchange 2010 SP1 o posterior, recibirá la siguiente advertencia:

    WARNING: Database management scopes will only be applied when a user connects to a server running Exchange 2010 SP1 or later. Servers running a version of Exchange prior to Exchange 2010 SP1 won't apply any roles from a role assignment linked to a database scope. Database management scopes also won't be visible to the Get-ManagementScope cmdlet when it's run from a pre-Exchange 2010 SP1 server.

Cuando cree un ámbito de base de datos, solo se aplicará a los usuarios que se conecten a los servidores que ejecutan Exchange 2010 SP1 o posterior. Los usuarios que se conecten a servidores anteriores a Exchange 2010 SP1 no tendrán ninguna asignación de roles asociada a los ámbitos de la base de datos que se les aplica. Esto significa que no se otorgarán a los usuarios los permisos proporcionados por estas asignaciones de roles cuando se conecten a los servidores anteriores a Exchange 2010 SP1. Los ámbitos de bases de datos no se pueden crear, quitar, modificar ni visualizar desde los servidores anteriores a Exchange 2010 SP1.

El ámbito de la base de datos puede incluir cualquier base de datos en su organización de Exchange. Esto incluye Exchange Server 2007, Exchange 2010 y los servidores Exchange 2013. Lo habilita a controlar las bases de datos que pueden administrar los usuarios, independientemente de la versión de Exchange. Al igual que otros ámbitos de bases de datos, las asignaciones de roles asociadas con ámbitos de bases de datos que contienen bases de datos de Exchange 2007 y Exchange 2010 solo se aplican a los usuarios cuando se conectan con un servidor Exchange 2010 SP1 o posterior.

Los usuarios que se conectan a un servidor anterior a Exchange 2010 SP1 pueden ver y modificar asignaciones de roles asociadas con ámbitos de bases de datos. Esto incluye el cambio de ámbito de configuración en una asignación de roles existente a un ámbito de servidor si en la actualidad está asociado con un ámbito de base de datos. No obstante, si el ámbito de configuración de una asignación de roles se cambia a un ámbito de servidor y, posteriormente, un usuario quiere que vuelva a ser un ámbito de base de datos, o si el usuario desea cambiar el ámbito de configuración a otro ámbito de base de datos, el usuario debe efectuar el cambio mientras está conectado con un servidor Exchange 2010 SP1 o posterior. Los usuarios solamente pueden especificar ámbitos de servidor cuando cambian el ámbito de configuración de una asignación de roles si están conectados a un servidor anterior a Exchange 2010 SP1.

