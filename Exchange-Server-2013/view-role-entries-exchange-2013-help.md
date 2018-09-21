---
title: 'Ver entradas de papel: Exchange 2013 Help'
TOCTitle: Ver entradas de papel
ms:assetid: d9bb0d14-db59-456c-8f50-a8d7f7323df9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351179(v=EXCHG.150)
ms:contentKeyID: 49895951
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver entradas de papel

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Cada entrada de función de administración representa un solo cmdlet o una secuencia de comandos. Los parámetros que se incluyen en una entrada de función determinan los parámetros del cmdlet o de la secuencia de comandos a los que el usuario puede obtener acceso.

La identidad de las entradas de funciones consta del nombre de la función de administración a la que está asociada la entrada de función y de la secuencia de comandos o cmdlet al que hace referencia la entrada de función. Para obtener más información acerca de las entradas de funciones de Microsoft Exchange Server 2013, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con las entradas de funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - En este tema se habla sobre la canalización, el cmdlet de **Format-List**, los objetos y las propiedades. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:
    
      - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))
    
      - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)
    
      - [Datos estructurados](https://technet.microsoft.com/es-es/library/aa996386\(v=exchg.150\))

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Visualización de una lista de entradas de funciones

Puede usar el cmdlet **Get-ManagementRoleEntry** para recuperar una lista de entradas de funciones. Cuando use el cmdlet **Get-ManagementRoleEntry**, deberá especificar un valor que contenga el nombre de la función que contiene las entradas de funciones que desea que aparezcan en la lista y el nombre del cmdlet de la entrada de función que desea que aparezca en la lista. Si combina el nombre de la función y el nombre del cmdlet con el carácter comodín (\*), puede recuperar listas amplias o específicas de entradas de funciones.

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)).

## Visualización de una lista con todas las entradas de funciones de una función

Para ver una lista con todas las entradas de funciones de una función determinada, use la sintaxis siguiente.

    Get-ManagementRoleEntry <role name>\*

En este ejemplo se recuperan todas las entradas de funciones de la función `Recipient Administrators`.

    Get-ManagementRole "Recipient Administrators\*"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)).

## Visualización de una lista de funciones que contienen una entrada de función determinada

Para ver una lista con todas las funciones que contienen una entrada de función determinada, use la sintaxis siguiente.

    Get-ManagementRoleEntry *\<cmdlet name>

En este ejemplo se recuperan todas las funciones que contienen la entrada de función **Set-Mailbox**.

    Get-ManagementRoleEntry *\Set-Mailbox

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)).

## Visualización de una lista de funciones que contienen entradas de funciones similares

Para ver una lista con todas las funciones que contienen cmdlets con nombres similares, use la sintaxis siguiente.

    Get-ManagementRoleEntry *<partial role name>*\*<partial cmdlet name>*

En este ejemplo se devuelve una lista de las entradas de funciones que contienen la cadena `Mailbox` y que se encuentran en funciones que contienen la cadena `Tier 1` en el nombre.

    Get-ManagementRoleEntry "*Tier 1*\*Mailbox*"

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)).

## Visualización de una sola entrada de función

Para ver los detalles de un solo grupo de funciones, use la sintaxis siguiente.

```powershell
Get-ManagementRoleEntry <role name>\<cmdlet name> | Format-List
```

En este ejemplo se recuperan los detalles de la función de entrada **Set-Mailbox** en la función `Recipient Administrators`.

```powershell
Get-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" | Format-List
```

Si la entrada de función que ve tiene demasiados parámetros para indicar usando el cmdlet **Format-List**, consulte la sección "Visualización de los parámetros de una sola entrada de función" más adelante en este mismo tema.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)).

## Visualización de los parámetros de una sola entrada de función

Algunas entradas de función tienen más parámetros de los que se pueden ver canalizando el resultado del cmdlet **Get-ManagementRoleEntry** al cmdlet **Format-List**. Si necesita ver todos los parámetros de una entrada de función, deberá obtener acceso directamente a la propiedad **Parameters** del objeto de entrada de función.

Para ver los parámetros almacenados en la propiedad **Parameters** de un objeto de entrada de función, use la sintaxis siguiente.

    (Get-ManagementRoleEntry <role name>\<cmdlet name>).Parameters

En este ejemplo se recuperan los parámetros de la entrada de función **Set-Mailbox** en la función de destinatarios de correo.

    (Get-ManagementRoleEntry "Mail Recipients\Set-Mailbox").Parameters

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd335210\(v=exchg.150\)).

