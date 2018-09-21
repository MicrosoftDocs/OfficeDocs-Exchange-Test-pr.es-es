---
title: 'Quitar una entrada de función de una función: Exchange 2013 Help'
TOCTitle: Quitar una entrada de función de una función
ms:assetid: 4736367a-750f-44d3-8a20-5149bd35e9ff
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd297947(v=EXCHG.150)
ms:contentKeyID: 49895606
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una entrada de función de una función

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Las entradas de funciones de administración en una función de administración determinan cmdlets y los parámetros disponibles en una función de administración. Si quita las entradas o los parámetros de función en una entrada de función, puede restringir las acciones que pueden realizar los usuarios asignados a esa función de administración. Para obtener más información acerca de las entradas de funciones de administración en Microsoft Exchange Server 2013, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Cómo quitar una entrada de función de una función

Al quitar una entrada de función de una función, los usuarios asignados a dicha función pierden la capacidad de obtener acceso al cmdlet o la secuencia de comandos asociado.

Para quitar toda una entrada de función de administración de una función, emplee la sintaxis siguiente.

```powershell
Remove-ManagementRoleEntry <management role>\<management role entry>
```

En este ejemplo, el cmdlet **Enable-MailUser** se quita de la función Administradores de servidores de Seattle.

```powershell
Remove-ManagementRoleEntry "Seattle Server Administrators\Enable-MailUser"
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Remove-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351187\(v=exchg.150\)).

## Cómo quitar varias entradas de función de una función

Al quitar varias entradas de función de una función, los usuarios asignados a dicha función pierden la capacidad de obtener acceso a los cmdlets o las secuencias de comandos asociados.

Para quitar varias entradas de función de una función, debe obtener la lista de entradas de función que quitar mediante el cmdlet **Get-ManagementRoleEntry**. A continuación, debe canalizar la salida al cmdlet **Remove-ManagementRoleEntry**. Puede usar los caracteres comodín con el cmdlet **Get-ManagementRoleEntry** para coincidir con varias entradas de función. Es aconsejable usar el parámetro *WhatIf* para comprobar que esté quitando las entradas de función correctas. Use la siguiente sintaxis.

    Get-ManagementRoleEntry <management role>\<role entry with wildcard character> | Remove-ManagementRoleEntry -WhatIf

En este ejemplo, se quitan todas las entradas de función que contienen el diario de palabras de la función Administradores de servidores de Seattle.

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry -WhatIf

Si ejecuta el comando con el parámetro *WhatIf*, el cmdlet genera una lista con todas las entradas de función que se van a borrar. Si la lista es correcta, ejecute el comando de nuevo, está vez sin el parámetro *WhatIf*, para quitar las entradas de función.

    Get-ManagementRoleEntry "Seattle Server Administrators\*Journal*" | Remove-ManagementRoleEntry

Para obtener más información acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)) y [Remove-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351187\(v=exchg.150\)).

## Cómo quitar parámetros de una entrada de función en una función

Si quita parámetros de una entrada de función en una función, los usuarios asignados a esa función ya no pueden obtener acceso a ellos.

Para quitar parámetros de una entrada de función, emplee la sintaxis siguiente.

    Set-ManagementRoleEntry <management role>\<role entry> -Parameters <parameter 1>,<parameter 2...> -RemoveParameter

En este ejemplo, se quitan los parámetros *MaxSafeSenders*, *MaxSendSize*, *SecondaryAddress* y *UseDatabaseQuotaDefaults* de la entrada de función **Set-Mailbox** en la función Administradores de servidores de Seattle.

    Set-ManagementRoleEntry "Seattle Server Administrators\Set-Mailbox" -Parameters MaxSafeSenders,MaxSendSize,SecondaryAddress,UseDatabaseQuotaDefaults -RemoveParameter

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

