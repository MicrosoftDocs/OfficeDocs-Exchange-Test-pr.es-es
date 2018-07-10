---
title: 'Descripción de los roles de administración: Exchange 2013 Help'
TOCTitle: Descripción de los roles de administración
ms:assetid: 887b0a64-84b1-4b8c-9547-e456ea6f5dbd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298116(v=EXCHG.150)
ms:contentKeyID: 49895756
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de los roles de administración

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Las funciones de administración forman parte del modelo de permisos de control de acceso basado en funciones (RBAC) usado en Microsoft Exchange Server 2013. Los roles actúan como una agrupación lógica de cmdlets que se combinan para permitir el acceso a la visualización o modificación de la configuración de los componentes de Exchange 2013, como por ejemplo los de buzones de correo, reglas de transporte y destinatarios. Los roles de administración pueden combinarse en agrupaciones más grandes denominadas "grupos de roles de administración" y "directivas de asignación de roles de administración", que permiten la administración de áreas de características y de la configuración de destinatarios. Los grupos de funciones y las directivas de asignación asignan permisos a los administradores y a los usuarios finales, respectivamente. Para obtener más información sobre los grupos de funciones de administración y las directivas de asignación de funciones, vea [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).


> [!NOTE]
> Este tema se centra en las funciones avanzadas de RBAC. Si desea administrar los permisos básicos de Exchange&nbsp;2013, como usar el Panel de control de Exchange (EAC) para agregar y quitar miembros de grupos de roles, crear y modificar grupos de roles o crear y modificar directivas de asignación de roles, consulte <A href="permissions-exchange-2013-help.md">Permisos</A>.



**Contenido**

Roles de administración integrados

Roles de administración de nivel superior sin ámbito

Roles de administración personalizados

Jerarquía de funciones de administración

Entradas de funciones de administración

Entradas de roles de nivel superior sin ámbito

Tipos de roles de administración

Más información

Los ámbitos de funciones de administración y las asignaciones de funciones de administración son componentes importantes de la operación de las funciones de administración. Para obtener más información acerca de estos componentes, vea los temas siguientes:

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

¿Está buscando tareas de administración relacionadas con los roles de administración? Vea [Permisos](permissions-exchange-2013-help.md).

## Roles de administración integrados

Exchange 2013 proporciona varias funciones integradas de administración que pueden usarse para administrar una organización. Cada función incluye los cmdlets y los parámetros necesarios para que los usuarios administren componentes de Exchange específicos. Los siguientes son ejemplos de algunas funciones integradas de administración:

  - **Destinatarios de correo**   Permite a los administradores administrar los buzones de correo, los contactos y los usuarios de correo electrónico.

  - **Reglas de transporte**   habilita a los administradores o usuarios expertos que tienen asignada la función de administrar las características de las reglas de transporte.

  - **Grupos de distribución**   habilita a los administradores o usuarios expertos que tienen asignada la función de administrar grupos de distribución y miembros de los grupos de distribución.

  - **MyPersonalInformation**   Permite a los usuarios finales modificar su propio número de teléfono y la dirección de su sitio web.

Para obtener una lista completa de las funciones de administración incluidas con Exchange 2013, vea [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md).

Puede combinar los roles integrados que se incluyen con Exchange 2013 de la forma que desee para crear modelos de permisos que funcionen en su empresa. Por ejemplo, si desea que los miembros de un grupo de roles administren destinatarios y carpetas públicas, debe asignar las funciones Destinatarios de correo y Carpetas públicas al grupo de roles. A menudo, se asignan funciones a grupos de funciones o a directivas de asignación de funciones. También puede asignar funciones de administración directamente a usuarios si desea controlar permisos a nivel granular. Se recomienda usar grupos de funciones y directivas de asignación de funciones en lugar de la asignación directa de funciones de usuario para simplificar el modelo de permisos.


> [!NOTE]
> Solo se pueden asignar funciones de administración de usuarios finales a las directivas de asignación de funciones.



No es posible cambiar las funciones integradas de administración. Sin embargo, puede crear funciones de administración basadas en las funciones integradas de administración y, luego, asignar las funciones nuevas a grupos de funciones o directivas de asignación de funciones. A continuación, se pueden cambiar las nuevas funciones de administración para satisfacer sus necesidades. Esa es una tarea avanzada que debe realizar en ocasiones excepcionales, si alguna vez es necesario hacerlo.

Para obtener más información acerca de la creación de funciones personalizadas, en las funciones Exchange integradas, vea Roles de administración personalizados que se desarrolla más adelante en este tema.

Debe asignar funciones de administración para que surtan efecto. A menudo, se asignan funciones de administración a grupos de funciones y a directivas de asignación de funciones. En determinadas circunstancias, también es posible asignar funciones directamente a los usuarios, si bien es una tarea avanzada que debe realizarse solo en ocasiones excepcionales, si alguna vez es necesario.

Para obtener más información acerca de la asignación de funciones, vea estos temas:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Para obtener más información acerca de las asignaciones de funciones de administración, vea [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

Volver al principio

## Roles de administración de nivel superior sin ámbito

Los roles de administración de nivel superior sin ámbito son un tipo especial de rol de administración que permite conceder acceso a los scripts personalizados y a cmdlets distintos de Exchange para los usuarios de RBAC. Las funciones de administración normales proporcionan acceso solo a los cmdlets Exchange. Si desea proporcionar acceso a cmdlets distintos de Exchange que se ejecutan en un servidor Exchange, o si desea publicar un script que puedan ejecutar los usuarios, debe agregarlos a una función sin ámbito. Se denominan roles de nivel superior porque al crearse un nuevo rol sin ámbito que no deriva de otro rol primario, no tiene elemento primario y se encuentra en el mismo nivel que las funciones integradas de administración que se incluyen con Exchange 2013. Para indicar que desea crear una entrada de rol de nivel superior sin ámbito, debe usar el conmutador *UnscopedTopLevel* con el cmdlet **New-ManagementRole**.

Las funciones sin ámbito tienen esa denominación porque, a diferencia de las funciones de administración normales, no pueden ser asignadas a un destino específico. Las funciones sin ámbito siempre se aplican en toda la organización. Esto significa que alguien a quien se asignó un rol sin ámbito puede modificar cualquier objeto de la organización de Exchange 2013. Por este motivo, es necesario asegurarse de que los scripts y cmdlets disponibles a través de una función sin ámbito se prueben en detalle para asegurarse de qué elementos modificarán y de asignar las funciones sin ámbito cuidadosamente.

Es posible asignar roles sin ámbito a usuarios a los que se asignan roles, como grupos de roles, roles de administración, usuarios y grupos de seguridad universales (USG). No se pueden asignar a las directivas de asignación de funciones de administración.

Si bien los cmdlets Exchange no pueden agregarse como entradas de funciones de administración en una función sin ámbito, pueden incluirse en scripts agregados como entradas de función. Esto le permite crear scripts personalizados que ejecutan tareas de Exchange que luego pueden asignarse a los usuarios. Una situación útil es donde el usuario debe realizar una tarea con muchos privilegios que, normalmente, se encuentra fuera de su nivel administrativo y donde crear un nuevo rol de administración o un nuevo grupo de roles sería problemático. Es posible crear un script que ejecute esta función específica, agregarlo a una función sin ámbito y, luego, asignar la función sin ámbito al usuario. Luego, el usuario puede ejecutar solamente la función específica proporcionada por el script.

Las entradas de roles que agrega a un rol sin ámbito también deben ser designadas como entradas de rol de nivel superior sin ámbito. Para obtener más información acerca de las entradas de roles de nivel superior sin ámbito, vea Entradas de roles de nivel superior sin ámbito que se desarrolla más adelante en este tema.

El grupo de funciones Administración de la organización no tiene, de manera predeterminada, permisos para crear o administrar grupos de funciones sin ámbito. Esto ayuda a evitar que se creen o se modifiquen por error grupos de funciones sin ámbito. El grupo de funciones Administración de la organización puede delegarse a sí mismo y a otros usuarios a los que se asignan funciones la función Administración de funciones sin ámbito. Para obtener más información acerca de cómo crear un rol de administración de nivel superior sin ámbito, vea [Crear un rol sin ámbito](create-an-unscoped-role-exchange-2013-help.md).

Volver al principio

## Roles de administración personalizados

Es posible crear roles de administración personalizados basadas en roles de Exchange integrados cuando los roles integrados de administración no satisfacen las necesidades de los usuarios. Al crear una función de administración personalizada, la nueva función secundaria hereda todas las entradas de la función de administración de la función principal. Luego, puede elegir las entradas de administración que desea mantener en la función de administración personalizada y quitar todas las entradas que no desee.

Las funciones personalizadas se convierten en funciones secundarias de la función usada para crear la nueva función. Solamente puede usar entradas de funciones de administración en la nueva función secundaria que existe en la función principal. Para obtener más información, vea las secciones siguientes más adelante en este tema:

  - Jerarquía de funciones de administración

  - Entradas de funciones de administración

La creación de funciones de administración personalizadas requiere varios pasos y es una tarea avanzada que solamente debe realizar en ocasiones excepcionales, si alguna vez es necesario. Antes de crear una función de administración personalizada, asegúrese de que una de las funciones integradas de administración existentes no proporcione los permisos que necesita. Para obtener más información acerca de las funciones integradas de administración, o si desea crear funciones de administración personalizadas, vea los temas siguientes:

  - [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md)

  - [Permisos avanzados](advanced-permissions-exchange-2013-help.md)

Para obtener información acerca de cómo crear un rol nuevo, vea [Crear un rol](create-a-role-exchange-2013-help.md).

Volver al principio

## Jerarquía de funciones de administración

Las funciones de administración existen en una jerarquía primaria y secundaria. En la parte superior de la jerarquía se encuentran los roles integrados de administración que se proporcionan de manera predeterminada en Exchange 2013. Al crear un rol nuevo, se crea una copia del rol primario. La nueva función es una función secundaria de la función copiada. A continuación, puede personalizar la nueva función para que se adapte a las necesidades de los administradores o los usuarios a los que les desea asignar dicha función.

Los roles personalizados pueden usarse para crear nuevos roles. Al crear un nuevo rol a partir de un rol personalizado existente, el rol personalizado existente permanece como rol secundario de su rol primario, pero, además, se convierte en rol primario del nuevo rol. Cada vez que se copia una función, la nueva función secundaria solo puede contener las entradas de función que existen en la función principal inmediata.

A cada función de administración se le asigna un tipo de función que no se puede cambiar. El tipo de función define el contexto base de uso para la función. El tipo de función se copia de la función principal al crearse la función secundaria.

**Jerarquía de funciones de administración**

![Diagrama jerárquico de función de administración RBAC](images/Dd298116.6851c829-ca8f-40e7-a67c-cc9e85c33953(EXCHG.150).gif "Diagrama jerárquico de función de administración RBAC")

La figura anterior muestra la relación jerárquica de varias funciones de administración. Las funciones Destinatarios de correo y Servicio de asistencia son funciones integradas. Todas las funciones secundarias derivadas de estas funciones heredan el tipo de función de cada función integrada. Por ejemplo, todas las funciones secundarias derivadas directa o indirectamente de la función Destinatarios de correo heredan el tipo de función `MailRecipients`.

La función personalizada Administradores de destinatarios de Seattle es una función secundaria integrada de la función Destinatarios de correo, pero también es una función principal de la función personalizada Administradores de destinatarios de ventas de Seattle y Administradores de destinatarios legales de Seattle. La función personalizada Administradores de destinatarios de Seattle incluye solo un subconjunto de cmdlets que están disponibles en la función Destinatarios de correo. Los roles secundarios del rol personalizado Administradores de destinatarios de Seattle solo puede incluir cmdlets que también existan en ese rol. Por ejemplo, si existe un cmdlet en el rol Destinatarios de correo, pero no existe en el rol personalizado Administradores de destinatarios de correo, no se puede agregar el cmdlet al rol personalizado Administradores de destinatarios de ventas de Seattle.

Todas las funciones personalizadas siguen el mismo patrón que las funciones analizadas anteriormente. Para obtener más información acerca de cómo se controla el acceso a los cmdlets en las funciones de administración, vea Entradas de funciones de administración a continuación, en este tema.

Volver al principio

## Entradas de funciones de administración

Todas las funciones de administración, ya sean funciones personalizadas de Exchange o sin ámbito, deben tener, como mínimo, una entrada de función de administración. Las entradas consisten de un cmdlet simple y sus parámetros, un script o un permiso especial que usted desea que esté disponible. Si un cmdlet o script no aparece como una entrada en una función de administración, no se obtendrá acceso a ese cmdlet o script mediante esa función. Del mismo modo, si un parámetro no existe en una entrada, no se obtendrá acceso al parámetro en ese cmdlet o script mediante esa función.

Exchange 2013 permite administrar entradas de roles basándose en los roles integrados de administración de nivel superior de Exchange y en las entradas de roles basadas en roles de administración de nivel superior sin ámbito. Los roles basados en roles integrados de nivel superior de Exchange solo pueden contener entradas que sean cmdlets de Exchange 2013. Para agregar scripts personalizados o cmdlets distintos de Exchange para que los usuarios puedan usarlos, debe agregarlos como entradas de roles sin ámbito a un rol de nivel superior sin ámbito. Para obtener más información acerca de las entradas de roles sin ámbito, vea Entradas de roles de nivel superior sin ámbito más adelante en este tema.

Todas las entradas de función, independientemente de si la entrada de función es una entrada de función basada en cmdlet Exchange o una entrada de función sin ámbito, cumplen con los mismos principios explicados en las secciones siguientes.

Para obtener más información acerca de la administración de entradas de funciones, vea [Funciones y administración de entradas de papel](management-roles-and-role-entries-exchange-2013-help.md).

## Relación entre roles de administración primarios y secundarios

Como se mencionó anteriormente, debe existir una entrada de función de administración, que incluya el cmdlet y sus parámetros, en la función principal inmediata para agregar la entrada a la función secundaria. Por ejemplo, si la función principal no tiene una entrada para **New-Mailbox**, no se puede asignar la función secundaria a ese cmdlet. Asimismo, si **Set-Mailbox** se encuentra en la función principal pero el parámetro *Database* se ha quitado de la entrada, el parámetro *Database* del cmdlet **Set-Mailbox** no se puede agregar a la entrada de la función secundaria.

Dado que no es posible agregar entradas de roles de administración a roles secundarios si las entradas no aparecen en los roles primarios y que el rol se basa en un tipo específico de rol, debe elegir atentamente el rol principal que va a copiar cuando desee crear un rol personalizado.

Volver al principio

## Nombres de entradas de roles de administración

Los nombres de las entradas de las funciones de administración son una combinación de la función de administración a las que están asociadas y el nombre del cmdlet o script. El nombre de la función y del cmdlet o script están separados por un carácter de barra invertida (\\). Por ejemplo, el nombre de la entrada de la función del cmdlet **Set-Mailbox** de la función Destinatarios de correo es `Mail Recipients\Set-Mailbox`. Si el nombre de una entrada de función contiene espacios, escriba el nombre completo entre comillas (").

El carácter comodín (\*) puede usarse en el nombre de la entrada de función para obtener todas las entradas de funciones que coincidan con lo que se escribe. El carácter comodín puede usarse a cualquiera de los lados del carácter de barra invertida. La siguiente tabla contiene algunas variaciones del uso posible del carácter de comodín en el nombre de la entrada de una función.

**Nombre de entrada de una función de administración con caracteres comodín**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Ejemplo</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>*\*</code></p></td>
<td><p>Devuelve una lista de todas las entradas de función para todas las funciones.</p></td>
</tr>
<tr class="even">
<td><p><code>*\Set-Mailbox</code></p></td>
<td><p>Devuelve una lista de todas las entradas de función que contienen el cmdlet <strong>Set-Mailbox</strong>.</p></td>
</tr>
<tr class="odd">
<td><p><code>Mail Recipients\*</code></p></td>
<td><p>Devuelve una lista de todas las entradas de función de la función Destinatarios de correo.</p></td>
</tr>
<tr class="even">
<td><p><code>Mail Recipients\*Mailbox</code></p></td>
<td><p>Devuelve una lista de todas las entradas de roles del rol Destinatarios de correo que terminan con Mailbox.</p></td>
</tr>
<tr class="odd">
<td><p><code>My*\*Group*</code></p></td>
<td><p>Devuelve una lista de todas las entradas de rol que contienen la cadena Group en el nombre del cmdlet para todos los roles que comienzan con My.</p></td>
</tr>
</tbody>
</table>


## Entradas de roles de nivel superior sin ámbito

Las entradas de rol de nivel superior sin ámbito se usan con funciones de administración de nivel superior sin ámbito para crear funciones basadas en scripts personalizados o cmdlets distintos de Exchange. Cada entrada de función sin ámbito se asocia a un script personalizado único o a un cmdlet distinto de Exchange. Para indicar que desea crear un rol sin ámbito en un rol sin ámbito, debe especificar el parámetro *UnscopedTopLevel* en el cmdlet **Add-ManagementRoleEntry**.

Al agregar la entrada de función sin ámbito, debe especificar todos los parámetros que se pueden usar con el script o el cmdlet distinto deExchange. Exchange intenta comprobar los parámetros proporcionados al agregar la entrada de función. Solo los parámetros que agregue a la entrada de función al crearla se encontrarán disponibles para los usuarios asignados a la función sin ámbito. Si agrega parámetros al script o al cmdlet distinto de Exchange, o si se cambia el nombre de un parámetro, debe actualizar la entrada de función de forma manual. Exchange no comprueba si los parámetros existentes de una entrada de función sin ámbito han sido modificados. Si un parámetro de una entrada de función cambia en un script y usted intenta usarlo, el comando falla.

Los scripts que se agregan a las entradas de función sin ámbito deben residir en el directorio de scripts de Exchange 2013 en cada servidor al que se conectan los administradores y los usuarios mediante el Shell de administración de Exchange. Si intenta agregar una entrada de función sin ámbito basada en un script que no existe en el directorio de scripts de Exchange 2013 en el servidor que está utilizando para agregar la entrada de función, se producirá un error. La instalación predeterminada del directorio de scripts de Exchange 2013 es C:\\Archivos de programa\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

Los cmdlets distintos de Exchange que se agregan a las entradas de función sin ámbito deben estar instalados en cada servidor Exchange 2013 al que se conectan los administradores y los usuarios mediante el Shell y que desean usar los cmdlets. Si intenta agregar una entrada de función sin ámbito basada en un cmdlet distinto de Exchange que no se ha instalado en el servidor Exchange 2013 que está utilizando para agregar la entrada de función, se producirá un error. Al agregar un cmdlet distinto de Exchange, debe especificar el nombre del complemento de Windows PowerShell que contiene el cmdlet distinto de Exchange.

Para obtener más información acerca de cómo agregar una entrada de función de administración sin ámbito, vea [Agregar una entrada de función a una función](add-a-role-entry-to-a-role-exchange-2013-help.md).

Volver al principio

## Tipos de roles de administración

Los tipos de funciones de administración son la base de todas las funciones de administración. Los tipos definen los ámbitos implícitos definidos en todas las funciones de administración de un tipo de función específico y también actúan como agrupamiento lógico de las funciones relacionadas. Todas las funciones de administración derivadas de la función de administración integrada principal tienen el mismo tipo de función. Vea el gráfico de jerarquías de funciones de administración que aparece más arriba en este tema para ver una ilustración de estas relaciones. Los tipos de roles de administración también representan el conjunto máximo de cmdlets y sus parámetros que pueden agregarse a un rol asociado a un tipo de rol.

Los tipos de funciones de administración se dividen en las siguientes categorías:

  - **Administrativo o experto**   Los roles relacionados con unos tipos de roles administrativos o expertos tienen un alcance más amplio en la organización de Exchange. Las funciones de este tipo habilitan tareas, como la administración de servidores o destinatarios, la configuración de organizaciones, la administración de cumplimiento y las auditorías, entre otras cosas.

  - **Centrado en el usuario**   Los roles asociados a un tipo de rol centrado en el usuario tienen un alcance estrechamente vinculado con un usuario individual. Las funciones de este tipo habilitan tareas, como la configuración y la autoadministración del perfil de usuario y la administración de grupos de distribución que pertenecen a usuarios, entre otras cosas.
    
    Los nombres de los roles asociados con los tipos de roles centrados en el usuario y los nombres de los tipos de roles centrados en el usuario comienzan con My.

  - **Específicos**   Los roles asociados con tipos de roles específicos habilitan tareas que no son de tipo administrativo ni centrados en el usuario. Las funciones de este tipo habilitan tareas, como la suplantación de aplicaciones y el uso de cmdlets distintos de Exchange o scripts.

En la siguiente tabla, figuran todos los tipos administrativos de funciones de administración en Exchange 2013; asimismo, se indica si se aplica la configuración permitida por el tipo de función en toda la organización de Exchange o solamente en un servidor individual. Para obtener más información acerca de cada una de las funciones de administración asociadas a estos tipos de funciones, incluida una descripción de cada función, de quién puede beneficiarse de recibir la asignación de la función y otra información, vea [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md).

**Tipos de funciones administrativas**


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de función de administración</th>
<th>Roles integrados de administración</th>
<th>Descripción</th>
<th>Organización o servidor</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>ActiveDirectoryPermissions</code></p></td>
<td><p><a href="active-directory-permissions-role-exchange-2013-help.md">Rol Permisos de Active Directory</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores configurar permisos de Active Directory en una organización. Algunas de las características que utilizan permisos de Active Directory o una lista de control de acceso (ACL) incluyen conectores de envío y recepción de transporte, y permisos Enviar como y Enviar en nombre de para los buzones.</p>

> [!NOTE]
> Es posible que los permisos establecidos directamente en objetos Active Directory no se exijan a través de RBAC.


</td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>AddressLists</code></p></td>
<td><p><a href="address-lists-role-exchange-2013-help.md">Rol Listas de direcciones</a></p></td>
<td><p>Este tipo de rol se asocia con roles que les permiten a los administradores administrar listas de direcciones, listas globales de direcciones (LGD) y listas de direcciones sin conexión en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>ApplicationImpersonation</code></p></td>
<td><p><a href="applicationimpersonation-role-exchange-2013-help.md">Rol ApplicationImpersonation</a></p></td>
<td><p>Este tipo de rol está asociado con roles que permiten a las aplicaciones usurpar la identidad de los usuarios de una organización para realizar tareas en su nombre.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>ArchiveApplication</code></p></td>
<td><p><a href="archiveapplication-role-exchange-2013-help.md">Rol ArchiveApplication</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten que las aplicaciones asociadas archiven elementos en los buzones de correo de los usuarios de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>AuditLogs</code></p></td>
<td><p><a href="audit-logs-role-exchange-2013-help.md">Rol Registros de auditoría</a></p></td>
<td><p>Este tipo de rol está asociado con roles que les permiten a los administradores administrar la configuración de registro de auditoría de administrador en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>CmdletExtensionAgents</code></p></td>
<td><p><a href="cmdlet-extension-agents-role-exchange-2013-help.md">Rol Agentes de extensión de cmdlet</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar agentes de extensión de cmdlets en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>DataLossPrevention</code></p></td>
<td><p><a href="data-loss-prevention-role-exchange-2013-help.md">Rol Prevención de pérdida de datos</a></p></td>
<td><p>Este tipo de rol está asociado a roles que crean y administran las directivas de prevención de pérdida de datos (DLP) y las reglas entre ellas en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>DatabaseAvailabilityGroups</code></p></td>
<td><p><a href="database-availability-groups-role-exchange-2013-help.md">Rol Grupos de disponibilidad de base de datos</a></p></td>
<td><p>Este tipo de rol está asociado con funciones que les permiten a los administradores administrar grupos de disponibilidad de bases de datos (DAG) en una organización. Los administradores que tienen asignada esta función directa o indirectamente son los administradores de nivel más alto responsables de la configuración de alta disponibilidad en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>DatabaseCopies</code></p></td>
<td><p><a href="database-copies-role-exchange-2013-help.md">Rol Copias de base de datos</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar copias de bases de datos en servidores individuales.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>Databases</code></p></td>
<td><p><a href="databases-role-exchange-2013-help.md">Rol Bases de datos</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores crear, administrar, montar y desmontar bases de datos de buzones de correo en servidores individuales.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>DisasterRecovery</code></p></td>
<td><p><a href="disaster-recovery-role-exchange-2013-help.md">Rol Recuperación ante desastres</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores restaurar los buzones de correo y las bases de datos de los buzones de correo, crear bases de datos de buzones de correo, y realizar cambios y revertirlos en el centro de datos para los grupos de disponibilidad de bases de datos de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>DistributionGroups</code></p></td>
<td><p><a href="distribution-groups-role-exchange-2013-help.md">Rol de grupos de distribución</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores crear y administrar grupos de distribución y miembros de grupos de distribución en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>EdgeSubscriptions</code></p></td>
<td><p><a href="edge-subscriptions-role-exchange-2013-help.md">Rol Suscripciones perimetrales</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores administrar la sincronización perimetral y la configuración de suscripciones entre servidores de transporte perimetral de Exchange 2010 y servidores de buzones de correo de Exchange 2013 en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>EmailAddressPolicies</code></p></td>
<td><p><a href="e-mail-address-policies-role-exchange-2013-help.md">Rol Directivas de dirección de correo electrónico</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores administrar las directivas de direcciones de correo electrónico de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeConnectors</code></p></td>
<td><p><a href="exchange-connectors-role-exchange-2013-help.md">Rol Conectores de Exchange</a></p></td>
<td><p>Este tipo de rol está asociado con roles que permiten a los administradores crear, modificar, ver y quitar conectores de agentes de entrega.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeServerCertificates</code></p></td>
<td><p><a href="exchange-server-certificates-role-exchange-2013-help.md">Rol Certificados del servidor de Exchange</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores crear, importar, exportar y administrar certificados de servidor de Exchange en servidores individuales.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>ExchangeServers</code></p></td>
<td><p><a href="exchange-servers-role-exchange-2013-help.md">Rol Servidores de Exchange</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar la configuración del servidor Exchange en servidores individuales.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>ExchangeVirtualDirectories</code></p></td>
<td><p><a href="exchange-virtual-directories-role-exchange-2013-help.md">Rol Directorios virtuales de Exchange</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores administrar Outlook Web App, Microsoft ActiveSync, la libreta de direcciones sin conexión (OAB), Detección automática, Windows PowerShell y directorios virtuales del Centro de administración de Exchange en servidores individuales.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>FederatedSharing</code></p></td>
<td><p><a href="federated-sharing-role-exchange-2013-help.md">Rol Uso compartido federado</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar elementos compartidos entre bosques y entre organizaciones en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>InformationRightsManagement</code></p></td>
<td><p><a href="information-rights-management-role-exchange-2013-help.md">Rol Administración de derechos de información</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar las características de Information Rights Management (IRM) de Exchange en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>Journaling</code></p></td>
<td><p><a href="journaling-role-exchange-2013-help.md">Rol Registro en diario</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar la configuración de registro en diario en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>LegalHold</code></p></td>
<td><p><a href="legal-hold-role-exchange-2013-help.md">Rol Retención legal</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores realizar tareas de configuración si los datos de un buzón deben conservarse para litigios en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxImportExport</code></p></td>
<td><p><a href="mailbox-import-export-role-exchange-2013-help.md">Rol Importar/Exportar buzón</a></p></td>
<td><p>Este tipo de rol está asociado con los roles que permiten a los administradores importar y exportar contenido de buzones de correo y purgar el contenido no deseado de un buzón.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>MailboxSearch</code></p></td>
<td><p><a href="mailbox-search-role-exchange-2013-help.md">Rol Búsqueda entre buzones</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores buscar el contenido de uno o más buzones en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>MailboxSearchApplication</code></p></td>
<td><p><a href="mailboxsearchapplication-role-exchange-2013-help.md">Rol MailboxSearchApplication</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten que las aplicaciones asociadas establezcan y vean el estado de retención legal de un buzón de correo de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>MailEnabledPublicFolders</code></p></td>
<td><p><a href="mail-enabled-public-folders-role-exchange-2013-help.md">Rol Carpetas públicas habilitadas para correo</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores realizar tareas de configuración si las carpetas públicas individuales están habilitadas o deshabilitadas para correo en una organización.</p>
<p>Este tipo de rol le permite administrar las propiedades de correo electrónico solamente de las carpetas públicas. No le permite administrar las propiedades de las carpetas públicas que no son propiedades del correo electrónico. Para administrar propiedades de carpetas públicas ajenas que no son propiedades de correo electrónico, se le debe asignar un rol asociado a un tipo de rol de <code>PublicFolders</code>.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>MailRecipientCreation</code></p></td>
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Rol Creación de destinatarios de correo</a></p>
<p></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores crear y administrar buzones de correo, contactos de correo, grupos de distribución y grupos de distribución dinámicos en una organización. Las funciones asociadas a este tipo de función se pueden combinar con funciones asociadas al tipo de función de <code>MailRecipients</code> para habilitar la creación y la administración de destinatarios.</p>
<p>Este tipo de función no le permite habilitar carpetas públicas para el correo. Para habilitar carpetas públicas para el correo, se le debe asignar una función asociada al tipo de función de <code>MailEnabledPublicFolders</code>.</p>
<p>Si su organización mantiene un modelo de permisos divididos en el que la creación de destinatarios la realiza un grupo distinto del que realiza la administración de destinatarios, asigne el rol <code>MailRecipientCreation</code> al grupo que realiza la creación de destinatarios y el rol <code>MailRecipients</code> al grupo que realiza la administración de destinatarios.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>MailRecipients</code></p></td>
<td><p><a href="mail-recipients-role-exchange-2013-help.md">Rol Destinatarios de correo</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar buzones de correo, usuarios de correo, contactos de correo, grupos de distribución y grupos de distribución dinámicos existentes en una organización. Las funciones asociadas a este tipo de función no pueden crear estos destinatarios, pero pueden combinarse con funciones asociadas al tipo de función de <code>MailRecipientCreation</code> para habilitar la creación y la administración de destinatarios.</p>
<p>Este tipo de función no lo habilita a administrar carpetas públicas habilitadas para correo o grupos de distribución. Para administrar carpetas públicas habilitadas para correo, se le debe asignar una función asociada al tipo de función de <code>MailEnabledPublicFolders</code>. Para administrar grupos de distribución, debe recibir una función asociada al tipo de función de <code>DistributionGroups</code>.</p>
<p>Si su organización mantiene un modelo de permisos divididos en el que la creación de destinatarios la realiza un grupo distinto del que realiza la administración de destinatarios, asigne el rol <code>MailRecipientCreation</code> al grupo que realiza la creación de destinatarios y el rol <code>MailRecipients</code> al grupo que realiza la administración de destinatarios.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>MailTips</code></p></td>
<td><p><a href="mail-tips-role-exchange-2013-help.md">Rol Sugerencias para correo electrónico</a></p></td>
<td><p>Este tipo de rol está asociado con roles que les permiten a los administradores administrar las sugerencias de correo en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>MessageTracking</code></p></td>
<td><p><a href="message-tracking-role-exchange-2013-help.md">Rol Seguimiento de mensajes</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores realizar un seguimiento de los mensajes en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>Migration</code></p></td>
<td><p><a href="migration-role-exchange-2013-help.md">Rol de migración</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores migrar buzones y el contenido de los buzones hacia un servidor o fuera de él.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>Monitoring</code></p></td>
<td><p><a href="monitoring-role-exchange-2013-help.md">Rol Supervisión</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores supervisar los servicios de Microsoft Exchange y la disponibilidad de componentes en una organización. Además de los administradores, las funciones asociadas a este tipo de función pueden usarse con la cuenta de servicio usada por las aplicaciones de supervisión a fin de recopilar información acerca del estado de los servidores Exchange.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>MoveMailboxes</code></p></td>
<td><p><a href="move-mailboxes-role-exchange-2013-help.md">Rol Mover buzones</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores mover buzones entre servidores en una organización y entre servidores en la organización local y otra organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>OfficeExtensionApplication</code></p></td>
<td><p><a href="officeextensionapplication-role-exchange-2013-help.md">Rol OfficeExtensionApplication</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten que las aplicaciones de extensiones de Microsoft Office accedan a los buzones de correo de los usuarios de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>OrgCustomApps</code></p></td>
<td><p><a href="org-custom-apps-role-exchange-2013-help.md">Rol Aplicaciones personalizadas de la organización</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores ver y modificar las aplicaciones personalizadas de su organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>OrgMarketplaceApps</code></p></td>
<td><p><a href="org-marketplace-apps-role-exchange-2013-help.md">Rol de aplicaciones del mercado de la organización</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores ver y modificar las aplicaciones del catálogo de soluciones de su organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationClientAccess</code></p></td>
<td><p><a href="organization-client-access-role-exchange-2013-help.md">Rol Acceso de clientes de la organización</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar la configuración del servidor de acceso de cliente en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>OrganizationConfiguration</code></p></td>
<td><p><a href="organization-configuration-role-exchange-2013-help.md">Rol Configuración de la organización</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar las configuraciones de toda una organización. La configuración de la organización que se puede controlar con este tipo de función incluye lo siguiente (entre otras cosas):</p>
<ul>
<li><p>Si se habilitan o deshabilitan las sugerencias de correo electrónico para la organización.</p></li>
<li><p>La dirección URL de la página principal de la carpeta administrada.</p></li>
<li><p>La dirección de destinatario SMTP de Microsoft Exchange y las direcciones de correo electrónico alternativas.</p></li>
<li><p>La configuración de esquema de propiedades del buzón de recursos.</p></li>
<li><p>Las direcciones URL del Centro de administración de Exchange y Outlook Web App.</p></li>
</ul>
<p>Este tipo de función no incluye los permisos incluidos en los tipos de función <code>OrganizationClientAccess</code> o <code>OrganizationTransportSettings</code>.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>OrganizationTransportSettings</code></p></td>
<td><p><a href="organization-transport-settings-role-exchange-2013-help.md">Rol Configuración de transporte de la organización</a></p></td>
<td><p>Este tipo de rol se asocia a roles que permiten que los administradores administren las configuraciones de transporte de toda la organización, como los mensajes del sistema, la configuración del sitio de Active Directory y otras configuraciones de transporte de una organización.</p>
<p>Esta función no permite crear ni administrar conectores de envío o recepción, colas, higiene, agentes, dominios remotos o aceptados, ni reglas de transporte. Para crear o administrar cada una de las características de transporte, se le deben asignar funciones asociadas a los siguientes tipos de funciones:</p>
<ul>
<li><p><strong>Conectores de recepción</strong> <code>ReceiveConnectors</code></p></li>
<li><p><strong>Conectores de envío</strong> <code>SendConnectors</code></p></li>
<li><p><strong>Colas de transporte</strong> <code>TransportQueues</code></p></li>
<li><p><strong>Higiene de transporte</strong> <code>TransportHygiene</code></p></li>
<li><p><strong>Agentes de transporte</strong> <code>TransportAgents</code></p></li>
<li><p><strong>Dominios remotos y aceptados</strong> <code>RemoteAndAcceptedDomains</code></p></li>
<li><p><strong>Reglas de transporte</strong> <code>TransportRules</code></p></li>
</ul></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>POP3AndIMAP4Protocols</code></p></td>
<td><p><a href="pop3-and-imap4-protocols-role-exchange-2013-help.md">Rol Protocolos POP3 e IMAP4</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar la configuración de POP3 e IMAP4, como los parámetros de autenticación y conexión de servidores individuales.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>PublicFolders</code></p></td>
<td><p><a href="public-folders-role-exchange-2013-help.md">Rol Carpetas públicas</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar las carpetas públicas en una organización.</p>
<p>Este tipo de rol no le permite administrar si las carpetas públicas tienen correo habilitado. Para habilitar o deshabilitar una carpeta pública para el correo, se le debe asignar una función asociada al tipo de función de <code>MailEnabledPublicFolders</code>.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>ReceiveConnectors</code></p></td>
<td><p><a href="receive-connectors-role-exchange-2013-help.md">Rol Conectores de recepción</a></p></td>
<td><p>Este tipo de rol está asociado con roles que les permiten a los administradores administrar la configuración del conector de recepción de transporte, como los límites de tamaño de un servidor individual.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="odd">
<td><p><code>RecipientPolicies</code></p></td>
<td><p><a href="recipient-policies-role-exchange-2013-help.md">Rol Directivas de destinatarios</a></p></td>
<td><p>Este tipo de rol se asocia a roles que permiten que los administradores administren directivas de destinatarios en una organización, como las directivas de aprovisionamiento y de dispositivos móviles.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>RemoteAndAcceptedDomains</code></p></td>
<td><p><a href="remote-and-accepted-domains-role-exchange-2013-help.md">Rol Dominios remotos y aceptados</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar dominios remotos y aceptados en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>ResetPassword</code></p></td>
<td><p><a href="reset-password-role-exchange-2013-help.md">Rol Restablecer contraseña</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los usuarios restablecer sus propias contraseñas y a los administradores, restablecer las contraseñas de los usuarios en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>RetentionManagement</code></p></td>
<td><p><a href="retention-management-role-exchange-2013-help.md">Rol Administración de la retención</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar las directivas de retención en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>RoleManagement</code></p></td>
<td><p><a href="role-management-role-exchange-2013-help.md">Rol Administración de roles</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar grupos de funciones de administración, directivas de asignación de funciones, funciones de administración, entradas de funciones, asignaciones y ámbitos en una organización.</p>
<p>Los usuarios a los que se asignaron funciones asociadas a este tipo de función pueden anular el grupo de funciones <strong>role group managed by</strong>, configurar cualquier grupo de funciones, y agregar miembros a cualquier grupo de funciones o quitarlos de él.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>SecurityGroupCreationAndMembership</code></p></td>
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Rol Pertenencia y Creación de grupos de seguridad</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores crear y administrar UGS y sus miembros en una organización.</p>
<p>Si su organización mantiene un modelo de permisos divididos en los que la creación y la administración de USG son realizadas por un grupo diferente del que administra los servidores de Exchange, asigne roles asociados a este tipo de rol a ese grupo.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>SendConnectors</code></p></td>
<td><p><a href="send-connectors-role-exchange-2013-help.md">Rol Conectores de envío</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar los conectores de envío de transporte en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>SupportDiagnostics</code></p></td>
<td><p><a href="support-diagnostics-role-exchange-2013-help.md">Rol Diagnósticos de soporte</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores realizar diagnósticos avanzados con la dirección de los Servicios de soporte técnico de Microsoft en una organización.</p>

> [!WARNING]
> Las funciones asociadas a este tipo de función conceden permisos a cmdlets y scripts que solo deben utilizarse con la dirección del servicio de soporte técnico y atención al cliente de Microsoft.


</td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>TeamMailboxes</code></p></td>
<td><p><a href="team-mailboxes-role-exchange-2013-help.md">Rol Buzones de equipo</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores definir una o más directivas de aprovisionamiento de buzones de correo del sitio y gestionar los buzones de correo del sitio de una organización. Los administradores a los que se les asigna roles asociados a este tipo de rol pueden administrar buzones de correo del sitio de los que no son propietarios.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>TeamMailboxLifecycleApplication</code></p></td>
<td><p><a href="teammailboxlifecycleapplication-role-exchange-2013-help.md">Rol TeamMailboxLifecycleApplication</a></p></td>
<td><p>Este tipo de rol se asocia a roles que permiten que las aplicaciones asociadas actualicen los estados de ciclo de vida de buzones de correo del sitio de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportAgents</code></p></td>
<td><p><a href="transport-agents-role-exchange-2013-help.md">Rol Agentes de transporte</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar agentes de transporte en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>TransportHygiene</code></p></td>
<td><p><a href="transport-hygiene-role-exchange-2013-help.md">Rol Higiene de transporte</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores administrar características de protección contra el correo no deseado y antivirus en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>TransportQueues</code></p></td>
<td><p><a href="transport-queues-role-exchange-2013-help.md">Rol Colas de transporte</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar colas de transporte en servidores individuales.</p></td>
<td><p>Servidor</p></td>
</tr>
<tr class="even">
<td><p><code>TransportRules</code></p></td>
<td><p><a href="transport-rules-role-exchange-2013-help.md">Rol Reglas de transporte</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar reglas de transporte en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>UMMailboxes</code></p></td>
<td><p><a href="um-mailboxes-role-exchange-2013-help.md">Rol Buzones de mensajería unificada</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores administrar la configuración de mensajería unificada (MU) de los buzones y otros destinatarios en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>UMPrompts</code></p></td>
<td><p><a href="um-prompts-role-exchange-2013-help.md">Rol Mensajes de mensajería unificada</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores crear y administrar mensajes de asistencia por voz de MU en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>UnifiedMessaging</code></p></td>
<td><p><a href="unified-messaging-role-exchange-2013-help.md">Rol Mensajería unificada</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores administrar los servicios de mensajería unificada de una organización.</p>
<p>Esta función no lo habilita a administrar la configuración de buzones específicos de mensajería unificada o mensajes de mensajería unificada. Para administrar la configuración específica del buzón de MU, utilice las funciones asociadas con el tipo de función <code>UMMailboxes</code>. Para administrar mensajes de MU, utilice las funciones asociadas con el tipo de función <code>UMPrompts</code>.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>UnScopedRoleManagement</code></p></td>
<td><p><a href="unscoped-role-management-role-exchange-2013-help.md">Rol Administración de roles sin ámbito</a></p></td>
<td><p>Este tipo de rol está asociado a funciones que les permiten a los administradores crear y administrar roles de administración de nivel superior sin ámbito en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>UserOptions</code></p></td>
<td><p><a href="user-options-role-exchange-2013-help.md">Rol Opciones de usuario</a></p></td>
<td><p>Este tipo de rol está asociado a roles que les permiten a los administradores ver las opciones de Outlook Web App de un usuario en una organización. Los roles asociados a este tipo de rol pueden usarse para ayudar a un usuario a diagnosticar problemas con su configuración.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>UserApplication</code></p></td>
<td><p><a href="userapplication-role-exchange-2013-help.md">Rol UserApplication</a></p></td>
<td><p>Este tipo de rol se asocia a roles que permiten que las aplicaciones asociadas actúen en nombre de los usuarios finales de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyAuditLogs</code></p></td>
<td><p><a href="view-only-audit-logs-role-exchange-2013-help.md">Rol Registros de auditoría con permiso de vista</a></p></td>
<td><p>Este tipo de rol está asociado con roles que les permiten a los administradores buscar el registro de auditoría de administrador en una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>ViewOnlyConfiguration</code></p></td>
<td><p><a href="view-only-configuration-role-exchange-2013-help.md">Rol Configuración con permiso de vista</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores ver todas las opciones de configuración distintas de las de los destinatarios de Exchange en una organización. Ejemplos visibles de configuración son la configuración de servidores, la configuración de transporte, la configuración de bases de datos y la configuración de toda la organización.</p>
<p>Las funciones asociadas a este tipo de función se pueden combinar con funciones asociadas al tipo de función de <code>ViewOnlyRecipients</code> para crear una función que pueda ver cada objeto de una organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="odd">
<td><p><code>ViewOnlyRecipients</code></p></td>
<td><p><a href="view-only-recipients-role-exchange-2013-help.md">Rol Destinatarios con permiso de vista</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los administradores ver la configuración de los destinatarios, como buzones de correo, usuarios de correo, contactos de correo, grupos de distribución y grupos de distribución dinámicos.</p>
<p>Las funciones asociadas a este tipo de función se pueden combinar con funciones asociadas al tipo de función de <code>ViewOnlyConfiguration</code> para crear una función que pueda ver cada objeto de la organización.</p></td>
<td><p>Organización</p></td>
</tr>
<tr class="even">
<td><p><code>WorkloadManagement</code></p></td>
<td><p><a href="workloadmanagement-role-exchange-2013-help.md">Rol WorkloadManagement</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los administradores administrar las directivas de administración de carga de trabajo de una organización. Los administradores pueden configurar las definiciones de estado de los recursos, las clasificaciones de carga de trabajo y habilitar o deshabilitar la administración de cargas de trabajo.</p></td>
<td><p>Organización</p></td>
</tr>
</tbody>
</table>


La siguiente tabla enumera todos los tipos de roles de administración centrados en el usuario y los roles de administración incorporados asociados en Exchange 2013.

**Tipos de funciones centradas en el usuario**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Tipo de rol de administración</th>
<th>Roles integrados centrados en el usuario</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>MyBaseOptions</code></p></td>
<td><p><a href="mybaseoptions-role-exchange-2013-help.md">Rol MyBaseOptions</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los usuarios individuales ver y modificar la configuración básica de sus propios buzones y parámetros asociados.</p></td>
</tr>
<tr class="even">
<td><p><code>MyContactInformation</code></p></td>
<td><p><a href="myaddressinformation-role-exchange-2013-help.md">Función MyAddressInformation</a></p>
<p><a href="mycontactinformation-role-exchange-2013-help.md">Rol MyContactInformation</a></p>
<p><a href="mymobileinformation-role-exchange-2013-help.md">Función MyMobileInformation</a></p>
<p><a href="mypersonalinformation-role-exchange-2013-help.md">Función MyPersonalInformation</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los usuarios individuales modificar su información de contacto. Esta información incluye la dirección y los números de teléfono.</p></td>
</tr>
<tr class="odd">
<td><p>MyCustomApps</p></td>
<td><p><a href="my-custom-apps-role-exchange-2013-help.md">Rol Mis aplicaciones personalizadas</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los usuarios individuales ver y modificar sus aplicaciones personalizadas.</p></td>
</tr>
<tr class="even">
<td><p>MyDiagnostics</p></td>
<td><p><a href="mydiagnostics-role-exchange-2013-help.md">Rol MyDiagnostics</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los usuarios individuales realizar diagnósticos básicos en sus buzones de correo, como recuperar información de diagnóstico del calendario.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyDistributionGroupMembership</code></p></td>
<td><p><a href="mydistributiongroupmembership-role-exchange-2013-help.md">Rol MyDistributionGroupMembership</a></p></td>
<td><p>Este tipo de función está asociado a las funciones que les permiten a los usuarios individuales ver y modificar su membresía de grupos de distribución de una organización, siempre que dichos grupos de distribución permitan la manipulación de las membresías de los grupos.</p></td>
</tr>
<tr class="even">
<td><p><code>MyDistributionGroups</code></p></td>
<td><p><a href="mydistributiongroups-role-exchange-2013-help.md">Rol MyDistributionGroups</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los usuarios individuales crear, modificar y ver grupos de distribución, y modificar, ver, quitar y agregar miembros en sus propios grupos de distribución.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyProfileInformation</code></p></td>
<td><p><a href="mydisplayname-role-exchange-2013-help.md">Función MyDisplayName</a></p>
<p><a href="myname-role-exchange-2013-help.md">Función minombre</a></p>
<p><a href="myprofileinformation-role-exchange-2013-help.md">Rol MyProfileInformation</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los usuarios individuales modificar su nombre.</p></td>
</tr>
<tr class="even">
<td><p>MyMarketplaceApps</p></td>
<td><p><a href="my-marketplace-apps-role-exchange-2013-help.md">Rol My Marketplace Apps</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los usuarios individuales ver y modificar sus aplicaciones del catálogo de soluciones.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyRetentionPolicies</code></p></td>
<td><p><a href="myretentionpolicies-role-exchange-2013-help.md">Rol MyRetentionPolicies</a></p></td>
<td><p>Este tipo de función está asociada a funciones que les permiten a los usuarios individuales ver sus etiquetas de retención, y ver y modificar los parámetros y los valores predeterminados de su etiqueta de retención.</p></td>
</tr>
<tr class="even">
<td><p>MyTeamMailboxes</p></td>
<td><p><a href="myteammailboxes-role-exchange-2013-help.md">Rol MyTeamMailboxes</a></p></td>
<td><p>Este tipo de rol está asociado a roles que permiten a los usuarios individuales crear buzones de correo del sitio y conectarlos a los sitios de Microsoft SharePoint.</p></td>
</tr>
<tr class="odd">
<td><p><code>MyTextMessaging</code></p></td>
<td><p><a href="mytextmessaging-role-exchange-2013-help.md">Rol MyTextMessaging</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los usuarios individuales crear, ver y modificar los parámetros de los mensajes de texto.</p></td>
</tr>
<tr class="even">
<td><p><code>MyVoiceMail</code></p></td>
<td><p><a href="myvoicemail-role-exchange-2013-help.md">Rol MyVoiceMail</a></p></td>
<td><p>Este tipo de función está asociado a funciones que les permiten a los usuarios individuales ver y modificar los parámetros del correo de voz.</p></td>
</tr>
</tbody>
</table>


Volver al principio

## Más información

[New-ManagementRole](https://technet.microsoft.com/es-es/library/dd298073\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\))

[New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\))

[Set-ManagementScope](https://technet.microsoft.com/es-es/library/dd297996\(v=exchg.150\))

[New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\))

[Set-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335173\(v=exchg.150\))

