---
title: 'Habilitar deshabilitar reconocer automático voz usuario Outlook Voice Access | Microsoft Docs'
TOCTitle: Habilitar o deshabilitar el reconocimiento automático de voz para un usuario de Outlook Voice Access User
ms:assetid: 58f41016-e725-432b-953e-415d61e0664c
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb232062(v=EXCHG.150)
ms:contentKeyID: 50556788
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar el reconocimiento automático de voz para un usuario de Outlook Voice Access User

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Puede configurar el reconocimiento de voz automático (ASR) para un usuario habilitado para la mensajería unificada (MU) y el correo de voz. Cuando ASR está habilitado en el buzón de un usuario de Outlook Voice Access, el usuario puede moverse por los menús del buzón mediante comandos de voz. ASR está habilitado de manera predeterminada. Si ASR está deshabilitado, el usuario debe usar entradas de multifrecuencia de tono dual (DTMF), también conocidas como "marcación por tonos", para desplazarse por los menús. 


> [!NOTE]
> No puede usar el Centro de Administración de Exchange para configurar esta característica. Debe usar el Shell para habilitar o deshabilitar ASR para un usuario de correo de voz.



Para otras tareas de administración relacionadas con los usuarios de mensajería unificada o correo de voz, consulte [Administrar la configuración de correo de voz para un usuario](manage-voice-mail-settings-for-a-user-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que el buzón del usuario esté habilitado para la MU. Para conocer los pasos detallados, consulte [Habilitar a un usuario para el correo de voz](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para habilitar o deshabilitar ASR para un usuario habilitado para la MU

En este ejemplo, se habilita ASR para un usuario habilitado para la MU denominado `tonysmith`.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $true

En este ejemplo, se deshabilita ASR para un usuario habilitado para la mensajería unificada denominado `tonysmith`.

    Set-UMMailbox -Identity tonysmith@contoso.com -AutomaticSpeechRecognitionEnabled $false

