---
title: 'Crear un rol sin ámbito: Exchange 2013 Help'
TOCTitle: Crear un rol sin ámbito
ms:assetid: 5a042ccf-4d5f-4609-a91b-21c20d1e6459
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd876886(v=EXCHG.150)
ms:contentKeyID: 49895646
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear un rol sin ámbito

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-06-09_

Se puede usar una función de administración sin ámbito para proporcionar acceso a los administradores y los usuarios expertos a los scripts de Windows PowerShell y a los cmdlets que no son Exchange. Puede crear una función de nivel superior sin ámbito y agregar scripts o cmdlets que no son Exchange a esa función o crear una función que se base en una función existente de nivel superior sin ámbito. Después de crear y personalizar una función sin ámbito, se la puede asignar a grupos de funciones de administración, usuarios y grupos de seguridad universales (USG). No se pueden asignar funciones sin ámbito a directivas de asignación de funciones de administración. Para obtener más información acerca de las funciones sin ámbito, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).


> [!WARNING]
> Las funciones sin ámbito pueden ser muy eficaces ya que, como lo indica su nombre, no se les aplica ningún ámbito de administración. Esto significa que los scripts y los cmdlets que no son Exchange que contienen se pueden ejecutar en cualquier objeto de su organización Exchange. Téngalo en cuenta cuando agregue scripts o cmdlets que no son Exchange a una función sin ámbito y cuando asigne la función sin ámbito.




> [!NOTE]
> Si desea crear una función que contenga cmdlets de Exchange, debe crear una función que se base en una función de administración existente. Para obtener más información acerca de cómo crear funciones con cmdlets deExchange, consulte <A href="create-a-role-exchange-2013-help.md">Crear un rol</A>.



¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - La capacidad para crear funciones sin ámbito no se incluye en ningún grupo de funciones de administración de manera predeterminada. Para que el usuario pueda crear un grupo de funciones, debe asignar primero la función Administración de funciones sin ámbito a un usuario, o a un USG o un grupo de funciones del cual el usuario es miembro. Para obtener más información acerca de la adición de una función a un usuario, grupo de seguridad universal o grupo de funciones, consulte los siguientes temas:
    
      - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)
    
      - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Crear una función de administración de nivel superior sin ámbito

Si desea que los scripts o los cmdlets que no son Exchange estén disponibles para los administradores o los expertos de su organización, debe crear una función de nivel superior sin ámbito. Los scripts y los cmdlets que no son Exchange solamente se pueden agregar a una función sin ámbito creada como función de nivel superior porque la función sin ámbito inicial no hereda de las otras funciones. La nueva función de nivel superior sin ámbito puede ser la función principal de otras funciones sin ámbito que también pueden usar los scripts y los cmdlets que no son Exchange agregados.

A continuación, figuran los pasos para crear una función de nivel superior sin ámbito:

## Paso 1: Crear la función de nivel superior sin ámbito

Las funciones de nivel superior sin ámbito no tienen una función principal. Debe especificar el conmutador de *UnscopedTopLevel* para crear una función sin una principal. Use la siguiente sintaxis para crear una nueva función.

```powershell
New-ManagementRole <name of new role> -UnscopedTopLevel
```

En este ejemplo, se crea la función de nivel superior sin ámbito de scripts de TI.

```powershell
New-ManagementRole "IT Scripts" -UnscopedTopLevel
```

Después de crearla, la función permanece vacía hasta que le agregue los scripts o los cmdlets que no son Exchange.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRole](https://technet.microsoft.com/es-es/library/dd298073\(v=exchg.150\)).

## Paso 2a: Agregar entradas de función de administración de script

Si desea agregar un script a una nueva función sin ámbito, use este paso. Si desea agregar un cmdlet que no es Exchange a la nueva función sin ámbito, use Step 2b.

Para agregar un script de Windows PowerShell a una función de nivel superior sin ámbito, debe agregar una entrada de función de administración a la función. La entrada de función contiene el nombre del script y los parámetros que desea poner a disposición en la función.

El script debe residir en el directorio `RemoteScripts` en la ruta de instalación de Microsoft Exchange Server 2013, en todos los servidores que ejecuten Exchange 2013 y a los cuales los usuarios puedan conectarse para ejecutar el script. Si un usuario tiene acceso para ejecutar un script, pero el script no se encuentra en el servidor de Exchange 2013 al cual se conecta el usuario, se produce un error. De manera predeterminada, la ruta al directorio `RemoteScripts` es C:\\Archivos de programa\\Microsoft\\Exchange Server\\V15\\RemoteScripts.

Después de que copia el script en los servidores de Exchange 2013 adecuados y decide cuáles parámetros de script se deben usar, cree la entrada de función mediante la siguiente sintaxis.

```powershell
Add-ManagementRoleEntry <unscoped top-level role name>\<script filename> -Parameters <parameter 1, parameter 2, parameter...> -Type Script -UnscopedTopLevel
```

En este ejemplo, se agrega el script BulkProvisionUsers.ps1 a la función scripts de TI con los parámetros *Name* y *Location*.

```powershell
Add-ManagementRoleEntry "IT Scripts\BulkProvisionUsers.ps1" -Parameters Name, Location -Type Script -UnscopedTopLevel
```


> [!NOTE]
> El cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza la validación básica para asegurarse de que agregue solamente los parámetros que existen en el script. No obstante, no se realiza otra validación después de que se agrega la entrada de función. Si los parámetros se agregan o quitan después, debe actualizar manualmente las entradas de función que contienen el script.



## Paso 2b: Agregar entradas de función de cmdlet que no son de Exchange

Si desea agregar un cmdlet que no es Exchange a la nueva función sin ámbito, use este paso. Si desea agregar un script a la nueva función sin ámbito, use Step 2a.

Para agregar cmdlet que no es Exchange a una función de nivel superior sin ámbito, debe agregar una entrada de función de administración a la función. La entrada de función contiene el complemento de cmdlet, el nombre del cmdlet y los parámetros del cmdlet que desea poner a disposición en la función.

Si agrega cmdlets que no son Exchange a la nueva función, los cmdlets se deben instalar en todos los servidores de Exchange 2013 en los cuales los usuarios puedan conectarse para ejecutar los cmdlets. Para saber cómo instalar y registrar correctamente los complementos de Windows PowerShell que contienen los cmdlets que desea usar, consulte la documentación para su producto.

Después de instalar el componente PowerShell de Windows que contiene los cmdlet en los servidores de Exchange 2013 adecuados y de decidir qué parámetros de cmdlet se deben usar, cree la entrada de función con la siguiente sintaxis.

```powershell
Add-ManagementRoleEntry <unscoped top-level role name>\<cmdlet name> -PSSnapinName <snap-in name> -Parameters <parameter 1, parameter 2, parameter...> -Type Cmdlet -UnscopedTopLevel
```

En este ejemplo, se agrega el cmdlet **Set-WidgetConfiguration** en el complemento Contoso.Admin.Cmdlets para la función de cmdlets de Widget con los parámetros *Database* y *Size*.

```powershell
Add-ManagementRoleEntry "Widget Cmdlets\Set-WidgetConfiguration" -PSSnapinName Contoso.Admin.Cmdlets -Parameters Database, Size -Type Cmdlet -UnscopedTopLevel
```


> [!NOTE]
> El cmdlet <STRONG>Add-ManagementRoleEntry</STRONG> realiza la validación básica para asegurarse de que agregue solamente los parámetros que existen en el cmdlet. No obstante, no se realiza otra validación después de que se agrega la entrada de función. Si el cmdlet se cambia más adelante y se agregan o quitan parámetros, debe actualizar manualmente las entradas de función que contienen el cmdlet.



## Paso 3: Asignar la función de administración

El último paso al crear y configurar una función es asignarla a un usuario al que se le asigna la función.


> [!IMPORTANT]
> Los ámbitos de administración no se pueden configurar en asignaciones de funciones que asignen una función sin ámbito. Ya sea que elija crear una asignación de función para un grupo de funciones, un usuario o un grupo de seguridad universal, debe elegir la opción para crear una asignación de función sin el ámbito de administración.



Puede asignar la nueva función a un grupo de funciones, un usuario o un grupo de seguridad universal. Para obtener más información al respecto, consulte los temas siguientes:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

## Crear una función sin ámbito basada en otra función sin ámbito

Si tiene una función de nivel superior sin ámbito existente u otras funciones sin ámbito que desee usar como base para las nuevas funciones sin ámbito, puede crear funciones secundarias sin ámbito. Las funciones secundarias sin ámbito pueden contener un subconjunto de los scripts y los cmdlets que existen en las funciones principales sin ámbito. Esto resulta útil, por ejemplo, si desea que solo un subconjunto de scripts o cmdlets esté disponible en una función principal sin ámbito para un administrador menos experimentado.

A continuación, figuran los pasos para crear una función secundaria sin ámbito:

## Paso 1: Crear la función secundaria sin ámbito

Las funciones secundarias sin ámbito nuevas se pueden basar en las funciones sin ámbito existentes. Cuando crea una función, la función existente y sus entradas de funciones de administración se copian en la función nueva. La función existente se convierte en la función principal de la función secundaria nueva. Si crea una función sin ámbito basada en otra función sin ámbito, debe elegir una función que contenga todos los cmdlets y los parámetros necesarios para usar y, luego, quitar los que no desea. Las funciones secundarias sin ámbito tienen entradas de funciones de administración que no existen en la función principal.


> [!NOTE]
> Si debe crear una función sin ámbito que contenga los scripts o los cmdlets que no son Exchange que no existen en ninguna otra función sin ámbito, cree una función de nivel superior sin ámbito. Para obtener más información, consulte Create an unscoped top-level management role, que figura anteriormente en este tema.



Use la siguiente sintaxis para crear una nueva función.

```powershell
New-ManagementRole -Parent <existing unscoped role to copy> -Name <name of new unscoped role>
```

En este ejemplo, se copia la función Scripts de TI global y sus entradas de funciones de administración en la función Scripts de TI de diagnóstico.

```powershell
New-ManagementRole -Parent "IT Global Scripts" -Name "Diagnostic IT Scripts"
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRole](https://technet.microsoft.com/es-es/library/dd298073\(v=exchg.150\)).

## Paso 2: Cambiar las entradas de funciones de administración de la función

Después de haber creado la función, deberá cambiar las entradas de la función. Puede eliminar una entrada de función completa, que elimina el acceso al script o al cmdlet que no es Exchange asociado por completo. O puede quitar los parámetros de una entrada de función para eliminar el acceso a esos parámetros específicos en el script o cmdlet que no es Exchange asociado.

No puede agregar entradas de función o parámetros a las entradas de función, a menos que existan en la función principal. Debido a que, en el Paso 1, acaba de crear una función a partir de la función principal, no puede agregar otras entradas de función ni parámetros en la función porque no existen en la función principal.

Cuando cambia una entrada de función de una función, puede realizar alguna de las siguientes acciones:

  - Quitar una única entrada de función completa.

  - Quitar varias entradas de función completas.

  - Quitar los parámetros de una entrada de función.

Para quitar entradas de función de una función nueva, consulte [Quitar una entrada de función de una función](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Paso 3: Asignar la función de administración

El último paso al crear y configurar una función es asignarla a un usuario al que se asigna la función.


> [!IMPORTANT]
> Los ámbitos de administración no se pueden configurar en asignaciones de funciones que asignen una función sin ámbito. Ya sea que elija crear una asignación de función para un grupo de funciones, un usuario o un grupo de seguridad universal, debe elegir la opción para crear una asignación de función sin el ámbito de administración.



Puede asignar la nueva función a un grupo de funciones, un usuario o un grupo de seguridad universal. Para obtener más información al respecto, consulte los temas siguientes:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

