---
title: 'Descripción de las asignaciones de funciones de administración: Exchange 2013 Help'
TOCTitle: Descripción de las asignaciones de funciones de administración
ms:assetid: 1dc33dd6-52fb-4852-a5ce-027bc73e1d8f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335131(v=EXCHG.150)
ms:contentKeyID: 49895505
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Descripción de las asignaciones de funciones de administración

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2012-10-04_

Una *asignación de funciones de administración*, que es parte del modelo de permisos de control de acceso basado en funciones (RBAC) de Microsoft Exchange Server 2013, representa el vínculo entre una función de administración y un usuario al que se le asigna una función. Un *usuario al que se asigna una función* es un grupo de funciones, una directiva de asignación de funciones, un usuario o un grupo de seguridad universal (USG). Una función debe estar asignada a un usuario al que se le asigna una función para que surta efecto. Para obtener más información acerca RBAC, consulte [Descripción del control de acceso basado en funciones](understanding-role-based-access-control-exchange-2013-help.md).


> [!NOTE]
> Este tema se centra en las funciones avanzadas de RBAC. Si desea administrar los permisos básicos de Exchange&nbsp;2013, como usar el Panel de control de Exchange (EAC) para agregar y quitar miembros de grupos de roles, crear y modificar grupos de roles o crear y modificar directivas de asignación de roles, consulte <A href="permissions-exchange-2013-help.md">Permisos</A>.



Este tema presenta la asignación de funciones a los grupos de funciones y las directivas de asignación de funciones, y la asignación de funciones directas a usuarios y grupos de seguridad universal. No se trata de la asignación de grupos de funciones o de directivas de asignación de funciones a usuarios. Para obtener más información sobre los grupos de funciones y las directivas de asignación de funciones, que son la forma recomendada para asignar permisos a usuarios, consulte los siguientes temas:

  - [Descripción de los grupos de roles de administración](understanding-management-role-groups-exchange-2013-help.md)

  - [Descripción de las directivas de asignación de roles de administración](understanding-management-role-assignment-policies-exchange-2013-help.md)

Puede crear los siguientes tipos de asignaciones de funciones, que se explican detalladamente más adelante en este tema:

  - Asignaciones de roles normales y de delegación

  - Asignaciones de roles exclusivos

## Administración de asignaciones de roles

Cuando cambia las asignaciones de funciones, los cambios que realice, probablemente, sean entre los grupos de funciones y las directivas de asignación de funciones. Si se agregan, se quitan o se modifican asignaciones de funciones de los usuarios a los que se asigna una función, puede controlar qué permisos se otorgan a los administradores y usuarios al activar o desactivar la administración de características relacionadas.

También es posible que desee asignar funciones directamente a los usuarios o grupos de seguridad universal. Esta es una tarea más avanzada que le permite definir, en un nivel granular, qué permisos se otorgan a los usuarios. Aunque esto proporciona flexibilidad, también aumenta la complejidad del modelo de permisos. Por ejemplo, si el usuario cambia de trabajo, es posible que deba reasignar a otro usuario, de manera manual, las funciones que estaban asignadas a ese usuario. Es por ello que se recomienda utilizar grupos de funciones y directivas de asignación de funciones para otorgar permisos a los usuarios. Puede asignar las funciones a un grupo de funciones o a una directiva de asignación de funciones y, a continuación, simplemente, agregar o quitar miembros del grupo de funciones o cambiar las directivas de asignación de funciones según sea necesario.

Es posible agregar, quitar y habilitar asignaciones de funciones, modificar el ámbito de administración de una asignación de funciones existente y mover las asignaciones de funciones a otros usuarios a los que se asigna una función. Este proceso de asignación de funciones a grupos de funciones, directivas de asignación de funciones, usuarios y grupos de seguridad universal es, en su mayoría, igual para todos los usuarios a los que se asigna una función. Las únicas excepciones son las siguientes:

  - Las directivas de asignación de funciones solo se pueden asignar a funciones de administración de usuarios finales.

  - A las directivas de asignación de funciones no se les puede asignar asignaciones de funciones de delegación.

  - No puede especificar el ámbito de administración cuando crea una asignación de funciones para directivas de asignación de funciones.

Para obtener más información sobre cómo administrar asignaciones de funciones, consulte los siguientes temas:

  - Grupos de funciones:
    
      - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - Directivas de asignación de funciones:
    
      - [Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md)
    
      - [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md)

  - Usuarios y grupos de seguridad universal:
    
      - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)
    
      - [Quitar una función de un usuario o un grupo de seguridad universal](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)
    
      - [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md)
    
      - [Cambiar el ámbito de una función](change-a-role-scope-exchange-2013-help.md)
    
      - [Delegar asignaciones de funciones](delegate-role-assignments-exchange-2013-help.md)

## Asignaciones de roles normales y de delegación

Las asignaciones de funciones normales permiten que el usuario al que se asigna una función acceda a entradas de funciones de administración que la función de administración asociada puso a disposición. Si un usuario al que se asigna una función tiene asignadas varias funciones de administración, se agregan y aplican las entradas de funciones de administración de cada función de administración. Esto significa que si un usuario al que se asignan funciones tiene asignadas las funciones de reglas de transporte y funciones de registro en diario, las funciones se combinan y se dan al usuario al que se asigna una función todas las entradas de funciones de administración asociadas. Si el usuario al que se asigna una función es un grupo de funciones o una directiva de asignación de funciones, los permisos provistos por las funciones son otorgados a los usuarios asignados al grupo de funciones o a la directiva de asignación de funciones. Para obtener más información sobre las funciones de administración y las entradas de funciones, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

Las asignaciones de funciones de delegación no proporcionan acceso para administrar las características. Las asignaciones de funciones de delegación permiten que un usuario al que se asigna una función asigne la función especificada a otros usuarios. Si el usuario al que se asigna una función es un grupo de funciones, cualquier miembro del grupo puede asignar la función a otro usuario al que se asigna una función. De manera predeterminada, solamente el grupo de funciones de administración de la organización puede asignar funciones a otros usuarios a los que se asigna una función. De forma predeterminada, solamente el usuario que instaló Exchange 2013 es miembro del grupo de funciones de administración de la organización. Sin embargo, si es necesario, se puede agregar otros usuarios a este grupo de funciones o crear otros grupos de funciones y asignar asignaciones de funciones de delegación a esos grupos.


> [!NOTE]
> Las asignaciones de funciones de delegación permiten que los usuarios a los que se asigna una función deleguen funciones de administración a otros usuarios. Esto no permite a los usuarios delegar grupos de funciones. Para obtener más información acerca de la delegación de los grupos de funciones, consulte <A href="understanding-management-role-groups-exchange-2013-help.md">Descripción de los grupos de roles de administración</A>.



Si desea que un usuario pueda administrar una característica y asignar a otros usuarios una función que otorgue permisos para usar la característica, asigne lo siguiente:

1.  Una asignación de funciones normal para cada función de administración que otorga acceso a las características que deben administrarse.

2.  Una asignación de funciones de delegación para cada función de administración que usted permite asignar a otros usuarios a los que se asigna una función.

No es necesario que las asignaciones de funciones normales y de delegación para un usuario al que se asigna una función sean idénticas. Por ejemplo, un usuario es un miembro de un grupo de funciones asignado a la función reglas de transporte mediante una asignación de funciones normal. Esto permite al usuario administrar la característica de reglas de transporte. Sin embargo, el usuario no tiene asignada una asignación de funciones de delegación para la función regla de transporte, por lo que no puede asignar esta función a otros usuarios. No obstante, el usuario es un miembro del grupo al cual se le asignó la función de administración de registro en diario mediante una asignación de funciones de delegación. El grupo de funciones al cual pertenece el usuario no tiene una asignación de funciones normal para la función de registro en diario, pero, dado que tiene una asignación de funciones de delegación, el usuario puede asignar la función a otros usuarios a los que se les asignan funciones.

## Ámbitos de administración

Cuando crea una asignación de funciones de administración normales o de delegación, tiene la opción de crear la asignación con un ámbito de administración para limitar los objetos que puedan ser manipulados por el usuario. Puede crear ámbitos de destinatarios o ámbitos de configuración. Los ámbitos de destinatarios el permiten controlar quién puede manipular buzones de correo, usuarios de corro, grupos de distribución y demás. Los ámbitos de configuración le permiten controlar quién puede manipular bases de datos y servidores.

Los ámbitos de destinatarios y de configuración le permiten segmentar la administración de objetos del servidor, la base de datos o los destinatarios de la organización. Por ejemplo, se puede agregar un ámbito de destinatario a una asignación de rol de modo que los administradores de Vancouver solamente puedan administrar destinatarios en la misma oficina. Se podría agregar un ámbito de configuración de servidor a una asignación de rol servidor diferente de modo que los administradores en Sídney solamente puedan administrar los servidores de su sitio de Active Directory.

Los ámbitos permiten asignar permisos a grupos de usuarios y permiten determinar el lugar en que los administradores pueden realizar su tarea de administración. Esto permite crear un modelo de permisos que asigne los límites geográficos u organizacionales.

Puede crear una asignación con un ámbito predefinido o puede agregar un ámbito personalizado a la asignación. Los ámbitos predefinidos, como el limitar a un usuario solamente a su buzón o grupos de distribución, se pueden aplicar con las opciones disponibles en la misma asignación. También puede crear un ámbito de configuración o destinatario personalizado y, a continuación, agregar ese ámbito a una asignación de roles. Los ámbitos personalizados le otorgan mayor granularidad de los objetos incluidos en el ámbito.

No se puede especificar ámbitos predefinidos y personalizados en la misma asignación. Tampoco se pueden mezclar ámbitos exclusivos y normales en la misma asignación.

Todas las asignaciones de roles solamente pueden tener un ámbito de destinatario y u ámbito de configuración. Si desea aplicar más de un ámbito de destinatario o un ámbito de configuración a una asignación de roles para el mismo rol de administración, debe crear varias asignaciones de roles.

Con un ámbito personalizado o predefinido, las asignaciones de roles están limitadas a los ámbitos de destinatario y de configuración definidos en el rol. Estos ámbitos se denominan ámbitos implícitos. Cualquier asignación de roles que no tenga un ámbito predefinido o personalizado, heredará los ámbitos implícitos del rol al que está asociada.

Para obtener más información sobre los ámbitos, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

## Asignaciones de roles exclusivos

Las asignaciones de funciones exclusivas se crean cuando asocia un ámbito exclusivo con una asignación de funciones. Los ámbitos exclusivos funcionan como los ámbitos normales y permiten que los usuarios a los que se asigna una función administren destinatarios que coincidan con el ámbito exclusivo. Sin embargo, a diferencia de los ámbitos normales, los demás los usuarios a los que se asigna una función no pueden administrar el destinatario, incluso, si éste coincide con los ámbitos aplicados a sus asignaciones de funciones. Puede ser útil cuando desea establecer un límite de quién puede administrar un destinatario solamente para algunos administradores. Solo administradores específicos pueden administrar el destinatario, y se le niega el acceso a todos los otros destinatarios.

Por ejemplo, considere lo siguiente:

  - Juan es un ejecutivo de Contoso. Su buzón coincide con un ámbito exclusivo llamado Usuarios VIP, que está asociado con la asignación exclusiva VIP restringidos.

  - Su buzón también está incluido en un ámbito normal llamado Usuarios Redmond, que está asociado con la asignación normal de Administración Redmond.

  - Federico es un administrador que está asociado con la asignación exclusiva VIP restringido.

  - Andrés es un administrador que está asociado con la asignación normal Administración Redmond.

Debido a que el buzón de Juan coincide con el ámbito exclusivo Usuarios VIP, solo Federico puede administrar su buzón. Aunque el buzón de Juan también coincide con el ámbito normal Usuarios Redmond, Andrés no está asociado con la asignación exclusiva VIP restringido. Por lo tanto, Exchange niega a Federico la posibilidad de administrar el buzón de Juan. Como Andrés administra el buzón de Juan, Andrés necesita tener una asignación exclusiva que tenga un ámbito exclusivo que coincida con el buzón de Juan.

Para obtener más información, consulte [Descripción de ámbitos exclusivos](understanding-exclusive-scopes-exchange-2013-help.md).

