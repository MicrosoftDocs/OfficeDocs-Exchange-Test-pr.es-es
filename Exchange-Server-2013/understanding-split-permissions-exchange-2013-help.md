---
title: 'Descripción de los permisos divididos: Exchange 2013 Help'
TOCTitle: Descripción de los permisos divididos
ms:assetid: 2b709e15-63a2-4841-94bc-b289b71166d0
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638106(v=EXCHG.150)
ms:contentKeyID: 49895536
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de los permisos divididos

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Las organizaciones que separan la administración de los objetos de Microsoft Exchange Server 2013 y los objetos de Active Directory usan un modelo denominado *permisos divididos*. Los permisos divididos permiten a las organizaciones asignar permisos específicos y tareas relacionadas a grupos específicos dentro de la organización. Esta separación de tareas ayuda a mantener estándares y flujos de trabajo, y a controlar los cambios en la organización.

El nivel más alto de permisos divididos es la separación de la administración de Exchange y la administración de Active Directory. Muchas organizaciones cuentan con dos grupos: administradores que administran la infraestructura de Exchange de la organización, incluidos servidores y destinatarios, y administradores que administran la infraestructura de Active Directory. Esta separación es importante para muchas organizaciones dado que la infraestructura de Active Directory suele abarcar muchas ubicaciones, dominios, servicios, aplicaciones e incluso bosques de Active Directory. Los administradores de Active Directory deben asegurarse de que los cambios que se realizan a Active Directory no afecten negativamente a ninguno de los demás servicios. En consecuencia, generalmente se permite solo a un pequeño grupo de administradores administrar dicha infraestructura.

Al mismo tiempo, la infraestructura de Exchange, incluidos servidores y destinatarios, también puede ser compleja y puede requerir conocimiento especializado. Además, Exchange almacena información extremadamente confidencial sobre el negocio de la organización. Los administradores de Exchange podrían obtener acceso a esta información. Al limitar la cantidad de administradores de Exchange, la organización limita quién puede realizar cambios a la configuración de Exchange y quién puede tener acceso a la información confidencial.

Por lo general, los permisos divididos hacen una distinción entre la creación de entidades de seguridad en Active Directory, por ejemplo, usuarios y grupos de seguridad, y la posterior configuración de dichos objetos. Esto ayuda a reducir la posibilidad del acceso no autorizado a la red al controlar quién puede crear objetos que concedan acceso a ella. En la mayoría de los casos, solo los administradores de Active Directory pueden crear entidades de seguridad, mientras que otros administradores, como los administradores de Exchange, pueden administrar atributos específicos en objetos de Active Directory existentes.

A fin de admitir las necesidades cambiantes para separar la administración de Exchange y Active Directory, Exchange 2013 permite elegir si desea tener un modelo de permisos compartidos o un modelo de permisos divididos. Exchange 2013 ofrece dos tipos de modelos de permisos divididos: RBAC y Active Directory. Valores predeterminados de Exchange 2013 para un modelo de permisos compartidos.

**Contenido**

Explicación del control de acceso basado en roles y Active Directory

Permisos compartidos

Permisos divididos

Permisos divididos RBAC

Permisos divididos de Active Directory

## Explicación del control de acceso basado en roles y Active Directory


Para comprender los permisos divididos, debe comprender la forma en que el modelo de permisos de control de acceso basado en roles (RBAC) de Exchange 2013 funciona con Active Directory. El modelo RBAC controla quién puede realizar determinadas acciones y sobre qué objetos se pueden realizar dichas acciones. Para obtener más información acerca de los diversos componentes de RBAC tratados en este tema, vea [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

En Exchange 2013, todas las tareas que se realizan en los objetos de Exchange se deben llevar a cabo a través del Shell de administración de Exchange o la interfaz del Centro de administración (EAC) de Exchange. Ambas herramientas de administración usan RBAC para autorizar todas las tareas que se realizan.

RBAC es un componente que existe en todos los servidores que ejecutan Exchange 2013. RBAC comprueba si el usuario que realiza una acción está autorizado para realizarla:

  - Si el usuario no está autorizado para realizar la acción, RBAC no permite continuar con la acción.

  - Si el usuario está autorizado para realizar la acción, RBAC comprueba si el usuario está autorizado para realizar la acción respecto del objeto específico que se solicita:
    
      - Si el usuario está autorizado, RBAC permite continuar con la acción.
    
      - Si el usuario no está autorizado, RBAC no permite continuar con la acción.

Si RBAC permite continuar con la acción, esta se realiza en el contexto del Subsistema de confianza de Exchange y no en el contexto del usuario. El Subsistema de confianza de Exchange es un grupo de seguridad universal con privilegios elevados (USG) que dispone de acceso de lectura y escritura a todos los objetos relacionados con Exchange de la organización de Exchange. También es miembro del grupo de seguridad local Administradores y del grupo de seguridad universal de permisos de Windows de Exchange, que permite a Exchange crear y administrar objetos de Active Directory.


> [!WARNING]
> No realice cambios manuales a la pertenencia del grupo de seguridad del subsistema de confianza de Exchange. Tampoco agregue ni quite el grupo de listas de control de acceso de objetos (ACL). Si realiza cambios en el USG del subsistema de confianza de Exchange por su cuenta, podría causar daños irreparables a la organización de Exchange.



Es importante comprender que no importan los permisos de Active Directory que tenga un usuario al usar las herramientas de administración de Exchange. Si el usuario está autorizado, a través de RBAC, para realizar una acción con las herramientas de administración de Exchange, puede realizar la acción independientemente de los permisos de Active Directory que tenga. Al contrario, si un usuario es un administrador de la organización de Active Directory pero no está autorizado para realizar una acción (por ejemplo, crear un buzón de correo) con las herramientas de administración de Exchange, la acción no se realizará correctamente porque el usuario no dispone de los permisos necesarios de acuerdo con RBAC.


> [!IMPORTANT]
> Si bien el modelo de permisos RBAC no se aplica a la herramienta de administración Usuarios y equipos de Active Directory, los usuarios y equipos de Active Directory no pueden administrar la configuración de Exchange. Por ello, a pesar de que un usuario puede tener acceso para modificar algunos atributos en los objetos de Active Directory, como el nombre para mostrar de un usuario, el usuario debe usar las herramientas de administración de Exchange y, por lo tanto, debe tener la autorización de RBAC para administrar los atributos de Exchange.



Volver al principio

## Permisos compartidos

El modelo de permisos compartidos es el modelo predeterminado de Exchange 2013. No es necesario cambiar nada si este es el modelo de permisos que quiere usar. Este modelo no separa la administración de los objetos de Exchange y de Active Directory dentro de las herramientas de administración de Exchange. Permite a los administradores que usan las herramientas de administración de Exchange crear entidades de seguridad en Active Directory.

En la tabla siguiente se muestran los roles que permiten crear entidades de seguridad en Exchange y los grupos de roles de administración a los que están asignadas de forma predeterminada.

### Roles de administración de entidades de seguridad

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de administración</th>
<th>Grupo de roles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Rol Creación de destinatarios de correo</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Rol Pertenencia y Creación de grupos de seguridad</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
</tbody>
</table>


Solo los grupos de roles, usuarios o USG que tienen asignado el rol creación de destinatarios de correo pueden crear entidades de seguridad tales como usuarios de Active Directory. De manera predeterminada, la Administración de la organización y la Recipient Management se asignan a grupos funciones de esta función. Por lo tanto, los miembros de estos grupos de roles pueden crear entidades de seguridad.

Solo los grupos de roles, usuarios o USG que tienen asignado el rol Pertenencia y creación de grupos de seguridad pueden crear grupos de seguridad o administrar su pertenencia a los grupos. De manera predeterminada, solo se asigna esta función al grupo de funciones de Administración de la organización. Por lo tanto, solo los miembros del grupo de roles de Administración de la organización pueden crear o administrar la pertenencia a grupos de seguridad.

Puede asignar el rol creación de destinatarios de correo y el rol Pertenencia y creación de grupos de seguridad a otros grupos de roles, usuarios o USG si desea que otros usuarios puedan crear entidades de seguridad.

Para permitir la administración de entidades de seguridad existentes en Exchange 2013, el rol Destinatarios de correo está asignado a los grupos de funciones Administración de la organización y Recipient Management de manera predeterminada. Solo los grupos de roles, usuarios o USG que tienen asignado el rol Destinatarios de correo pueden administrar entidades de seguridad existentes. Si desea que otros grupos de roles, usuarios o USG puedan administrar entidades de seguridad existentes, debe asignarles el rol Destinatarios de correo.

Para obtener más información acerca de la adición de roles a grupos de roles, usuarios o grupos de seguridad universal, vea estos temas:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Si cambió a un modelo de permisos divididos y desea volver a cambiar a un modelo de permisos compartidos, vea [Configurar Exchange 2013 para permisos compartidos](configure-exchange-2013-for-shared-permissions-exchange-2013-help.md).

Volver al principio

## Permisos divididos

Si la organización separa la administración de Exchange y la administración de Active Directory, debe configurar Exchange de manera que admita el modelo de permisos divididos. Cuando se configura correctamente, solo los administradores que usted desea que creen entidades de seguridad, como los administradores de Active Directory, podrán hacerlo y solo los administradores de Exchange podrán modificar los atributos de Exchange en entidades de seguridad existentes. La división de permisos además se encuentra aproximadamente a lo largo de particiones de dominio y configuración en Active Directory. Las particiones también se denominan contextos de nombres. La partición de dominios almacena los usuarios, los grupos y otros objetos de un dominio específico. La partición de configuración almacena la información de configuración de los servicios de todo el bosque que utilizaron Active Directory, como Exchange. Los datos almacenados en la partición de dominio generalmente son administrados por administradores de Active Directory, aunque los objetos pueden contener atributos específicos de Exchange que pueden administrar los administradores de Exchange. Los datos almacenados en la partición de configuración son administrados por los administradores de cada servicio respectivo que almacena los datos en esta partición. En Exchange, suelen ser los administradores de Exchange.

Exchange 2013 es compatible con los dos siguientes tipos de permisos divididos:

  - **Permisos divididos de RBAC**   Los permisos para crear entidades de seguridad en la partición de dominio de Active Directory se controlan mediante RBAC. Solo pueden crear entidades de seguridad los servidores y servicios de Exchange y los usuarios que sean miembros de los grupos de roles adecuados. 

  - **Permisos divididos de Active Directory**   Los permisos para crear entidades de seguridad en la partición de dominio de Active Directory se quitan completamente de cualquier usuario, servicio o servidor de Exchange. En el RBAC, no se brinda ninguna opción para crear entidades de seguridad. La creación de entidades de seguridad en Active Directory se debe realizar mediante el uso de las herramientas de administración de Active Directory.
    

    > [!IMPORTANT]
    > Aunque los permisos divididos de Active Directory no se pueden habilitar ni deshabilitar ejecutando la instalación en un equipo que tenga Exchange&nbsp;2013 instalado, la configuración de permisos divididos de Active Directory se aplica a los servidores de Exchange&nbsp;2013 y Exchange 2010. Sin embargo, no afecta ningún servidor Exchange Server 2007 de Microsoft.



Si su organización opta por utilizar un modelo de permisos dividido en lugar de permisos compartidos, le recomendamos utilizar el modelo de permisos divididos RBAC. El modelo de permisos divididos de RBAC brinda significativamente mayor flexibilidad mientras proporciona casi la misma separación de administración que los permisos divididos de Active Directory, con la excepción que los servidores y los servicios de Exchange pueden crear entidades de seguridad en el modelo de permisos divididos de RBAC.

Se le pregunta si desea habilitar permisos divididos de Active Directory durante la instalación. Si opta por habilitar permisos divididos de Active Directory, solo podrá cambiar a permisos compartidos o permisos divididos RBAC al ejecutar a instalación y deshabilitar los permisos divididos de Active Directory. Esta elección se aplica a todos los servidores de Exchange 2010 y Exchange 2013 de la organización.

Las siguientes secciones describen el RBAC y los permisos divididos de Active Directory de forma más detallada.

Volver al principio

## Permisos divididos RBAC

El modelo de seguridad de RBAC modifica las asignaciones de roles de administración predeterminadas para diferenciar quién puede crear entidades de seguridad en la partición de dominio de Active Directory de los usuarios que se encargan de administrar los datos de la organización de Exchange en la partición de configuración de Active Directory. Los administradores que sean miembros de los roles creación de destinatarios de correo, creación de grupos de seguridad y pertenencia pueden crear entidades de seguridad, como usuarios con buzones de correo y grupos de distribución. Estos permisos permanecen separados de los permisos necesarios para crear entidades de seguridad fuera de las herramientas de administración de Exchange. Los administradores de Exchange que no tengan asignado el rol creación de destinatarios de correo, creación de grupos de seguridad y pertenencia pueden modificar los atributos relacionados con Exchange en las entidades de seguridad. Los administradores de Active Directory además tienen la opción de usar las herramientas de administración de Exchange para crear entidades de seguridad de Active Directory.

Los servidores de Exchange y el subsistema de confianza de Exchange también tienen permisos para crear entidades de seguridad en Active Directory en nombre de usuarios y programas de terceros que se integran con RBAC.

Los permisos divididos RBAC son una buena elección para su organización si se cumplen las siguientes condiciones:

  - Su organización no necesita que la creación de entidades de seguridad se realice únicamente con la utilización de herramientas de administración de Active Directory y que solo la realicen usuarios a quienes se les asigne permisos de Active Directory específicos.

  - La organización habilita servicios, por ejemplo, servidores de Exchange, para crear entidades de seguridad.

  - Desea simplificar el proceso necesario para la creación de buzones de correo, usuarios habilitados para correo, grupos de distribución y grupos de roles al habilitar la creación desde las herramientas de administración de Exchange.

  - Desea administrar la pertenencia a los grupos de distribución y grupos de roles desde las herramientas de administración de Exchange.

  - Tiene programas de terceros que necesitan que servidores de Exchange puedan crear entidades de seguridad en su nombre.

Si su organización necesita una separación completa de la administración de Exchange y Active Directory, y la administración de Active Directory no se puede llevar a cabo mediante las herramientas de administración de Exchange o mediante servicios de Exchange, vea la sección Permisos divididos de Active Directory más adelante en este tema.

La conmutación de permisos compartidos a permisos divididos RBAC es un proceso manual en el que quitan los permisos necesarios para crear entidades de seguridad de los grupos de funciones asignados de manera predeterminada. En la tabla siguiente se muestran los roles que permiten crear entidades de seguridad en Exchange y los grupos de roles de administración a los que están asignadas de forma predeterminada.

### Roles de administración de entidades de seguridad

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Rol de administración</th>
<th>Grupo de roles</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="mail-recipient-creation-role-exchange-2013-help.md">Rol Creación de destinatarios de correo</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p>
<p><a href="recipient-management-exchange-2013-help.md">Administración de destinatarios</a></p></td>
</tr>
<tr class="even">
<td><p><a href="security-group-creation-and-membership-role-exchange-2013-help.md">Rol Pertenencia y Creación de grupos de seguridad</a></p></td>
<td><p><a href="organization-management-exchange-2013-help.md">Administración de organizaciones</a></p></td>
</tr>
</tbody>
</table>


De forma predeterminada, los miembros de los grupos de funciones Administración de la organización y Recipient Management pueden crear entidades de seguridad. Debe transferir la capacidad para crear entidades de seguridad de los grupos de roles integrados a un nuevo grupo de roles que cree.

Para configurar un permisos divididos RBAC, debe realizar lo siguiente:

1.  Deshabilitar permisos divididos de Active Directory si está habilitado.

2.  Cree un grupo de roles, que contendrá los administradores de Active Directory que podrán crear entidades de seguridad.

3.  Cree asignaciones de roles regulares y de delegación entre el rol creación de destinatarios de correo y el nuevo grupo de roles.

4.  Cree asignaciones de roles regulares y de delegación entre el rol Pertenencia y creación de grupos de seguridad y el nuevo grupo de roles.

5.  Quite las asignaciones de roles de administración regulares y de delegación entre el rol creación de destinatarios de correo y los grupos de funciones Administración de la organización y Recipient Management.

6.  Quite las asignaciones de roles regulares y de delegación entre el rol pertenencia y creación de grupos de seguridad y el grupo de funciones de Administración de la organización.

Después de realizar estas acciones, solo los miembros del nuevo grupo de roles que cree podrán crear entidades de seguridad, tales como buzones de correo. El grupo nuevo solo podrá crear los objetos. No podrá configurar los atributos de Exchange en el nuevo objeto. Un administrador de Active Directory, que es miembro del nuevo grupo, deberá crear el objeto y, a continuación, un administrador de Exchange deberá configurar los atributos de Exchange del objeto. Los administradores de Exchange no podrán usar los cmdlets siguientes:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

No obstante, los administradores de Exchange podrán crear y administrar objetos específicos de Exchange, como reglas de transporte, grupos de distribución, etc. y administrar atributos relacionados con Exchange en cualquier objeto.

Además, las características asociadas en el EAC y Outlook Web App, como el Asistente para buzón nuevo, ya no estarán disponibles o generarán un error si intenta usarlas.

Si desea que el nuevo grupo de roles también pueda administrar los atributos de Exchange del objeto nuevo, también debe asignar el rol Destinatarios de correo al nuevo grupo de roles.

Para obtener más información acerca de la configuración de un modelo de permisos divididos, vea [Configurar Exchange 2013 para permisos divididos](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Volver al principio

## Permisos divididos de Active Directory

En los permisos divididos de Active Directory, la creación de entidades de seguridad en la partición de dominio de Active Directory, como buzones de correo y grupos de distribución, se debe realizar mediante herramientas de administración de Active Directory. Se realizan diversos cambios a los permisos otorgados al subsistema de confianza de Exchange y servidores de Exchange a fin de limitar lo que pueden hacer los administradores y servidores de Exchange. Cuando se habilitan los permisos divididos de Active Directory, se producen los cambios de funcionalidad siguientes:

  - Se quitan la creación de buzones de correo, los usuarios habilitados para correo electrónico, los grupos de distribución y otras entidades de seguridad de las herramientas de administración de Exchange.

  - No se puede agregar ni quitar miembros de grupos de distribución desde las herramientas de administración de Exchange.

  - Se quitan todos los permisos otorgados al subsistema de confianza de Exchange y a los servidores de Exchange para crear entidades de seguridad.

  - Los servidores deExchange y las herramientas de administración de Exchange solo pueden modificar los atributos de Exchange de entidades de seguridad existentes en Active Directory.

Por ejemplo, para crear un buzón de correo con permisos divididos de Active Directory habilitado, primero se deberá crear un usuario con las herramientas de Active Directory y lo deberá realizar un usuario con los permisos de Active Directory necesarios. A continuación, se puede habilitar al usuario para el buzón de correo con las herramientas de administración de Exchange. Solo los atributos relacionados con Exchange del buzón de correo pueden ser modificados por administradores de Exchange con las herramientas de administración de Exchange.

Los permisos divididos de Active Directory son una buena elección para su organización si se cumplen las siguientes condiciones:

  - Su organización necesita que se creen entidades de seguridad mediante la utilización de únicamente herramientas de administración de Active Directory o que solo la realicen usuarios que tengan permisos específicos en Active Directory.

  - Desea separar por completo la posibilidad de crear entidades de seguridad de los usuarios que administran la organización de Exchange.

  - Desea realizar la totalidad de la administración de grupos de distribución, incluida la creación de grupos de distribución y agregar y quitar miembros de esos grupos mediante las herramientas de administración de Active Directory.

  - No desea tener servidores de Exchange ni programas de terceros que usen Exchange en su nombre para crear entidades de seguridad.


> [!IMPORTANT]
> El cambio de permisos divididos de Active Directory es una elección que puede hacer cuando instala Exchange&nbsp;2013 con la utilización del asistente de instalación o con la utilización del parámetro de <EM>ActiveDirectorySplitPermissions</EM> mientras ejecuta <CODE>setup.exe</CODE> en la línea de comandos. Además puede habilitar o deshabilitar los permisos divididos de Active Directory después de haber instalado Exchange&nbsp;2013 al volver a ejecutar <CODE>setup.exe</CODE> en la línea de comandos. Para habilitar los permisos divididos de Active Directory, configure el parámetro <EM>ActiveDirectorySplitPermissions</EM> en <CODE>true</CODE>. Para deshabilitarlo, configúrelo en <CODE>false</CODE>. Siempre debe especificar la conmutación <EM>PrepareAD</EM> junto con el parámetro <EM>ActiveDirectorySplitPermissions</EM>.<BR>Si dispone de varios dominios en el mismo bosque, también debe especificar el modificador <EM>PrepareAllDomains</EM> al aplicar permisos divididos de Active Directory o al ejecutar el programa de instalación con el modificador <EM>PrepareDomain</EM> en cada dominio. Si decide ejecutar el programa de instalación con el modificador <EM>PrepareDomain</EM> en cada dominio, en lugar de usar el modificador <EM>PrepareAllDomains</EM>, tendrá que preparar cada uno de los dominios que contenga servidores de Exchange, objetos habilitados para correo o servidores de catálogo global a los que se puede obtener acceso mediante un servidor de Exchange.




> [!IMPORTANT]
> No puede habilitar permisos divididos de Active Directory si ha instalado Exchange 2010 o Exchange&nbsp;2013 en un controlador de dominio.<BR>Después de habilitar o deshabilitar los permisos divididos de Active Directory, le recomendamos reiniciar los servidores de Exchange 2010 y Exchange&nbsp;2013 de su organización a fin de obligarlos a seleccionar el nuevo token de acceso de Active Directory con los permisos actualizados.



Exchange 2013 obtiene permisos divididos de Active Directory al quitar los permisos y la pertenencia del grupo de seguridad de permisos de ExchangeWindows. En permisos compartidos y en permisos divididos RBAC, este grupo de seguridad obtiene permisos a diversos atributos y objetos no pertenecientes a Exchange en todo Active Directory. Al quitar los permisos y la pertenencia de este grupo de seguridad, se impide a los administradores y a los servicios de Exchange crear o modificar los objetos no pertenecientes a Exchange Active Directory.

Para obtener la lista de cambios que se producen en el grupo de seguridad de permisos de Exchange Windows y otros componentes de Exchange al habilitar o deshabilitar permisos divididos de Active Directory, consulte la tabla siguiente.


> [!NOTE]
> Las asignaciones de roles a los grupos de roles que habilitan a los administradores de Exchange para crear entidades de seguridad se quitan al habilitar los permisos divididos de Active Directory. Esto se hace para quitar el acceso a los cmdlets que de otro modo generarían error al ejecutarse porque no tienen permisos para crear el objeto asociado de Active Directory.



### Cambios de permisos divididos de Active Directory

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Acción</th>
<th>Cambios realizados por Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Habilitar permisos divididos de Active Directory durante la primera instalación del servidor Exchange 2013</p></td>
<td><p>Cuando habilite los permisos divididos de Active Directory mediante el asistente de configuración o al ejecutar <code>setup.exe</code> con parámetros <code>/PrepareAD</code> y <code>/ActiveDirectorySplitPermissions:true</code>, sucederá lo siguiente:</p>
<ul>
<li><p>Se crea una unidad organizativa (OU) denominada <strong>grupos protegidos de Microsoft Exchange</strong>.</p></li>
<li><p>Se crea un grupo de seguridad de <strong>permisos de Exchange Windows</strong> en la unidad organizativa de <strong>grupos protegidos de Microsoft Exchange</strong>.</p></li>
<li><p>No se agrega el grupo de seguridad del <strong>subsistema de confianza de Exchange</strong> al grupo de seguridad de <strong>permisos Windows Exchange</strong>.</p></li>
<li><p>Se omite la creación de asignaciones de roles de administración sin delegación a roles de administración con los siguientes tipos de roles de administración:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Las entradas de control de acceso (ACE) que se hubieran asignado al grupo de seguridad de <strong>permisos Exchange Windows</strong> no se agregan al objeto de dominio de Active Directory.</p></li>
</ul>
<p>Si ejecuta el programa de instalación con el modificador <em>PrepareAllDomains</em> o <em>PrepareDomain</em>, sucede lo siguiente en cada uno de los dominios secundarios preparados:</p>
<ul>
<li><p>Todas las ACE asignadas al grupo de seguridad <strong>Permisos de Windows de Exchange</strong> se quitan del objeto de dominio.</p></li>
<li><p>Las ACE se establecen en cada dominio con la excepción de las ACE que se asignan al grupo de seguridad <strong>permisos de Windows de Exchange</strong>.</p></li>
</ul>
<p></p></td>
</tr>
<tr class="even">
<td><p>Cambiar de permisos compartidos o permisos divididos RBAC a permisos divididos de Active Directory</p></td>
<td><p>Cuando se ejecuta el comando de <code>setup.exe</code> con los parámetros <code>/PrepareAD</code> y <code>/ActiveDirectorySplitPermissions:true</code>, sucede lo siguiente:</p>
<ul>
<li><p>Se crea una unidad organizativa denominada <strong>grupos protegidos de Microsoft Exchange</strong> .</p></li>
<li><p>El grupo de seguridad de <strong>permisos Exchange Windows</strong> se traslada a la unidad organizativa de grupos <strong>protegidos de Microsoft Exchange</strong>.</p></li>
<li><p>Se quita el grupo de seguridad del <strong>subsistema de confianza de Exchange</strong> del grupo de seguridad de <strong>permisos Windows Exchange</strong>.</p></li>
<li><p>Se quitan todas las asignaciones de roles sin delegación a los roles de administración con los siguientes tipos de roles:</p>
<ul>
<li><p><code>MailRecipientCreation</code></p></li>
<li><p><code>SecurityGroupCreationandMembership</code></p></li>
</ul></li>
<li><p>Todas las ACE asignadas al grupo de seguridad <strong>Permisos de Windows de Exchange</strong> se quitan del objeto de dominio.</p></li>
</ul>
<p>Si ejecuta el programa de instalación con el modificador <em>PrepareAllDomains</em> o <em>PrepareDomain</em>, sucede lo siguiente en cada uno de los dominios secundarios preparados:</p>
<ul>
<li><p>Todas las ACE asignadas al grupo de seguridad <strong>Permisos de Windows de Exchange</strong> se quitan del objeto de dominio.</p></li>
<li><p>Las ACE se establecen en cada dominio con la excepción de las ACE que se asignan al grupo de seguridad <strong>permisos de Windows de Exchange</strong>.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Cambiar de permisos divididos de Active Directory a permisos compartidos o permisos divididos RBAC</p></td>
<td><p>Cuando se ejecuta el comando de <code>setup.exe</code> con los parámetros <code>/PrepareAD</code> y <code>/ActiveDirectorySplitPermissions:false</code>, sucede lo siguiente:</p>
<ul>
<li><p>El grupo de seguridad de <strong>permisos de Windows Exchange</strong> se traslada a la unidad organizativa de <strong>grupos de seguridad de Microsoft Exchange</strong>.</p></li>
<li><p>Se quita la unidad organizativa de <strong>grupos protegidos de Microsoft Exchange</strong>.</p></li>
<li><p>Se agrega el grupo de seguridad del <strong>subsistema de confianza de Exchange</strong> al grupo de seguridad de <strong>permisos Windows Exchange</strong>.</p></li>
<li><p>Las ACE se agregan al objeto de dominio del grupo de seguridad <strong>Permisos de Windows de Exchange</strong>.</p></li>
</ul>
<p>Si ejecuta el programa de instalación con el modificador <em>PrepareAllDomains</em> o <em>PrepareDomain</em>, sucede lo siguiente en cada uno de los dominios secundarios preparados:</p>
<ul>
<li><p>Las ACE se agregan al objeto de dominio del grupo de seguridad <strong>Permisos de Windows de Exchange</strong>.</p></li>
<li><p>Las ACE se definen en cada dominio incluyendo las ACE asignadas al grupo de seguridad <strong>permisos de Windows de Exchange</strong>.</p></li>
</ul>
<p>Las asignaciones de roles a la creación de destinatarios de correo y creación de grupos de seguridad y roles de pertenencia no se crean automáticamente cuando se cambia de permisos divididos a compartidos de Active Directory. Si se han personalizado asignaciones de roles de delegación antes de habilitar los permisos divididos de Active Directory, esas personalizaciones se dejan intactas. Para crear asignaciones de roles entre estos roles y el grupo de roles de Administración de la organización, vea <a href="configure-exchange-2013-for-shared-permissions-exchange-2013-help.md">Configurar Exchange 2013 para permisos compartidos</a>.</p></td>
</tr>
</tbody>
</table>


Después de habilitar los permisos divididos de Active Directory, los siguientes cmdlets ya no estarán disponibles:

  - **New-Mailbox**

  - **New-MailContact**

  - **New-MailUser**

  - **New-RemoteMailbox**

  - **Remove-Mailbox**

  - **Remove-MailContact**

  - **Remove-MailUser**

  - **Remove-RemoteMailbox**

Después de habilitar los permisos divididos de Active Directory, los siguientes cmdlets son accesibles pero no se pueden utilizar para crear grupos de distribución ni modificar la pertenencia a grupos de distribución:

  - **Add-DistributionGroupMember**

  - **New-DistributionGroup**

  - **Remove-DistributionGroup**

  - **Remove-DistributionGroupMember**

  - **Update-DistributionGroupMember**

Aunque aún estén disponibles, algunos cmdlets solo podrán ofrecer funcionalidad limitada al utilizarlos con permisos divididos de Active Directory. Esto ocurre porque pueden permitir configurar objetos de destinatario que se encuentran en la partición de dominio de Active Directory y objetos de configuración de Exchange que se encuentran en la partición de configuración de Active Directory. Además le podrán permitir configurar atributos relacionados con Exchange en objetos almacenados en la partición de dominio. Los intentos por utilizar cmdlets para crear objetos o modificar atributos no relacionados con Exchange en objetos de la partición de dominio provocarán un error. Por ejemplo, el cdmlet **Add-ADPermission** devolverá un error si intenta agregar permisos a un buzón de correo. Sin embargo, el cdmlet **Add-ADPermission** se completará satisfactoriamente si configura permisos en un conector de recepción. Esto ocurre porque el buzón de correo se almacena en la partición de dominio mientras que los conectores de recepción se almacenan en la partición de configuración.

Además, las características asociadas al Centro de administración de Exchange y a Outlook Web App, como el Asistente para buzón nuevo, también dejarán de estar disponibles o generarán un error si intenta usarlas.

No obstante, los administradores de Exchange podrán crear y administrar objetos específicos de Exchange, como reglas de transporte, etc.

Para obtener más información acerca de la configuración de un modelo de permisos divididos de Active Directory, vea [Configurar Exchange 2013 para permisos divididos](configure-exchange-2013-for-split-permissions-exchange-2013-help.md).

Volver al principio

