---
ms.localizationpriority: medium
description: Admin can learn about the different recipient types in Exchange Online.
ms.topic: article
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 50d16941-5cd7-435d-8715-e2b69f8410ab
f1.keywords:
- NOCSH
title: Recipients in Exchange Online
ms.reviewer:
ms.collection:
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
manager: serdars
ms.custom: seo-marvel-apr2020
---

# Recipients in Exchange Online

A recipient is any mail-enabled object in Exchange Online that can receive email messages. Exchange Online includes several recipient types. Each recipient type is identified in the Exchange admin center (EAC) and has a unique value in the _RecipientTypeDetails_ property in Exchange Online PowerShell.

> [!NOTE]
> In Exchange Online, the new EAC enhances the admin experience with a different look and feel. The **Mailboxes** and **Shared** mailboxes tabs under **Recipients** in the Classic EAC are now merged into a single **Mailboxes** tab under **Recipients** in the new EAC. On the **Mailboxes** tab, you can view shared mailboxes and user mailboxes under one list view. For more information, see [Exchange admin center in Exchange Online](../exchange-admin-center.md).

The following table describes the different types of recipients in Exchange Online and provides links to articles that explain how to manage and configure them.

|Recipient type|Description|
|---|---|
|**Users**||
|User mailbox|A mailbox that's assigned to an individual user in your Exchange Online organization. A mailbox contains the user's email messages, calendar items, contacts, tasks, and other important business data. <p> [Create user mailboxes in Exchange Online](create-user-mailboxes.md).|
|Shared mailbox|A mailbox that's designed for access by multiple users. <p> Shared mailboxes do not require licenses in Exchange Online. <p> [Shared mailboxes in Exchange Online](../collaboration-exo/shared-mailboxes.md)|
|Mail contact|A mail contact contains information about a person who's outside of your Exchange Online organization. A mail contact has an external email address, but the mail contact is visible in your organization's shared address book (also known as the global address list or GAL) and other address lists. <p> [Manage mail contacts](manage-mail-contacts.md)|
|Mail user|A mail user (also known as a _mail-enabled user_) is similar to a mail contact in that it represent a user with an external email address and is visible in your organization's shared address book and other address lists. However, a mail user also has a user account in your organization, and you can assign permissions to the mail user. <p> Mail users do not require licenses in Exchange Online. <p> [Manage mail users](manage-mail-users.md)|
|**Resources**||
|Room mailbox|A type of resource mailbox that's assigned to a meeting location, such as a conference room, auditorium, or training room. Room mailboxes can be included as resources in meeting requests. <p> [Manage resource mailboxes](manage-resource-mailboxes.md)|
|Equipment mailbox|A type of resource mailbox that's assigned to a resource that's not location-specific, such as a portable computer, projector, microphone, or a company car. Equipment mailboxes can be included as resources in meeting requests. <p> [Manage resource mailboxes](manage-resource-mailboxes.md)|
|**Groups**||
|Distribution group|Distribution groups (also known as _distribution lists_) provide a single point of contact for delivering email to the members of the group. <p> [Create and manage distribution groups](manage-distribution-groups/manage-distribution-groups.md).|
|Mail-enabled security group|Like a distribution group, a mail-enabled security group provides a single point of contact for delivering email to the members of the group. However, a mail-enabled security group is also a _security principal_, which means you can assign permissions to the group that affect all group members who are also security principals (user mailboxes, mail users, other mail-enabled security groups, etc.). <p> [Manage mail-enabled security groups](manage-mail-enabled-security-groups.md).|
|Dynamic distribution group|A dynamic distribution group uses recipient filters and conditions to periodically calculate the membership of the group. <p> [Manage dynamic distribution groups](manage-dynamic-distribution-groups/manage-dynamic-distribution-groups.md)|
|**Collaboration**||
|Microsoft 365 group|Microsoft 365 groups (formerly known as Office 365 groups), are used for collaboration between teams, both inside and outside your company, by providing group email and a shared workspace for conversations, files, and calendars. <p> For email, the benefit of a Microsoft 365 group over traditional groups is: the email history of the group is preserved. If a new user joins an old Microsoft 365 group, the entire email history of the group is available to them. <p> [Create and manage groups](create-and-manage-groups.md)|
|Mail-enabled public folder|A public folder is designed for shared access to collect, organize, and share information. <p> [Public folders in Microsoft 365, Office 365, and Exchange Online](../collaboration-exo/public-folders/public-folders.md)|

## See also

- [Manage permissions for recipients](manage-permissions-for-recipients.md)
- [Plus Addressing](plus-addressing-in-exchange-online.md)
- To find information about message and recipient limits in Exchange Online, check out the new article at [Exchange Online Limits](/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits).
