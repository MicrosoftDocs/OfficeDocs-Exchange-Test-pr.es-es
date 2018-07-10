---
title: 'Deshabilitar o volver a habilitar compartir federados para la organización de Exchange: Exchange 2013 Help'
TOCTitle: Deshabilitar o volver a habilitar compartir federados para la organización de Exchange
ms:assetid: d36490d8-0268-47b9-a6d4-e56427f1b02e
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657497(v=EXCHG.150)
ms:contentKeyID: 49895935
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Deshabilitar o volver a habilitar compartir federados para la organización de Exchange

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-17_

There may be situations when you need to temporarily disable federated sharing for your organization. Instead of deleting the existing federation trust or deleting organization relationships and sharing policies that you may need in the future, you can simply disable the organization identifier (OrgID) for the federation trust.


> [!WARNING]
> For hybrid deployments with Office&nbsp;365, disabling the federation trust for your on-premises servers will also disable hybrid features such as shared calendar free/busy information, MailTips, and message tracking. However, secure mail transport won’t be disabled in the hybrid deployment if the federation trust for the on-premises organization is disabled.



To learn more about federation trusts, see [Federación](federation-exchange-2013-help.md). To learn more about federated sharing, see [Uso compartido](sharing-exchange-2013-help.md).

For additional management tasks related to federated sharing, see [Procedimientos de la Federación](federation-procedures-exchange-2013-help.md).


> [!IMPORTANT]
> Esta característica de Exchange Server 2013 no es totalmente compatible con Office 365 operado por 21Vianet en China y pueden aplicarse ciertas limitaciones en las características. Para obtener más información, consulte <A href="https://go.microsoft.com/fwlink/?linkid=313640">Acerca de Office 365 operado por 21Vianet</A>.



## What do you need to know before you begin?

  - Estimated time to complete: 5 minutes.

  - Deberá tener asignados permisos antes de poder llevar a cabo este procedimiento o procedimientos. Para ver qué permisos necesita, consulte el *Federation and certificates* permissions entry in the [Permisos de infraestructura de la Shell y de Exchange](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md) topic.

  - Any existing organization relationships and sharing policies for other federated Exchange organizations won’t be modified and won’t be functional. Sharing policies that are configured to provide Internet recipients with access to calendar information won’t be affected.

  - You can’t use the Exchange Administration Center (EAC) to disable or enable the OrgID for a federation trust. You must use the Shell.

## Use the Shell to disable or re-enable federated sharing

This example disables the OrgID and disables federation and federated sharing for the Exchange organization.

    Set-FederatedOrganizationIdentifier -Enabled $false

This example enables the OrgID and re-enables federation and federated sharing for the Exchange organization.

    Set-FederatedOrganizationIdentifier -Enabled $true

For detailed syntax and parameter information, see [Set-FederatedOrganizationIdentifier](https://technet.microsoft.com/es-es/library/dd351037\(v=exchg.150\)).

## How do you know this worked?

Successful completion of the **Set-OrganizationIdentifier** cmdlet will be the first indication that the OrgID has been disabled or enabled.

To further verify success, run the following Shell command and verify the value returned for the *Enabled* parameter

    Get-FederatedOrganizationIdentifier


> [!TIP]
> ¿Tiene algún problema? Solicite ayuda en los foros de Exchange. Visite los foros en <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, o <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Exchange Online Protection</A>.


