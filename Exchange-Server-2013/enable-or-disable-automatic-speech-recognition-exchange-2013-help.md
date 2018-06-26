---
title: 'Habilitar o deshabilitar el reconocimiento de voz automático: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar el reconocimiento de voz automático
ms:assetid: 92b3b679-b503-4068-8e88-25ec0f4537ab
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232128(v=EXCHG.150)
ms:contentKeyID: 52061851
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o deshabilitar el reconocimiento de voz automático

 

_**Se aplica a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:**2012-12-12_

Puede habilitar su operador automático de mensajería unificada (UM) para Reconocimiento de voz automático (ASR). Tras habilitar para voz un operador automático de mensajería unificada, los llamantes pueden responder verbalmente a los mensajes del operador automático y desplazarse por el sistema de menús del mismo. De forma predeterminada, cuando un operador automático se crea, no está habilitado para voz. Tras habilitar la voz del operador automático, quienes llaman pueden usar solamente comandos de voz para explorar el sistema de menús del operador automático, y no se pueden usar entradas de teclado.

Aunque no es obligatorio, se recomienda configurar un operador automático de reserva DTMF (multifrecuencia de tono dual) para cada operador automático habilitado para voz con el fin de que las personas que llaman puedan usar entradas de tonos si este operador no reconoce o comprende las palabras que dicen. Si se configura un operador automático de reserva DTMF, las personas que llaman usan entradas DTMF, denominadas también entradas de tonos, para desplazarse por el sistema de menús del operador automático, deletrear un nombre de usuario o usar un mensaje de menú personalizado. No recomendamos habilitar para voz un operador automático de reserva DTMF.

Para conocer tareas de administración adicionales relacionadas con los operadores automáticos de mensajería unificada, consulte [Procedimientos operador automático de mensajería unificada](um-auto-attendant-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el contenido "Operadores automáticos de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un operador automático de MU. Para conocer los pasos detallados, consulte [Crear un operador automático de mensajería unificada](create-a-um-auto-attendant-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Usar el EAC para habilitar para voz un operador automático de mensajería unificada

1.  En el EAC, vaya a **Mensajería unificada** \> **Planes de marcado de mensajería unificada**. En la vista de lista, seleccione el plan de marcado de mensajería unificada que desea cambiar y haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  En la página **Plan de marcado de MU**, en **Operadores automáticos de mensajería unificada**, seleccione el operador automático de UM que desee habilitar para voz y, a continuación, haga clic en **Editar**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

3.  En la página **Operador automático de mensajería unificada** \> **General**, seleccione la casilla al lado de **Ajustar el operador automático para que responda a los comandos de voz** para habilitar el reconocimiento de voz. Para deshabilitar el reconocimiento automático de voz, desactive esta casilla

4.  Haga clic en **Guardar**.

## Usar el Shell para habilitar para voz un operador automático de mensajería unificada

En este ejemplo, se habilita ASR en un operador automático de MU denominado `MySpeechEnabled AA`.

    Set-UMAutoAttendant -Identity MySpeechEnabledAA -SpeechEnabled $true

