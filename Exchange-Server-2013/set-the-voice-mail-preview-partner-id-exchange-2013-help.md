---
title: 'Establecer identificador socio vista previa correo voz: Exchange 2013 Help'
TOCTitle: Establezca el identificador del socio de vista previa del correo de voz
ms:assetid: ab98c320-9952-47a7-b141-ddfc2c0ad419
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff630924(v=EXCHG.150)
ms:contentKeyID: 51406531
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establezca el identificador del socio de vista previa del correo de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-13_

Puede establecer un identificador de socio de Vista previa de correo de voz en una directiva de buzón de mensajería unificada (MU). Después de configurar el identificador de socio de vista previa de correo de voz en una directiva de buzones de correo de mensajería unificada, la configuración se aplicará a todos los usuarios con mensajería unificada enlazados a esta directiva de buzones de correo.


> [!NOTE]
> Debe usar el Shell para establecer un identificador de socio de vista previa de correo de voz.



Para obtener más información acerca del programa de asociados de vista previa de correo de voz, consulte [Asesor de vista previa de correo de voz](voice-mail-preview-advisor-exchange-2013-help.md).

Para otras tareas de administración relacionadas con la vista previa de correo de voz, consulte [Procedimientos de vista previa del correo de voz](voice-mail-preview-procedures-exchange-2013-help.md).

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 1 minuto.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el el contenido "Directivas de buzón de MU" en el tema [Permisos de mensajería unificada](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear un plan de marcado de mensajería unificada](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de llevar a cabo estos procedimientos, confirme que se haya creado un plan de marcado de MU. Para conocer los pasos detallados, consulte [Crear una directiva de buzón de mensajería unificada](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>..



## Uso del Shell para establecer el identificador de socio de vista previa de correo de voz en una directiva de buzones de correo de mensajería unificada

En este ejemplo se establece el identificador de socio de Vista previa de correo de voz en CON123-2010 en una directiva de buzón de MU denominada *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy 
    -VoiceMailPreviewPartnerAssignedID CON123-2010

