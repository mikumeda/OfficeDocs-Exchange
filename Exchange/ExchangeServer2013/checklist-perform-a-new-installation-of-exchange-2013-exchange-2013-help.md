---
title: 'Checklist: Perform a new installation of Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Checklist: Perform a new installation of Exchange 2013'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 49289467
ms.topic: article
description: Use this checklist to deploy Microsoft Exchange Server 2013.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Checklist: Perform a new installation of Exchange 2013

_**Applies to:** Exchange Server 2013_

Use this checklist to deploy Microsoft Exchange Server 2013. Before you start working with this checklist, make sure you're familiar with the concepts discussed in:

- [Planning and deployment](planning-and-deployment-for-exchange-2013-installation-instructions.md)

- [Deployment security checklist](deployment-security-checklist-exchange-2013-help.md)

This checklist is generic in that it provides guidance for a typical scenario.

> [!NOTE]
> The Exchange Server Deployment Assistant provides you with customized step-by-step guidance about how to deploy Exchange Server. The Deployment Assistant can help you deploy a new installation of Exchange Server 2013, upgrade a previous version to Exchange 2013, or configure a hybrid deployment of Exchange 2013 and Exchange Online. To learn more, see [Exchange Server Deployment Assistant](exchange-server-deployment-assistant-exchange-2013-help.md).

## Checklist for a new installation of Exchange 2013

|Done?|Task|Topic|
|:---:|---|---|
|☐|1. Read the release notes.|[Release notes for Exchange 2013](release-notes-for-exchange-2013-exchange-2013-help.md)|
|☐|2. Verify system requirements.|[Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md)|
|☐|3. Confirm prerequisite steps are done.|[Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md)|
|☐|4. Configure disjoint namespace. <br/><br/> **Note**: This step is optional. It's only necessary if your organization is running a disjoint namespace.|
|[Disjoint namespace scenarios](disjoint-namespace-scenarios-exchange-2013-help.md)|
|☐|5. Install the Mailbox server role.|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)|
|☐|6. Install the Client Access server role.|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)|
|☐|7. Install the Edge Transport server role. <br/><br/> **Note**: This step is optional. It's only necessary if you want to install an Edge Transport server. For more information, see [Edge Transport servers](edge-transport-servers-exchange-2013-help.md).|[Install the Exchange 2013 Edge Transport role using the Setup wizard](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md)|
|☐|8. Create an EdgeSync subscription. <br/><br/> This step is optional. It's only necessary if you've installed an Edge Transport server and want to configure an EdgeSync subscription between your Edge Transport server and a Hub Transport server. For more information, see [Edge Subscriptions](edge-subscriptions-exchange-2013-help.md).|[Configure Internet mail flow through a subscribed Edge Transport server](configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md)|
|☐|9. Configure Transport.|[Create a Send connector](configure-mail-flow-and-client-access-exchange-2013-help.md)|
|☐|10. Add additional accepted domains.|[Add additional accepted domains](configure-mail-flow-and-client-access-exchange-2013-help.md)|
|☐|11. Configure email address policies.|[Configure the default email address policy](configure-mail-flow-and-client-access-exchange-2013-help.md)|
|☐|12. Configure settings on virtual directories, including the offline address book, Exchange Web Services, Exchange admin center (EAC), Outlook Web App, and Exchange ActiveSync virtual directories. <br/><br/> **Note**: This step is necessary if you want to use Exchange Web Services, Outlook Anywhere, or the offline address book. It also may be required if you need to change any of the default settings for EAC, Outlook Web App, or Exchange ActiveSync.|[Configure external URLs](configure-mail-flow-and-client-access-exchange-2013-help.md) <br/><br/> [Configure internal URLs](configure-mail-flow-and-client-access-exchange-2013-help.md)|
|☐|13. Add digital certificates on the Client Access server.|[Configure an SSL certificate](configure-mail-flow-and-client-access-exchange-2013-help.md)|
|☐|14. Configure Unified Messaging. <br/><br/> **Note**: This step is optional. It's only necessary if you want to use Unified Messaging in your organization.|
|[Deploying voice mail and UM](deploying-voice-mail-and-um-exchange-2013-help.md)|
|☐|15. Configure additional Unified Messaging and Lync Server settings. <br/><br/> **Note**: This step is optional. It's only necessary if you've configured Unified Messaging in your organization and want to integrate it with Lync Server.|[Deploying Exchange 2013 UM and Lync Server overview](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)|
|☐|16. Post-installation tasks.|[Exchange 2013 post-Installation tasks](exchange-2013-post-installation-tasks-exchange-2013-help.md)|
