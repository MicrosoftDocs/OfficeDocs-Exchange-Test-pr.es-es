---
title: 'Permitir o evitar la llamada a responder en un servidor de acceso de cliente: Exchange 2013 Help'
TOCTitle: Permitir o evitar la llamada a responder en un servidor de acceso de cliente
ms:assetid: 8287bb78-2621-4b80-a128-8f2ccd67923a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb123529(v=EXCHG.150)
ms:contentKeyID: 50556836
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Permitir o evitar la llamada a responder en un servidor de acceso de cliente

 

_**Se aplica a:**Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-11-18_

Puede permitir que el servicio de enrutador de llamadas de mensajería unificada de Microsoft Exchange en un servidor de acceso de cliente responda llamadas nuevas o evitar que lo haga. De forma predeterminada, el servidor de acceso de cliente está habilitado una vez instalado. Cuando configure el servidor de acceso de cliente para que acepte llamadas de voz entrantes, de fax, de operador automático y de Outlook Voice Access, use el cmdlet **Set-ServerComponentState**.

Al configurar el modo de mantenimiento para un servidor de acceso de cliente, puede colocar al servidor fuera de servicio. Para un servidor de acceso de cliente, estar fuera de servicio significa que no aceptará ninguna llamada entrante de puertas de enlace VoIP, IP PBX, PBX con SIP habilitado o controladores de borde de sesión (SBC).

En Exchange 2007 y en Exchange 2010, existe un parámetro de estado que permite controlar el estado operativo de un servidor de mensajería unificada. En Exchange 2013, no hay ningún parámetro de estado para dicho propósito en el cmdlet **Set-UMCallRouterSettings** en un servidor de acceso de cliente.


> [!IMPORTANT]
> No es necesario que los servidores de buzones de correo y de acceso de cliente se agreguen a un plan de marcado de mensajería unificada antes de que puedan procesar llamadas para la mensajería unificada, excepto cuando vaya a integrar la mensajería unificada y Microsoft Office Communications Server 2007 R2 o Microsoft Lync Server. De forma predeterminada, todos los servidores de acceso de cliente y de buzones de correo de una organización están disponibles para contestar llamadas entrantes.



Para otras tareas de administración relacionadas con servidores de acceso de cliente, consulte [Procedimientos de servicios de mensajería unificada](um-services-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 3 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Valores de configuración de Exchange Server" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Compruebe que el servidor de acceso de cliente esté instalado, ya sea en el mismo ordenador que el servidor de buzones de correo, ya sea en otro equipo.

  - Si coloca un servidor de acceso de cliente en modo de mantenimiento, verifique que tenga suficiente capacidad correcta en la matriz de acceso de cliente para permitir que el servidor esté fuera de servicio.

  - Antes de quitar a un servidor del modo de mantenimiento, verifique el mantenimiento del servidor y asegúrese de que está preparado para entrar en servicio.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Usar el Shell para permitir o evitar que se respondan llamadas en un servidor de acceso de cliente

Este ejemplo permite que un servidor de acceso de cliente `UMCallRouter-05x.contoso.com` responda llamadas de voz entrantes, de fax, de operador automático o de Outlook Voice Access desde puertas de enlace VoIP, IP PBX, PBX con SIP habilitado y SBC, y escribe el cambio en el registro en el servidor UMCallRouter-05x.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Active -LocalOnly

Este ejemplo evita que un servidor de acceso de cliente `UMCallRouter-05x.contoso.com` responda llamadas de voz entrantes, de fax, de operador automático o de Outlook Voice Access desde puertas de enlace VoIP, IP PBX, PBX con SIP habilitado y SBC, y escribe el cambio en Active Directory.

    Set-ServerComponentState -Component UnifiedMessaging -Identity UMCallRouter-05x.contoso.com -Requester Maintenance -State Inactive -RemoteOnly

