---
title: 'Visualización de asignaciones de funciones: Exchange 2013 Help'
TOCTitle: Visualización de asignaciones de funciones
ms:assetid: 0be4def9-af6d-476a-9c97-7155ae11b587
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335086(v=EXCHG.150)
ms:contentKeyID: 49895453
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Visualización de asignaciones de funciones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Las asignaciones de funciones de administración asignan una función de administración a un usuario al que se le asigna una función. Para obtener más información acerca de las asignaciones de funciones en Microsoft Exchange Server 2013, consulte [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Asignaciones de roles" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Este tema hace uso de la canalización y el cmdlet **Format-List**. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:
    
      - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))
    
      - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Ver una lista de todas las asignaciones de funciones

Para ver una lista de todas las asignaciones de funciones configuradas en la organización, ejecute el cmdlet **Get-ManagementRoleAssignment**. Si desea recuperar una lista de las asignaciones de funciones que coinciden con una cadena parcial que haya especificado, utilice caracteres comodín (\*). En este ejemplo, se recupera una lista de todas las asignaciones de funciones que comienzan con la cadena "Tier 1".

    Get-ManagementRoleAssignment "Tier 1*"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver los detalles de una asignación de funciones específica

También puede ver los detalles de una función específica canalizando los resultados del cmdlet **Get-ManagementRoleAssignment** al cmdlet **Format-List**. Use la siguiente sintaxis.

    Get-ManagementRoleAssignment <assignment name> | Format-List

En este ejemplo, se recuperan los detalles de la asignación de funciones Asignación del Servicio de asistencia.

    Get-ManagementRoleAssignment "Help Desk Assignment" | Format-List

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver la lista de asignaciones de funciones asignadas a un usuario específico

Para ver una lista de asignaciones de funciones asociadas con un grupo de funciones de administración, una función o una directiva de asignación de funciones, o asociadas con un usuario o un grupo de seguridad universal (USG), utilice la sintaxis siguiente.

    Get-ManagementRoleAssignment -RoleAssignee <role assignee name>

En este ejemplo, se recuperan todas las asignaciones de funciones asociadas con el grupo de funciones Administración de servidor.

    Get-ManagementRoleAssignment -RoleAssignee "Server Management"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver las asignaciones de funciones asociadas con una función específica

Cada función puede tener varias asignaciones de funciones. Puede utilizar el cmdlet **Get-ManagementRoleAssigment** para ver una lista de asignaciones de funciones asociadas con una función específica.

Para ver una lista de asignaciones de funciones asociadas con una función específica, utilice la sintaxis siguiente.

    Get-ManagementRoleAssignment -Role <role name>

En este ejemplo, se recuperan todas las asignaciones de funciones asociadas con la función Destinatarios de correo.

    Get-ManagementRoleAssignment -Role "Mail Recipients"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver una lista de asignaciones de funciones que utilizan un ámbito predefinido específico

Para ver una lista de asignaciones de funciones que utilizan un ámbito predefinido específico, utilice la sintaxis siguiente.

    Get-ManagementRoleAssignment -RecipientWriteScope < MyGAL | MyDistributionGroups | Organization | Self | CustomRecipientScope | ExecutiveRecipientScope >

En este ejemplo, se recuperan todas las asignaciones de funciones que utilizan el ámbito predefinido Organización.

    Get-ManagementRoleAssignment -RecipientWriteScope Organization

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver una lista de asignaciones de funciones para las que se ha definido un ámbito en una unidad organizativa específica

Para ver una lista de asignaciones de funciones para las que se ha definido un ámbito en una unidad organizativa (OU) específica, utilice la sintaxis siguiente.

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope <OU>

En este ejemplo, se recuperan todas las asignaciones de funciones para las que se ha definido un ámbito en la unidad organizativa Norteamérica\\Ingeniería\\Usuarios en el dominio contoso.com.

    Get-ManagementRoleAssignment -RecipientOrganizationalUnitScope "contoso.com/North America/Engineering/Users"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver una lista de asignaciones que utilizan un ámbito personalizado específico

Para ver una lista de asignaciones de funciones que utilizan un ámbito personalizado específico, primero debe determinar si el ámbito es un ámbito de destinatarios, un ámbito de configuración, un ámbito exclusivo de destinatarios o un ámbito exclusivo de configuración. Cada tipo de ámbito utiliza un parámetro diferente en el cmdlet **Get-ManagementRoleAssignment**. En las listas siguientes, se enumeran los ámbitos y los parámetros asociados con cada uno de ellos:

  - **Ámbitos de destinatarios** *CustomRecipientWriteScope*

  - **Ámbitos de configuración** *CustomConfigWriteScope*

  - **Ámbitos exclusivos de destinatarios** *ExclusiveRecipientWriteScope*

  - **Ámbitos exclusivos de configuración** *ExclusiveConfigWriteScope*

La sintaxis para cada parámetro es la misma. Especifique el nombre del ámbito con el parámetro que coincide con el tipo de ámbito.

En este ejemplo, se recuperan todas las asignaciones de funciones que utilizan el ámbito de destinatarios Destinatarios de Vancouver.

    Get-ManagementRoleAssignment -CustomRecipientWriteScope "Vancouver Recipients"

En este ejemplo, se recuperan todas las asignaciones de funciones que utilizan el ámbito exclusivo de configuración Sitio de AD en Seattle.

    Get-ManagementRoleAssignment -ExclusiveConfigWriteScope "Seattle AD Site"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver una lista de ámbitos normales o exclusivos

Para ver una lista de asignaciones de funciones normales o exclusivas, utilice la sintaxis siguiente.

    Get-ManagementRoleAssignment -Exclusive < $True | $False >

Por ejemplo, para ver una lista de ámbitos exclusivos, ejecute el siguiente comando:

    Get-ManagementRoleAssignment -Exclusive $True

En este ejemplo, se recupera una lista de ámbitos normales sin ámbitos exclusivos.

    Get-ManagementRoleAssignment -Exclusive $False

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver los usuarios que pueden modificar un destinatario o servidor específico

Para ver una lista de asignaciones de funciones que pueden modificar un destinatario o servidor específico, utilice los parámetros *WritableRecipient* y *WritableServer*. Especifique el nombre del destinatario con el parámetro *WritableRecipient* y el nombre del servidor con el parámetro *WritableServer*.

En este ejemplo, se recupera una lista de las asignaciones de funciones que pueden modificar el destinatario Brian.

    Get-ManagementRoleAssignment -WritableRecipient "Brian"

Puede combinar los parámetros *WritableRecipient* y *WritableServer* con otros parámetros, como el parámetro *RoleAssignee* y el modificador *GetEffectiveUsers*, para precisar su consulta y ampliar cualquier grupo de funciones o USG. En este ejemplo, se recuperan todos los usuarios que pueden modificar el servidor EX02 y que tienen asignado el grupo de funciones Administración de servidor.

    Get-ManagementRoleAssignment -WritableServer EX02 -RoleAssignee "Server Management" -GetEffectiveUsers

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver los usuarios que reciben permisos de una asignación a través de un grupo de funciones o USG

Para ver una lista de usuarios que reciben permisos de una asignación de funciones, utilice la sintaxis siguiente.

    Get-ManagementRoleAssignment <assignment name> -GetEffectiveUsers

En este ejemplo, se recupera una lista de usuarios en la asignación de roles Asignación del Servicio de asistencia.

    Get-ManagementRoleAssignment "Help Desk Assignment" -GetEffectiveUsers

Asimismo, puede combinar el modificador *GetEffectiveUsers* con otros parámetros en el cmdlet **Get-ManagementRoleAssignment** para ampliar los grupos de funciones y USG a los que se asignan las asignaciones de funciones. Para obtener un ejemplo de cómo utilizar el modificador *GetEffectiveUsers* con otros parámetros, consulte la sección "Ver los usuarios que pueden modificar un destinatario o servidor específico", mencionada anteriormente en este tema.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

## Ver una lista de asignaciones de funciones que están habilitadas o deshabilitadas

Para ver una lista de asignaciones de funciones que están habilitadas o deshabilitadas, utilice la sintaxis siguiente.

    Get-ManagementRoleAssignment -Enabled < $True | $False >

En este ejemplo, se recupera una lista de asignaciones de funciones que están deshabilitadas.

    Get-ManagementRoleAssignment -Enabled $False

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleAssignment](https://technet.microsoft.com/es-es/library/dd351024\(v=exchg.150\)).

