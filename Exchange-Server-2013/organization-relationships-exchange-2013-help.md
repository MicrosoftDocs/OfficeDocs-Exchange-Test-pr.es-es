﻿---
title: 'Relaciones entre organizaciones: Exchange 2013 Help'
TOCTitle: Relaciones entre organizaciones
ms:assetid: 4c48db61-3370-462b-a3f8-2a6311c6e4ee
ms:mtpsurl: https://technet.microsoft.com/es-es/library/JJ657445(v=EXCHG.150)
ms:contentKeyID: 49895616
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Relaciones entre organizaciones

 

_**Se aplica a:** Exchange Server 2013_

_**Última modificación del tema:** 2014-02-20_

Set up an organization relationship to share calendar information with an external business partner. Exchange admins can set up an organization relationship with an Office 365 organization or with another Exchange on-premises organization. If you want to share calendars with another on-premises Exchange organization, both on-premises Exchange administrators have to set up an authentication relationship with the cloud (also known as “federation”) and must meet minimum software requirements.

An organization relationship is a one-to-one relationship between businesses to allow users in each organization to view calendar availability information. When you set up the organization relationship, you are setting up your side of the relationship and specifying the level of information that the users in the external organization can view. The external organization may set up the same or different settings on their side. For example, if Contoso creates an organization relationship with Tailspin Toys, the users at Tailspin Toys will be able to schedule meetings with the users at Contoso by adding their email address to the meeting invitation. The availability of the invited Contoso user would display to the Tailspin Toys user. However, before Contoso can also see availability for users at Tailspin Toys, their administrator needs to set up an organization relationship with Contoso.

There are three of levels of access that you can specify:

  - No access

  - Access to availability (free/busy) time only

  - Access to free/busy, including time, subject, and location


> [!NOTE]
> If users don't want to share their free/busy information with others, they can change the Default permission entry in Outlook. To do this, users go to the <STRONG>Calendar Properties</STRONG> &gt; <STRONG>Permissions</STRONG> tab, select the <STRONG>Default</STRONG> permission, and select <STRONG>None</STRONG> from the <STRONG>Permission Level</STRONG> list. Their free/busy information won't be seen by internal or external users, even if an organization relationship exists. The permissions set by the user will apply.



The following topics will help you configure and manage organization relationships as a part of sharing for your organization:

[Crear una relación de organización](create-an-organization-relationship-exchange-2013-help.md)

[Modificar una relación de la organización](modify-an-organization-relationship-exchange-2013-help.md)

[Quitar una relación de la organización](remove-an-organization-relationship-exchange-2013-help.md)

Looking for more information about federated sharing? See [Uso compartido](sharing-exchange-2013-help.md).

