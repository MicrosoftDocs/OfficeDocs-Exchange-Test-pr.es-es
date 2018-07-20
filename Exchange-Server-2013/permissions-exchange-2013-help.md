---
title: 'Permisos: Exchange 2013 Help'
TOCTitle: Permisos
ms:assetid: d8dd605e-0af1-4e18-9ce6-e51d04e161ba
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351175(v=EXCHG.150)
ms:contentKeyID: 48268744
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permisos

 

_**Se aplica a:** Exchange Server, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Microsoft Exchange Server 2013 incluye una amplia variedad de permisos predefinidos, basados en el modelo de permisos Control de acceso basado en roles (RBAC), que puede usar de inmediato para conceder de forma fácil permisos a los administradores y usuarios. Puede usar las características de permisos de Exchange 2013 para preparar y poner en marcha la nueva organización de forma rápida.


> [!NOTE]
> Varios conceptos y características de RBAC no se incluyen en este tema porque son características avanzadas. Si las funciones tratadas en este tema no satisfacen sus necesidades y quiere personalizar todavía más el modelo de permisos, vea <A href="understanding-role-based-access-control-exchange-2013-help.md">Descripción del control de acceso basado en funciones</A>.



¿Busca una lista de todos los temas de permisos? Consulte Permissions documentation.

**Contenido**

Role-based permissions

Role groups and role assignment policies

Work with role groups

Work with role assignment policies

## Permisos basados en roles

En Exchange 2013, los permisos que concede a los administradores y usuarios se basan en roles de administración. Un rol define el conjunto de tareas que un administrador o usuario puede realizar. Por ejemplo, un rol de administración denominado `Mail Recipients` define las tareas que alguien puede realizar en un conjunto de buzones de correo, contactos y grupos de distribución. Cuando un rol se asigna a un administrador o usuario, a dicha persona se conceden los permisos que proporciona el rol en cuestión.

Existen dos tipos de roles: los roles administrativos y los roles de usuario final:

  - **Roles administrativos**   Estos roles contienen permisos que se pueden asignar a los administradores o usuarios especialistas mediante grupos de roles que administran una parte de la organización de Exchange, como destinatarios, servidores o bases de datos.

  - **Roles de usuario final**   Estos roles, asignados mediante directivas de asignación de roles, permiten a los usuarios administrar aspectos de su propio buzón de correo y de los grupos de distribución de que disponen. Los roles de usuario final empiezan por el prefijo `My`.

Los roles conceden a los administradores y usuarios permisos para realizar tareas poniendo cmdlets a disposición de aquellos usuarios que tienen asignados los roles en cuestión. Dado que el centro de administración de Exchange (EAC) y el Shell de administración de Exchange usan cmdlets para administrar Exchange, conceder acceso a un cmdlet le brinda al administrador o al usuario permiso para realizar la tarea en cada una de las interfaces de administración de Exchange.

Exchange 2013 incluye aproximadamente 86 roles que pueden usarse para conceder permisos. Para obtener una lista de los roles incluidos en Exchange 2013, vea [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md).

Volver al principio

## Grupos de roles y directivas de asignación de roles

Los roles conceden permisos para realizar tareas en Exchange 2013, pero se necesita un método sencillo para asignar los roles a los administradores y usuarios. Para ello, Exchange 2013 proporciona los elementos siguientes:

  - **Grupos de roles**   Los grupos de roles permiten conceder permisos a administradores y usuarios especialistas.

  - **Directivas de asignación de roles**   Las directivas de asignación de roles permiten conceder permisos a los usuarios finales para cambiar la configuración de su propio buzón o de los grupos de distribución de que disponen.

Para obtener más información sobre los grupos de roles y las directivas de asignación de roles, consulte las secciones siguientes.

## Grupos de funciones

Cada uno de los administradores que administran Exchange 2013 deben tener asignado por lo menos uno o más roles. Los administradores pueden tener más de un rol porque pueden realizar funciones de trabajo que abarcan varias áreas de Exchange. Por ejemplo, un administrador puede administrar tanto los destinatarios como los servidores de Exchange. En tal caso, es posible asignar al administrador el rol `Mail Recipients` y `Exchange Servers`.

Para que resulte más sencillo asignar varios roles a un administrador, Exchange 2013 incluye grupos de roles. Los grupos de roles son grupos de seguridad universal especiales (USG) usados por Exchange 2013 y que contienen usuarios de Active Directory, USG y otros grupos de roles. Cuando se asigna un rol a un grupo de roles, los permisos concedidos por el rol se conceden a todos los miembros del grupo de roles. De esta forma, puede asignar varios roles a varios miembros del grupo de roles al mismo tiempo. Los grupos de roles suelen abarcar áreas de administración más amplias, como la administración de destinatarios. Solamente se usan con roles administrativos y no pueden usarse con roles de usuario final.


> [!NOTE]
> Es posible asignar un rol directamente a un usuario o USG sin usar un grupo de roles. Sin embargo, este método de asignación de roles es un procedimiento avanzado y no se trata en este tema. Se recomienda usar grupos de roles para administrar los permisos.



En la figura siguiente se muestra la relación entre usuarios, grupos de roles y roles.

**Roles, grupos de roles y miembros de grupos de roles**

![Rol, relación de los miembros y grupo de roles](images/Dd351175.3fb0b47d-333a-4953-ae38-d710d327bde0(EXCHG.150).gif "Rol, relación de los miembros y grupo de roles")

Exchange 2013 incluye varios grupos de roles integrados, cada uno de los cuales proporciona permisos para administrar áreas específicas de Exchange 2013. Algunos grupos de roles pueden solaparse con otros. En la tabla siguiente se enumera cada uno de los grupos de roles con una descripción de su uso. Si quiere ver los roles que tiene asignado cada uno de los grupos de roles, haga clic en el nombre del grupo de roles en la columna "Grupo de roles" y luego abra la sección "Roles de administración asignados a este grupo de roles".

### Grupos de funciones integradas

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupo de roles</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
<td><p>Los administradores que son miembros del grupo de roles Administración de la organización tienen acceso administrativo a toda la organización de Microsoft Exchange 2013 y pueden realizar prácticamente todas las tareas relacionadas con los objetos de Exchange 2013, con algunas excepciones, como el rol <code>Discovery Management</code>.</p>

> [!IMPORTANT]
> Como el grupo de roles Administración de la organización&nbsp;es un rol muy eficaz, solamente deben ser miembros de este grupo de roles los usuarios o grupos de seguridad universal (USG) que realicen tareas administrativas a nivel organizativo y que puedan afectar potencialmente a toda la organización de Exchange.


</td>
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
<td><p>Los administradores que son miembros del grupo de roles de administración de mensajería unificada pueden administrar características de la organización de Exchange, como la configuración del servicio de mensajería unificada, las propiedades de mensajería unificada en los buzones, los mensajes de asistencia por voz de mensajería unificada y la configuración del operador automático para mensajería unificada.</p></td>
</tr>
<tr class="odd">
<td><p><a href="help-desk-exchange-2013-help.md">Servicio de asistencia</a></p></td>
<td><p>De forma predeterminada, el grupo de roles del servicio de asistencia permite a los miembros ver y modificar las opciones de OfficeOutlook Web App de cualquier usuario de la organización. Estas opciones podrían incluir la modificación del nombre para mostrar, la dirección o el teléfono. No incluyen opciones que no están disponibles en las opciones de Outlook Web App, como la modificación del tamaño de un buzón o la configuración de la base de datos de buzones en la que se encuentra un buzón.</p></td>
</tr>
<tr class="even">
<td><p><a href="hygiene-management-exchange-2013-help.md">Administración de higiene</a></p></td>
<td><p>Los administradores que pertenecen al grupo de roles Administración de higiene pueden configurar las funciones antivirus y contra correo electrónico no deseado de Exchange 2013. Los programas de terceros que se integran con Exchange 2013 pueden agregar cuentas de servicio a este grupo de roles para que dichos programas puedan tener acceso a los cmdlets que se requieren para recuperar y establecer la configuración de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="records-management-exchange-2013-help.md">Administración de registros</a></p></td>
<td><p>Los usuarios que son miembros del grupo de funciones Records Management pueden configurar las características de cumplimiento, como las etiquetas de directiva de retención, las clasificaciones de mensajes y las reglas de transporte.</p></td>
</tr>
<tr class="even">
<td><p><a href="discovery-management-exchange-2013-help.md">Administración de la detección</a></p></td>
<td><p>Los administradores o usuarios que son miembros del grupo de roles Discovery Management pueden realizar búsquedas en buzones de correo de la organización de Exchange para obtener datos que cumplan determinados criterios y pueden configurar retenciones legales de buzones de correo.</p></td>
</tr>
<tr class="odd">
<td><p><a href="public-folder-management-exchange-2013-help.md">Administración de carpetas públicas</a></p></td>
<td><p>Los administradores que son miembros del grupo de roles Administración de carpetas públicas pueden administrar carpetas públicas en los servidores que ejecuten Exchange 2013.</p></td>
</tr>
<tr class="even">
<td><p><a href="server-management-exchange-2013-help.md">Administración de servidor</a></p></td>
<td><p>Los administradores que son miembros del grupo de roles Administración de servidor pueden establecer la configuración específica de servidor del transporte, la mensajería unificada, el acceso de clientes y las características de buzón, como copias de las bases de datos, certificados, colas de transporte y conectores de envío, directorios virtuales y protocolos de acceso de cliente.</p></td>
</tr>
<tr class="odd">
<td><p><a href="delegated-setup-exchange-2013-help.md">Configuración delegada</a></p></td>
<td><p>Los administradores que pertenecen al grupo de funciones Configuración delegada pueden implementar servidores que ejecutan Exchange 2013 que ya han sido aprovisionados por un miembro del grupo de funciones Administración de la organización.</p></td>
</tr>
<tr class="even">
<td><p><a href="compliance-management-exchange-2013-help.md">Administración de cumplimiento</a></p></td>
<td><p>Los usuarios que pertenecen al grupo de roles de administración de cumplimiento pueden configurar y administrar la configuración de cumplimiento de Exchange de acuerdo con la directiva de la organización.</p></td>
</tr>
</tbody>
</table>


Si trabaja en una organización pequeña que únicamente tiene unos pocos administradores, es posible que solamente necesite agregarlos al grupo de roles Administración de la organización y que nunca necesite usar el resto de grupos de roles. En cambio, si trabaja en una organización de mayor tamaño, tendrá administradores que realicen tareas específicas para la administración de Exchange, como la administración de destinatarios o servidores. En estos casos, puede agregar un administrador al grupo de roles Recipient Management y otro administrador al grupo de roles Administración de servidor. De esta forma, dichos administradores pueden administrar áreas específicas de Exchange 2013 pero no tendrán permisos para administrar áreas de las que no son responsables.

Si los grupos de roles integrados en Exchange 2013 no coinciden con la función de trabajo de los administradores, puede crear grupos de roles y agregar roles a ellos. Para obtener más información, consulte Work with Role Groups más adelante en este tema.

Volver al principio

## Directivas de asignación de roles

Exchange 2013 proporciona directivas de asignación de roles para que permiten controlar las opciones que los usuarios pueden configurar en sus propios buzones de correo y en los grupos de distribución de que disponen. Estas opciones incluyen el nombre para mostrar, la información de contacto, la configuración de correo de voz y la pertenencia a grupos de distribución.

La organización de Exchange 2013 puede tener asignadas varias directivas de asignación de roles que proporcionan distintos niveles de permisos para los diversos tipos de usuarios de sus organizaciones. Algunos usuarios pueden tener permiso para cambiar su dirección o crear grupos de distribución, mientras que otros no, según la directiva de asignación de roles que esté asociada a su buzón de correo. Las directivas de asignación de roles se agregan directamente a los buzones de correo, y cada uno de ellos solamente puede asociarse con una directiva de asignación de roles a la vez.

Una de las directivas de asignación de roles de la organización se marca como predeterminada. La directiva de asignación de roles predeterminada se asocia con los nuevos buzones a los que no se asigna de forma explícita una directiva de asignación de roles en el momento de su creación. La directiva de asignación de roles predeterminada tiene que contener los permisos que deben aplicarse a la mayoría de los buzones.

Los permisos se agregan a las directivas de asignación de roles usando roles de usuario final. Los roles de usuario final empiezan por `My` y conceden permisos a los usuarios para administrar solo sus buzones de correo o los grupos de distribución que tienen. No pueden usarse para administrar ningún otro buzón de correo. A las directivas de asignación de roles solo pueden asignarse roles de usuario final.

Cuando se asigna un rol de usuario final a una directiva de asignación de roles, todos los buzones asociados con la directiva de asignación de roles reciben los permisos concedidos por el rol. Esto permite agregar o quitar permisos a conjuntos de usuarios sin tener que configurar buzones por separado. En la figura siguiente vemos que:

  - Los roles de usuario final se asignan a las directivas de asignación de roles. Las directivas de asignación de roles pueden compartir los mismos roles de usuario final.

  - Las directivas de asignación de roles se asocian con buzones. Cada buzón puede asociarse con una única directiva de asignación de roles.

  - Después de asociar un buzón con una directiva de asignación de roles, los roles de usuario final se aplican al buzón en cuestión. Los permisos concedidos por los roles se conceden al usuario del buzón.

**Roles, directivas de asignación de roles y buzones**

![Relaciones de buzón de correo, rol, directiva de asignación de roles](images/Dd351175.82e07b3d-da59-465b-b349-e0bfde369ace(EXCHG.150).gif "Relaciones de buzón de correo, rol, directiva de asignación de roles")

La directiva de asignación de roles predeterminada se incluye en Exchange 2013. Como su nombre indica, es una directiva de asignación de roles por defecto. Si desea cambiar los permisos proporcionados por esta directiva de asignación de roles o si desea crear directivas de asignación de roles, consulte Work with Role Assignment Policies más adelante en este tema.

## Trabajar con grupos de roles

Para administrar los permisos con grupos de roles en Exchange 2013, recomendamos que use el centro de administración de Exchange. Al usar el EAC para administrar grupos de roles, es posible agregar y quitar roles y miembros, crear grupos de roles y copiar los grupos de roles con unos pocos clics. El EAC proporciona cuadros de diálogo sencillos, como el cuadro de diálogo **Nuevo grupo de roles**, que se muestra en la figura siguiente, para realizar estas tareas.

**Cuadro de diálogo Nuevo grupo de roles en el EAC**

![Cuadro de diálogo Nuevo grupo de roles en el EAC](images/Dd351175.e0577090-73e6-4671-ae98-78a8064fde87(EXCHG.150).jpg "Cuadro de diálogo Nuevo grupo de roles en el EAC")

Exchange 2013 incluye varios grupos de roles que separan los permisos en áreas administrativas específicas. Si los grupos de roles existentes proporcionan los permisos que los administradores necesitan para administrar la organización de Exchange 2013, solamente tendrá que agregar los administradores como miembros de los grupos de roles pertinentes. Después de agregar los administradores a un grupo de roles, podrán administrar las características que estén relacionadas con el grupo de roles en cuestión. Para agregar o quitar miembros de un grupo de roles, abra el grupo de roles en el EAC y, a continuación, agregue o quite los miembros de la lista de pertenencia. Para obtener una lista de los grupos de roles integrados, vea [Grupos de funciones integradas](built-in-role-groups-exchange-2013-help.md).


> [!IMPORTANT]
> Si un administrador es miembro de más de un grupo de roles, Exchange&nbsp;2013 concederá al administrador todos los permisos que proporcionen los grupos de roles de los que es miembro.



Si ninguno de los grupos de roles incluidos en Exchange 2013 tiene los permisos que necesita, puede usar el EAC para crear un grupo de roles y agregar los roles que tengan los permisos que necesita. Para el nuevo grupo de roles, deberá:

1.  Asignar un nombre al grupo de roles.

2.  Seleccionar los roles que quiere agregar al grupo de roles.

3.  Agregar miembros al grupo de roles.

4.  Guardar el grupo de roles.

Después de crear el grupo de roles, podrá administrarlo como cualquier otro grupo de roles.

Si existe algún grupo de roles que tiene algunos de los permisos que necesita, pero no todos, puede copiarlo y realizar cambios para crear un grupo de roles. Puede copiar un grupo de roles existente y realizar cambios en él, sin que ello afecte al grupo de roles original. Como parte del proceso de copia del grupo de roles, puede agregar un nombre y una descripción nuevos, agregar y quitar roles del nuevo grupo de roles y agregar miembros nuevos. Para crear o copiar un grupo de roles, se usa el mismo cuadro de diálogo que aparece en la figura anterior.

Los grupos de roles existentes también pueden modificarse. Puede agregar y quitar roles de los grupos de roles existentes, así como agregar y quitar miembros al mismo tiempo, mediante un cuadro de diálogo de EAC similar al cuadro de diálogo que se muestra en la figura anterior. Al agregar y quitar roles de grupos de roles, se activan y desactivan características administrativas para los miembros del grupo de roles en cuestión. Para obtener una lista de los roles que puede agregar a un grupo de roles, vea [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md).


> [!NOTE]
> A pesar de que puede cambiar los roles que se asignan a los grupos de roles integrados, se recomienda copiar los grupos de roles integrados, modificar la copia del grupo de roles y, a continuación, agregar los miembros a la copia del grupo de roles.



Volver al principio

## Trabajar con directivas de asignación de roles

Para administrar los permisos que concede a los usuarios finales para administrar su propio buzón de correo en Exchange 2013, se recomienda utilizar el EAC. Si usa el EAC para administrar los permisos de usuario final, puede agregar roles, quitar roles y crear directivas de asignación de roles con unos pocos clics. El EAC proporciona cuadros de diálogo sencillos, como el cuadro de diálogo **Directiva de asignación de roles**, que se muestra en la figura siguiente, para realizar estas tareas.

**Cuadro de diálogo Directiva de asignación de roles en el EAC**

![Cuadro de diálogo Directiva de asignación de roles en el EAC](images/Dd351175.ecdf3cd4-d50e-4014-95f8-1bd5dafacaff(EXCHG.150).jpg "Cuadro de diálogo Directiva de asignación de roles en el EAC")

Exchange 2013 incluye una directiva de asignación de roles denominada Directiva de asignación de roles predeterminada. Esta directiva de asignación de roles permite a los usuarios cuyos buzones de correo estén asociados con ella, hacer lo siguiente:

  - Abandonar o unirse a grupos de distribución que permiten a los miembros administrar su propia pertenencia.

  - Ver y modificar configuraciones de buzón básicas en su propio buzón de correo, como reglas de la Bandeja de entrada, comportamiento de la corrección ortográfica, configuración del correo no deseado y dispositivos de Microsoft ActiveSync.

  - Modificar la información de contacto, como la dirección de trabajo y los números telefónicos y del localizador.

  - Crear, modificar o ver la configuración de los mensajes de texto.

  - Ver o modificar la configuración del correo de voz.

  - Ver y modificar sus aplicaciones del catálogo de soluciones.

  - Crear buzones de equipo y conectarlos a listas de Microsoft SharePoint.

Si desea agregar o quitar permisos de la Directiva de asignación de roles predeterminada o de cualquier otra directiva de asignación de roles, puede usar el EAC. El cuadro de diálogo que debe usar es similar al cuadro de diálogo que aparece en la figura anterior. Cuando abra la directiva de asignación de roles en el EAC, active la casilla situada junto a los roles que quiera asignarle o desactive la casilla situada junto a los roles que quiera quitar. El cambio que realice en la directiva de asignación de roles se aplica a todos los buzones de correo que tenga asociados.

Si quiere asignar permisos de usuario final distintos a los diferentes tipos de usuario de la organización, puede crear directivas de asignación de roles. Al crear una directiva de asignación de roles, se ve un cuadro de diálogo parecido al de la figura anterior. Puede especificar un nombre nuevo para la directiva de asignación de roles y luego seleccionar los roles que quiere asignar a la directiva. Después de crear una directiva de asignación de roles, puede asociarla con buzones usando el EAC.

Si quiere cambiar la directiva de asignación de roles predeterminada, hay que usar el Shell. Al cambiar la directiva de asignación de roles predeterminada, todos los buzones que se creen se asociarán a la nueva directiva de asignación de roles predeterminada si todavía no se había especificado ninguna de forma explícita. La directiva de asignación de roles asociada con los buzones existentes no cambia al seleccionar una nueva directiva de asignación de roles predeterminada.


> [!NOTE]
> Si activa la casilla de verificación de un rol con roles secundarios, las casillas de verificación de los roles secundarios también se desactivarán. Si desactiva la casilla de verificación de un rol con roles secundarios, las casillas de verificación de los roles secundarios también se desactivarán.<BR>Para obtener los pasos detallados sobre cómo crear directivas de asignación de roles o realizar cambios en las directivas de asignación de roles existentes, vea los temas siguientes: 
> <UL>
> <LI>
> <P><A href="manage-role-assignment-policies-exchange-2013-help.md">Administrar directivas de asignación de funciones</A></P>
> <LI>
> <P><A href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Cambiar la directiva de asignación en un buzón</A></P></LI></UL>



Volver al principio

## Documentación de permisos

La siguiente tabla contiene vínculos a temas que lo ayudarán a obtener información de los permisos de Exchange 2013 y a administrarlos.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tema</th>
<th>Descripción</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="understanding-role-based-access-control-exchange-2013-help.md">Descripción del control de acceso basado en funciones</a></p></td>
<td><p>Infórmese sobre los componentes que constituyen el RBAC y cómo crear modelos de permisos avanzados si los grupos de roles y los roles de administración no son suficientes.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-multiple-forest-permissions-exchange-2013-help.md">Descripción de permisos de bosques múltiples</a></p></td>
<td><p>Obtenga información acerca de la implementación de permisos de RBAC en organizaciones con bosques cuenta y recursos.</p></td>
</tr>
<tr class="odd">
<td><p><a href="understanding-split-permissions-exchange-2013-help.md">Descripción de los permisos divididos</a></p></td>
<td><p>Obtenga información acerca de la división de Exchange y la administración de la entidad de seguridad mediante RBAC y permisos divididos de Active Directory.</p></td>
</tr>
<tr class="even">
<td><p><a href="understanding-permissions-coexistence-with-exchange-2007-and-exchange-2010-exchange-2013-help.md">Descripción de la coexistencia de permisos en Exchange 2007 y Exchange 2010</a></p></td>
<td><p>Configure permisos para habilitar la administración de Exchange 2013 en organizaciones de Exchange 2007 y Exchange 2010 existentes.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-role-groups-exchange-2013-help.md">Administrar grupos de roles</a></p></td>
<td><p>Configure permisos para los administradores de Exchange y los usuarios especialistas mediante grupos de roles.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-group-members-exchange-2013-help.md">Administrar miembros de grupos de roles</a></p></td>
<td><p>Agregue y quite miembros a grupos de roles. Al agregar y quitar miembros a grupos de roles, se configura quién puede administrar características de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="manage-linked-role-groups-exchange-2013-help.md">Administrar grupos de funciones vinculadas</a></p></td>
<td><p>Configure permisos para los administradores de Exchange y los usuarios especialistas en implementaciones de Exchange de varios bosques.</p></td>
</tr>
<tr class="even">
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Administrar directivas de asignación de funciones</a></p></td>
<td><p>Configure las características a las que tienen acceso los usuarios finales en sus buzones de correo mediante directivas de asignación de roles.</p></td>
</tr>
<tr class="odd">
<td><p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Cambiar la directiva de asignación en un buzón</a></p></td>
<td><p>Configure qué directiva de asignación de roles se aplica a uno o más buzones.</p></td>
</tr>
<tr class="even">
<td><p><a href="create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md">Crear grupos de funciones vinculadas que reflejan grupos de funciones integradas</a></p></td>
<td><p>Recree los grupos de roles integrados como grupos de roles vinculados en implementaciones de Exchange de varios bosques.</p></td>
</tr>
<tr class="odd">
<td><p><a href="view-effective-permissions-exchange-2013-help.md">Ver permisos efectivos</a></p></td>
<td><p>Vea quién tiene permisos para administrar las características de Exchange.</p></td>
</tr>
<tr class="even">
<td><p><a href="feature-permissions-exchange-2013-help.md">Permisos de características</a></p></td>
<td><p>Obtenga más información acerca de los permisos necesarios para administrar servicios y características de Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><a href="advanced-permissions-exchange-2013-help.md">Permisos avanzados</a></p></td>
<td><p>Use características avanzadas de RBAC para crear modelos de permisos sumamente personalizados a fin de satisfacer las necesidades de cualquier organización.</p></td>
</tr>
</tbody>
</table>

