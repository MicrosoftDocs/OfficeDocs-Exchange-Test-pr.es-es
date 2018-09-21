---
title: 'Agregar una entrada de función a una función: Exchange 2013 Help'
TOCTitle: Agregar una entrada de función a una función
ms:assetid: 30cd37bc-b3e8-4f39-a8ba-a4c20b1b27b7
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335180(v=EXCHG.150)
ms:contentKeyID: 49895551
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Agregar una entrada de función a una función

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-04_

Si desea permitir el acceso a cmdlet, necesitará agregar la entrada de la función de administración asociada a la función de administración. Después de agregar la entrada de función a la función, los usuarios asignados a la función podrán tener acceso a ese cmdlet. Para obtener más información acerca de las entradas de funciones de administración en Microsoft Exchange Server 2013, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

No puede agregar entradas de función a las funciones integradas. Si desea personalizar funciones, debe crear una nueva función. Para obtener información acerca de cómo crear una función nueva, vea [Crear un rol](create-a-role-exchange-2013-help.md).


> [!NOTE]
> Este tema no describe cómo agregar entradas de administración sin ámbito a una función de administración sin ámbito. Para obtener más información acerca de cómo crear entradas de función sin ámbito, consulte <A href="add-a-role-entry-to-an-unscoped-top-level-role-exchange-2013-help.md">Agregar una entrada de función a una función de nivel superior sin ámbito</A>.



¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Una entrada de función que desea agregar a una función de administración debe existir en esa función de administración principal inmediata de la función.

  - Este tema hace uso de canalización. Para obtener más información acerca de la canalización, consulte [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\)).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Agregar una entrada de función única de una función primaria

Puede agregar una entrada de función a una función exactamente como aparece en la función primaria al utilizar la siguiente sintaxis.

```powershell
Add-ManagementRoleEntry <child role name>\<cmdlet>
```

En este ejemplo, se agrega el cmdlet de **Set-Mailbox** a la función de administradores de destinatarios.

```powershell
Add-ManagementRoleEntry "Recipient Administrators\Set-Mailbox"
```

Este comando comprueba la función principal y, si la entrada de la función existe, la agrega a la función secundaria. Si la entrada de la función ya existe en la función secundaria, puede incluir el parámetro *Overwrite* para sobrescribir la entrada de función existente.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Add-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351236\(v=exchg.150\)).

## Agregar una entrada de función única de una función primaria e incluir solamente parámetros específicos

Si desea agregar una entrada de función de una función primaria, pero desea incluir solamente parámetros específicos en la entrada de función en la función secundaria, utilice la siguiente sintaxis.

    Add-ManagementRoleEntry <child role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>

En este ejemplo, se agrega el cmdlet **Set-Mailbox** a la función de Servicio de asistencia, pero incluye solamente los parámetros *DisplayName* y *EmailAddresses* en la entrada en la función secundaria.

```powershell
Add-ManagementRoleEntry "Help Desk\Set-Mailbox" -Parameters DisplayName, EmailAddresses
```

Este comando comprueba la función principal y, si la entrada de la función existe, la agrega a la función secundaria. Si la entrada de la función ya existe en la función secundaria, puede incluir el parámetro *Overwrite* para sobrescribir la entrada de función existente.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Add-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351236\(v=exchg.150\)).

## Agregar varias entradas de la función de una función primaria

Si desea agregar más de una entrada de función a una función, deberá recuperar una lista de las entradas de la función que existe en la función primaria que desea agregar a la función secundaria, y luego, agregarlas a la función secundaria. Para hacer esto, debe recuperar la lista de las entradas de función en una función primaria al usar el cmdlet **Get-ManagementRoleEntry**. A continuación, canalice los resultados del cmdlet **Get-ManagementRoleEntry** al cmdlet **Add-ManagementRoleEntry**. Para recuperar varias entradas de la función, deberá utilizar el carácter comodín (\*).

Para agregar múltiples entradas de una función primaria a una función secundaria, use la siguiente sintaxis.

    Get-ManagementRoleEntry <parent role name>\*<partial cmdlet name>* | Add-ManagementRoleEntry -Role <child role name>

En este ejemplo, se agrega todas las entradas de la función que contiene la cadena `Mailbox` en el nombre de cmdlet en la función primaria de Destinatarios de correo a la función secundaria de Destinatarios de correo de Seattle.

    Get-ManagementRoleEntry "Mail Recipients\*Mailbox*" | Add-ManagementRoleEntry -Role "Seattle Mail Recipients"

Si las entradas de la función ya existen en la función secundaria, puede incluir el parámetro *Overwrite* para sobrescribir las entradas de función existentes.

Para obtener más información acerca de cómo recuperar una lista de entradas de la función de administración, vea [Ver entradas de papel](view-role-entries-exchange-2013-help.md).

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)) y [Add-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351236\(v=exchg.150\)).

