---
title: 'Configurar servicio socios vista previa correo voz usuarios Exchange 2013 Help'
TOCTitle: Configurar servicios de socios de vista previa del correo de voz para los usuarios
ms:assetid: 7bb914ca-5502-4e64-bae5-555034138d8a
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff630920(v=EXCHG.150)
ms:contentKeyID: 51406528
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar servicios de socios de vista previa del correo de voz para los usuarios

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2016-12-09_

Puede configurar un socio de la vista previa de correo de voz en una directiva de buzón de mensajería unificada (MU). Después de haber realizado la configuración del socio de vista previa de correo de voz, tal como la Id. del socio de vista previa de correo de voz y la dirección del socio de vista previa de correo de voz, en una directiva de buzón de mensajería unificada, la configuración que realice se aplicará a todos los usuarios habilitados para mensajería unificada que están vinculados con esa directiva de buzón.


> [!NOTE]
> Debe usar el Shell para configurar el socio de vista previa de correo de voz.



Para conocer tareas de administración adicionales relacionadas con las directivas de buzones de mensajería unificada, consulte [Procedimientos de políticas de buzón de mensajería unificada](um-mailbox-policy-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar:  5 minutos.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado una directiva de buzón de mensajería unificada. Para obtener información acerca de los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## ¿Cómo realiza esto?

## Paso 1: Suscribirse con un servicio de socios

Para buscar la lista de asociados de negocios certificados y obtener instrucciones detalladas acerca de cómo suscribirse, consulte [Asesor de vista previa de correo de voz](voice-mail-preview-advisor-exchange-2013-help.md) o visite el sitio Web de [Microsoft PinPoint](https://go.microsoft.com/fwlink/p/?linkid=281966) . Una vez que se ha suscrito, proporcionará el socio de vista previa del correo de voz es un ID de socio y la dirección SMTP se utiliza para reenviar los mensajes de voz.

En el Paso 2, aplicará la Id. de socio y la dirección SMTP que adquirió en el Paso 1 en las directivas de buzón de mensajería unificada requeridas.

## Paso 2: Establecer la dirección e Id. de socio de vista previa de correo de voz

Este ejemplo establece la dirección de socio de la vista previa de correo de voz en exumvmp@fabrikam.com y la Id. de socio de la vista previa de correo de voz en CON123-2010 en una directiva de buzón de mensajería unificada, denominada *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com
    -VoiceMailPreviewPartnerAssignedID CON123-2010

## Paso 3: Configurar la configuración avanzada de socio de vista previa de correo de voz

Si el socio requiere una configuración personalizada, es posible que desee establecer dos parámetros adicionales para la vista previa de correo de voz tal como se muestra a continuación:

  - *VoiceMailPreviewPartnerMaxMessageDuration*

  - *VoiceMailPreviewPartnerMaxDeliveryDelay*

Este ejemplo establece la duración máxima del mensaje en 300 segundos (5 minutos) y el retraso máximo en la entrega en 600 segundos (10 minutos) en una directiva de buzón de mensajería unificada denominada *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerMaxMessageDuration 300 -VoiceMailPreviewPartnerMaxDeliveryDelay 600

## Paso 4: Asignar un usuario habilitado para mensajería unificada a una directiva de buzón de mensajería unificada para un socio de vista previa de correo de voz

Si desea configurar el servicio de socio de vista previa de correo de voz pata algunos, pero no para todos los usuarios habilitados para mensajería unificada del plan de marcado de mensajería unificada, debe crear una nueva directiva de buzón de mensajería unificada y debe realizar la configuración de socios. Cuando haya finalizado, puede aplicar la nueva directiva a los usuarios habilitados para mensajería unificada seleccionados. Para obtener más información acerca de cómo asignar usuarios habilitados para mensajería unificada a una directiva de buzón de mensajería unificada, consulte los siguientes temas:

  - [Asignar una directiva de buzón de mensajería unificada](assign-a-um-mailbox-policy-exchange-2013-help.md)

  - [Set-UMMailbox](https://technet.microsoft.com/es-es/library/bb124893\(v=exchg.150\))

Para obtener más información acerca del programa de asociados de vista previa de correo de voz, consulte [Asesor de vista previa de correo de voz](voice-mail-preview-advisor-exchange-2013-help.md).

