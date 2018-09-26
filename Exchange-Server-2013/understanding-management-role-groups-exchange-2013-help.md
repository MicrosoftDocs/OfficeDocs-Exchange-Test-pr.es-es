---
title: 'Descripción de los grupos de roles de administración: Exchange 2013 Help'
TOCTitle: Descripción de los grupos de roles de administración
ms:assetid: 2a92e06c-523e-4fd4-a937-152562b7741d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638105(v=EXCHG.150)
ms:contentKeyID: 49895534
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de los grupos de roles de administración

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Un *grupo de roles de administración* es un grupo de seguridad universal (USG) usado en el modelo de permisos de Control de acceso basado en roles (RBAC) en Microsoft Exchange Server 2013. Un grupo de roles de administración simplifica la asignación de roles de administración a un grupo de usuarios. A todos los miembros de un grupo de funciones se les asigna el mismo conjunto de funciones. Los grupos de funciones son funciones de administrador y de especialistas asignadas que definen las tareas administrativas principales de Exchange 2013, tales como la administración de la organización, la administración de destinatarios y otras tareas. Los grupos de funciones le permiten asignar fácilmente un conjunto de permisos más amplio a un grupo de administradores o usuarios especialistas.


> [!NOTE]
> Este tema se centra en las funciones avanzadas de RBAC. Si desea administrar los permisos básicos de Exchange&nbsp;2013, como usar el Panel de control de Exchange (EAC) para agregar y quitar miembros de grupos de roles, crear y modificar grupos de roles o crear y modificar directivas de asignación de roles, consulte <A href="permissions-exchange-2013-help.md">Permisos</A>.



**Contenido**

Capas de grupos de roles

Administración del grupo de roles

Grupos de funciones integradas

Grupos de roles vinculados

Delegación de grupo de roles

Pertenencia a un grupo de roles

Flujo de trabajo de la creación de un grupo de roles


> [!NOTE]
> Si desea asignar permisos a usuarios para que administren su propio buzón o grupos de distribución, consulte <A href="understanding-management-role-assignment-policies-exchange-2013-help.md">Descripción de las directivas de asignación de roles de administración</A>.



## Capas de grupos de roles

Las siguientes son las capas que constituyen el modelo de grupo de funciones:

  - **Miembro de grupo de roles**   Un *miembro de grupo de roles* es un buzón de correo, un grupo de seguridad universal (USG) u otro grupo de roles que se puede agregar como un miembro de un grupo de roles. Cuando un buzón de correo, USG u otro grupo de roles se agrega como miembro de un grupo de roles, las asignaciones que se hayan hecho entre los roles de administración y el grupo de roles se aplican al nuevo miembro. Esto otorga al nuevo miembro todos los permisos proporcionados por los roles de administración.

  - **Grupo de roles de administración**   El *grupo de roles de administración* es un USG especial que contiene buzones de correo, USGs y otros grupos de roles que son miembros del grupo en cuestión. Aquí es donde agrega o quita miembros y, además, a donde se asignan las funciones de administración. La combinación de todos los roles de un grupo de roles define todo lo que los miembros agregaron a un grupo de roles de la organización Exchange.

  - **Asignación de funciones de administración**   Una *asignación de funciones de administración* vincula una función de administración con un grupo de funciones. La asignación de funciones de administración para un grupo de funciones permite que los miembros del grupo de funciones usen los cmdlets y los parámetros definidos en la función de administración. Las asignaciones de funciones pueden usar ámbitos de administración para controlar dónde se puede usar la asignación. Para obtener más información, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

  - **Ámbito de funciones de administración**   Un *ámbito de funciones de administración* es el ámbito de influencia o de impacto en una asignación de funciones. Cuando una función se asigna con un ámbito a un grupo de funciones, el ámbito de administración define qué objetos puede administrar esa asignación. La asignación y su ámbito se otorgan luego a los miembros del grupo de funciones, lo cual restringe lo que pueden administrar esos miembros. Un ámbito puede estar formado por listas de servidores o bases de datos, unidades organizativas o filtros en los objetos del servidor, la base de datos o los destinatarios. Para obtener más información, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

  - **Función de administración**   Una *función de administración* es un contenedor para una agrupación de entradas de funciones de administración. Las funciones se usan para definir las tareas específicas que pueden realizar los miembros de un grupo de funciones asignados a una función. Para obtener más información, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

  - **Entradas de funciones de administración**  Las *entradas de funciones de administración* son las entradas individuales de una función de administración que brindan acceso a los cmdlets, scripts y otros permisos especiales que dan acceso para realizar una tarea específica. La mayoría de las veces, las entradas de roles constan de un solo cmdlet o script y de los parámetros a los cuales se puede tener acceso mediante el rol de administración y, por lo tanto, el grupo de roles al cual se asigna el rol.

La siguiente figura muestra cada una de las capas del grupo de funciones de la lista precedente y cómo todas las capas se relacionan entre sí.

**Capas del grupo de funciones de administración**

![Capas del grupo de funciones de administración](images/Dd638105.a98c237c-7bdb-434b-8c98-22509e46cccf(EXCHG.150).gif "Capas del grupo de funciones de administración")

Para obtener más información acerca de RBAC, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

Volver al principio

## Administración del grupo de roles

Cuando crea un grupo de funciones, usted crea un grupo de seguridad universal que tiene los miembros de un grupo de funciones y crea las asignaciones entre el grupo de funciones y las funciones de administración que especifica. De modo opcional, puede especificar un ámbito de administración para aplicar a las asignaciones de funciones y puede agregar los buzones que desee que sean miembros del nuevo grupo de funciones.

Después de crear un grupo de funciones, cada capa se convierte en un objeto independiente. El grupo de funciones continúa siendo el punto central donde todas las capas están unidas; sin embargo, cada una de las capas se administra de manera individual. Por ejemplo, para modificar el ámbito de administración que aplicó al grupo de funciones cuando fue creado, necesita cambiar el ámbito de cada asignación de funciones individual después de crear el grupo de funciones. La administración del modelo del grupo de funciones se realiza con los cmdlets que administran las capas individuales del modelo de grupo de funciones.

La siguiente lista enumera la capa del grupo de funciones y los temas de procedimiento que puede usar para administrar cada capa.

### Temas de administración del grupo de funciones

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Capa del modelo del grupo de funciones</th>
<th>Tema de administración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Miembro del grupo de rol</p></td>
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Administrar miembros de grupos de roles</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Grupo de funciones</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Administrar grupos de roles</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Funciones de administración y asignaciones</p></td>
<td><p><a href="manage-role-groups-exchange-2013-help.md">Administrar grupos de roles</a></p></td>
</tr>
<tr class="even">
<td><p>Entradas de funciones de administración</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Agregar una entrada de función a una función</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Cambiar una entrada de función</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Quitar una entrada de función de una función</a></p>

> [!NOTE]
> Modificar las entradas de funciones de administración en funciones de administración de un grupo de funciones es una tarea avanzada y, en la mayoría de los casos, no suele ser necesaria. En cambio, es posible que pueda usar un rol de administración preexistente que se adecue a sus requisitos. Para obtener más información, consulte <A href="built-in-role-groups-exchange-2013-help.md">Grupos de funciones integradas</A>.


</td>
</tr>
</tbody>
</table>


Volver al principio

## Grupos de funciones integradas

Los grupos de funciones integrados son funciones que se entregan con Exchange 2013. Proveen un conjunto de grupos de funciones que puede usar para proporcionar niveles variados de permisos administrativos a los grupos de usuarios. Puede agregar usuarios a cualquier grupo de funciones integrado o quitarlos de ellos. Además, puede agregar las asignaciones de funciones a la mayoría de los grupos de funciones o quitarlas de ellos. Las únicas excepciones son las siguientes:

  - No puede quitar ninguna asignación de funciones de delegación del grupo de funciones Administración de la organización.

  - No puede quitar la función de administración de funciones del grupo de funciones Administración de la organización.

En la siguiente tabla, se enumeran todos los grupos de roles integrados incluidos en Exchange 2013. Para obtener más información sobre los grupos de funciones integrados, consulte [Grupos de funciones integradas](built-in-role-groups-exchange-2013-help.md).

### Grupos de funciones integradas

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupo de funciones</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
<td><p>Los administradores que son miembros del grupo de roles Administración de la organización tienen acceso administrativo a toda la organización de Exchange 2013 y pueden realizar prácticamente todas las tareas relacionadas con los objetos de Exchange 2013, con algunas excepciones. De forma predeterminada, los miembros de este grupo de funciones no pueden realizar búsquedas en el buzón de correo ni administrar funciones de administración de nivel superior sin ámbito.</p></td>
</tr>
<tr class="even">
<td><p><a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
<td><p>Los administradores que son miembros del grupo de funciones Ver solamente la administración de la organización pueden ver las propiedades de todos los objetos de la organización de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
<td><p>Los administradores miembros del grupo de funciones Recipient Management tienen acceso administrativo para crear o modificar destinatarios de Exchange 2013 dentro de la organización de Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="um-management-exchange-2013-help.md">Administración de MU</a></p></td>
<td><p>Los administradores que son miembros del grupo de roles UM Management pueden administrar características en la organización Exchange, como la configuración del servicio de mensajería unificada, las propiedades de Mensajería unificada en los buzones, los mensajes de Mensajería unificada y la configuración del operador automático para Mensajería unificada.</p></td>
</tr>
<tr class="odd">
<td><p><a href="discovery-management-exchange-2013-help.md">Administración de la detección</a></p></td>
<td><p>Los administradores o usuarios que son miembros del grupo de roles Discovery Management pueden realizar búsquedas en buzones de correo de la organización de Exchange para obtener datos que cumplan determinados criterios y pueden configurar retenciones por juicio de buzones de correo.</p></td>
</tr>
<tr class="even">
<td><p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
<td><p>Los usuarios miembros del grupo de funciones Records Management pueden configurar las características de compatibilidad, como las etiquetas de directivas de retención, las clasificaciones de mensajes, las reglas de transporte y más.</p></td>
</tr>
<tr class="odd">
<td><p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
<td><p>Los administradores que son miembros de este grupo de roles pueden establecer la configuración específica de servidor de transporte, acceso de clientes, y características de buzón, como copias de las bases de datos, certificados, colas de transporte y conectores de envío, directorios virtuales y protocolos de acceso de cliente.</p></td>
</tr>
<tr class="even">
<td><p><a href="help-desk-exchange-2013-help.md">Servicio de asistencia</a></p></td>
<td><p>Los usuarios miembros del grupo de funciones del servicio de asistencia pueden administrar, de manera limitada, los destinatarios de Exchange 2013.</p></td>
</tr>
<tr class="odd">
<td><p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
<td><p>Los usuarios que son miembros del grupo de roles Administración de higiene pueden configurar las características contra el correo electrónico no deseado y antimalware de Exchange 2013. Los programas de terceros que se integran con Exchange 2013 pueden agregar cuentas de servicio a este grupo de roles para que dichos programas puedan tener acceso a los cmdlets que se requieren para recuperar y establecer la configuración de Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Administración de cumplimiento</a></p></td>
<td><p>Los usuarios que son miembros del grupo de roles de administración de cumplimiento pueden configurar y administrar la configuración del cumplimiento de Exchange de acuerdo con sus directivas.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Administración de carpetas públicas</a></p></td>
<td><p>Los administradores que son miembros del grupo de roles Administración de carpetas públicas pueden administrar carpetas públicas en los servidores que ejecuten Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="delegated-setup-exchange-2013-help.md">Configuración delegada</a></p></td>
<td><p>Los administradores que pertenecen al grupo de funciones Configuración delegada pueden implementar servidores que ejecutan Exchange 2013 que ya han sido aprovisionados por un miembro del grupo de funciones Administración de la organización.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Grupos de roles vinculados

Los grupos de funciones vinculados se usan en una organización que instala Exchange 2013 en un bosque de recursos dedicados y coloca a los usuarios en otros bosques externos de confianza. Los grupos de funciones vinculados, tal como implica el nombre, crean un vínculo entre un grupo de funciones en el bosque de Exchange y el grupo de seguridad universal en un bosque externo. Esto es útil cuando las cuentas de usuario de los servicios de dominio (AD DS) Active Directory de los administradores que desea administrar en Exchange no residen en el mismo bosque de recursos que Exchange. Los grupos de funciones vinculados solamente pueden asociarse con un grupo de seguridad universal externo. Además, no es necesario crear una confianza bidireccional entre el bosque de Exchange y el bosque externo. El bosque de Exchange necesita confiar en el bosque externo, pero no es necesario que el bosque externo confíe en el bosque de Exchange.

Para obtener más información sobre los permisos en las topologías de varios bosques, consulte [Descripción de permisos de bosques múltiples](understanding-multiple-forest-permissions-exchange-2013-help.md).

Un grupo de funciones vinculado consta de dos partes:

  - **Grupo de funciones vinculado**   El grupo de funciones vinculado es un objeto contenedor que asocia el grupo de seguridad universal externo con las asignaciones de funciones de administración asignadas al grupo de funciones.

  - **Grupo de seguridad universal externo**   El grupo de seguridad universal externo contiene lo miembros a los que se les deben otorgar permisos provistos por el grupo de funciones vinculados.

Cuando crea un grupo de funciones vinculadas, proporciona un controlador de dominio en el bosque externo que contiene los usuarios que desea que manejen el bosque de Exchange y el grupo de seguridad universal que tiene esos usuarios como miembros, el nombre del grupo de seguridad universal y las credenciales requeridas para tener acceso al bosque externo. Exchange agrega el identificador de seguridad (SID) del grupo de seguridad universal externo al grupo de funciones vinculado. Debido a que el SID del grupo de seguridad universal es la única identificación del grupo de seguridad universal externo, se recomienda especificar el bosque externo en el grupo de funciones en caso de que haya varios bosques externos.

Un grupo de funciones vinculado no tiene ningún miembro. Todos los miembros de ese grupo de funciones se administran mediante el grupo de seguridad universal externo. Esto significa que no puede usar los cmdlets **Update-RoleGroupMember**, **Add-RoleGroupMember** ni **Remove-RoleGroupMember** para agregar ni para quitar miembros del grupo de funciones. Cuando agrega miembros a un grupo de seguridad universal externo, estos reciben permisos del grupo de funciones vinculado.

No puede cambiar un grupo de funciones estándar que contiene miembros propios por un grupo de funciones vinculado (o viceversa). Si desea cambiar un grupo de funciones de un grupo de funciones estándar a un grupo de funciones vinculado, debe crear un grupo de funciones vinculado y replicar las asignaciones de funciones de administración que están presentes en el grupo de funciones estándar del grupo de funciones vinculado. Lo mismo sucede con los grupos de funciones integrados, debido a que son grupos de funciones estándar. Si desea administrar totalmente el bosque de Exchange desde un bosque externo, es necesario crear grupos de roles vinculados nuevos y agregar los roles de administración que existen en los grupos de roles integrados a los grupos de roles vinculados. Para obtener más información acerca de cómo conseguirlo, consulte [Crear grupos de funciones vinculadas que reflejan grupos de funciones integradas](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md).

Volver al principio

## Delegación de grupo de roles

De manera predeterminada, los miembros del grupo de funciones Administración de la organización pueden agregar miembros a los grupos de funciones y quitarlos de allí. Sin embargo, es posible que quiera habilitar usuarios que no son miembros del grupo de funciones Administración de la organización para agregar o quitar miembros de los grupos de funciones. Si es así, puede usar la delegación de grupos de funciones.

La delegación de grupo de funciones está controlada por la propiedad **ManagedBy** de cada grupo de trabajo. La propiedad **ManagedBy** contiene una lista de usuarios que pueden agregar o quitar miembros de ese grupo de funciones o cambiar la configuración de un grupo de funciones. Los usuarios no tienen ningún permiso asignado provisto por el grupo de funciones salvo que también sean miembros del grupo de funciones.

Si la propiedad **ManagedBy** está establecida en el grupo de funciones, solamente los usuarios que están enumerados como administradores de grupos de funciones en esa propiedad pueden modificar un grupo de funciones o la suscripción de un grupo de funciones de manera predeterminada. Sin embargo, un parámetro opcional en los cmdlets que modifican los grupos de funciones o la suscripción de grupos de funciones pueden invalidar esa restricción. El conmutador *BypassSecurityGroupManagerCheck* puede ser usado por los usuarios que son miembros de la función Administración de la organización o que tienen asignada, ya sea directa o indirectamente, la función de administración de administración de funciones. Cuando se usa este conmutador, la propiedad **ManagedBy** se ignora y el usuario puede modificar el grupo de funciones o la suscripción del grupo de funciones.

Si la propiedad **ManagedBy** no se establece en un grupo de funciones, solo los usuarios que son miembros de la función Administración de la organización o la tienen asignada, ya sea directa o indirectamente, la función de administración de administración de funciones pueden modificar un grupo de funciones o una suscripción de grupos de funciones.


> [!NOTE]
> Las funciones asignadas a un grupo de funciones pueden estar asignadas mediante asignaciones de funciones de delegación. Con las asignaciones de funciones de delegación, los miembros de un grupo de funciones que tienen asignada una función delegada pueden asignar esa función a otro grupo de funciones, una directiva de asignación o un grupo de seguridad universal. Los miembros del grupo de funciones pueden asignar solo esa función y no pueden delegar el grupo de funciones salvo que además estén agregados a la propiedad <STRONG>ManagedBy</STRONG>. Para obtener más información sobre las asignaciones de funciones delegadas, consulte <A href="understanding-management-role-assignments-exchange-2013-help.md">Descripción de las asignaciones de funciones de administración</A>.



Para obtener más información sobre cómo administrar la delegación de grupos de funciones, consulte [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

Volver al principio

## Pertenencia a un grupo de roles

Cuando un usuario se convierte en miembro de un grupo de funciones, las funciones de administración asignadas al grupo de funciones se asignan al usuario. Si un usuario es un miembro de varios grupos de funciones, las funciones de administración de cada grupo de funciones se agregan y asignan al usuario. Los usuarios, los grupos de seguridad universal y otros grupos de funciones pueden ser miembros de grupos de funciones.

Solamente los usuarios miembros de Administración de la organización o de los grupos de trabajo de administración de funciones y los usuarios a quienes se les ha delegado la posibilidad de agregar usuarios a los grupos de funciones y quitarlos de allí pueden administrar la suscripción del grupo de funciones.

Para obtener más información sobre cómo administrar la pertenencia de grupos de roles, consulte [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

## Flujo de trabajo de la creación de un grupo de roles

Como se mencionó anteriormente, un grupo de funciones se compone de varias capas. Para ayudar a comprender qué sucede cuando se crea un grupo de funciones, tenga en cuenta el siguiente ejemplo, el cual crea un grupo de funciones nuevo.

  ```powershell
  New-RoleGroup -Name "Seattle Recipient Management" -Roles "Mail Recipients", "Distribution Groups", "Move Mailboxes", "UM Mailboxes" -CustomRecipientWriteScope "Seattle Users", -ManagedBy "Brian", "David", "Katie" -Members "Ray", "Jenn", "Maria", "Chris", "Maija", "Carter", "Jenny", "Sam", "Lukas", "Isabel", "Katie"
  ```

Cuando se ejecuta el comando anterior, ocurre lo siguiente:

1.  Se crea un objeto de grupo de funciones nuevo, que es un grupo de seguridad universal, llamado Administración de destinatarios de Seattle.

2.  Los buzones de Ray, Jenn, Maria, Chris, Maija, Carter, Jenny, Sam, Lukas, Isabel y Katie se agregan como miembros del grupo de roles. Estos usuarios reciben los permisos proporcionados por este grupo de funciones.

3.  Los usuarios Brian y David se agregan a la propiedad **ManagedBy** del grupo de funciones. Estos usuarios pueden agregar miembros al grupo de funciones y quitarlos de allí, pero no tendrán permisos provistos por el grupo de funciones debido a que no son miembros. Katie, también, se agrega a la propiedad de **ManagedBy** del grupo de funciones. Debido a que se la agrega a la propiedad **ManagedBy** y ella es miembro del grupo de funciones, ella puede agregar miembros al grupo de funciones, quitarlos de allí y, además, recibe los permisos provistos por el grupo de funciones.

4.  Se crean las siguientes asignaciones de funciones de administración. Las asignaciones de funciones asignan cada función de administración especificada en el comando del grupo de funciones. A cada asignación de funciones se le agrega el ámbito de administración de usuarios de Seattle. El nombre de cada asignación de funciones es una combinación de la función de administración que se está asignando y el nombre del grupo de funciones.
    
      - `Mail Recipients_Seattle Recipient Management`
    
      - `Distribution Groups_Seattle Recipient Management`
    
      - `Move Mailboxes_Seattle Recipient Management`
    
      - `UM Mailboxes_Seattle Recipient Management`

Si compara los resultados de este comando con la figura de las capas del grupo de funciones de administración que aparecen anteriormente en este tema, puede ver en donde se correlaciona cada paso con las capas de grupos de funciones. Después, puede consultar los temas de administración del grupo de roles de administración mostradas anteriormente en "Administración de grupos de roles" de este tema para administrar cada capa del grupo de roles.

Volver al principio

