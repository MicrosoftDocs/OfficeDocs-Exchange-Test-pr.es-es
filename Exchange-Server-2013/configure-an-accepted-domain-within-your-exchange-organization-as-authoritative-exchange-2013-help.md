---
title: 'Configurar dominio aceptado dentro su organización Exchange como autoritativo'
TOCTitle: Configurar un dominio aceptado dentro de su organización de Exchange como autoritativo
ms:assetid: e182d54f-e58a-47ba-a5c1-28c0dfa86eed
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657734(v=EXCHG.150)
ms:contentKeyID: 49895973
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Configurar un dominio aceptado dentro de su organización de Exchange como autoritativo

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-17_

If a domain belonging to your organization hosts mailboxes for all the recipients within an SMTP namespace, that domain is considered to be authoritative. By default, one accepted domain is configured as authoritative for the Exchange organization. If your organization has more than one SMTP namespace, you can configure more than one accepted domain as authoritative.

## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el "Accepted domains" entry in the [Permisos de flujo del correo](mail-flow-permissions-exchange-2013-help.md) topic.

  - Si tiene un servidor Transporte perimetral con suscripción en la red perimetral, puede configurar dominios aceptados en un servidor de buzones de la organización de Exchange. La configuración de los dominios aceptados se replica al servidor Transporte perimetral durante la sincronización de EdgeSync. Para obtener más información, consulte [Suscripciones perimetrales](edge-subscriptions-exchange-2013-help.md).

  - You can't create an accepted domain that has the same name as an already configured remote domain. For example, if you have fabrikam.com configured as a remote domain, you can't create an accepted domain for fabrikam.com.

  - Before you configure an accepted domain, you must verify that a public Domain Name System (DNS) MX resource record for that SMTP namespace exists and that the MX resource record references a server name and an IP address associated with your Exchange organization.

  - Para obtener información acerca de los métodos abreviados de teclado aplicables a los procedimientos de este tema, consulte [Métodos abreviados de teclado en el Centro de administración de Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.



## Use the EAC to configure an accepted domain as authoritative

If an accepted domain for your Exchange organization hosts all the mailboxes for recipients within that domain’s SMTP namespace, you may want to configure it as an authoritative domain.

1.  In the EAC, navigate to **Mail flow** \> **Accepted domains**, and click **Add**![Agregar icono](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Agregar icono").

2.  In the **Name** field, enter the display name for the accepted domain. Each accepted domain for your organization must have a unique display name This may be different than the accepted domain. For example, the domain contoso.com could have a display name of Contoso Local Accepted Domain.

3.  In the **Accepted domain** field, enter the accepted domain. Specify an SMTP namespace for which your organization accepts email messages. (for example, Contoso.com).

4.  Select **Authoritative domain**. This option is for email relayed to servers within your Exchange organization for an accepted domain that hosts mailboxes for all the recipients within an SMTP namespace.

5.  Click **Save**.


> [!TIP]
> To configure an accepted domain that has already been created, select the domain from the accepted domains list and click <STRONG>Edit</STRONG><IMG title="Icono Editar" alt="Icono Editar" src="images/Bb124582.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif">. You can configure more than one domain as authoritative.



## How do you know this worked?

Your new accepted domain will appear in the accepted domains list in the EAC. To verify that you have successfully configured the accepted domain as authoritative, send mail to the domain and verify that it is received.

