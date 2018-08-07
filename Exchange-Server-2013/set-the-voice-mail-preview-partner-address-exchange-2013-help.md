---
title: 'Establecer la dirección socio vista previa correo de voz: Exchange 2013 Help'
TOCTitle: Establecer la dirección del socio de vista previa del correo de voz
ms:assetid: 57fbed1e-1b14-4939-95e6-ef7c072f32a9
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Ff630917(v=EXCHG.150)
ms:contentKeyID: 51406499
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Establecer la dirección del socio de vista previa del correo de voz

 

_**Se aplica a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Última modificación del tema:** 2013-02-13_

Se puede establecer una dirección de socio comercial de vista previa de correo de voz en una directiva de buzón de mensajería unificada (MU). Una vez establecida la dirección de socio comercial de vista previa de correo de voz en una directiva de buzón de mensajería unificada, la configuración se aplica a todos los usuarios habilitados para mensajería unificada que estén vinculados a esa directiva de buzón.


> [!NOTE]
> Debe usar el Shell para establecer una dirección de socio comercial de vista previa de correo de voz.



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



## Usar el Shell para establecer la dirección del socio comercial de vista previa de correo de voz en una directiva de buzón de mensajería unificada

En este ejemplo la dirección de socio comercial de vista previa del correo de voz se establece como exumvmp@fabrikam.com en una directiva de buzón de MU con el nombre *MyUMMailboxPolicy*.

    Set-UMMailboxPolicy -identity MyUMMailboxPolicy -VoiceMailPreviewPartnerAddress exumvmp@fabrikam.com

