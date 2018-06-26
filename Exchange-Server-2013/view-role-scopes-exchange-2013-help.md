---
title: 'Ver ámbitos de roles: Exchange 2013 Help'
TOCTitle: Ver ámbitos de roles
ms:assetid: 0bb3a434-6651-473a-94eb-4eb9a34e6f70
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335084(v=EXCHG.150)
ms:contentKeyID: 49895467
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ver ámbitos de roles

 

_**Se aplica a:**Exchange Server 2013_

_**Última modificación del tema:**2012-10-03_

Los ámbitos de función de administración determinan qué objetos estarán disponibles para un usuario de modo que los objetos se puedan cambiar mediante el uso de parámetros y cmdlets asignados a éstos. Es posible ver los ámbitos para determinar cuáles se han agregado a la organización, la configuración de un ámbito específico o los ámbitos que son huérfanos.

Para obtener más información acerca de los ámbitos de función de administración en Microsoft Exchange Server 2013, consulte [Descripción de los ámbitos de roles de administración](understanding-management-role-scopes-exchange-2013-help.md).

¿Está buscando otras tareas de administración relacionadas con los ámbitos de función? Consulte [Permisos avanzados](advanced-permissions-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Ámbitos de administración" en el tema [Permisos de administración de roles](role-management-permissions-exchange-2013-help.md).

  - Debe usar el Shell para hacer este tipo de procedimientos.

  - Este tema hace uso de la canalización y el cmdlet **Format-List**. Para obtener más información acerca de estos conceptos, consulte los siguientes temas:
    
      - [Canalización](https://technet.microsoft.com/es-es/library/aa998260\(v=exchg.150\))
    
      - [Trabajar con salidas de comandos](working-with-command-output-exchange-2013-help.md)

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Ver un ámbito específico

Puede ver los detalles de una ámbito canalizando el resultado del cmdlet **Get-ManagementScope** al cmdlet **Format-List**.

Para ver los detalles de un ámbito específico, utilice la sintaxis siguiente.

    Get-ManagementScope <scope name> | Format-List

En este ejemplo, se recuperan los detalles del ámbito Servidores de Seattle.

    Get-ManagementScope "Seattle Servers" | Format-List

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementScope](https://technet.microsoft.com/es-es/library/dd298180\(v=exchg.150\)).

## Enumerar todos los ámbitos

En este ejemplo, se recupera una lista de ámbitos de la organización.

    Get-ManagementScope

Este cmdlet recupera ámbitos exclusivos y normales. Si solamente desea devolver ámbitos exclusivos o ámbitos normales, consulte la sección "Enumerar todos los ámbitos exclusivos o normales solamente", que aparece más adelante en este tema.

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementScope](https://technet.microsoft.com/es-es/library/dd298180\(v=exchg.150\)).

## Enumerar todos los ámbitos huérfanos

Los *ámbitos huérfanos* son ámbitos que no están asociados a ninguna asignación de funciones de administración.

En este ejemplo, se recupera una lista de ámbitos huérfanos.

    Get-ManagementScope -Orphan

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementScope](https://technet.microsoft.com/es-es/library/dd298180\(v=exchg.150\)).

## Enumerar todos los ámbitos exclusivos o normales solamente

De forma predeterminada, el cmdlet **Get-ManagementScope** devuelve una lista de ámbitos que contiene los ámbitos exclusivos y normales. Si desea devolver solamente los ámbitos exclusivos o solo los ámbitos normales, utilice la sintaxis siguiente.

    Get-ManagementScope -Exclusive < $true | $false >

En este ejemplo, se devuelven solamente los ámbitos exclusivos.

    Get-ManagementScope -Exclusive $true

En este ejemplo, se devuelve una lista de los ámbitos normales solamente.

    Get-ManagementScope -Exclusive $false

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Get-ManagementScope](https://technet.microsoft.com/es-es/library/dd298180\(v=exchg.150\)).

