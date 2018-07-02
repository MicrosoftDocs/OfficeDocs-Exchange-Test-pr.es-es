---
title: 'Crear un rol: Exchange 2013 Help'
TOCTitle: Crear un rol
ms:assetid: e614ad8f-5946-4135-b130-89ea626afcd4
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351214(v=EXCHG.150)
ms:contentKeyID: 49895983
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Crear un rol

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-17_

Puede crear una función de administración, cambiar las entradas de funciones de administración, agregar un ámbito si es preciso y, a continuación, asignar la función a un usuario. Raramente necesitará realizar este procedimiento. Se recomienda comprobar si es posible utilizar una función de administración integrada en lugar de crear una función de administración. Para obtener una lista de las funciones de administración integradas, vea [Roles de administración integrados](built-in-management-roles-exchange-2013-help.md).

Para obtener más información acerca de las funciones de administración en Microsoft Exchange Server 2013, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).


> [!NOTE]
> Este tema no aborda la creación de una función de administración sin ámbito. Para obtener más información acerca de cómo crear una función de administración sin ámbito, consulte <A href="create-an-unscoped-role-exchange-2013-help.md">Crear un rol sin ámbito</A>.



¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar este procedimiento: 10 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Cómo realiza esto?

## Paso 1: Crear la función de administración

Las nuevas funciones de administración se basan en las funciones existentes. Cuando crea una función, la función existente y sus entradas de funciones de administración se copian en la función nueva. La función existente se convierte en la función principal de la función secundaria nueva. Siempre debe elegir una función que contenga todos los cmdlets y parámetros que necesite utilizar, y eliminar los que no desee. Las funciones secundarias no pueden tener entradas de funciones de administración que no existan en la función principal.

Use la siguiente sintaxis para crear una nueva función.

    New-ManagementRole -Parent <existing role to copy> -Name <name of new role>

Este ejemplo copia la función de destinatarios de correo y sus entradas de función de administración en la función de destinatarios de correo de Seattle.

    New-ManagementRole -Parent "Mail Recipients" -Name "Seattle Mail Recipients"

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [New-ManagementRole](https://technet.microsoft.com/es-es/library/dd298073\(v=exchg.150\)).

## Paso 2: Cambiar las entradas de función de administración de la nueva función

Después de haber creado la función, deberá cambiar las entradas de la función. Puede eliminar una entrada de función completa, con lo cual se elimina el acceso al cmdlet asociado por completo. También puede eliminar los parámetros de una entrada de función para eliminar el acceso a esos parámetros específicos en el cmdlet asociado.

No puede agregar nuevos parámetros o entradas de funciones en las entradas de función, a menos que existan en la función principal. Debido a que, en el Paso 1, acaba de crear una función a partir de la función principal, no puede agregar otras entradas de función ni parámetros en la función porque no existen en la función principal.

Cuando cambia una entrada de función de una función, puede realizar alguna de las siguientes acciones:

  - Quitar una única entrada de función completa.

  - Quitar varias entradas de función completas.

  - Quitar los parámetros de una entrada de función.

Para quitar entradas de función de una función nueva, consulte [Quitar una entrada de función de una función](remove-a-role-entry-from-a-role-exchange-2013-help.md).

## Paso 3: Crear un ámbito de función de administración personalizado, si es necesario

Los ámbitos de funciones de administración determinan los objetos que un usuario puede ver o cambiar utilizando las entradas de función configuradas en el paso 2. Las nuevas funciones de administración heredan los ámbitos de función de administración de lectura y escritura de su función principal. Se denominan *ámbitos implícitos*. Sin embargo, en ocasiones puede ser necesario modificar el ámbito de escritura de la nueva función para que se adapte a sus necesidades empresariales. Cuando se crea un ámbito personalizado, se modifica el ámbito de escritura implícito de la función. El ámbito de lectura implícito de la función no cambia. Para obtener más información sobre los ámbitos de funciones de administración, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

Puede crear un ámbito personalizado, crear un ámbito exclusivo, utilizar un ámbito predefinido o crear un ámbito para una asignación de una unidad organizativa (OU). El nuevo ámbito debe estar dentro del ámbito de lectura implícito de la función. Para utilizar un ámbito predefinido o especificar una unidad organizativa, vaya al paso 4.

Para agregar un ámbito personalizado a su nueva función, vea [Crear un ámbito normal o exclusivo](create-a-regular-or-exclusive-scope-exchange-2013-help.md).

## Paso 4: Asignar la nueva función de administración

El último paso al crear y configurar una función es asignarla a un usuario al que se asigna la función.

Cuando crea una asignación de función, puede realizar una de las siguientes acciones:

  - Crear la asignación de funciones sin ningún ámbito.

  - Crear la asignación de funciones con un ámbito predefinido.

  - Crear la asignación de funciones con una unidad organizativa sin un filtro de restricción de dominio.

  - Cree la asignación de funciones con el ámbito personalizado o exclusivo que creó en el paso 3.
    

    > [!NOTE]
    > No puede especificar un ámbito cuando crea una asignación entre una función y una directiva de asignación de funciones de administración.



Puede asignar la nueva función a un grupo de funciones, una directiva de asignación de funciones o un grupo de seguridad universal (USG). Para obtener más información al respecto, consulte los temas siguientes:

  - [Administrar grupos de roles](manage-role-groups-exchange-2013-help.md)

  - [Administrar directivas de asignación de funciones](manage-role-assignment-policies-exchange-2013-help.md)

  - [Agregar una función a un usuario o grupo de seguridad universal](add-a-role-to-a-user-or-usg-exchange-2013-help.md)

