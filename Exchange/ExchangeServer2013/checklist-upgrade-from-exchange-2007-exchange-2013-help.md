---
title: 'Checklist: Upgrade from Exchange 2007: Exchange 2013 Help'
TOCTitle: 'Checklist: Upgrade from Exchange 2007'
ms:assetid: 53aaa370-4562-43e4-9b75-7a705400c5a5
ms:mtpsurl: https://technet.microsoft.com/library/Ff805032(v=EXCHG.150)
ms:contentKeyID: 50874004
ms.topic: article
description: Use this checklist to upgrade from Microsoft Exchange Server 2007 to Exchange Server 2013.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Checklist: Upgrade from Exchange 2007

_**Applies to:** Exchange Server 2013_

Use this checklist to upgrade from Microsoft Exchange Server 2007 to Exchange Server 2013. Before you start working with this checklist, make sure you're familiar with the concepts discussed in:

- [Planning and deployment](planning-and-deployment-for-exchange-2013-installation-instructions.md)

- [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

This checklist is generic in that it provides guidance for a typical upgrade scenario.

> [!NOTE]
> The Exchange Server Deployment Assistant provides you with customized step-by-step guidance about how to deploy Exchange Server. The Deployment Assistant can help you deploy a new installation of Exchange Server 2013, upgrade a previous version to Exchange 2013, or configure a hybrid deployment of Exchange 2013 and Exchange Online. To learn more, see [Exchange Server Deployment Assistant](exchange-server-deployment-assistant-exchange-2013-help.md).

## Checklist for upgrading from Exchange 2007 to Exchange 2013

|Done?|Task|Topic(s)|
|:---:|---|---|
|☐|1. Read the release notes.|[Release notes for Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md)|
|☐|2. Verify system requirements|[Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md)|
|☐|3. Confirm prerequisite steps are done|[Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md) <br/><br/> [Deployment security checklist](deployment-security-checklist-exchange-2013-help.md)|
|☐|4. Configure disjoint namespace <br/><br/> **Note**: This step is optional. It's only necessary if your organization is running a disjoint namespace.|[Configure the DNS suffix search list for a disjoint namespace](configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md)|
|☐|5. Select an offline address book for all Exchange 2007 mailbox databases|[How to Provision Recipients for Offline Address Book Downloads](/previous-versions/office/exchange-server-2007/aa996345(v=exchg.80))|
|☐|6. Create legacy Exchange hostname|[Create a legacy Exchange host name](/previous-versions/exchange-server/exchange-150/dn130105(v=exchg.150))|
|☐|7. Install Exchange 2013|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md) <br/><br/> [Install the Exchange 2013 Edge Transport role using the Setup wizard](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md) <br/><br/> [Verify an Exchange 2013 installation](verify-an-exchange-2013-installation-exchange-2013-help.md)|
|☐|8. Create an Exchange 2013 mailbox|[Create user mailboxes](create-user-mailboxes-exchange-2013-help.md)|
|☐|9. Configure Exchange-related virtual directories <br/><br/> **Note**: This step is necessary if you want to use Exchange Web Services, Outlook Anywhere, or the offline address book. It also may be required if you need to change any of the default settings for Exchange Control Panel, Microsoft Office Outlook Web App, or Exchange ActiveSync|
|[Exchange 2013 Client Access server configuration](exchange-2013-client-access-server-configuration-exchange-2013-help.md)|
|☐|10. Configure Exchange 2013 certificates|[Digital certificates and SSL](digital-certificates-and-ssl-exchange-2013-help.md)|
|☐|11. Configure Exchange 2007 certificates|[Managing SSL for a Client Access Server](/previous-versions/office/exchange-server-2007/bb310795(v=exchg.80))|
|☐|12. Configure Edge Transport server <br/><br/> **Note**: This step is optional. It's only necessary if your organization is uses an Edge Transport server.|[Configure Internet mail flow through a subscribed Edge Transport server](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md)|
|☐|13. Configure Unified Messaging **Note**: This step is optional. It's only necessary if you want to use Unified Messaging in your organization.|[Planning for Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md) <br/><br/> [Deploy Exchange 2013 UM](deploy-exchange-2013-um-exchange-2013-help.md)|
|☐|14. Enable and configure Outlook Anywhere|[Outlook Anywhere](outlook-anywhere-exchange-2013-help.md)|
|☐|15. Configure service connection point|[Exchange 2013 Client Access server configuration](exchange-2013-client-access-server-configuration-exchange-2013-help.md)|
|☐|16. Configure Exchange 2007 URLs|[Configure Exchange 2007 external URLs](/previous-versions/exchange-server/exchange-150/dn282262(v=exchg.150))|
|☐|17. Configure DNS records|[Configure DNS records for Exchange 2007 multiple-server install](/previous-versions/exchange-server/exchange-150/dn283988(v=exchg.150))|
|☐|18. Move mailboxes from Exchange 2007 to Exchange 2013|[Mailbox moves in Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)|
|☐|19. Move public folder data from Exchange 2007 to Exchange 2013 **Note**: This step is optional. It's only necessary if your organization is uses public folders.|[Public folders](public-folders-exchange-2013-help.md) <br/><br/> [Use serial migration to migrate public folders to Exchange 2013 from previous versions](/previous-versions/exchange-server/exchange-150/jj150486(v=exchg.150))|
|☐|20. Post-installation tasks|[Exchange 2013 post-Installation tasks](exchange-2013-post-installation-tasks-exchange-2013-help.md)|
