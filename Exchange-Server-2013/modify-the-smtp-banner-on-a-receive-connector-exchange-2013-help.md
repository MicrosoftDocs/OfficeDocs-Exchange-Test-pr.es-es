---
title: 'Modificar el título SMTP en un conector de recepción: Exchange 2013 Help'
TOCTitle: Modificar el título SMTP en un conector de recepción
ms:assetid: d667704e-fd69-4aca-9c35-eef7006944b2
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb124740(v=EXCHG.150)
ms:contentKeyID: 52062065
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Modificar el título SMTP en un conector de recepción

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

The *SMTP banner* is the SMTP connection response that a remote SMTP messaging server receives after it connects to a Receive connector that's configured on a computer running Microsoft Exchange Server 2013.

This is the default response received by a remote SMTP messaging server after it connects to the Receive connector:

```powershell
220 <Servername> Microsoft ESMTP MAIL service ready at <RegionalDay-Date-24HourTimeFormat> <RegionalTimeZoneOffset>
```

When you specify a custom value for SMTP banner on a Receive connector, a remote SMTP messaging server that connects to that SMTP Receive connector receives the following response.

```powershell
220 <Banner Text>
```

You may want to modify the SMTP banner for Internet-facing SMTP Receive connectors so the server name and messaging server software aren't disclosed by the SMTP banner.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Receive connectors" entry in the [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md) topic.

  - Solo puede usar el Shell para realizar este procedimiento.

  - The replacement SMTP banner text string must always start with `220`. As defined in RFC 2821, the default service ready SMTP response code is 220.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the Shell to modify the SMTP banner on a Receive connector

Run the following command:

```powershell
Set-ReceiveConnector <ConnectorIdentity> -Banner "220 <Banner Text>"
```

This example modifies the SMTP banner on the existing Receive connector named From the Internet so the SMTP banner displays `220 Contoso Corporation`.

```powershell
Set-ReceiveConnector "From the Internet" -Banner "220 Contoso Corporation"
```

This example removes the custom SMTP banner on the Receive connector named From the Internet, which returns the SMTP banner to the default value.

```powershell
Set-ReceiveConnector "From the Internet" -Banner $null
```

## How do you know this worked?

To verify that you have successfully modified the SMTP banner on a Receive connector, do the following:

1.  Open a telnet client on a computer that can access the Receive connector, and run the following command:
    
    ```powershell
    open <Connector FQDN or IP address> <Port>
    ```

2.  Verify the response from the Receive connector contains the SMTP banner you configured.

Note that this procedure only works on Receive connectors that allow anonymous or Basic authentication. For more information, see [Usar Telnet para probar la comunicación SMTP](use-telnet-to-test-smtp-communication-exchange-2013-help.md).

