---
title: 'Cambiar una entrada de función: Exchange 2013 Help'
TOCTitle: Cambiar una entrada de función
ms:assetid: 5aa4f39c-16a4-4815-ac4f-2cdcfa2b3ee1
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd298005(v=EXCHG.150)
ms:contentKeyID: 49895648
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cambiar una entrada de función

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2012-10-03_

Cada entrada de función de administración en una función de administración representa un solo cmdlet. Al agregar o quitar parámetros de una entrada de función que luego se agrega a una función de administración, se controla si esos parámetros están disponibles en ese cmdlet. Para obtener más información acerca de las entradas de funciones de administración en Microsoft Exchange Server 2013, consulte [Descripción de los roles de administración](understanding-management-roles-exchange-2013-help.md).

No se pueden modificar las entradas de función en funciones integradas de administración.


> [!NOTE]
> En este tema, no se explica cómo modificar entradas de función de administración sin ámbito en una función de administración sin ámbito. Para obtener más información acerca de cómo modificar entradas de función sin ámbito, consulte <A href="create-a-role-exchange-2013-help.md">Crear un rol</A>.




> [!WARNING]
> Para agregar o quitar parámetros de una entrada de función, debe usar los parámetros <EM>AddParameter</EM> o <EM>RemoveParameter</EM>. Si omite el parámetro <EM>AddParameter</EM> o <EM>RemoveParameter</EM> al ejecutar el cmdlet <STRONG>Set-ManagementRoleEntry</STRONG>, solo se incluirán en la entrada de función los parámetros especificados mediante <EM>Parameters</EM>. Se quitarán todos los demás parámetros de la entrada de función.



¿Está buscando otras tareas de administración relacionadas con funciones? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Funciones de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Si desea agregar parámetros a una entrada de función, los parámetros que agregue deben existir en la entrada de función de la función principal. Los parámetros también deben existir en el cmdlet que especifique.

  - Si desea quitar parámetros de una entrada de función, los parámetros que quite no pueden existir en entradas de función de ninguna función secundaria. Debe quitar los parámetros de las entradas de función de las funciones secundarias. Use el procedimiento "Usar el Shell para quitar uno o más parámetros de una entrada de función" que figura más adelante en este tema, a fin de quitar los parámetros de entradas de función de todas las funciones secundarias.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para agregar uno o más parámetros a una entrada de función

Para agregar parámetros a una entrada de función, debe especificar los parámetros que desea agregar con el parámetro *Parameters*. Luego debe especificar el parámetro *AddParameter* para indicar que desea realizar una operación de adición.

Para agregar parámetros a una entrada de función, use la siguiente sintaxis.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -AddParameter
```

En este ejemplo, se agregan los parámetros *EmailAddresses* y *Type* al cmdlet **Set-Mailbox** en la función Administradores de destinatarios.

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-Mailbox" -Parameters EmailAddresses, Type -AddParameter
```

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

## Use el Shell para quitar uno o más parámetros de una entrada de función

Para quitar parámetros de una entrada de función, debe especificar los parámetros que desea quitar con el parámetro *Parameters*. Luego debe especificar el parámetro *RemoveParameter* para indicar que desea realizar una operación de eliminación.

Para quitar parámetros de una entrada de función, use la siguiente sintaxis.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...> -RemoveParameter
```

En este ejemplo, se quitan los parámetros *Port*, *ProtocolLoggingLevel* y *SmartHostAuthMechanism* del cmdlet **Set-SendConnector** en la función Administrador de servidores de nivel 1.

```powershell
Set-ManagementRoleEntry "Tier 1 Server Administrators\Set-SendConnector" -Parameters Port, ProtocolLoggingLevel, SmartHostAuthMechanism -RemoveParameter
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

## Usar el Shell para quitar todos los parámetros de una entrada de función

Para quitar todos los parámetros de una entrada de función, debe especificar el valor `$Null` en el parámetro *Parameters*. No es necesario incluir el parámetro *RemoveParameters*.

Quitar todos los parámetros de una entrada de función resulta muy útil cuando desea que solo algunos parámetros estén disponibles en un cmdlet y que todos los demás se excluyan. Si no desea que la función tenga acceso a un cmdlet, quite la entrada de función asociada por completo de la función en lugar de quitar solamente los parámetros. Para obtener más información acerca de cómo quitar una entrada de función de una función, consulte [Quitar una entrada de función de una función](remove-a-role-entry-from-a-role-exchange-2013-help.md).


> [!WARNING]
> No puede deshacer las operaciones en las que se quitan elementos. Si, por error, quita todos los parámetros de una entrada de función, debe agregarlos nuevamente de forma manual.



Para quitar todos los parámetros de una entrada de función, use la siguiente sintaxis.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters $Null 
```

En este ejemplo se quitan todos los parámetros del cmdlet **Set-CASMailbox** en el rol de administradores de destinatarios.

```powershell
Set-ManagementRoleEntry "Recipient Administrators\Set-CASMailbox" -Parameters $Null 
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

## Usar el Shell para aplicar un conjunto específico de parámetros

Si desea que se incluya solo un conjunto de parámetros específico en una entrada de función, especifique sólo el parámetro *Parameters*. No incluya los parámetros *AddParameter* ni *RemoveParameter*. Cuando solamente especifica el parámetro *Parameters*, solo los parámetros que especifique en el comando se incluirán en la entrada de función. El resto de parámetros se quitan.

Para especificar un conjunto de parámetros, use la siguiente sintaxis.

```powershell
Set-ManagementRoleEntry <role name>\<cmdlet> -Parameters <parameter 1>, <parameter 2>, <parameter...>
```

En este ejemplo, se incluyen solo los parámetros *Identity*, *DisplayName*, *MissedCallNotificationEnabled* y *PersonalAuthAttendantEnabled* en el cmdlet **Set-UMMailbox** en la función Grupo de destinatarios de Seattle.

```powershell
Set-ManagementRoleEntry "Seattle Mail Recipients\Set-UMMailbox" -Parameters Identity, DisplayName, MissedCallNotificationEnabled, PersonalAutoAttendantEnabled
```

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-ManagementRoleEntry](https://technet.microsoft.com/es-es/library/dd351162\(v=exchg.150\)).

