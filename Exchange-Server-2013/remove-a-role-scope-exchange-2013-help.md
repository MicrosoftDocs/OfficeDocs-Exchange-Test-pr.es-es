---
title: 'Quitar un ámbito de función: Exchange 2013 Help'
TOCTitle: Quitar un ámbito de función
ms:assetid: ad17cba0-a8d3-4f40-b3c9-c37e6e5c3f36
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351051(v=EXCHG.150)
ms:contentKeyID: 49895832
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Quitar un ámbito de función

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-02_

Los ámbitos de funciones de administración determinan los objetos a los que puede tener acceso un usuario, que los puede cambiar mediante los cmdlets y los parámetros que estén asignados a dicho usuario. Si deja de usar un ámbito, se puede quitar. Para obtener más información acerca de los ámbitos de función de administración en Microsoft Exchange Server 2013, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Ámbitos de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Antes de poder quitar un ámbito, el ámbito se debe quitar de todas las asignaciones de funciones de administración que lo pudieran usar. Para obtener más información acerca de cómo quitar un ámbito de una asignación de función, consulte [Modificar una asignación de roles](change-a-role-assignment-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Uso del Shell para quitar un ámbito

Para quitar un ámbito, utilice la sintaxis siguiente.

    Remove-ManagementScope <scope name>

Por ejemplo, para quitar el ámbito de "Servidores de Dublín", utilice el siguiente comando.

    Remove-ManagementScope "Dublin Servers"

