---
title: 'Agregar entrada función a función nivel superior sin ámbito Exchange 2013 Help | Microsoft Docs'
TOCTitle: Agregar una entrada de función a una función de nivel superior sin ámbito
ms:assetid: 52fd3f20-c348-49d5-9bdb-f2cbf780cf2d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd979789(v=EXCHG.150)
ms:contentKeyID: 49895629
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregar una entrada de función a una función de nivel superior sin ámbito

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Puede agregar scripts y cmdlets que no son de Exchange a funciones de administración de nivel superior sin ámbito si desea que nuevos scripts o cmdlets que no son de Exchange estén disponibles para las funciones sin ámbito existentes. Estos scripts y cmdlets que no son de Exchange se agregan como entradas de función de administración a las funciones de administración de nivel superior sin ámbito. De esa manera, esas entradas de función de nivel superior sin ámbito o cualquier función sin ámbito derivada de funciones de nivel superior pueden usarlos. Para obtener más información acerca de las entradas de funciones sin ámbito, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> Si desea cambiar una entrada de función en una función de administración que contenga cmdlets de Exchange, consulte <A href="change-a-role-entry-exchange-2013-help.md">Cambiar una entrada de función</A>.



¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - La capacidad de agregar una entrada de función en una función de nivel superior sin ámbito no se incluye en ningún grupo de función de administración de manera predeterminada. Para que el usuario pueda agregar una entrada de función de nivel superior sin ámbito, debe asignar primero la función Administración de funciones sin ámbito a un usuario o a un grupo de seguridad universal (USG) o un grupo de función del cual el usuario es miembro. Para obtener más información acerca de la adición de una función a un grupo de funciones, un usuario o un grupo de seguridad universal, consulte los siguientes temas:
    
      - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)
    
      - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Agregar una entrada de función de script a una función de nivel superior sin ámbito

Si desea agregar un script a una función sin ámbito existente, use este procedimiento. Si desea agregar un cmdlet que no es de Exchange a una función sin ámbito existente, consulte "Agregar una entrada de función de cmdlet que no es de Exchange a una función de nivel superior sin ámbito" más adelante en este tema.

Para agregar un script de Windows PowerShell a una función de nivel superior sin ámbito, debe agregar una entrada de función de administración a la función. La entrada de función contiene el nombre del script y los parámetros que desea poner a disposición en la función.

El script debe residir en el directorio de scripts en la ruta de instalación de Microsoft Exchange Server 2013 en todos los servidores que ejecuten Exchange 2013 en los cuales los usuarios puedan conectarse para ejecutar el script. Si un usuario tiene acceso para ejecutar un script, pero el script no se encuentra en el servidor de Exchange 2013 al cual se conecta el usuario, se produce un error. De manera predeterminada, la ruta al directorio de scripts es C:\\Archivos de programa\\Microsoft\\Exchange Server\\V15\\Scripts.

Después de que copia el script en los servidores de Exchange 2013 adecuados y decide cuáles parámetros de script se deben usar, cree la entrada de función mediante la siguiente sintaxis.

    Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel

En este ejemplo, se agrega el script BulkProvisionUsers.ps1 a la función scripts de TI con los parámetros *Name* y *Location*.

    Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel


> [!NOTE]
> El cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza la validación básica para asegurarse de que agregue solamente los parámetros que existen en el script. No obstante, no se realiza otra validación después de que se agrega la entrada de función. Si los parámetros se agregan o quitan después, debe actualizar manualmente las entradas de función que contienen el script.



## Agregar una entrada de función de cmdlet que no es de Exchange a una función de nivel superior sin ámbito

Si desea agregar un cmdlet que no es de Exchange a una función sin ámbito existente, use este procedimiento. Si desea agregar un script a un rol sin ámbito, consulte "Agregar una entrada de función de script a una función de nivel superior sin ámbito" más arriba en este tema.

Para agregar cmdlet que no es Exchange a una función de nivel superior sin ámbito, debe agregar una entrada de función de administración a la función. La entrada de función contiene el complemento de cmdlet, el nombre del cmdlet y los parámetros del cmdlet que desea poner a disposición en la función.

Si agrega cmdlets que no son Exchange a la nueva función, los cmdlets se deben instalar en todos los servidores de Exchange 2013 en los cuales los usuarios puedan conectarse para ejecutar los cmdlets. Para saber cómo instalar y registrar correctamente los complementos de Windows PowerShell que contienen los cmdlets que desea usar, consulte la documentación para su producto.

Después de instalar el componente PowerShell de Windows que contiene los cmdlet adecuados en los servidores de Exchange 2013 y de decidir qué parámetros de cmdlet se deben usar, cree la entrada de función con la siguiente sintaxis.

    Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel

En este ejemplo, se agrega el cmdlet **Set-WidgetConfiguration** en el complemento Contoso.Admin.Cmdlets para la función de cmdlets de Widget con los parámetros *Database* y *Size*.

    Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel


> [!NOTE]
> El cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza la validación básica para asegurarse de que agregue solamente los parámetros que existen en el cmdlet. No obstante, no se realiza otra validación después de que se agrega la entrada de función. Si el cmdlet se cambia más adelante y se agregan o quitan parámetros, debe actualizar manualmente las entradas de función que contienen el cmdlet.



## Otras tareas

Después de agregar una entrada de función o una función de nivel superior sin ámbito, es posible que también desee realizar las siguientes tareas:

[Agregar una entrada de función a una función](add-a-role-entry-to-a-role-exchange-2013-help.md)

[Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

[Administrar miembros de grupos de roles](manage-role-group-members-exchange-2013-help.md)

[Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

[Quitar una función de un usuario o un grupo de seguridad universal](remove-a-role-from-a-user-or-usg-exchange-2013-help.md)

