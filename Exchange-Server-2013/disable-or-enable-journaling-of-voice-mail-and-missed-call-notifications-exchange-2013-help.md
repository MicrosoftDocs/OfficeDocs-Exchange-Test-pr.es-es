---
title: 'Deshabilitar o habilitar el registro en diario de correo de voz y notificaciones de llamadas perdidas: Exchange 2013 Help'
TOCTitle: Deshabilitar o habilitar el registro en diario de correo de voz y notificaciones de llamadas perdidas
ms:assetid: 5164a92e-69e6-4339-b80c-0cfbf0dc0198
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb201690(v=EXCHG.150)
ms:contentKeyID: 49895624
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar o habilitar el registro en diario de correo de voz y notificaciones de llamadas perdidas

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

En Microsoft Exchange Server 2013, cuando se crea una regla de registro en diario para registrar en diario mensajes de correo electrónico enviados o recibidos por remitentes o destinatarios en una organización de Exchange, se incluyen el correo de voz y las notificaciones de llamadas perdidas generadas por el servicio de mensajería unificada (UM). Siga los procedimientos de este tema para activar o desactivar esta característica para toda la organización.

¿Está buscando otras tareas de administración relacionadas con el registro en diario? Consulte [Administrar registro en diario](manage-journaling-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el Entrada "Registro en diario" en el tema [Permisos de directivas de mensajería y conformidad](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar el Shell para habilitar o deshabilitar el registro en diario del correo de voz y de las notificaciones de llamadas perdidas

En este ejemplo, se deshabilita el registro en diario del correo de voz y los avisos de llamadas perdidas al configurar el parámetro *VoicemailJournalingEnabled* en `$false`.

    Set-TransportConfig -VoicemailJournalingEnabled $false

En este ejemplo, se habilita el registro en diario del correo de voz y de las notificaciones de llamadas perdidas al configurar el mismo parámetro en `$true`.

    Set-TransportConfig -VoicemailJournalingEnabled $true

Para obtener información más detallada acerca de la sintaxis y los parámetros, consulte [Set-TransportConfig](https://technet.microsoft.com/es-es/library/bb124151\(v=exchg.150\)).

## Para obtener más información

[Registro en diario](journaling-exchange-2013-help.md)

[Administrar registro en diario](manage-journaling-exchange-2013-help.md)

