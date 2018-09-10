---
title: 'Habilitar o deshabilitar envío mensajes de voz a usuarios: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el envío de mensajes de voz a usuarios
ms:assetid: faa300d8-2534-40db-8ef9-428be8bb7934
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Dd351277(v=EXCHG.150)
ms:contentKeyID: 52061951
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar el envío de mensajes de voz a usuarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-12-13_

Puede habilitar a las personas que llaman para que envíen mensajes de voz a usuarios desde un operador automático de mensajería unificada (UM), o bien impedir que lo hagan. De forma predeterminada, esta opción está habilitada y permite que las personas que llaman dejen mensajes de voz a usuarios del plan de marcado de UM asociado con el operador automático de UM. Si deshabilita esta opción, el operador automático no invitará a las personas que llaman a enviar un mensaje de voz durante el mensaje del sistema.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/um-auto-attendant-procedures).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](https://docs.microsoft.com/es-es/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para permitir que los autores de las llamadas envíen mensajes de voz o para evitar que lo hagan

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada que desee administrar y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **Libreta de direcciones y acceso de operador**, en **Opciones para ponerse en contacto con los usuarios**, active la casilla situada al lado de **Permitir que los autores de llamadas dejen mensajes de voz para los usuarios** para permitir que los autores de llamadas dejen mensajes de voz. Para evitar que los autores de llamadas dejen mensajes de voz, desactive la casilla.

4.  Haga clic en **Guardar**.


> [!NOTE]
> Si deshabilita esta opción y también deshabilita la opción <STRONG>Permitir que los autores de llamadas marquen a usuarios</STRONG>, las opciones en <STRONG>Opciones para las búsquedas en la libreta de direcciones</STRONG> también se deshabilitan.



## Usar el Shell para permitir a las personas que llaman que envíen mensajes de voz o impedir que lo hagan

En este ejemplo se impide que las personas que llaman a un operador automático denominado `MyUMAutoAttendant` puedan enviar mensajes de voz.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $false

Este ejemplo permite que las personas que llaman a un operador automático de mensajería unificada denominado `MyUMAutoAttendant` envíen mensajes de voz.

    Set-UMAutoAttendant -Identity MyUMAutoAttendant -SendVoiceMsgEnabled $true

