---
title: 'Habilitar o deshabilitar sugerencias de correo electrónico: Exchange 2013 Help'
TOCTitle: Habilitar o deshabilitar sugerencias de correo electrónico
ms:assetid: 11ad3848-f303-4ad5-a21d-9b0883db4bda
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ649321(v=EXCHG.150)
ms:contentKeyID: 49895481
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Habilitar o deshabilitar sugerencias de correo electrónico

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

Puede usar el Shell de administración de Exchange para configurar varios parámetros que definen cómo usar información sobre correo en su organización.

## ¿Qué necesita saber antes de comenzar?

  - Tiempo estimado para finalizar: 5 minutos

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el entrada "Información sobre correo" en el tema [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md).

  - Solo puede usar el Shell para realizar este procedimiento.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Usar Shell para habilitar o deshabilitar sugerencias de correo electrónico

Use el cmdlet **Set-OrganizationConfig** para habilitar o deshabilitar sugerencias de correo electrónico en su organización. Las sugerencias de correo electrónico están habilitadas de forma predeterminada cuando instala una nueva organización de Exchange. En este ejemplo, se muestra cómo habilitar sugerencias de correo electrónico en su organización.

    Set-OrganizationConfig -MailTipsAllTipsEnabled $true

Para obtener información detallada acerca de la sintaxis y los parámetros, consulte [Set-OrganizationConfig](https://technet.microsoft.com/es-es/library/aa997443\(v=exchg.150\)).

