---
title: 'Quitar una función: Exchange 2013 Help'
TOCTitle: Quitar una función
ms:assetid: 2fb6f453-f37a-4636-8353-3f9927f81298
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335178(v=EXCHG.150)
ms:contentKeyID: 49895549
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar una función

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Las funciones de administración que ya no se requieren pueden ser eliminadas de la organización. Un usuario solamente puede quitar las funciones de administración que definió. No se pueden quitar las funciones de administración integradas. Para obtener más información acerca de las funciones de administración en Microsoft Exchange Server 2013, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Antes de quitar la función de administración, debe eliminar todas las asignaciones de función de administración. Si desea obtener más información sobre cómo quitar una asignación de función, consulte [Quitar una función de un usuario o un grupo de seguridad universal](remove-a-role-from-a-user-or-usg-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Quitar una función de administración sin funciones secundarias

Para quitar una función sin funciones secundarias, use la siguiente sintaxis.

```powershell
Remove-ManagementRole <role name>
```

En este ejemplo, se quita la función Administrador de servidor de Seattle.

```powershell
Remove-ManagementRole "Seattle Server Administrators"
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Remove-ManagementRole](https://technet.microsoft.com/es-es/library/dd351170\(v=exchg.150\)).

## Quitar una función de administración con funciones secundarias

Si una función que desea quitar tiene funciones secundarias, debe también eliminar todas las funciones secundarias. Recibirá un mensaje de error si intenta quitar una función que tiene funciones secundarias, a menos que utilice el modificador *Recurse*. Si usa el modificador *Recurse* al quitar una función, se eliminarán la función que especifique y todas sus las funciones secundarias.


> [!WARNING]
> Si usa el modificador <EM>Recurse</EM>, todas las funciones secundarias de la función especificada que desee quitar también serán eliminadas. Asegúrese de tener en cuenta qué funciones serán eliminadas antes de ejecutar este comando.



Para asegurarse de que solamente quitará las funciones que desea, use el modificador *WhatIf* con el comando para comprobar que todo esté correcto. Use la siguiente sintaxis.

```powershell
Remove-ManagementRole <role name> -Recurse -WhatIf
```

El modificador *WhatIf* ejecuta el comando sin realizar ningún cambio e informa qué funciones hubiera eliminado. Para obtener más información sobre el modificador *WhatIf*, consulte [Modificadores WhatIf, Confirm y ValidateOnly](whatif-confirm-and-validateonly-switches-exchange-2013-help.md).

Después de confirmar que solo se eliminarán las funciones que desea, ejecute el mismo comando sin el modificador *WhatIf*. En este ejemplo, se quita la función Administrador de Londres y todas sus funciones secundarias.

```powershell
Remove-ManagementRole "London Administrators" -Recurse
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-ManagementRole](https://technet.microsoft.com/es-es/library/dd351170\(v=exchg.150\)).

## Quitar una función de administración sin ámbito

Para eliminar una función sin ámbito, se pueden aplicar los mismos procedimientos anteriormente utilizados en este tema proporcionados en Remove a management role with no child roles y Remove a management role with child roles. La única diferencia es que cuando elimina una función sin ámbito, debe especificar el modificador *UnScopedTopLevel* al ejecutar este comando. En este ejemplo, se quita una función sin ámbito y todas sus funciones secundarias.

```powershell
Remove-ManagementRole "Custom IT Scripts" -Recurse -UnScopedTopLevel
```

Al quitar otras funciones, debe utilizar el modificador *WhatIf* para comprobar que se están quitando las funciones correctas.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Remove-ManagementRole](https://technet.microsoft.com/es-es/library/dd351170\(v=exchg.150\)).

