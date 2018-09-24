---
title: 'Configure Internet mail flow through a subscribed Edge Transport server: Exchange 2013 Help'
TOCTitle: Configurar el flujo de correo de Internet por medio de un servidor de transporte perimetral suscrito
ms:assetid: d12ea770-99ce-4ab4-a373-96f2554641fa
ms:mtpsurl: https://technet.microsoft.com/es-es/library/Bb738158(v=EXCHG.150)
ms:contentKeyID: 61183335
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configure Internet mail flow through a subscribed Edge Transport server

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2015-04-08_

To establish Internet mail through an Edge Transport server, subscribe the Edge Transport server to an Active Directory site. This automatically creates the two Send connectors required for Internet mail flow:

  - A Send connector configured to send outbound email to all Internet domains.

  - A Send connector configured to send inbound email from the Edge Transport server to an Exchange 2013 Mailbox server.

If you don't want to subscribe the Edge Transport server to an Active Directory site, it's possible to manually create the Send connectors required to establish mail flow between the Mailbox server and the Edge Transport server. For more information, see [Configurar el flujo de correo de Internet a través de un servidor de transporte perimetral sin usar EdgeSync](configure-internet-mail-flow-through-an-edge-transport-server-without-using-edgesync-exchange-2013-help.md). However, we recommend you subscribe the Edge Transport server to the Active Directory site whenever possible.

## Before you begin

  - Estimated time to complete: 20 minutes.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "EdgeSync" entry and the "Edge Transport servers" in the [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md) topic.

  - Before you subscribe an Edge Transport server to your organization, you will first need to configure authoritative domains and email address policies for your Exchange organization.

  - Enable the secure LDAP port 50636/TCP through the firewall separating your perimeter network from the Exchange organization. The Edge Transport server needs to be able to communicate with all Exchange 2013 Mailbox servers in the subscribed Active Directory site.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Configure Internet mail flow through a subscribed Edge Transport server

1.  On the Edge Transport server, create the Edge Subscription file using the following syntax.
    
    ```powershell
    New-EdgeSubscription -FileName <FileName>.xml [-Force]
    ```
    
    The following example creates an Edge Subscription file named EdgeSubscriptionInfo.xml in the folder C:\\My Documents. The *Force* parameter suppresses prompts confirming commands that will be disabled and warnings that configuration data will be overwritten on the Edge Transport server.
    
    ```powershell
    New-EdgeSubscription -FileName "C:\My Documents\EdgeSubscriptionInfo.xml" -Force
    ```

2.  Copy the resulting Edge Subscription file to a Mailbox server in the Active Directory site you're subscribing the Edge Transport server to.

3.  On the Mailbox server, to import the Edge Subscription file, use the following syntax.
    
    ```powershell
    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "<FileName>.xml" -Encoding Byte -ReadCount 0)) -Site <SiteName>
    ```
    
    This example imports the Edge Subscription file named EdgeSubscriptionInfo.xml from the folder D:\\Data, and subscribes the Edge Transport server to the Active Directory site named "Default-First-Site-Name".
    
    ```powershell
    New-EdgeSubscription -FileData ([byte[]]$(Get-Content -Path "D:\Data\EdgeSubscriptionInfo.xml" -Encoding Byte -ReadCount 0)) -Site "Default-First-Site-Name"
    ```
    

    > [!NOTE]
    > You can use the <EM>CreateInternetSendConnector</EM> or <EM>CreateInboundSendConnector</EM> parameters to prevent one or both of the required Send connectors from being automatically created. For more information, see <A href="edge-subscriptions-exchange-2013-help.md">Suscripciones perimetrales</A>.



4.  On the Mailbox server, run the following command to start the first EdgeSync synchronization.
    
    ```powershell
    Start-EdgeSynchronization
    ```

5.  When you're finished, we strongly recommend you delete the Edge Subscription file from both the Edge Transport server and from the Mailbox server. The Edge Subscription file contains information about credentials used during the LDAP communication process.

