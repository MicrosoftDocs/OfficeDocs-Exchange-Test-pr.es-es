---
title: 'Administrar la configuración de UM en servidor de buzones: Exchange 2013 Help'
TOCTitle: Administrar la configuración de mensajería unificada en un servidor de buzones
ms:assetid: 6df4853d-21d2-473f-b0ca-ebc996d8794a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa998815(v=EXCHG.150)
ms:contentKeyID: 50556810
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Servers.UnifiedMessaging.UMServerPropertiesPropertyPage
ms.translationtype: MT
---

# Administrar la configuración de mensajería unificada en un servidor de buzones

 

_**Se aplica a:** Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-11_

Después de instalar un servidor de buzones que ejecute el servicio de mensajería unificada de Microsoft Exchange, puede configurar varias opciones, incluidos la cantidad de llamadas simultáneas, los puertos de escucha de TCP y Seguridad de la capa de transporte (TLS), el estado y el modo de inicio de mensajería unificada.


> [!IMPORTANT]
> No es necesario que se agreguen servidores de buzones a un plan de marcado de mensajería unificada antes de poder procesar llamadas para la mensajería unificada, excepto cuando se integran la mensajería unificada y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. De manera predeterminada, todos los servidores de buzones en una organización están disponibles para contestar las llamadas entrantes.



Para tareas de administración adicionales relacionadas con servidores de buzones y mensajería unificada, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de buzones de correo (servicio de mensajería unificada)" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que el servidor de buzones está instalado, bien en el mismo equipo que el servidor de acceso de clientes o en otro distinto.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso del Shell para configurar las propiedades de la mensajería unificada en un servidor de buzones

En este ejemplo, se elimina un servidor de buzones denominado `MyMailboxServer` de todos los planes de marcado del Protocolo de inicio de sesión (SIP).

    Set-UMService -Identity MyMailboxServer -DialPlans $null

En este ejemplo, se agrega el servidor de buzones denominado `MyMailboxServer` a un plan de marcado de SIP de mensajería unificada denominado `MySIPDialPlanName` y también SE establece el número máximo de llamadas de voz entrantes.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -MaxCalls 150 

En este ejemplo, se establece el modo de inicio para un servidor de buzones en modo Dual denominado `MyUMServer`.

    Set-UMService -Identity MyMailboxServer -DialPlans MySIPDialPlanName -UMStartUpMode -Dual 

## Uso del Shell para ver las propiedades del servidor de buzones

En este ejemplo, se muestra una lista de todos los servidores de buzones.

    Get-UMService

En este ejemplo, se muestra una lista con formato de las propiedades del servidor de buzones `MyMailboxServer`.

    Get-UMService -Identity MyMailboxServer | Format-List

