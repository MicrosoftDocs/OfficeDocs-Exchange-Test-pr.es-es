---
title: 'Quitar una directiva de buzón de Outlook Web App de Exchange: Exchange 2013 Help'
TOCTitle: Quitar una directiva de buzón de Outlook Web App de Exchange
ms:assetid: edab7bac-b62c-4b82-8f21-dcac77cf0e8f
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351239(v=EXCHG.150)
ms:contentKeyID: 49896000
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Quitar una directiva de buzón de Outlook Web App de Exchange

 

_**Se aplica a:**Exchange Online, Exchange Server 2013_

_**Última modificación del tema:**2013-03-15_

Para quitar una directiva de buzón de MicrosoftOutlook Web App de una organización de Exchange, puede usar el EAC o el Shell.

Para conocer tareas de administración adicionales relacionadas con directivas de buzón de Outlook Web App, consulte [Directivas de buzones de Outlook Web App](outlook-web-app-mailbox-policies-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para completar cada procedimiento:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Directivas de buzón de Outlook Web App" en el tema [Permisos de dispositivos móviles y clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de EAC para quitar una directiva de buzón de Outlook Web App

1.  En el EAC, haga clic en **Permisos** \> **Directivas de Outlook Web App**.

2.  En el panel de resultados, haga clic para seleccionar la directiva de buzón que desea quitar.

3.  Haga clic en el botón **Eliminar**.

4.  En la ventana de confirmación, haga clic en **Sí** para quitar la directiva de buzones o en **No** para cancelar.

## Uso del Shell para quitar una directiva de buzones de Outlook Web App

Este ejemplo quita una directiva de buzones de Outlook Web App denominada `Policy1`.

    Remove-OwaMailboxPolicy -Name Policy1 

Para obtener más información sobre sintaxis y parámetros, consulte [Remove-OwaMailboxPolicy](https://technet.microsoft.com/es-es/library/dd298103\(v=exchg.150\)).

## ¿Cómo saber si el proceso se ha completado correctamente?

Para comprobar que eliminó correctamente una directiva de buzón de Outlook Web App:

  - En el EAC, haga clic en **Permisos** \> **Directivas de Outlook Web App**. La directiva que quitó ya no debería aparecer en la lista.

