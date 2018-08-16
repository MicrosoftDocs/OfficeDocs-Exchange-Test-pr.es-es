---
title: 'Descripción de directivas asignación roles administración: Exchange 2013 Help'
TOCTitle: Descripción de las directivas de asignación de roles de administración
ms:assetid: 25913e43-326a-4371-90b5-021a35f100fe
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd638100(v=EXCHG.150)
ms:contentKeyID: 49895524
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de las directivas de asignación de roles de administración

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-03-09_

Una *directiva de asignación de funciones de administración* es una colección de una o más funciones de administración de usuarios finales que permite a los usuarios finales administrar su propio buzón Microsoft Exchange Server 2013 y la configuración de un grupo de distribución. Las directivas de asignación de funciones, que son parte del modelo de permisos de control de acceso basado en funciones (RBAC) en Exchange 2013, le permiten controlar qué configuración de un buzón específico y un grupo de distribución podrán modificar los usuarios finales. Los diferentes grupos de usuarios pueden tener directivas de asignación de funciones especializadas.


> [!NOTE]
> Este tema se centra en las funciones avanzadas de RBAC. Si desea administrar los permisos básicos de Exchange&nbsp;2013, como usar el Panel de control de Exchange (EAC) para agregar y quitar miembros de grupos de roles, crear y modificar grupos de roles o crear y modificar directivas de asignación de roles, consulte <A href="permissions-exchange-2013-help.md">Permisos</A>.



Para obtener más información acerca de RBAC, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

**Contenido**

Capas de directivas de asignación de roles

Directivas de asignación de roles predeterminadas y explícitas

Uso directivas de asignación de roles

Administración de la directiva de asignación de roles

## Capas de directivas de asignación de roles

Las siguientes lista describe las capas que constituyen el modelo de directivas de asignación de roles:

  - **Buzón**   A los buzones se les asigna una única directiva de asignación de funciones. Cuando se asigna una directiva de asignación de funciones a un buzón, se aplican al buzón las asignaciones entre funciones de administración y una directiva de asignación de funciones. Esto otorga al buzón todos los permisos proporcionados por las funciones de administración.

  - **Directiva de asignación de roles de administración**   La *directiva de asignación de roles de administración* es un objeto especial de Exchange 2013. Los usuarios se asocian con una directiva de asignación de funciones al crear sus buzones o si se cambia la directiva de asignación de funciones en un buzón. También es a lo que usted asigna funciones de administración de los usuarios finales. La combinación de todas las funciones en una directiva de asignación de funciones define todo lo que puede administrar un usuario en su buzón o grupo de distribución.

  - **Asignación de funciones de administración**   Una *asignación de funciones de administración* es el vínculo entre una función de administración y una directiva de asignación de funciones. La asignación de una función de administración a una directiva de asignación de funciones garantiza la posibilidad de usar cmdlets y parámetros definidos en la función de administración. Cuando crea una asignación de funciones entre una directiva de asignación de funciones y una función de administración, no puede especificar ningún ámbito. El ámbito que aplica la asignación se basa en la función de administración y no es `Self` ni `MyGAL`. Para obtener más información, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

  - **Función de administración**   Una *función de administración* es un contenedor para una agrupación de entradas de funciones de administración. Las funciones se usan para definir tareas específicas que un usuario puede realizar en su buzón o en sus grupos de distribución. Una *entrada de función de administración* es un cmdlet, un script o un permiso especial que permite que se realice cada tarea específica en una función de administración. Solo se pueden usar funciones de administración de usuario final con directivas de asignación de funciones. Para obtener más información, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

  - **Entrada de función de administración**   Las entradas de función de administración son entradas individuales de una función de administración que determinan qué cmdlets y qué parámetros están disponibles para la función de administración y el grupo de funciones. Cada entrada de función consiste en un único cmdlet y los parámetros a los que se puede tener acceso mediante la función de administración.

La siguiente figura muestra cada capa de directiva de asignación de funciones de la lista anterior y cómo cada una de las capas se relaciona con la otra.

**Modelo de directiva de asignación de funciones de administración**

![Relaciones del modelo de asignación de funciones](images/Dd638100.7f7c11ca-0d61-464d-98a3-a9991ec811b5(EXCHG.150).jpg "Relaciones del modelo de asignación de funciones")

Para obtener más información acerca de las funciones de administración, las asignaciones de funciones y los ámbitos, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).

## Directivas de asignación de roles predeterminadas y explícitas

Las siguientes secciones describen los dos clases de directivas de asignación de funciones en Exchange 2013.

## Directiva de asignación de funciones predeterminada

Una directiva de asignación de funciones predeterminada es una directiva asignada a un buzón cuando éste se crea o se mueve a un servidor que ejecuta Exchange 2013 sin proporcionar una directiva de asignación de funciones con el parámetro *RoleAssignmentPolicy* de los cmdlets**New-Mailbox** o **Enable-Mailbox**.

Exchange 2013 incluye una directiva de asignación de funciones predeterminada que otorga a los usuarios los permisos usados con más frecuencia. Es posible agregar o eliminar funciones de administración para modificar los permisos predeterminados de la directiva de asignación de funciones.

Si desea sustituir la directiva de asignación de funciones predeterminada con su propia directiva de asignación de funciones predeterminada, puede usar el cmdlet **Set-RoleAssignmentPolicy** para seleccionarla. Cuando hace esto, si no especifica una directiva de asignación de funciones, todos los buzones nuevos se asignan a la directiva de asignación de funciones que especificó como predeterminada.

Al cambiar la directiva de asignación de funciones predeterminada, los buzones asignados a ésta no se asignan de manera automática a la nueva directiva de asignación de funciones predeterminada. Si desea actualizar los buzones creados anteriormente para que usen la directiva de asignación de funciones que estableció como predeterminada, debe usar el cmdlet **Set-Mailbox**.

## Directiva de asignación de funciones explícita

Una directiva de asignación de funciones es una directiva que asigna a un buzón en forma manual con el parámetro *RoleAssignmentPolicy* de los cmdlets **New-Mailbox**, **Set-Mailbox** o **Enable-Mailbox**. Al asignar una directiva de asignación de funciones explícita, la nueva directiva se aplica inmediatamente y sustituye a la directiva de asignación de funciones explícita anterior.

## Uso directivas de asignación de roles

Las directivas de asignación de roles le permiten diseñar permisos según sus necesidades comerciales y lo que necesita que puedan configurar sus usuarios. Si la directiva de asignación de funciones cumple con sus necesidades, no precisa realizar ninguna personalización. Sin embargo, si tiene muchos grupos de usuarios diferentes con necesidades especializadas, puede crear directivas de asignación de funciones para cada uno de ellos.

La directiva de asignación de funciones predeterminada que use, debe contener permisos que se apliquen a la mayor cantidad de usuarios posible. A continuación, cree directivas de asignación de funciones para cada grupo de usuarios especializados y personalícelas para garantizar a los usuarios más o menos permisos restrictivos. Cuando organiza las directivas de asignación de funciones de esta manera, reduce la complejidad al asignar directivas de asignación de funciones de manera explícita a los usuarios especializados, mientras que la mayoría de los usuarios reciben los permisos más comunes proporcionados por la directiva de asignación de funciones predeterminada.

Un buzón puede tener solamente una directiva de asignación de funciones. Todos los usuarios, incluidos los administradores y los usuarios especializados, tienen asignada una directiva de asignación de funciones. Si desea que un usuario tenga un conjunto de permisos diferente, debe asignar al buzón de ese usuario otra directiva de asignación de funciones con los permisos requeridos.

## Administración de la directiva de asignación de roles

Para agregar una nueva directiva de asignación de funciones, primero debe crear una y decidir si será la directiva de asignación de funciones predeterminada. Después de crear una directiva de asignación de funciones, asigne funciones de administración a la directiva de asignación de funciones y, a continuación, asigne la directiva de asignación de funciones a un buzón. Posteriormente, podrá elegir si desea agregar o eliminar funciones de administración o seleccionar una directiva de asignación de funciones para que sea la predeterminada.

La siguiente tabla enumera la capa de directiva de asignación de funciones y los temas de procedimientos que puede usar para administrar cada capa.

### Temas de administración de directivas de asignación de funciones

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Capa de modelos de directivas de asignación de funciones</th>
<th>Temas de administración</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Buzón</p></td>
<td><p><a href="manage-user-mailboxes-exchange-2013-help.md">Administrar los buzones de usuario</a></p>
<p><a href="change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md">Cambiar la directiva de asignación en un buzón</a></p></td>
</tr>
<tr class="even">
<td><p>Directiva de asignación de funciones</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Administrar directivas de asignación de funciones</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p>Funciones de administración y asignaciones</p></td>
<td><p><a href="manage-role-assignment-policies-exchange-2013-help.md">Administrar directivas de asignación de funciones</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p>Entradas de funciones de administración</p></td>
<td><p><a href="add-a-role-entry-to-a-role-exchange-2013-help.md">Agregar una entrada de función a una función</a></p>
<p><a href="change-a-role-entry-exchange-2013-help.md">Cambiar una entrada de función</a></p>
<p><a href="remove-a-role-entry-from-a-role-exchange-2013-help.md">Quitar una entrada de función de una función</a></p>

> [!NOTE]
> Modificar las entradas de funciones de administración en funciones de administración de una directiva de asignación de funciones es una tarea avanzada y, en la mayoría de los casos, no suele ser necesaria. En cambio, es posible que pueda usar una función de administración preexistente que se adecue a sus requisitos. Para obtener más información, consulte <A href="built-in-role-groups-exchange-2013-help.md">Grupos de funciones integradas</A>.


</td>
</tr>
</tbody>
</table>

