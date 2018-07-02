---
title: 'Descripción de permisos de bosques múltiples: Exchange 2013 Help'
TOCTitle: Descripción de permisos de bosques múltiples
ms:assetid: 8241033f-e201-4799-b17c-4f120c6e6445
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298099(v=EXCHG.150)
ms:contentKeyID: 49895748
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de permisos de bosques múltiples

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Muchas organizaciones implementan bosques múltiples para crear límites de seguridad dentro de sus organizaciones. El uso de bosques múltiples ayuda a los administradores a definir dichos límites de seguridad de tal forma que se adapten mejor a sus requisitos, ya sea asegurándose de que muy pocas personas tienen acceso a los recursos o segmentando las divisiones de una organización.

Microsoft Exchange Server 2013 admite dos tipos de topologías de bosques múltiples:

  - **Entre bosques**   Las topologías entre bosques pueden tener bosques múltiples, cada uno con su propia instalación de Exchange.

  - **Bosque de recursos**   Las topologías de bosque de recursos tienen un bosque de Exchange y uno o varios bosques de cuentas.

A los efectos de este tema, se dice que el bosque que contiene los grupos de seguridad universal (USG), y los usuarios de fuera del bosque en el que está instalado Exchange 2013, ya se trate de un bosque de cuentas o de otro bosque de recursos, es un bosque externo.

La configuración de los permisos en una topología de bosques múltiples reside en la configuración correcta de las confianzas de los bosques y en la sincronización de la lista global de direcciones (GAL) para la creación de buzones vinculados. El bosque de Exchange 2013 tiene que confiar en el bosque externo que contiene los grupos de seguridad universal asociados con los grupos de roles vinculados y los usuarios asociados con los buzones vinculados.

Exchange 2013 utiliza un modelo de permisos de control de acceso basado en roles (RBAC). Los grupos de roles de administración a los que pertenecen los administradores, así como las directivas de asignación de roles de administración que los usuarios finales tienen asignadas, determinan lo que cada administrador y cada usuario final pueden hacer. Para entender bien los permisos de bosques múltiples, es necesario estar familiarizado con RBAC. Para obtener más información acerca de RBAC, los grupos de roles de administración y las directivas de asignación de roles, vea estos temas:

  - [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md)

  - [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md)

  - [Descripción de las directivas de asignación de roles de administración](understanding-management-role-assignment-policies-exchange-2013-help.md)

¿Busca tareas de administración relacionadas con la administración de los permisos? Vea [Permisos](permissions-exchange-2013-help.md).

**Contenido**

Permisos en una topología de bosques múltiples

Permisos entre límites

Configurar permisos entre límites

## Permisos en una topología de bosques múltiples

RBAC aplica permisos a todos los objetos de Exchange dentro de un único bosque, y la configuración RBAC de cada bosque se realiza de forma independiente a la de los demás bosques. Cuando se crea un grupo de roles en un bosque, ese grupo no existe en ningún otro bosque, por lo que los permisos que se le conceden se aplican sólo al bosque en el que se creó. Por ejemplo, un miembro de un grupo de roles que concede permisos para crear un buzón de correo, podrá crearlo sólo en el bosque que contiene dicho grupo de roles.

Si tiene varios bosques de Exchange y desea configurar permisos idénticos en cada bosque, debe aplicar explícitamente la misma configuración en cada bosque. Por ejemplo, si tiene dos bosques de Exchange 2013 y quiere crear un grupo de roles de administración de cumplimiento para administrar los permisos de su departamento de asesoría legal, debe hacer lo siguiente:

  - En cada bosque, cree un grupo de roles denominado Administración de cumplimiento. Si sus administrados están en un bosque externo distinto de cualquiera de los dos bosques de Exchange, cree los dos grupos de roles como grupos de roles vinculados. Para obtener más información acerca de los grupos de roles, vea la sección Permisos entre límites.

  - En cada bosque, cree asignaciones de roles entre los nuevos grupos de roles y los roles que desea utilizar.

  - Como parte de las nuevas asignaciones de roles, opcionalmente puede agregar ámbitos de administración que incluyan al servidor y a los objetos de destinatarios de cada bosque.

  - Si creó los grupos de roles como grupos de roles vinculados, agregue miembros al grupo de seguridad universal asociado en el bosque externo.

La siguiente figura muestra cómo los grupos de roles configurados dentro de los bosques de Exchange 2013 están unidos a sus respectivos bosques. El grupo de roles Administración de la organización del bosque A de Exchange 2013 concede permisos sólo para administrar los buzones de correo y los servidores que están dentro de ese bosque. De igual forma, los grupos de roles del bosque B de Exchange 2013 conceden permisos sólo a los buzones de correo y los servidores de dentro de ese bosque.

La figura también muestra que en cada bosque se crea el grupo de roles personalizado A. A pesar de que se crearon con el mismo nombre, cada uno es una entidad independiente. De hecho, tal y como se puede ver en la figura, a cada uno se le pueden asignar distintos roles de administración en sus respectivos bosques. Al grupo de roles personalizado A del bosque A de Exchange 2013 se le asignan los roles Búsqueda en el buzón y Seguimiento de mensajes, mientras que al grupo de roles personalizado A del bosque B de Exchange 2013 se le asignan los roles Búsqueda en el buzón y Administración de la retención.

Finalmente, los ámbitos de administración creados en cada bosque también están enlazados por el bosque. Los ámbitos de servidor creados en cada bosque sólo pueden contener los servidores que son miembros de ese bosque. El ámbito de servidor A sólo puede contener los servidores que hay dentro del bosque A de Exchange 2013, mientras que el ámbito de servidor B sólo puede contener los servidores que están dentro del bosque B de Exchange 2013. De igual forma, el ámbito de destinatarios del bosque B de Exchange 2013 sólo puede contener los buzones de correo que se hallan el bosque B de Exchange 2013.

**Relación entre RBAC y el ámbito del límite del bosque**

![Relaciones de RBAC y el ámbito del límite del bosque](images/Dd298099.220da7c3-cbb8-42ac-9d58-084d996bf837(EXCHG.150).gif "Relaciones de RBAC y el ámbito del límite del bosque")

## Permisos entre límites

Los permisos que concede RBAC sólo permiten a los usuarios ver o modificar objetos de Exchange contenidos en un determinado bosque. No obstante, es posible conceder permisos para ver y modificar objetos de Exchange de un bosque a usuarios que estén fuera de ese bosque. Con los permisos entre límites podrá centralizar las cuentas de administración de Exchange en un único bosque, en vez de tener que autenticarlas en cada bosque individual para realizar las tareas.


> [!NOTE]
> Los permisos que se conceden a un usuario externo a un bosque de Exchange siguen aplicándose sólo a ese bosque de Exchange en concreto. Por ejemplo, si un usuario de un bosque externo es miembro del grupo de roles vinculado Administración de la organización, situado en el bosque&nbsp;A, el usuario puede administrar sólo los objetos de Exchange contenidos en el bosque&nbsp;A. Para obtener los permisos necesarios para administrar todos los bosques, un usuario tiene que ser miembro de los grupos de roles vinculados de cada bosque de Exchange.



Los permisos entre límites también per permiten aplicar directivas de asignación de roles a los buzones de los usuarios que tienen buzones en un bosque de Exchange, pero que tienen cuentas de usuario que residen en un bosque de cuentas. Exchange 2013 admite permisos entre límites si utiliza grupos de roles vinculados y buzones vinculados, un aspecto que aparece en las siguientes secciones.

## Permisos administrativos

Se conceden límites entre bosques a los permisos administrativos, a través del uso de grupos de roles vinculados y buzones vinculados.

En la organización de Exchange 2013 se crea un grupo de roles vinculado, que se vincula a un grupo de seguridad universal más allá del límite del bosque, en el bosque externo. El grupo de seguridad universal al que está vinculado el grupo de roles vinculado puede ser cualquiera de los siguientes:

  - Un grupo de seguridad universal dedicado para el uso específico del grupo de roles vinculado

  - Un grupo de seguridad universal que está vinculado por grupos de roles vinculados en bosques múltiples de Exchange 2013

  - Un grupo de seguridad universal de un grupo de roles en otro bosque de Exchange 2013

  - Un grupo de seguridad universal asociado a un rol administrativo de Exchange Server 2007 o a un grupo de roles de Exchange 2010

El grupo de seguridad universal al que se vincula un grupo de roles vinculado tiene que estar en otro bosque. No se puede vincular un grupo de roles vinculado a un grupo de seguridad universal que esté en el mismo bosque.

La siguiente figura muestra que los grupos de seguridad universal de un bosque de cuentas se pueden asociar a grupos de roles en uno o varios bosques de recursos de Exchange 2013. Los miembros de los grupos de seguridad universal en el bosque de cuentas se convierten de hecho en miembros de los grupos de roles a través de los grupos de seguridad universal.

**Grupos de roles vinculados asociados a USG en un bosque independiente**

![Grupo de funciones vinculado y relaciones del Grupo de seguridad universal](images/Dd298099.23f245e8-b80f-4082-8628-ee6701259be6(EXCHG.150).gif "Grupo de funciones vinculado y relaciones del Grupo de seguridad universal")

Cuando se crea un grupo de roles vinculado, se asignan roles al grupo vinculado en el bosque de Exchange 2013. Las asignaciones que asocian los roles al grupo de roles vinculado pueden incluir ámbitos de administración, si fuera necesario. Estos ámbitos se confinan al bosque en el que se crea el grupo de roles vinculado.

Para administrar la pertenencia al grupo de roles vinculado, se agregan y se quitan miembros del grupo de seguridad universal del bosque externo. Al agregar miembros a este grupo de seguridad universal, se les conceden los permisos asignados al grupo de roles vinculado del mismo bosque de Exchange 2013. Si ha vinculado a un mismo grupo de seguridad universal varios grupos de roles vinculados, los miembros de ese grupo de seguridad universal reciben los permisos asignados a cada grupo de roles vinculado de cada bosque de Exchange 2013.

No es posible administrar la pertenencia a un grupo de roles vinculado desde el bosque de Exchange 2013.

Un segundo método para asignar permisos administrativos más allá de los límites de los bosques es hacerlo mediante el uso de buzones vinculados. Para que los usuarios de un bosque de cuentas utilicen una implementación de Exchange 2013 en un bosque de recursos de Exchange 2013 aparte, tendrá que configurar buzones vinculados para cada usuario. Los buzones vinculados pueden agregarse como miembros a los grupos de roles dentro del bosque de Exchange 2013. Cuando un buzón de correo vinculado se convierte en miembro de un grupo de roles, ese buzón vinculado, y a su vez el usuario del bosque de cuentas asociado con el buzón vinculado, recibe los permisos que proporciona el grupo de roles.

La siguiente figura muestra la relación entre los usuarios de un bosque de cuentas, los buzones de correo vinculados asociados a ellos y los grupos de roles de los que son miembros.

**Usuarios de un bosque de cuentas asociado a buzones de correo vinculados que son miembros de grupos de roles**

![Relaciones del grupo de funciones y el buzón de correo vinculado](images/Dd298099.e59242f6-5c63-4114-90f7-6b6c2478570c(EXCHG.150).gif "Relaciones del grupo de funciones y el buzón de correo vinculado")

Tanto los grupos de roles vinculados, como los buzones de correo vinculados, tienen ventajas y desventajas cuando se utilizan para asignar permisos administrativos más allá de los límites de los bosques. En la tabla siguiente se describen algunas de ellas.

### Grupo de roles vinculado y buzón de correo vinculado: ventajas y desventajas

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Grupos de roles vinculados o buzones de correo vinculados</th>
<th>Ventaja</th>
<th>Desventaja</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Grupos de roles vinculados</p></td>
<td><p>Puede asociar varios grupos de roles vinculados procedentes de múltiples bosques de Exchange 2013 a un único grupo de seguridad universal, en un bosque de cuentas o en otro bosque de recursos de Exchange. Esto le permite administrar complejas topologías de bosques de Exchange a través de un pequeño conjunto de grupos de seguridad universal en un único bosque.</p></td>
<td><p>No se puede convertir un grupo de roles regular en un grupo de roles vinculado. Es necesario crear manualmente los grupos de roles vinculados para reemplazar cada grupo de roles regular que tiene los permisos que desea conceder más allá del límite de un bosque. Para obtener más información, vea Configurar permisos entre límites.</p></td>
</tr>
<tr class="even">
<td><p>Buzones vinculados</p></td>
<td><p>Los buzones vinculados permiten utilizar los grupos de roles existentes dentro del bosque de Exchange. Los buzones vinculados se agregan como miembros a los grupos de roles existentes, igual que se hace con los buzones regulares, los grupos de seguridad universal y los usuarios del mismo bosque de Exchange.</p></td>
<td><p>Si concede permisos en bosques múltiples de Exchange 2013 mediante buzones de correo vinculados que se vinculan a un único usuario en un bosque de cuentas, a la hora de modificar los permisos concedidos al usuario, deberá modificar la pertenencia al grupo de roles en cada bosque de Exchange 2013.</p></td>
</tr>
</tbody>
</table>


Recomendamos que utilice grupos de roles vinculados para conceder permisos entre límites de bosques, si planea tener múltiples bosques de recursos de Exchange.

## Permisos de usuario final

Los permisos de usuario final se asignan a buzones individuales mediante las directivas de asignación de roles. Cuando Exchange 2013 está instalado en un bosque de recursos, en éste se crean buzones vinculados que, a su vez, se asocian a las cuentas de usuario del bosque de cuentas.

Cuando se crea un buzón vinculado, se asigna a una directiva de asignación de roles predeterminadas, igual que si se tratara de un buzón regular. La directiva de asignación de roles determina qué permisos de usuario final se conceden al buzón. Estos permisos permiten a los usuarios ver y modificar las configuraciones relacionadas con éstas y otras características:

  - Información de perfil de usuario final

  - Correo de voz de usuario final

  - Pertenencia a la distribución del usuario final y propiedad de la misma

Cuando se asigna una directiva de asignación de roles a un buzón vinculado, el usuario del bosque de cuentas asociado al buzón vinculado recibe permisos para administrar las características disponibles para ese usuario. Los permisos se aplican sólo a los recursos del bosque de Exchange en el que está situado el buzón vinculado. La siguiente figura muestra la relación entre el usuario final del bosque de cuentas, su buzón vinculado asociado y la directiva de asignación de roles asignada al buzón vinculado. De forma adicional, un buzón vinculado asociado a un usuario administrativo del bosque de cuentas se puede asociar a varios grupos de roles, además de a una directiva de asignación de roles.

**Usuarios de un bosque de cuentas asociado a buzones vinculados, a cada uno de los cuales se asigna una directiva de asignación de roles**

![Relaciones del grupo de funciones y la directiva de asignación](images/Dd298099.785b9b35-4292-43ce-917b-117d0174742e(EXCHG.150).gif "Relaciones del grupo de funciones y la directiva de asignación")

Volver al principio

## Configurar permisos entre límites

Para configurar permisos entre límites, en una topología de bosque múltiple, es necesario crear grupos de roles vinculados para cada uno de los grupos de roles que se desee vincular a los grupos de seguridad universal de un bosque externo. Eso significa que es necesario crear un grupo de roles vinculado para cada grupo de roles integrado. Se necesita:

1.  Crear un grupo de seguridad universal en el bosque externo por cada grupo de roles vinculado que haya que crear. Agregar miembros a este grupo de seguridad universal al que desee conceder permisos.

2.  Crear un grupo de roles vinculado para cada grupo de roles integrado. Cuando se crea el grupo de roles vinculado sucede lo siguiente:
    
      - Los mismos roles que están asignados al grupo de roles integrado se asignan al nuevo grupo de roles vinculado.
    
      - El grupo de roles vinculado está asociado al grupo de seguridad universal, en el bosque externo.

3.  Crear grupos de roles vinculados para cualquier grupo de roles personalizado que haya creado.

4.  Opcionalmente, asignar ámbitos personalizados a los nuevos grupos de roles vinculados.

Para obtener información detallada acerca de cómo realizar estos pasos, vea los temas siguientes:

  - [Crear grupos de funciones vinculadas que reflejan grupos de funciones integradas](create-linked-role-groups-that-mirror-built-in-role-groups-exchange-2013-help.md)

  - [Administrar grupos de funciones vinculadas](manage-linked-role-groups-exchange-2013-help.md)

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

Si necesita cambiar el grupo de seguridad universal al que está asociado un grupo de roles vinculado, vea [Administrar grupos de funciones vinculadas](manage-linked-role-groups-exchange-2013-help.md).

Cuando se crea un buzón de correo vinculado, automáticamente se asigna a una directiva de asignación de roles. Es posible cambiar tanto la directiva de asignación de roles que está asignada al buzón vinculado, como la directiva de asignación de roles que se asigna a los buzones de forma predeterminada cuando éstos se crean. Para obtener más información al respecto, vea los temas siguientes:

  - [Cambiar la directiva de asignación en un buzón](change-the-assignment-policy-on-a-mailbox-exchange-2013-help.md)

  - [Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md)

