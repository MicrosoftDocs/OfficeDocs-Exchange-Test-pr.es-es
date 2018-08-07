---
title: 'Formato de direcciones SMTP no admitido_SMTPAddressLiteral: Exchange 2013 Help'
TOCTitle: Formato de direcciones SMTP no Supported_SMTPAddressLiteral
ms:assetid: b8b55917-d81f-4c0a-ad65-7bb10ac58df8
ms:mtpsurl: https://technet.microsoft.com/es-es/library/ms.exch.setupreadiness.smtpaddressliteral(v=EXCHG.150)
ms:contentKeyID: 48268600
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Formato de direcciones SMTP no Supported\_SMTPAddressLiteral

 

_**Se aplica a:** Exchange Server_

_**Última modificación del tema:** 2016-12-09_

El contenido de este tema no se ha actualizado para Microsoft Exchange Server 2013. Aun así, se puede aplicar a Exchange 2013. Si necesita más ayuda, consulte los siguientes recursos de la comunidad.

¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), o [Exchange Online Protection](https://go.microsoft.com/fwlink/p/?linkid=285351).

Microsoft Exchange Server 2007 y Exchange Server 2010 Setup no pueden continuar porque la directiva de destinatarios especificada usa un formato de dirección SMTP (Protocolo simple de transferencia de correo) no admitido.

Exchange 2007 y Exchange 2010 Setup requieren que todas las direcciones SMTP usadas para las directivas de direcciones de correo electrónico no contengan literales de dirección IP, por ejemplo: *usuario@\[10.10.1.1\]*.

Para resolver este problema, cambie el valor de la dirección SMTP en la directiva de destinatario para que no contenga un literal de dirección IP. Reemplace los corchetes (\[\]) y los números (10.10.1.1) del literal de dirección IP con el formato de nombre DNS (Sistema de nombres de dominio), por ejemplo: *usuario@contoso.com* y después vuelva a ejecutar el programa de instalación de Exchange.

Para obtener más información acerca de cómo administrar las directivas de destinatarios en Exchange Server 2007, consulte "Administrar correo electrónico dirección de directivas" ([https://go.microsoft.com/fwlink/?LinkId=86653](https://go.microsoft.com/fwlink/?linkid=86653)).

Para obtener más información acerca de cómo administrar las directivas de destinatarios en Exchange Server 2010, consulte "Administrar correo electrónico dirección de directivas" ([https://go.microsoft.com/fwlink/?LinkId=179519](https://go.microsoft.com/fwlink/?linkid=179519)).

