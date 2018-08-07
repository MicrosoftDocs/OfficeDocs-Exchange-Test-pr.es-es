---
title: 'Descripción de la coexistencia de permisos en Exchange 2007 y Exchange 2010'
TOCTitle: Descripción de la coexistencia de permisos en Exchange 2007 y Exchange 2010
ms:assetid: 28ab1433-23ee-4914-8f21-9a32578792e5
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335157(v=EXCHG.150)
ms:contentKeyID: 54914900
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de la coexistencia de permisos en Exchange 2007 y Exchange 2010

 

_**Se aplica a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Al instalar Microsoft Exchange Server 2013 en una organización existente de Microsoft Exchange Server 2010 o Microsoft Exchange Server 2007, debe saber cómo funcionarán los permisos en la nueva organización. Lea la sección que se refiera a su organización.

  - Instalar Exchange 2013 en organizaciones de Exchange 2010 existentes

  - Instalar Exchange 2013 en organizaciones de Exchange 2007 existentes

## Instalar Exchange 2013 en organizaciones de Exchange 2010 existentes

Exchange 2013 usa el modelo de permisos Control de acceso basado en roles (RBAC) empleado en Exchange 2010. Al instalar Exchange 2013 en una organización de Exchange 2010 existente, se aplican los mismos grupos de roles de administración, roles de administración y ámbitos de administración a los servidores y destinatarios de Exchange 2013 y de Exchange 2010. Los miembros de los grupos de administración, o los usuarios asignados a los roles, pueden administrar cualquier servidor o destinatario de Exchange 2013 o Exchange 2013 incluido en el ámbito del rol o grupo de roles. Si no usa ámbitos en la organización y quiere que los miembros de los grupos de roles existentes administren los servidores y destinatarios de Exchange 2010 y Exchange 2013, no tiene que hacer nada más. Estos administradores podrán administrar los servidores y destinatarios de Exchange 2010 que estén agregados en la organización. Para recordar cómo funcionan los permisos en Exchange 2010 y Exchange 2013, vea [Permisos](permissions-exchange-2013-help.md).

En la organización nueva, es posible que quiera separar la administración de los servidores y destinatarios de Exchange 2010 y de Exchange 2013. Es posible que el grupo de administradores encargados de administrar los servidores y destinatarios de Exchange 2010 no tenga permiso para administrar los de Exchange 2013 y viceversa. En este caso, puede usar ámbitos de administración para definir los servidores y destinatarios que cada grupo de administradores podrá administrar. Después de crear los ámbitos que quiera, puede copiar grupos de roles existentes, agregar a los administradores que deben pertenecer a cada grupo y agregar los ámbitos a estos grupos de roles. Cuando acabe, los miembros de cada grupo de roles solo podrán administrar los servidores y destinatarios que coincidan con sus respectivos ámbitos.

Para más información sobre grupos de roles, ámbitos, copiar grupos de roles y agregar ámbitos a los grupos de roles, vea los temas siguientes:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md)

  - [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md)

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

## Instalar Exchange 2013 en organizaciones de Exchange 2007 existentes

Exchange 2013 incluye los permisos Control de acceso basado en roles (RBAC) que sustituye al modelo de autorización basado en la entrada de control de acceso (ACE) de Active Directory usado en Microsoft Exchange Server 2007. RBAC es el mecanismo de autorización usado para la mayor parte de la administración de Exchange 2013. Este mecanismo incluye las siguientes áreas de administración:

  - Shell de administración de Exchange

  - Centro de administración de Exchange (EAC)

  - Servicios Web Exchange

Para más información sobre cómo planear la coexistencia entre Exchange 2013 y Exchange 2007, vea [Actualizar de Exchange 2007 a Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md).

¿Está buscando las tareas de administración relacionadas con permisos? Vea [Permisos](permissions-exchange-2013-help.md).

## Permisos de Exchange 2013

El modelo de permisos RBAC de Exchange 2013 consta de grupos de roles de administración a los que se asigna uno de varios roles de administración. Estos roles contienen permisos que habilitan a los administradores para realizar tareas en la organización de Exchange. Los administradores se agregan como miembros de los grupos de roles y reciben todos los permisos que conceden los roles. La siguiente tabla proporciona un ejemplo de los grupos de roles, algunos de los roles asignados a dichos grupos y una descripción del tipo de usuario que puede formar parte del grupo de roles.

### Ejemplos de grupos de roles y roles de Exchange 2013

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupo de roles de administración</th>
<th>Roles de administración</th>
<th>Miembros de este grupo de roles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administración de la organización</p></td>
<td><p>Estos son algunos de los roles asignados a este grupo:</p>
<ul>
<li><p>Listas de direcciones</p></li>
<li><p>Servidores de Exchange</p></li>
<li><p>Registro en diario</p></li>
<li><p>Mail Recipients</p></li>
<li><p>Carpetas públicas</p></li>
</ul></td>
<td><p>Los usuarios que administran toda la organización de Exchange 2013 deben ser miembros de este grupo de roles. Con algunas excepciones, los miembros de este grupo de roles pueden administrar casi cualquier aspecto de la organización Exchange 2013.</p>
<p>De forma predeterminada, la cuenta de usuario usada para preparar Active Directory para Exchange 2013 pertenece a este grupo de roles.</p>
<p>Para obtener más información sobre este grupo de roles y para ver una lista completa de los roles asignados, consulte <a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a>.</p></td>
</tr>
<tr class="even">
<td><p>Ver solamente la administración de la organización</p></td>
<td><p>Estos son los roles asignados a este grupo:</p>
<ul>
<li><p>Supervisión</p></li>
<li><p>Configuración con permiso de vista</p></li>
<li><p>Destinatarios con permiso de vista</p></li>
</ul></td>
<td><p>Los usuarios que ven la configuración de toda la organización de Exchange 2013 deben ser miembros de este grupo de roles. Esos usuarios deben poder ver la configuración del servidor y la información del destinatario y ejecutar funciones de supervisión sin cambiar la configuración de la organización o de los destinatarios.</p>
<p>Para obtener más información acerca de este grupo de roles, consulte <a href="view-only-organization-management-exchange-2013-help.md">Administración de organización de solo lectura</a></p></td>
</tr>
<tr class="odd">
<td><p>Recipient Management</p></td>
<td><p>Estos son los roles asignados a este grupo:</p>
<ul>
<li><p>Grupos de distribución</p></li>
<li><p>Carpetas públicas habilitadas para correo</p></li>
<li><p>Creación de destinatario de correo</p></li>
<li><p>Destinatarios de correo</p></li>
<li><p>Seguimiento de mensajes</p></li>
<li><p>Migración</p></li>
<li><p>Mover buzones</p></li>
<li><p>Directivas de destinatarios</p></li>
</ul></td>
<td><p>Los usuarios que administran destinatarios, como buzones, contactos y grupos de distribución, en la organización de Exchange 2013, deben ser miembros de este grupo de roles. Esos usuarios pueden crear destinatarios, modificar o borrar los destinatarios existentes o mover buzones.</p>
<p>Para obtener más información sobre este grupo de roles y para ver una lista completa de los roles asignados, consulte <a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a>.</p></td>
</tr>
<tr class="even">
<td><p>Administración de servidor</p></td>
<td><p>Estos son algunos de los roles asignados a este grupo:</p>
<ul>
<li><p>Bases de datos</p></li>
<li><p>Conectores de Exchange</p></li>
<li><p>Servidores de Exchange</p></li>
<li><p>Conectores de recepción</p></li>
<li><p>Colas de transporte</p></li>
</ul></td>
<td><p>Los usuarios que administran la configuración del servidor de Exchange, como conectores de recepción, certificados, bases de datos y directorios virtuales, deben ser miembros de este grupo de roles. Estos usuarios pueden modificar la configuración del servidor de Exchange, crear bases de datos y reiniciar y manipular colas de transporte.</p>
<p>Para obtener más información sobre este grupo de roles y para ver una lista completa de los roles asignados, consulte <a href="server-management-exchange-2013-help.md">Administración de servidor</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Discovery Management</p></td>
<td><p>Estos son los roles asignados a este grupo:</p>
<ul>
<li><p>Retención legal</p></li>
<li><p>Búsqueda en el buzón</p></li>
</ul></td>
<td><p>Los usuarios que realizan búsquedas en buzones para permitir procedimientos legales o para configurar retenciones legales deben ser miembros de este grupo de roles.</p>
<p>Este es un ejemplo de grupo de roles que puede incluir usuarios que no sean administradores de Exchange, como el personal del departamento legal. El personal del departamento legal puede llevar a cabo sus tareas sin la intervención de los administradores de Exchange.</p>
<p>Para obtener más información sobre este grupo de roles y para ver una lista completa de los roles asignados, consulte <a href="discovery-management-exchange-2013-help.md">Administración de la detección</a>.</p></td>
</tr>
</tbody>
</table>


Esta tabla muestra que Exchange 2013 ofrece un nivel granular de control sobre los permisos concedidos a los administradores. Puede elegir entre 12 grupos de roles en Exchange 2013. Si desea una lista completa de los grupos de roles y los permisos que proporcionan, consulte [Grupos de funciones integradas](built-in-role-groups-exchange-2013-help.md).

Como Exchange 2013 ofrece muchos grupos de roles y debido a que es posible personalizarlo más creando grupos que tengan combinaciones de roles diferentes, no es necesario manipular listas de control de acceso (ACL) en los objetos de Active Directory; esto no surte ningún efecto. Las ACL ya no se usan para aplicar permisos a administradores individuales o grupos de Exchange 2013. Todas las tareas, como un administrador que crea un buzón o un usuario que tiene acceso a un buzón, se administran mediante RBAC. RBAC autoriza la tarea y, a continuación, Exchange realiza la tarea en nombre del usuario, si está permitida. Exchange realiza la tarea del grupo de seguridad universal (USG) del subsistema de confianza de Exchange. Con algunas excepciones, todas las ACL de objetos de Active Directory a las que Exchange 2010 tiene que obtener acceso se conceden al USG del subsistema de confianza de Exchange. Se trata de un cambio fundamental respecto a cómo se controlan los permisos en Exchange 2007.

Los permisos concedidos a un usuario en Active Directory son independientes de los que le concede el RBAC cuando el usuario usa las herramientas de administración de Exchange 2013.

Para obtener más información acerca de RBAC, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

## Permisos de Exchange 2007

El modelo administrativo de Exchange 2007 aprovecha los bosques de Active Directory para definir límites de seguridad. No existe aislamiento de los permisos de seguridad dentro un bosque concreto. Los propietarios del bosque y los administradores de la empresa siempre pueden tener acceso a todos los recursos de cualquier dominio. En Exchange 2007, es posible que deba otorgar derechos de administrador de empresa y de administrador de dominio de nivel superior, únicamente de manera temporaria.

Exchange 2007 proporciona los siguientes roles de administrador predefinidos:

  - **Rol de administrador de la organización de Exchange**   Este rol otorga permisos para controlar todos los aspectos de la organización de Exchange 2007. Además, un administrador con este rol puede otorgar permisos a otros administradores de Exchange. Este rol se otorga a la cuenta que se usa para instalar Exchange 2007.

  - **Rol Administrador de Exchange con permiso de vista**   Este rol concede permiso a un administrador de la configuración de Exchange. No obstante, un administrador con este rol no puede modificar objetos de la organización de Exchange 2007.

  - **Rol de administrador de destinatarios de Exchange**   Este rol otorga permisos para administrar destinatarios de correo electrónico. Un administrador con este rol puede modificar elementos relacionados con Exchange para usuarios, grupos, contactos y grupos de distribución.

  - **Rol de administrador de servidor de Exchange**   Este rol otorga permisos para administrar un servidor específico. No obstante, este rol no otorga permisos para realizar acciones que tengan un impacto global sobre la organización de Exchange 2007.

  - **Rol Administrador de carpetas públicas de Exchange**   Este rol se agregó en el Service Pack 1 de Exchange 2007**.** Este rol otorga permisos para administrar carpetas públicas en la organización de Exchange 2007.

Este modelo de permisos emplea grupos de seguridad universal para todos los roles, salvo para el rol Administrador de Exchange Server. Cuando se ejecuta el comando **Setup /PrepareAD** de Exchange 2007, el programa de instalación crea grupos de seguridad universal en el dominio raíz y les da un ámbito de bosque a los grupos de seguridad universal. A los USG se les asigna ACL para que administren objetos de Exchange en todo Active Directory.

En Exchange 2007, puede separar a los administradores asignándoles diversos roles. Los permisos se asignan directamente al usuario o al USG al que pertenece. Las acciones realizadas por el usuario se llevan a cabo en el contexto de su cuenta de Active Directory. En la siguiente tabla, se enumeran los roles de administrador de Exchange 2007, junto con sus permisos de Exchange relacionados.

### Roles de administrador de Exchange 2007

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de administrador</th>
<th>Miembros</th>
<th>Miembro de</th>
<th>Permisos de Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrador de organización de Exchange</p></td>
<td><p>La cuenta de administrador o la cuenta que se ha utilizado para instalar el primer servidor de Exchange 2007.</p></td>
<td><p>Administrador de destinatarios de Exchange</p>
<p>Grupo local de administradores de <em>&lt;nombre de servidor&gt;</em></p></td>
<td><p>Control completo del contenedor de Microsoft Exchange en Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Administrador con permiso de vista de Exchange</p></td>
<td><p>Administradores de destinatarios de Exchange</p>
<p>Administradores de servidores de Exchange (<em>&lt;nombre de servidor</em>&gt;)</p></td>
<td><p>Administradores de destinatarios de Exchange</p>
<p>Administradores de servidores de Exchange</p></td>
<td><p>Permiso de lectura en el contenedor de Microsoft Exchange en Active Directory.</p>
<p>Permiso de lectura en todos los dominios de Windows que tienen destinatarios de Exchange</p></td>
</tr>
<tr class="odd">
<td><p>Administrador de destinatarios de Exchange</p></td>
<td><p>Administradores de organización de Exchange</p></td>
<td><p>Administradores de Exchange con permiso de vista</p></td>
<td><p>Control completo de las propiedades de Exchange en los objetos de usuario de Active Directory</p></td>
</tr>
<tr class="even">
<td><p>Administrador de Exchange Server</p></td>
<td><p>Administradores de la organización de Exchange</p></td>
<td><p>Administradores de Exchange con permiso de vista</p>
<p>Grupo local de administradores de <em>&lt;nombre de servidor</em>&gt;</p></td>
<td><p>Control completo de Exchange <em>&lt;nombre de servidor</em>&gt;</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>Cada cuenta de equipo de Exchange 2007</p></td>
<td><p>Administradores de Exchange con permiso de vista</p></td>
<td><p>Especial</p></td>
</tr>
<tr class="even">
<td><p>Administrador de carpeta pública de Exchange</p></td>
<td><p>Administradores de la organización de Exchange</p></td>
<td><p>Administradores de Exchange con permiso de vista</p></td>
<td><p>Control completo para administrar todas las carpetas públicas (se otorgó el derecho extendido Crear carpeta pública de nivel superior)</p></td>
</tr>
</tbody>
</table>


Si necesita realizar más asignaciones de permisos granulares, puede modificar las ACL de objetos individuales de Exchange 2007, como listas de direcciones o bases de datos. Debe agregar el usuario o el grupo de seguridad al que pertenece el usuario directamente a la ACL. A continuación, las acciones se realizan en el contexto de cada usuario.

Para más información sobre cómo administrar permisos en Exchange 2007 vea [Configurar permisos en Exchange Server 2007](http://go.microsoft.com/fwlink/p/?linkid=90671).

## Permisos de coexistencia de Exchange 2013 y Exchange 2007

Dado que el modelo de permisos de Exchange 2013 difiere del de Exchange 2007, las asignaciones de permisos de Exchange 2013 son independientes de las asignaciones de permisos de Exchange 2007. Esto es así aunque ambas versiones de Exchange estén instaladas en el mismo bosque. Sin una configuración adicional, los administradores de Exchange 2013 no tienen los permisos necesarios para administrar los servidores basados en Exchange 2007 ni los administradores de Exchange 2007 tienen los permisos necesarios para administrar los servidores basados en Exchange 2013. Debe hacerse las siguientes preguntas:

  - ¿Quiere conceder a los administradores de Exchange 2013 acceso para administrar servidores de Exchange 2007?

  - ¿Quiere conceder a los administradores de Exchange 2007 acceso para administrar servidores de Exchange 2013?

  - ¿Quiere personalizar los permisos de Exchange 2013 para que coincidan con todas las personalizaciones realizadas en las ACL de Exchange 2007?

## Conceder permisos de Exchange 2010 a los administradores de Exchange 2013

Si quiere que los administradores de Exchange 2007 administren los servidores de Exchange 2013, debe agregar a los administradores de Exchange 2007 a uno o más grupos de roles de Exchange 2013. Puede agregar usuarios o USG a grupos de roles. Los permisos concedidos a los grupos de roles se aplican a los usuarios o a los USG que agregue como miembros.


> [!IMPORTANT]
> Si usa grupos de seguridad de Active Directory locales o globales, debe convertirlos en USG para agregarlos como miembros de un grupo de roles de Exchange&nbsp;2013. Exchange&nbsp;2013 solo admite USG.



En la siguiente tabla se describen las correspondencias entre los roles de administradores de Exchange 2007 y los grupos de roles de Exchange 2013.

### Roles de administradores de Exchange 2007 y grupos de roles de Exchange 2010

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de administrador de Exchange 2007</th>
<th>Grupo de roles de Exchange 2013</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administrador de la organización de Exchange</p></td>
<td><p>Administración de la organización</p></td>
</tr>
<tr class="even">
<td><p>Administrador de destinatarios de Exchange</p></td>
<td><p>Recipient Management</p></td>
</tr>
<tr class="odd">
<td><p>Administrador de Exchange Server</p></td>
<td><p>Administración de servidores</p></td>
</tr>
<tr class="even">
<td><p>Administrador de Exchange con permiso de vista</p></td>
<td><p>Ver solamente la administración de la organización</p></td>
</tr>
<tr class="odd">
<td><p>Exchange Server</p></td>
<td><p>No hay ningún grupo de roles equivalente en Exchange 2013.</p>
<p>(Para más información sobre cómo crear grupos de roles personalizados, vea <a href="manage-role-groups-exchange-2013-help.md">Administrar grupos de roles</a>).</p></td>
</tr>
<tr class="even">
<td><p>Administrador de carpetas públicas de Exchange</p></td>
<td><p>Administración de carpetas públicas</p></td>
</tr>
</tbody>
</table>


Si todos los administradores de Exchange 2007 son miembros de uno de los tres roles administrativos de Exchange 2007, podrá agregar a los miembros de cada uno de los grupos administrativos al grupo de roles de Exchange 2013 equivalente. Por ejemplo, si quiere dar a todos los administradores de la organización de Exchange 2007 acceso total a los objetos de Exchange 2013, agregue el grupo de seguridad universal Administradores de la organización de Exchange al grupo de roles Administración de la organización.

Para más información sobre cómo agregar usuarios y grupos de seguridad universal a grupos de roles, vea [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

Si modifica las ACL de los objetos de Exchange 2007 para conceder permisos más granulares a los administradores de Exchange 2007 y quiere asignar permisos similares en los servidores de Exchange 2013 a esos administradores, siga estos pasos:

1.  Revise las personalizaciones de ACL que se han realizado a los objetos de Exchange 2007 y ubique los administradores a los que se les concedieron permisos para cada objeto.

2.  Asigne una categoría a cada objeto de Exchange 2007. Por ejemplo, determine si el objeto es una base de datos, un servidor o un objeto de destinatario.

3.  Asigne los objetos al grupo de roles de Exchange 2013 correspondiente. Para obtener una lista de grupos de roles integrados, consulte [Grupos de funciones integradas](built-in-role-groups-exchange-2013-help.md).

4.  Agregue los USG o los usuarios de cada tipo de objeto a los grupos de roles de Exchange 2013 correspondientes. Para más información sobre cómo agregar usuarios y grupos de seguridad universal a grupos de roles, vea [Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md).

Después de completar estos pasos, los administradores de Exchange 2007 serán miembros del grupo de roles específico que está asignado a los objetos de Exchange 2013 correspondientes. Ahora, los administradores de Exchange 2007 podrán usar las herramientas de administración de Exchange 2013 para administrar los servidores y destinatarios de Exchange 2013.


> [!IMPORTANT]
> En general, los servidores y destinatarios de Exchange 2007 deben administrarse con herramientas de administración de Exchange 2007 y los de Exchange&nbsp;2013, con las herramientas de administración de Exchange&nbsp;2013.



Si los grupos de roles integrados no proporcionan el conjunto de permisos que desea conceder a determinados administradores, puede crear grupos de roles personalizados. Cuando crea un grupo de roles personalizado puede seleccionar qué roles agregarle. Puede definir las características específicas que desea que administren los miembros del grupo. Por ejemplo, si quiere que los administradores administren sólo grupos de distribución, puede crear un grupo de roles personalizado y elegir solo el rol Grupos de distribución. Después de hacerlo, los miembros de dicho grupo de roles personalizado podrán administrar solamente los grupos de distribución. Para más información sobre cómo crear grupos de roles personalizados, vea [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md).

Si asigna permisos selectivos a determinados objetos de Exchange 2007 (como, por ejemplo, permitir que los administradores administren solo bases de datos específicas) y quiere aplicar la misma configuración a los servidores de Exchange 2013, vea "Volver a crear la personalización de ACL de Exchange 2007 usando ámbitos de administración de Exchange 2013", más adelante en este tema.

## Conceder permisos de Exchange 2007 a los administradores de Exchange 2013

Si quiere que los administradores de Exchange 2013 administren servidores de Exchange 2007, agregue a los administradores de Exchange 2013 a los grupos de seguridad universal o al grupo de seguridad que se corresponda con el rol de administrador de Exchange 2007. De manera alternativa, si personalizó la configuración de ACL, agregue los administradores a las ACL correspondientes. Los grupos de roles son los grupos de seguridad universal, por lo que los grupos de roles pueden agregarse directamente a los USG del rol de administrador de Exchange 2007.

Cuando lo haga, los administradores de Exchange 2013 serán miembros del rol o los roles de administrador de Exchange 2007 correspondientes. Ahora, los administradores de Exchange 2013 podrán usar las herramientas de administración de Exchange 2007 para administrar los servidores y destinatarios de Exchange 2007.

## Volver a crear la personalización de ACL de Exchange 2007 usando ámbitos de administración de Exchange 2013

En Exchange 2007, cuando quiere limitar quién puede administrar un almacén de buzones específico, administrar usuarios específicos o controlar en qué almacén se crean los buzones, tiene que modificar las ACL de los objetos que quiere restringir. Exchange 2013 ofrece las mismas capacidades, pero sin tener que modificar las ACL. Para eso utiliza los ámbitos de administración, que son un componente de RBAC.

Los ámbitos de administración permiten usar ámbitos integrados y personalizados para definir los objetos que pueden administrar los administradores. Aplicando ámbitos de administración, es posible definir qué destinatarios se administran, en qué bases de datos pueden crearse buzones y qué destinatarios o servidores debe administrar exclusivamente un pequeño grupo de administradores.

Puede crear los siguientes tipos de ámbitos de administración:

  - **Relativos predefinidos**Exchange 2013 incluye ámbitos relativos predefinidos. Permiten controlar lo que un usuario ve y modifica. Por ejemplo, los ámbitos relativos predefinidos pueden controlar si los usuarios ven solo su propia información o información sobre toda la organización.

  - **Destinatario**   Los ámbitos de destinatarios controlan los destinatarios que un administrador puede crear, modificar o eliminar. Estas selecciones pueden basarse en una unidad organizativa (OU), en un filtro de destinatarios o en ambos. Los filtros de destinatarios especifican los criterios que un destinatario debe cumplir para estar incluido en el ámbito. Por ejemplo, podría crear un ámbito de filtro de destinatarios que incluye a todos los usuarios de una ubicación determinada o de un departamento específico. También podría combinar filtros de OU y destinatarios para que devuelva solo los usuarios de una OU específica que trabajan para un jefe concreto.

  - **Servidor**   Los ámbitos del servidor controlan qué servidores puede administrar un administrador. Puede especificar listas de servidores o filtros de servidores. En el caso de las listas, se define una lista estática de servidores que pueden administrarse. Los filtros de servidor funcionan igual que los de destinatario: se especifican criterios que deben cumplirse. Por ejemplo, podría crear un ámbito de servidor que coincida con todos los servidores de un sitio de Active Directory particular.

  - **Base de datos**   Los ámbitos de base de datos controlan qué bases de datos puede administrar un administrador. También controlan en qué bases de datos es posible crear buzones o a cuáles bases de datos pueden moverse los buzones. Al igual que los ámbitos del servidor, se pueden definir como listas o como filtros. Por ejemplo, podría crear una lista o un filtro que permita a los administradores crear buzones en bases de datos de buzones administradas por una subsidiaria específica o mover buzones a ella.

  - **Exclusivos**   Los ámbitos de destinatarios, servidor o base de datos también pueden crearse como ámbitos exclusivos. Los ámbitos exclusivos funcionan de la misma manera que las ACE de denegación en las ACL. Si algo coincide con un ámbito exclusivo, sólo los administradores asignados al ámbito exclusivo pueden administrar el objeto. Esto es así incluso si el mismo objeto coincide con otro ámbito que no sea exclusivo. Esto es especialmente útil cuando se desea que solo un pequeño grupo de personas de confianza puedan administrar el buzón de un ejecutivo. Aunque haya otro ámbito normal de destinatarios más amplio que incluya el buzón del ejecutivo, los administradores asignados al ámbito más amplio no podrán administrar el buzón de ese ejecutivo a no ser que tengan asignado también el ámbito exclusivo.

Los ámbitos de administración se usan con roles de administración, asignaciones de roles de administración y grupos de roles de administración para controlar qué objetos puede administrar cada persona y de qué manera puede hacerlo. Para obtener más información al respecto, consulte los temas siguientes:

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

  - [Descripción de ámbitos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

  - [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md)

  - [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md)

Para crear el mismo modelo de permisos en Exchange 2013 usando ámbitos de administración que ha definido con ACL personalizadas, debe realizar un inventario de las ACL que haya personalizado y luego crear ámbitos de administración coincidentes. Puede utilizar las propiedades que se filtran y estén disponibles en objetos de destinatario, servidor y base de datos para crear ámbitos de administración que incluyan los objetos a los que desee que cada ámbito de administración controle el acceso. Para obtener más información acerca de las propiedades que desea usar con los filtros de ámbitos de administración, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

Para obtener más información acerca de cómo crear ámbitos de administración, consulte [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

