---
title: 'Poner un buzón en retención: Exchange 2013 Help'
TOCTitle: Poner un buzón en retención
ms:assetid: 2baac4a7-3402-4142-bfb3-1649a950e677
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd335168(v=EXCHG.150)
ms:contentKeyID: 49895538
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Poner un buzón en retención

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2012-10-14_

Al colocar un buzón de correo en la suspensión de la retención se suspende, en ese buzón de correo, el procesamiento de una directiva de retención o de buzón de correo de carpeta administrada. La suspensión de la retención está diseñada, por ejemplo, para cuando el usuario está de vacaciones o ausente de manera temporal.

Durante la suspensión de la retención, el usuario puede iniciar sesión en su buzón de correo y modificar o eliminar elementos. Al realizar una búsqueda en el buzón de correo, los elementos eliminados que sean posteriores al período de retención de elementos eliminados no aparecerán entre los resultados de la búsqueda. Para asegurarse de que se conserven los elementos modificados o eliminados por el usuario en escenarios de retención legal, es necesario colocar el buzón de correo en retención legal. Para obtener más información, consulte [Crear o quitar una conservación local](create-or-remove-an-in-place-hold-exchange-2013-help.md).

También es posible incluir comentarios de retención en buzones de correo colocados en la suspensión de retención. Los comentarios se muestran en las versiones compatibles de Microsoft Outlook.

Para otras tareas de administración relacionadas con la administración de registros de mensajes (MRM), consulte [Procedimientos de administración de registros de mensajería](messaging-records-management-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Administración de los registros de mensajes" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - No puede usar el Centro de Administración de Exchange (EAC) para colocar un buzón en suspensión de la retención. Debe usar el Shell.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## ¿Qué desea hacer?

## Usar el Shell para colocar un buzón de correo en la suspensión de la retención

En este ejemplo, se coloca en la suspensión de la retención en el buzón de correo de Alfredo Maldonado.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $true

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## Usar el Shell para quitar la suspensión de la retención de un buzón de correo

En este ejemplo, se quita la suspensión de la retención del buzón de correo de Alfredo Maldonado.

    Set-Mailbox "Michael Allen" -RetentionHoldEnabled $false

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-Mailbox](https://technet.microsoft.com/es-es/library/bb123981\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para verificar que haya colocado un buzón de correo en suspensión de la retención, use el cmdlet [Get-Mailbox](https://technet.microsoft.com/es-es/library/bb123685\(v=exchg.150\)) para recuperar la propiedad *RetentionHoldEnabled* del buzón de correo.

Este comando recupera la propiedad *RetentionHoldEnabled* del buzón de Michael Allen.

    Get-Mailbox "Michael Allen" | Select RetentionHoldEnabled

Este comando recupera todos los buzones de correo en la organización de Exchange, filtra los buzones de correo que están en suspensión de la retención, y los enumera junto con la directiva de retención que se aplica a cada uno.


> [!IMPORTANT]
> Como <EM>RetentionHoldEnabled</EM> no es una propiedad filtrable en Exchange&nbsp;2013, puede usar el parámetro <EM>Filter</EM> con el cmdlet <STRONG>Get-Mailbox</STRONG> para filtrar buzones de correo que están en suspensión de la retención en el servidor. Este comando recupera una lista de todos los buzones de correo y filtros en el cliente que ejecute la sesión del Shell. En grandes entornos con miles de buzones de correo, este comando puede tardar mucho a completarse.



    Get-Mailbox -ResultSize unlimited | Where-Object {$_.RetentionHoldEnabled -eq $true} | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto

