---
title: 'Configurar dominio aceptado para una unidad de negocio independiente'
TOCTitle: Configure un dominio aceptado para una unidad de negocio independiente
ms:assetid: bc95dbdc-3669-4c06-ab94-90093bc0dbfd
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657491(v=EXCHG.150)
ms:contentKeyID: 49895876
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configure un dominio aceptado para una unidad de negocio independiente

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-17_

In some situations you may want to configure an accepted domain for an independent business unit with email servers outside your Exchange organization. In such scenarios, you can configure the accepted domain as an external relay domain.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Accepted domains" entry in the [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md) topic.

  - Si tiene un servidor Transporte perimetral con suscripción en la red perimetral, puede configurar dominios aceptados en un servidor de buzones de la organización de Exchange. La configuración de los dominios aceptados se replica al servidor Transporte perimetral durante la sincronización de EdgeSync. Para obtener más información, consulte [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

  - You can't create an accepted domain that has the same name as an already configured remote domain. For example, if you have fabrikam.com configured as a remote domain, you can't create an accepted domain for fabrikam.com.

  - Before you configure an accepted domain, you must verify that a public Domain Name System (DNS) MX resource record for that SMTP namespace exists and that the MX resource record references a server name and an IP address associated with your Exchange organization.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the EAC to configure the an accepted domain as an external relay domain

You may want to configure an accepted domain for a business unit with email servers outside your Exchange organization.

1.  In the EAC, navigate to **Mail flow** \> **Accepted domains**, select the domain you wish to configure, and click **Edit**![Icono Editar](images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif "Icono Editar").

2.  In the **Name** field, enter the display name for the accepted domain. Each accepted domain for your organization must have a unique display name. This may be different than the accepted domain. For example, the domain Contoso.com could have a display name of Contoso Local Accepted Domain.

3.  Select **External Relay Domain**. This option is for email is relayed to a server outside your Exchange organization.

4.  Click **Save**.

## How do you know this worked?

To verify that you have successfully configured an accepted domain as an external relay domain, send a message from the accepted domain you’ve configured as an external relay domain, and verify that it is received.

