---
title: 'Filtrado de datos adjuntos en servidores de transporte perimetral: Exchange 2013 Help'
TOCTitle: Filtrado de datos adjuntos en servidores de transporte perimetral
ms:assetid: be39a181-c82e-41f5-8846-085bf1f84164
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124399(v=EXCHG.150)
ms:contentKeyID: 60830020
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Filtrado de datos adjuntos en servidores de transporte perimetral

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-10_

In Microsoft Exchange Server 2013, you can use attachment filtering on Edge Transport servers to control the attachments that users receive in email messages. Attachment filtering is performed by the Attachment Filtering agent, which is available only on Edge Transport servers.

## Types of attachment filtering

You can use the following types of attachment filtering to control attachments that enter or leave your organization through an Edge Transport server:

  - **Filtering based on file name or file name extension**   You specify the exact file name or file name extension that you want to filter. An example of a file name filter is `BadFileName.exe`. An example of a file name extension filter is `*.exe`.

  - **Filtering based on file MIME content type**   You specify the MIME content type value that you want to filter. The MIME content type value indicates what the attachment is—for example, a JPEG image, an executable file, or a Microsoft Excel file. Content types are expressed as `type/subtype`. For example, a JPEG image file is expressed as `image/jpeg`.
    
    To view a complete list of file name extensions and content types that attachment filtering can detect, run the following command on the Edge Transport server:
    
      ```powershell
      Get-AttachmentFilterEntry | Format-List
      ```

After you define the files to look for, you can configure the action to take on messages that contain these attachments. You can't specify different actions for different types of attachments. You configure one of the following actions for all the messages that match any of the attachment filters:

  - **Reject (block) the message**   The message is blocked. The sender receives a non-delivery report (NDR) that explains that the message wasn't delivered because it contained an unacceptable attachment. You can customize the text in the NDR. The default text is: `Message rejected due to unacceptable attachments`.

  - **Strip the attachment but allow the message through**   The attachment is removed from the message. However, the message itself and any other attachments that don't match the filter are allowed through. If an attachment is stripped, it's replaced with a text file that explains why the attachment was removed. This is the default action.

  - **Silently delete the message**   The message is deleted. Neither the sender nor the recipient receives notification.

For more information, see [Administrar el filtrado de datos adjuntos en servidores de transporte perimetral](manage-attachment-filtering-on-edge-transport-servers-exchange-2013-help.md).


> [!NOTE]
> You can't retrieve messages that have been blocked or attachments that have been stripped. When you configure attachment filters, carefully examine all possible file name matches and verify that legitimate attachments won't be affected by the filter.<BR>Also, don't remove attachments from digitally signed, encrypted, or rights-protected email messages. If you remove attachments from such messages, you invalidate the digitally signed messages and make encrypted and rights-protected messages unreadable.


