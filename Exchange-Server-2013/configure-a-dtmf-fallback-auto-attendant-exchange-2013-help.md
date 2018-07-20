---
title: 'Configurar a un operador automático de reserva de DTMF: Exchange 2013 Help'
TOCTitle: Configurar a un operador automático de reserva de DTMF
ms:assetid: a82d85f7-de30-40db-8ee6-b091ac14da9d
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232158(v=EXCHG.150)
ms:contentKeyID: 49895824
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar a un operador automático de reserva de DTMF

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2012-11-30_

Puede configurar un operador automático de mensajería unificada habilitada para voz que posee un operador automático de reserva multifrecuencia de doble tono (DTMF). Un operador automático de reserva DTMF se usa cuando un operador automático de mensajería unificada habilitado para voz no entiende o no reconoce las entradas de voz de quienes llaman. Si se ha configurado un operador automático de reserva DTMF, la persona que llama debe usar entradas de tono de marcación multifrecuencia o entradas de teclado, para explorar el sistema de menús del operador automático, deletrear el nombre de usuario o usar un mensaje del menú personalizado. Si no se ha configurado un operador automático de reserva DTMF y se ha superado el número máximo de entradas de voz porque el sistema no entendió lo que decía el autor de la llamada, el sistema responderá con el siguiente mensaje: "Lo siento, no puedo ayudarle. Llame más tarde."

De forma predeterminada, cuando un operador automático se crea, no está habilitado para voz. Tras habilitar la voz del operador automático, quienes llaman pueden usar solamente comandos de voz para explorar el sistema de menús del operador automático, y no se pueden usar entradas de teclado. Aunque no sea necesario, se recomienda configurar un operador automático de reserva DTMF para cada operador automático habilitado para voz, de modo que quienes llamen puedan usar entradas de teclado si el operador automático habilitado para voz no reconoce o entiende las palabras que pronuncian. También se recomienda no habilitar con voz un operador automático de reserva DTMF.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de mensajería unificada. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para configurar un operador automático habilitado para voz con un operador automático de reserva DTMF

1.  En la EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que quiere cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de mensajería unificada**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de mensajería unificada que quiere que cree un operador automático de reserva DTMF. En la barra de herramientas, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **General**, seleccione la casilla al lado de **Use este operador automático cuando los comandos de voz no funcionen correctamente** y luego haga clic en **Explorar**.

4.  En la página **Seleccionar un operador automático de mensajería unificada**, seleccione el operador automático que desea utilizar a modo de operador automático de reserva DTMF y, a continuación, haga clic en **Guardar**.


> [!IMPORTANT]
> Primero debe habilitar para voz el operador automático antes de poder explorar para ver el operador automático de reserva DTMF que configuró.



## Uso del Shell para configurar un operador automático habilitado para voz con un operador automático de reserva DTMF

En este ejemplo, un operador automático de mensajería unificada denominado `MySpeechEnabledAA` se configura para que use un operador automático de reserva DTMF denominado `MyDTMFAA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -DTMFFallbackAutoAttendant MyDTMFAA

