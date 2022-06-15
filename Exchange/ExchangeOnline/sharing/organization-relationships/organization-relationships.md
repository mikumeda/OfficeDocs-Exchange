---
ms.localizationpriority: medium
description: Set up an organization relationship to share calendar information with an external business partner. Microsoft 365 and Office 365 admins can set up an organization relationship with another Microsoft 365 or Office 365 organization or with an Exchange on-premises organization. If you want to share calendars with an on-premises Exchange organization, the on-premises Exchange administrator has to set up an authentication relationship with the cloud (also known as federation) and must meet minimum software requirements.
ms.topic: article
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 58ac4338-b883-404f-a6be-eca38ccd8088
ms.reviewer: 
f1.keywords:
- NOCSH
title: Organization relationships in Exchange Online
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
manager: serdars

---

# Organization relationships in Exchange Online

Set up an organization relationship to share calendar information with an external business partner. Microsoft 365 or Office 365 admins can set up an organization relationship with another Microsoft 365 and Office 365 organization or with an Exchange on-premises organization. If you want to share calendars with an on-premises Exchange organization, the on-premises Exchange administrator has to set up an authentication relationship with the cloud (also known as "federation") and must meet minimum software requirements.

> [!NOTE]
> Organization functionality of the Classic Exchange admin center experience is available in the new Exchange admin center as we continue to work on updated versions. If you're using **Edge** incognito and this page isn't working, enable the [third-party cookies](https://support.microsoft.com/microsoft-edge/temporarily-allow-cookies-and-site-data-in-microsoft-edge-597f04f2-c0ce-f08c-7c2b-541086362bd2).

An organization relationship is a one-to-one relationship between businesses to allow users in each organization to view calendar availability information. When you set up the organization relationship, you're responsible for setting up your side of the relationship. You specify the level of information that users in the external organization can view in your organization. The external organization is responsible for setting up their side of the relationship and specifying their level of information that's visible to users in your organization (which might be different than yours). The point is: the organization relationship must be set up at both ends for calendar availability information to be shared.

For example, a Contoso admin creates an organization relationship with Tailspin Toys, and a Tailspin Toys admin creates an organization relationship with Contoso. As a result, Tailsping Toys users will be able to schedule meetings and view the availability of Contoso users Contoso by adding Contoso email addresses to meeting invitations. Likewise, Contoso users will also see the availability of Tailspin Toys users when scheduling meetings.

There are three levels of access that you can specify:

- No access.
- Access to availability (free/busy) time only.
- Access to free/busy, including time, subject, and location.

> [!NOTE]
> If users don't want to share their free/busy information with others, they can change their permissions entry in Outlook. To do this, users go to the **Calendar Properties** \> **Permissions** tab, select one or more users/groups, and select any of the **Permissions** options.
>
> To completely hide their calendar, they can remove the user/group from the list of those with which the calendar is shared. Their free/busy information won't be seen by internal or external users, even if an organization relationship exists. The permissions set by the user will apply.

The following articles will help you configure and manage organization relationships:

[Create an organization relationship in Exchange Online](create-an-organization-relationship.md)

[Modify an organization relationship in Exchange Online](modify-an-organization-relationship.md)

[Remove an organization relationship in Exchange Online](remove-an-organization-relationship.md)
