---
title: 'Restablecer el PIN del correo de voz.: Exchange 2013 Help'
TOCTitle: Restablecer el PIN del correo de voz.
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50556875
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: MT
---

# Restablecer el PIN del correo de voz.

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-22_

Cuando un usuario con correo de voz habilitado para mensajería unificada (UM) se bloquea en un buzón que usa Outlook Voice Access porque intentó iniciar sesión con un PIN incorrecto varias veces o se le olvidó el PIN, puede usar uno de los siguientes procedimientos para restablecer el PIN del usuario. Cuando restablece el PIN de Voice Access de un usuario de Outlook, puede configurar la mensajería unificada (UM) para generar automáticamente un PIN o para especificarlo manualmente. El nuevo PIN se envía al usuario por correo electrónico. Puede especificar opciones de PIN adicionales, como que se requiera que el usuario restablezca el PIN después de la primera vez que inicie sesión. Los usuarios también pueden restablecer el PIN de mensajería unificada mediante Outlook o Outlook Web App.


> [!NOTE]
> Para tener acceso a buzones con la mensajería unificada habilitada, los usuarios de Outlook Voice Access deben usar entradas de comandos de voz, también conocidas como multifrecuencia de tono dual (DTMF). El reconocimiento de voz no está disponible para la entrada de PIN.



Para conocer otras tareas relacionadas con la seguridad del PIN de Outlook Voice Access, consulte [Procedimientos de seguridad PIN](pin-security-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: Menos de 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el la entrada "Buzones de mensajería unificada" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Qué desea hacer?

## Uso de la EAC para restablecer un PIN de mensajería unificada

1.  En la EAC, vaya a **Destinatarios** . En la vista de lista, seleccione el buzón del usuario que desee ver.

2.  En el panel de detalles, en **Características de voz y teléfono**, en **Mensajería unificada**, haga clic en **Ver detalles**.

3.  En la página **Buzón de mensajería unificada**, en **Configuración de buzón de correo de mensajería unificada**, haga clic en **Restablecer NIP**.

4.  En la página **Restablecer PIN del buzón de mensajería unificada**, use las siguientes opciones para restablecer el PIN de un usuario habilitado para mensajería unificada:
    
      - **Generar un PIN automáticamente**   Use esta opción para generar automáticamente el PIN que el usuario debe usar para obtener acceso a su buzón en Outlook Voice Access. Esta opción está habilitada de forma predeterminada.
        
        El PIN generado automáticamente se enviará en un mensaje de correo electrónico al buzón del usuario. Después de recibir el PIN e iniciar sesión en su buzón, se le solicitará que cambie el PIN a uno que le resulte más familiar.
        
        El usuario también puede restablecer el PIN mediante Outlook Web App y Microsoft Outlook. El PIN se genera automáticamente según las directivas de PIN configuradas en la directiva de buzones de mensajería unificada asociada con el buzón del usuario. Se recomienda generar automáticamente los NIP para los usuarios de Outlook Voice Access.
    
      - **Escribir un PIN**   Use esta opción para especificar manualmente un PIN para un usuario de Outlook Voice Access. Esta opción está deshabilitada de manera predeterminada.
        
        Si especifica un PIN para un usuario, se enviará en un mensaje de correo electrónico al buzón del usuario. Después de recibir en PIN e iniciar sesión en el buzón, pueden cambiarlo mediante la configuración de opciones personales en Outlook Voice Access. Sin embargo, en Outlook Web App y en Microsoft Outlook, no es posible especificar un PIN manualmente.
    
      - **Pedir que el usuario restablezca su PIN la primera vez que inicia sesión**   Use esta opción para solicitar que el usuario restablezca su PIN la primera vez que inicie sesión en Outlook Voice Access. Esta opción está habilitada de manera predeterminada.
        
        Si selecciona la opción para generar automáticamente un PIN para un usuario, puede habilitar esta opción para obligar a los usuarios a cambiar el PIN la primera vez que inician sesión en Outlook Voice Access. Esto ayuda a proteger el PIN del usuario.

5.  Haga clic en **Guardar**.

## Uso del Shell para restablecer un PIN de mensajería unificada

En este ejemplo se establece el PIN de buzón de voz de "Tony Smith" como "1985848". Sin embargo, este PIN debe modificarse cuando el usuario iniciar sesión por primera vez en Outlook Voice Access.

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true

