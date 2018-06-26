---
title: 'Cambiar el ámbito de una función: Exchange 2013 Help'
TOCTitle: Cambiar el ámbito de una función
ms:assetid: 9180e1e0-c352-4ccd-8da6-885a2e309867
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298145(v=EXCHG.150)
ms:contentKeyID: 49895780
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambiar el ámbito de una función

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-03_

Los ámbitos de función de administración determinan qué objetos estarán disponibles para un usuario de modo que los objetos se puedan cambiar mediante el uso de parámetros y cmdlets asignados a éstos. Al cambiar un ámbito, puede cambiar los objetos disponibles para que los usuarios puedan crear, cambiar o quitar.

Puede cambiar un ámbito de administración personalizado. Puede cambiar los ámbitos exclusivos o los ámbitos normales. Si cambia un ámbito exclusivo, el nuevo ámbito surte efecto inmediatamente. Si desea cambiar una asignación de función de administración con un ámbito de administración predefinido o de unidad organizativa (OU), consulte [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

Para obtener más información sobre los ámbitos y las asignaciones de funciones de administración en Microsoft Exchange Server 2013, consulte los siguientes temas:

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

¿Está buscando otras tareas de administración relacionadas con los ámbitos de función? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Ámbitos de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Cambiar el nombre de un ámbito

Para cambiar el nombre de un ámbito, use la sintaxis siguiente.

    Set-ManagementScope <current scope name> -Name <new scope name>

En este ejemplo, se cambia el ámbito Servidores de Seattle a los servidores Exchange de Seattle.

    Set-ManagementScope "Seattle Servers" -Name "Seattle Exchange Servers"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementScope](https://technet.microsoft.com/es-es/library/dd297996\(v=exchg.150\)).

## Cambiar un filtro de destinatarios en un ámbito

Para cambiar el filtro de destinatarios en un ámbito, use la siguiente sintaxis.

    Set-ManagementScope <scope name> -RecipientRestrictionFilter { <new recipient filter> }

En este ejemplo, se cambia el filtro de destinatario de modo tal que coincida con todos los objetos de destinatario, donde la propiedad **Company** está establecida en contoso.

    Set-ManagementScope "Company Scope" -RecipientRestrictionFilter { Company -eq 'contoso' }

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementScope](https://technet.microsoft.com/es-es/library/dd297996\(v=exchg.150\)).

Para obtener más información acerca de los filtros de destinatario y para ver una lista de propiedades de destinatario filtrables, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

## Cambiar la raíz de unidad organizativa en un ámbito

Para cambiar la raíz de una unidad organizativa en un ámbito, use la sintaxis siguiente.

    Set-ManagementScope <scope name> -RecipientRoot <OU>

En este ejemplo, se cambia la raíz de una unidad organizativa de la unidad organizativa de usuarios de ventas del dominio contoso.com a Norteamérica/Ventas.

    Set-ManagementScope "Sales Users" -RecipientRoot "contoso.com/North America/Sales"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementScope](https://technet.microsoft.com/es-es/library/dd297996\(v=exchg.150\)).

## Cambiar un filtro de servidor en un ámbito

Para cambiar el filtro de servidor en un ámbito, use la siguiente sintaxis.

    Set-ManagementScope <scope name> -ServerRestrictionFilter { <new server filter> }

En este ejemplo se cambia el filtro del servidor para que coincida con todos los objetos el servidor en el que la propiedad **ServerSite** está establecida en 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com'.

    Set-ManagementScope "Company Scope" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementScope](https://technet.microsoft.com/es-es/library/dd297996\(v=exchg.150\)).

Para obtener más información acerca de los filtros de servidor y para ver una lista de propiedades de servidor filtrables, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

## Cambiar la lista de servidores en un ámbito

No puede cambiar la lista de servidores en un ámbito. Si necesita cambiar la lista de servidores, debe realizar las siguientes acciones:

1.  De ser necesario, recupere la lista de servidores actual en el ámbito que se debe reemplazar mediante el procedimiento "Ver un ámbito específico" en el tema [Ver ámbitos de roles](view-role-scopes-exchange-2013-help.md).

2.  Cree un ámbito con la nueva lista de servidor mediante el procedimiento "Paso 1: Crear un ámbito personalizado" en el tema [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

3.  Cambie todas las asignaciones de funciones de administración que usen el ámbito anterior para que empleen el ámbito nuevo mediante el procedimiento "Use el Shell para cambiar el filtro de servidor o el ámbito basado en lista en una asignación de función" en el tema [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

4.  Quitar el ámbito anterior mediante el procedimiento en el tema [Quitar un ámbito de función](remove-a-role-scope-exchange-2013-help.md).

## Cambie un filtro de base de datos en un ámbito

Para cambiar el filtro de base de datos en un ámbito, use la siguiente sintaxis.

    Set-ManagementScope <scope name> -DatabaseRestrictionFilter { <new database filter> }

En este ejemplo, se cambia el filtro de base de datos de modo tal que coincida con todos los objetos de base de datos, donde la propiedad **Name** contiene la cadena "Ejecutivo".

    Set-ManagementScope "Database Executive Scope" -DatabaseRestrictionFilter { Name -Like "*Executive*" }

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementScope](https://technet.microsoft.com/es-es/library/dd297996\(v=exchg.150\)).

Para obtener más información acerca de los filtros de base de datos y para ver una lista de propiedades de base de datos filtrables, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

## Cambie la lista de base de datos en un ámbito

No puede cambiar la lista de base de datos en un ámbito. Si necesita cambiar la lista de base de datos, debe realizar las siguientes acciones:

1.  De ser necesario, recupere la lista de base de datos actual en el ámbito que se debe reemplazar mediante el procedimiento "Ver un ámbito específico" en el tema [Ver ámbitos de roles](view-role-scopes-exchange-2013-help.md).

2.  Cree un ámbito con la nueva lista de base de datos mediante el procedimiento "Paso 1: Cree un procedimiento de ámbito personalizado" en el tema [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

3.  Cambie todas las asignaciones de funciones de administración que usen el ámbito anterior para que empleen el ámbito nuevo mediante el procedimiento "Use el Shell para cambiar el filtro de base de datos o el ámbito basado en lista en una asignación de función" en el tema [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

4.  Quitar el ámbito anterior mediante el procedimiento en el tema [Quitar un ámbito de función](remove-a-role-scope-exchange-2013-help.md).

