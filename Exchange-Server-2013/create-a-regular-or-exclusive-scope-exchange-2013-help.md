---
title: 'Crear un ámbito normal o exclusivo: Exchange 2013 Help'
TOCTitle: Crear un ámbito normal o exclusivo
ms:assetid: b97a5be3-15cc-4954-ba30-a824a95e21be
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351083(v=EXCHG.150)
ms:contentKeyID: 49895865
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Crear un ámbito normal o exclusivo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-07_

Los ámbitos de función de administración determinan qué objetos estarán disponibles para un usuario de modo que los objetos se puedan cambiar mediante el uso de parámetros y cmdlets asignados a éstos. Si agrega un ámbito de administración, puede configurar las asignaciones de los roles de administración de manera que los usuarios administren servidores, bases de datos, destinatarios y otros objetos de su organización pero que no tengan permiso para modificar otros objetos.


> [!IMPORTANT]
> Cuando crea un ámbito normal o exclusivo, invalida el ámbito de escritura que se define en la función de administración que va a asignar. No se puede invalidar el ámbito de lectura que está configurado en la función de administración.



Puede crear un ámbito personalizado y agregar o cambiar una asignación de roles de administración. Si desea crear una asignación de función de administración con un ámbito de administración integrado previamente o de una unidad organizativa (OU), consulte [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md).

Para obtener más información sobre los ámbitos y las asignaciones de funciones de administración en Microsoft Exchange Server 2013, consulte los siguientes temas:

  - [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md)

  - [Descripción de las asignaciones de funciones de administración](understanding-management-role-assignments-exchange-2013-help.md)

¿Está buscando otras tareas de administración relacionadas con ámbitos? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Ámbitos de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Crear un ámbito personalizado

Para crear un ámbito personalizado, elija uno de los siguientes tipos de ámbito.

## Ámbito de filtro de destinatarios

Los ámbitos basados en filtros de destinatarios se crean usando el parámetro *RecipientRestrictionFilter* del cmdlet **New-ManagementScope**. Cuando crea un filtro de destinatarios, además de las propiedades de los destinatarios para filtrar, puede especificar la OU en la que se ejecutará el filtro. Si especifica una OU básica, limita aún más el ámbito de escritura de la función.

Para obtener más información acerca de los filtros de ámbitos de administración, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

Use la sintaxis siguiente para crear un ámbito de filtro con restricción de dominio referida a una OU.

    New-ManagementScope -Name <scope name> -RecipientRestrictionFilter <filter query> [-RecipientRoot <OU>]

En este ejemplo se crea un ámbito que incluye todos los buzones de la OU contoso.com/Sales.

    New-ManagementScope -Name "Mailboxes in Sales OU" -RecipientRestrictionFilter { RecipientType -eq 'UserMailbox' } -RecipientRoot "contoso.com/Sales OU"


> [!NOTE]
> Puede omitir el parámetro <EM>RecipientRoot</EM> si desea que el filtro se aplique a todo el ámbito de lectura implícito de la función de administración y no sólo a una OU concreta.



Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Ámbito de configuración del filtro de servidor

Los ámbitos de configuración basados en filtros de servidores se crean usando el parámetro *ServerRestrictionFilter* del cmdlet **New-ManagementScope**. Un filtro de servidores le permite crear un ámbito que se aplica únicamente a los servidores que se correspondan con el filtro que especifique.

Para obtener más información acerca de los filtros de ámbito de administración y ver una lista de propiedades filtrables del servidor, consulte[Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

Use la sintaxis siguiente para crear un ámbito de filtro de servidor.

```powershell
New-ManagementScope -Name <scope name> -ServerRestrictionFilter <filter query>
```

En este ejemplo se crea un ámbito que incluye todos los servidores dentro del sitio AD 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' (Active Directory).

    New-ManagementScope -Name "Servers in Seattle AD site" -ServerRestrictionFilter { ServerSite -eq 'CN=Redmond,CN=Sites,CN=Configuration,DC=contoso,DC=com' }

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Ámbito de configuración de listas de servidores

Los ámbitos de configuración basados en listas de servidores se crean usando el parámetro *ServerList* del cmdlet **New-ManagementScope**. Un ámbito basado en listas de servidores permite crear un ámbito que se aplica únicamente a los servidores que se especifiquen en una lista.

Use la sintaxis siguiente para crear un ámbito basado en listas de servidores.

```powershell
New-ManagementScope -Name <scope name> -ServerList <server 1>, <server 2...>
```

En este ejemplo se crea un ámbito que se aplica sólo a MBX1, MBX3 y MBX5.

```powershell
New-ManagementScope -Name "Mailbox servers" -ServerList MBX1,MBX3,MBX5
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Ámbito de configuración del filtro de base de datos

Los ámbitos de configuración basados en filtros de base de datos se crean usando el parámetro *DatabaseRestrictionFilter* del cmdlet **New-ManagementScope**. Un filtro de base de datos permite crear un ámbito que se aplica únicamente a las bases de datos que se correspondan con el filtro que se especifique.


> [!IMPORTANT]
> Las asignaciones de funciones asociadas con ámbitos de base de datos se aplican solo a los usuarios que se conectan a servidores que utilizan Microsoft Exchange Server 2010 Service Pack 1 (SP1) o superiores o Exchange&nbsp;2013. Si un usuario con una asignación de funciones asociada con un ámbito de base de datos se conecta a una versión anterior del servidor Exchange 2010 SP1, la asignación de funciones no se aplica al usuario y este no goza de ninguno de los permisos concedidos por la asignación de funciones.



Para obtener más información acerca de los filtros de ámbito de administración y ver una lista de propiedades de base de datos que se pueden filtrar, consulte [Descripción de los filtros de ámbito de los roles de administración](understanding-management-role-scope-filters-exchange-2013-help.md).

Use la sintaxis siguiente para crear un filtro de restricción de base de datos.

```powershell
New-ManagementScope -Name <scope name> -DatabaseRestrictionFilter <filter query>
```

En este ejemplo se crea un ámbito que incluye todas las bases de datos que contienen la cadena "Ejecutivo" en la propiedad **Name** de la base de datos.

    New-ManagementScope -Name "Executive Databases" -DatabaseRestrictionFilter { Name -Like '*Executive*' }

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Ámbito de configuración de listas de bases de datos

Los ámbitos de configuración basados en listas de bases de datos se crean usando el parámetro *DatabaseList* del cmdlet **New-ManagementScope**. Un ámbito basado en listas de bases de datos permite crear un ámbito que se aplica únicamente a las bases de datos que se especifiquen en una lista.


> [!IMPORTANT]
> Las asignaciones de funciones asociadas con ámbitos de base de datos se aplican solo a los usuarios que se conectan a servidores que utilizan Microsoft Exchange Server 2010 Service Pack 1 (SP1) o superiores o Exchange&nbsp;2013. Si un usuario con una asignación de funciones asociada con un ámbito de base de datos se conecta a una versión anterior del servidor Exchange 2010 SP1, la asignación de funciones no se aplica al usuario y este no goza de ninguno de los permisos concedidos por la asignación de funciones.



Use la sintaxis siguiente para crear un ámbito basado en listas de bases de datos.

```powershell
New-ManagementScope -Name <scope name> -DatabaseList <database 1>, <database 2...>
```

En este ejemplo se crea un ámbito que se aplica solo a las bases de datos Database 1, Database 2 y Database 3.

```powershell
New-ManagementScope -Name "Primary databases" -DatabaseList "Database 1", "Database 2", "Database 3"
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Ámbito exclusivo

Cualquier ámbito que cree con el cmdlet **New-ManagementScope** puede llamarse ámbito exclusivo. Para crear un ámbito exclusivo, use los mismos comandos que en las secciones anteriores para crear un ámbito basado en filtros de destinatarios, un ámbito basado en filtros de servidores, un ámbito basado en lista de servidores, un ámbito basado en filtros de bases de datos o un ámbito basado en listas de bases de datos y agregue el modificador *Exclusive* al comando.


> [!WARNING]
> Cuando crea ámbitos de administración exclusivos, solo las personas a las que se han asignado funciones en ámbitos exclusivos que contienen objetos que se van a modificar pueden tener acceso a esos objetos. Solo aquellos administradores a los que se ha asignado una función con ámbito exclusivo puede acceder a dichos objetos exclusivos o protegidos.



En ese ejemplo se crea un ámbito exclusivo basado en un filtro de destinatarios que solo incluye a los usuarios en el departamento "Executives".

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive

Cuando se crea un ámbito exclusivo, se le solicita que reconozca que ha creado un ámbito exclusivo y que es consciente de los efectos que un ámbito exclusivo tiene en las asignaciones de roles no exclusivas ya existentes. Si desea suprimir la advertencia, puede usar el conmutador *Force*. En este ejemplo se crea el mismo ámbito que en el ejemplo anterior, pero sin advertencia.

    New-ManagementScope "Executive Users Exclusive Scope" -RecipientRestrictionFilter { Department -Eq "Executives" } -Exclusive -Force

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementScope](https://technet.microsoft.com/es-es/library/dd335137\(v=exchg.150\)).

## Paso 2: Agregar o cambiar una asignación de funciones de administración

Una vez creado el ámbito, debe agregarlo a una asignación de funciones de administración nueva o existente.

Si ha creado un ámbito de administración y desea agregarlo a una nueva asignación de roles de administración que va a crear, consulte los temas siguientes:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

Si ha creado un ámbito de administración y desea agregarlo a una asignación de funciones de administración existente, consulte los temas siguientes:

  - [Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md)

  - [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md)

