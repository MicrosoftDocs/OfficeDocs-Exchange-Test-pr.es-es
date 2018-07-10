---
title: 'Delegar asignaciones de funciones: Exchange 2013 Help'
TOCTitle: Delegar asignaciones de funciones
ms:assetid: ed2d00d9-90c9-49dc-ab8a-cd791569aeed
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351237(v=EXCHG.150)
ms:contentKeyID: 49895997
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Delegar asignaciones de funciones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-02_

La delegación de funciones de administración permite a los usuarios a los que se asigna la función asignar una función de administración específica a otros grupos de función, a directivas de asignación de funciones de administración o a grupos de seguridad universal (USG). De modo predeterminado, sólo los miembros del grupo de funciones de administración de la organización pueden delegar asignaciones de funciones. Cuando se implementa una nueva instalación de Microsoft Exchange Server 2013, sólo la cuenta de usuario que instala Exchange 2013 es miembro del grupo de funciones de administración de la organización.

Si asigna una asignación de funciones de delegación a un grupo de funciones, cualquier miembro del grupo de funciones puede delegar la función de administración asociada a otros usuarios a los que se asigna una función.


> [!IMPORTANT]
> Las asignaciones de funciones de delegación no otorgan al usuario al que se asigna la función los permisos que concede la función, sino sólo la posibilidad de asignar la función a otros usuarios. Si también desea otorgar los permisos que concede la función al usuario al que se asigna la función, debe crear una asignación de funciones regular. Para crear una asignación de funciones regular, vea los temas siguientes:<BR><A href="manage-role-groups-exchange-2013-help.md">Administrar grupos de roles</A><BR><A href="manage-role-assignment-policies-exchange-2013-help.md">Administrar directivas de asignación de funciones</A><BR><A href="add-a-role-to-a-user-or-usg-exchange-2013-help.md">Agregar una función a un usuario o grupo de seguridad universal</A>




> [!NOTE]
> En este tema se describe la delegación de asignación de funciones de administración. Si desea delegar quién puede agregar o quitar miembros de los grupos de funciones, lo cual constituye el método de delegación recomendado, consulte <A href="manage-role-groups-exchange-2013-help.md">Administrar grupos de roles</A>.



Para obtener más información acerca de las asignaciones de funciones regulares y las asignaciones de funciones de administración de delegación, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

¿Busca otras tareas de administración relacionadas con los permisos de administración? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Asignaciones de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use el Shell para delegar una función de administración

Puede crear asignaciones de funciones de delegación usando los mismos ámbitos predefinidos, los ámbitos basados en filtros de servidor o filtros de destinatario, los ámbitos basados en listas de servidores y los ámbitos de unidades organizativas que se pueden usar para crear ámbitos regulares o exclusivos. La única diferencia entre crear una asignación de funciones regular y una asignación de funciones de delegación es la incorporación del modificador *Delegating* al comando. Para obtener más información acerca de cómo crear asignaciones de funciones, consulte los siguientes temas:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)


> [!NOTE]
> No puede crear una asignación de funciones de delegación para una directiva de asignación de funciones de administración.



En este ejemplo se crea una asignación de funciones de delegación para permitir a los miembros del grupo de funciones de administración ejecutiva asignar la función de destinatarios de correo a cualquier usuario al que se asignen funciones en la organización de Exchange.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admin - Delegate" -Delegating

En este ejemplo se crea una asignación de funciones de delegación para permitir a los miembros del grupo de funciones de administración ejecutiva asignar la función de destinatarios de correo sólo a los usuarios de la unidad organizativa de ventas/usuarios del dominio contoso.com.

    New-ManagementRoleAssignment -Role "Mail Recipients" -SecurityGroup "Senior Admins" -Name "Mail Recipients_Senior Admins - Delegate" -RecipientOrganizationalUnitScope contoso.com/sales/users -Delegating

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd335193\(v=exchg.150\)).

