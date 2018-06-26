---
title: 'Permitir o impedir la contestación en un servidor de buzón de llamadas: Exchange 2013 Help'
TOCTitle: Permitir o impedir la contestación en un servidor de buzón de llamadas
ms:assetid: 4b860c09-6669-4e3d-b3dc-17b8018b3860
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Aa997908(v=EXCHG.150)
ms:contentKeyID: 50556796
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir o impedir la contestación en un servidor de buzón de llamadas

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-18_

Puede permitir que el servicio de mensajería unificada de Microsoft Exchange en un servidor de buzones responda nuevas llamadas, o evitar que lo haga. De manera predeterminada, un servidor de buzones está habilitado después de su instalación. Cuando configura el servidor de buzones para que acepte llamadas entrantes de voz, de fax, de operador automático y de Outlook Voice Access, usa el cmdlet **Set-ServerComponentState**.

La configuración del modo de mantenimiento para un servidor de buzones le permite poner el servidor fuera de servicio. Para un servidor de buzones, estar fuera de servicio significa que el servidor no hospedará bases de datos activas, todas las colas de transporte están vacías y el servidor no aceptará llamadas entrantes de servidores de acceso de cliente, puertas de enlace VoIP, IP-PBX, PBX habilitados para SIP ni controladores de borde de sesión (SBC).

En Exchange 2007 y en Exchange 2010, existe un parámetro de estado que permite controlar el estado operativo de un servidor de mensajería unificada. En Exchange 2013, no hay parámetros de estado disponibles para ese propósito en el cmdlet **Set-UMService** para un servidor de buzones.


> [!IMPORTANT]
> No es necesario que los servidores de buzones de correo y de acceso de cliente se agreguen a un plan de marcado de mensajería unificada antes de que puedan procesar llamadas para la mensajería unificada, excepto cuando integre la mensajería unificada y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. De forma predeterminada, todos los servidores de acceso de cliente y de buzones de correo de una organización están disponibles para contestar llamadas entrantes.



Para otras tareas de administración relacionadas con los servidores de buzones, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Valores de configuración de Exchange Server" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que el servidor de buzones está instalado, bien en el mismo equipo que el servidor de acceso de clientes o en otro distinto.

  - Si planea colocar a un servidor de buzones en el modo de mantenimiento, compruebe que haya suficiente redundancia de todas las copias de las bases de datos para permitir al servidor estar fuera de servicio.

  - Antes de quitar a un servidor del modo de mantenimiento, verifique el estado del servidor y asegúrese de que está preparado para entrar en servicio.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para permitir o bloquear el contestador automático en un servidor de buzones

En este ejemplo, se habilita un servidor de buzones `UMMBXr-05x.contoso.com` para que acepte llamadas de voz, de fax, de operador automático y de Outlook Voice Access desde puertas de enlace VoIP, IP PBX, PBX habilitados para SIP y SBC, y se escribe el cambio en el Registro en el servidor UMMBX-05x.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

En este ejemplo, se evita que un servidor de buzones `UMMBX-05x.contoso.com` acepte llamadas de voz, de fax, de operador automático y de Outlook Voice Access desde puertas de enlace VoIP, IP PBX, PBX habilitados para SIP y SBC, y se escribe el cambio solo en Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMMBX-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

