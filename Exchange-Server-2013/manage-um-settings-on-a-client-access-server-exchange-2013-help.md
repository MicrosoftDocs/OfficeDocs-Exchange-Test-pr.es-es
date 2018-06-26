---
title: 'Administrar la configuración de mensajería unificada en un servidor de acceso de cliente: Exchange 2013 Help'
TOCTitle: Administrar la configuración de mensajería unificada en un servidor de acceso de cliente
ms:assetid: 08667911-fa86-404e-84b1-65cedd94d579
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ673507(v=EXCHG.150)
ms:contentKeyID: 50556736
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Administrar la configuración de mensajería unificada en un servidor de acceso de cliente

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2013-04-09_

Después de instalar un servidor de acceso de cliente que ejecute el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange, puede configurar varias opciones, incluidos la cantidad de llamadas simultáneas, los puertos de escucha de TCP y Seguridad de la capa de transporte (TLS), el estado y el modo de inicio.


> [!NOTE]
> No es necesario que se agreguen servidores de acceso de cliente a un plan de marcado de UM para que este pueda procesar llamadas de Mensajería unificada (UM), excepto cuando se integran la UM y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. De manera predeterminada, todos los servidores de acceso de cliente de una organización están disponibles para contestar a las llamadas entrantes.



Para consultar otras tareas relacionadas con servidores de acceso de cliente y la mensajería unificada, vea [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Servidor de acceso de cliente (servicio de enrutamiento de llamadas de mensajería unificada)" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que el servidor de acceso de cliente esté instalado, bien en el mismo PC que el servidor de buzones, o bien en otro diferente.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el Shell para configurar las propiedades de la mensajería unificada en un servidor de acceso de cliente

En este ejemplo, se elimina un servidor de acceso de cliente llamado `MyClientAccessServer` de todos los planes de marcado del Protocolo de inicio de sesión (SIP).

    Set-UMCallRouterSettings -DialPlans $null - Server MyClientAccessServer

En este ejemplo se agrega un servidor de acceso de cliente llamado `MyClientAccessServer` a un plan de marcado de SIP denominado `MySIPDialPlan` y también se establece el número máximo de llamadas de voz entrantes.

    Set-UMCallRouterSettings -DialPlans MySIPDialPlan -MaxCalls 150 -Server MyClientAccessServer

En este ejemplo, se establece el puerto de escucha TCP de SIP en el 5077 y el modo de inicio en modo Dual en un servidor de acceso de cliente llamado `MyClientAccessServer`.

    Set-UMCallRouterSettings  -Server MyClientAccessServer-SipTCPListeningPort 5077 -UMStartUpMode -Dual 

## Usar el Shell para ver las propiedades del servidor de acceso de cliente

En este ejemplo, se muestra una lista de todos los servidores de acceso de cliente.

    Get-UMCallRouterSettings

En este ejemplo, se muestra una lista con formato de las propiedades del servidor de acceso de cliente.

    Get-UMCallRouterSettings | Format-List

