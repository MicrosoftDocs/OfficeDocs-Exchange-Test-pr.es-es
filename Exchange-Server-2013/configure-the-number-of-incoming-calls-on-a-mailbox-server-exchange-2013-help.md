---
title: 'Configurar n.º de llamadas entrantes en servidor de buzones Exchange 2013 Help | Microsoft Docs'
TOCTitle: Configurar el número de llamadas entrantes en un servidor de buzones
ms:assetid: 419e1de9-2bf8-48a8-824d-2a536b0a6d90
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997637(v=EXCHG.150)
ms:contentKeyID: 50556774
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar el número de llamadas entrantes en un servidor de buzones

 

_**Se aplica a:** Exchange Server, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-23_

Puede configurar el número de conexiones entrantes simultáneas que aceptará un servidor de buzones que ejecute el servicio de mensajería unificada de Microsoft Exchange. Esto incluye todas las llamadas entrantes, incluidos Outlook Voice Access, el contestador automático, los operadores automáticos y las llamadas de fax. Cuando se aumenta el número de conexiones simultáneas en un servidor de buzones, se necesitan más recursos del sistema que si se disminuye dicho número. La disminución del número de llamadas simultáneas es especialmente importante en los equipos más lentos en los que están instalados los servicios de mensajería unificada. El número de llamadas de voz simultáneas puede oscilar entre 0 y 200. El valor predeterminado es 100.

Para tareas adicionales relacionadas con servidores de buzones y mensajería unificada, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de buzones de correo (servicio de mensajería unificada)" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que se hayan instalado correctamente los servidores de buzones y de acceso de cliente.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para configurar el número de llamadas entrantes en un servidor de buzones

1.  En la consola EAC, desplácese hasta **Servidores** \> **Servidores**.

2.  En la vista de lista, seleccione el servidor Exchange que desea modificar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Exchange Server**, haga clic en **Mensajería unificada**.

4.  Bajo **Configuración del servicio de mensajería unificada**, en **Número máximo de llamadas permitidas**, escriba un número del 0 al 200 y haga clic en **Guardar**.

## Usar el Shell para configurar el número de llamadas entrantes en un servidor de buzones

En este ejemplo, se establece el número de llamadas de voz, de fax y de Outlook Voice Access entrantes que puede aceptar un servidor de buzones denominado `MyMailboxServer1` en 50.

    Set-UMService -Identity MyMailboxServer1 -MaxCallsAllowed 50

