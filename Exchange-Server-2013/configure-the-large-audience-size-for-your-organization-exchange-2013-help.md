---
title: 'Configurar el tamaño de gran audiencia para su organización Exchange 2013 Help'
TOCTitle: Configurar el tamaño de gran audiencia para su organización
ms:assetid: 8a37911c-4339-4921-b5d3-0a5a774d4517
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ659068(v=EXCHG.150)
ms:contentKeyID: 49895761
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar el tamaño de gran audiencia para su organización

 

_**Se aplica a:** Exchange Online, Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

Puede usar el Shell de administración de Exchange para configurar varios parámetros que definen cómo usar información sobre correo en su organización.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Información sobre correo" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use Shell para configurar el tamaño de la gran audiencia para su organización

Use el cmdlet **Set-OrganizationConfig** para configurar el tamaño de la gran audiencia para su organización. Cuando la dirección de los remitentes envía mensajes a una cantidad de destinatarios mayor que el tamaño configurado, se muestran en la gran audiencia de sugerencias de correo electrónico. De forma predeterminada, el tamaño de la gran audiencia está establecido en 25. En este ejemplo, se configura el tamaño de la gran audiencia en 50, en su organización.

    Set-OrganizationConfig -MailTipsLargeAudienceThreshold 50

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)).

