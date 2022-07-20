---
title: 'Checklist: Upgrade from Exchange 2010: Exchange 2013 Help'
TOCTitle: 'Checklist: Upgrade from Exchange 2010'
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 50873999
ms.topic: article
description: Use this checklist to upgrade from Microsoft Exchange 2010 to Exchange 2013.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Checklist: Upgrade from Exchange 2010

_**Applies to:** Exchange Server 2013_

Use this checklist to upgrade from Microsoft Exchange 2010 to Exchange 2013. Before you start working with this checklist, make sure you're familiar with the concepts discussed in:

- [Planning and deployment](planning-and-deployment-for-exchange-2013-installation-instructions.md)

- [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

This checklist is generic in that it provides guidance for a typical upgrade scenario.

> [!NOTE]
> The Exchange Server Deployment Assistant provides you with customized step-by-step guidance about how to deploy Exchange Server. The Deployment Assistant can help you deploy a new installation of Exchange Server 2013, upgrade a previous version to Exchange 2013, or configure a hybrid deployment of Exchange 2013 and Exchange Online. To learn more, see [Exchange Server Deployment Assistant](exchange-server-deployment-assistant-exchange-2013-help.md).

## Checklist for upgrading from Exchange 2010 to Exchange 2013

|Done?|Task|Topic(s)|
|:---:|---|---|
|☐|1. Read the release notes.|[Release notes for Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md)|
|☐|2. Verify system requirements|[Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md)|
|☐|3. Confirm prerequisite steps are done|[Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md) <br/><br/> [Deployment security checklist](deployment-security-checklist-exchange-2013-help.md)|
|☐|4. Configure disjoint namespace <br/><br/> **Note**: This step is optional. It's only necessary if your organization is running a disjoint namespace.|[Configure the DNS suffix search list for a disjoint namespace](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md)|
|☐|5. Select an offline address book for all Exchange 2010 mailbox databases|[Set mailbox database properties](<manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md) in [Manage mailbox databases in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md)|
|☐|6. Install Exchange 2013|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md) <br/><br/> [Install the Exchange 2013 Edge Transport role using the Setup wizard](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md) <br/><br/> [Verify an Exchange 2013 installation](verify-an-exchange-2013-installation-exchange-2013-help.md)|
|☐|7. Create an Exchange 2013 mailbox|[Create user mailboxes](create-user-mailboxes-exchange-2013-help.md)|
|☐|8. Configure Exchange-related virtual directories <br/><br/> **Note**: This step is necessary if you want to use Exchange Web Services, Outlook Anywhere, or the offline address book. It also may be required if you need to change any of the default settings for Exchange Control Panel, Microsoft Office Outlook Web App, or Exchange ActiveSync.|[Exchange 2013 Client Access server configuration](exchange-2013-client-access-server-configuration-exchange-2013-help.md)|
|☐|9. Add digital certificates on the Client Access server|[Digital certificates and SSL](digital-certificates-and-ssl-exchange-2013-help.md) |
|☐|10. Move arbitration mailbox|[Move the Exchange 2010 system mailbox to Exchange 2013](move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md)|
|☐|11. Configure Unified Messaging <br/><br/> **Note**: This step is optional. It's only necessary if you want to use Unified Messaging in your organization.|[Upgrade Exchange 2010 UM to Exchange 2013 UM](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md)|
|☐|12. Configure Edge Transport server <br/><br/> **Note**: This step is optional. It's only necessary if your organization is uses an Edge Transport server.|[Configure Internet mail flow through a subscribed Edge Transport server](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md)|
|☐|13. Enable and configure Outlook Anywhere|[Outlook Anywhere](outlook-anywhere-exchange-2013-help.md)|
|☐|14. Configure service connection point|[Exchange 2013 Client Access server configuration](exchange-2013-client-access-server-configuration-exchange-2013-help.md)|
|☐|15. Configure DNS records|[Configure DNS records for Exchange 2010 multiple-server install](/previous-versions/exchange-server/exchange-150/dn307232(v=exchg.150))|
|☐|16. Move mailboxes from Exchange 2010 to Exchange 2013|[Mailbox moves in Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)|
|☐|17. Move public folder data from Exchange 2013 to Exchange 2013|[Public folders](public-folders-exchange-2013-help.md) <br/><br/> [Use serial migration to migrate public folders to Exchange 2013 from previous versions](/previous-versions/exchange-server/exchange-150/jj150486(v=exchg.150))|
|☐|18. Post-installation tasks|[Exchange 2013 post-Installation tasks](exchange-2013-post-installation-tasks-exchange-2013-help.md)|
