---
title: 'Upgrade from Exchange 2010 to Exchange 2013: Exchange 2013 Help'
TOCTitle: Upgrade from Exchange 2010 to Exchange 2013
ms:assetid: c0558850-d583-4c4e-a9a0-0d3593f84fcc
ms:mtpsurl: https://technet.microsoft.com/library/JJ898583(v=EXCHG.150)
ms:contentKeyID: 50874011
ms.reviewer: 
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: How to upgrade from Microsoft Exchange 2010 to Exchange 2013
---

# Upgrade from Exchange 2010 to Exchange 2013

_**Applies to:** Exchange Server 2013_

Microsoft Exchange Server 2010 and Exchange Server 2007 have multiple server roles: Client Access, Mailbox, Hub Transport, Unified Messaging, and Edge Transport. With Exchange Server 2013, we reduced the number of server roles from five to three: Client Access, Mailbox, and Edge Transport. Unified Messaging is now considered a component or sub-feature of the voice-related features that are offered in Exchange 2013. (For more details about the changes, see "Exchange 2013 architecture" in [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).)

When you're upgrading your existing Exchange 2010 organization to Exchange 2013, there's a period of time when Exchange 2010 and Exchange 2013 servers will coexist within your organization. You can maintain this mode for an indefinite period of time, or you can immediately complete the upgrade to Exchange 2013 by moving all resources from Exchange 2010 to Exchange 2013, and then decommissioning the Exchange 2010 servers. You have a coexistence scenario if the following conditions are true:

- Exchange 2013 is deployed in an existing Exchange organization.
- More than one version of Microsoft Exchange provides messaging services to the organization.

You can't upgrade an existing Exchange 2003 organization directly to Exchange 2013. You must first upgrade the Exchange 2003 organization to either an Exchange 2007 or Exchange 2010 organization, and then you can upgrade the Exchange 2007 or Exchange 2010 organization to Exchange 2013. We recommend that you upgrade your organization from Exchange 2003 to Exchange 2010, and then upgrade from Exchange 2010 to Exchange 2013.

> [!WARNING]
> You need to remove all instances of Exchange 2003 from your organization before you can upgrade to Exchange 2013.

You can migrate all your Exchange 2003 mailboxes to Exchange Online. For more information about this approach, see [Ways to migrate multiple email accounts to Office 365](../ExchangeOnline/mailbox-migration/mailbox-migration.md).

The following table lists the scenarios in which coexistence between Exchange 2013 and earlier versions of Exchange is supported.

## Coexistence of Exchange 2013 and earlier versions of Exchange Server

|Exchange version|Exchange organization coexistence|
|---|---|
|Exchange Server 2003 and earlier versions|Not supported|
|Exchange 2007|Supported with the following minimum versions of Exchange: <ul><li>Update Rollup 10 for Exchange 2007 Service Pack 3 (SP3) on all Exchange 2007 servers in the organization, including Edge Transport servers.<sup>1</sup></li><li>Exchange 2013 Cumulative Update 2 (CU2) or later on all Exchange 2013 servers in the organization.</li></ul>|
|Exchange 2010|Supported with the following minimum versions of Exchange: <ul><li>Exchange 2010 SP3 on all Exchange 2010 servers in the organization, including Edge Transport servers.<sup>2</sup></li><li>Exchange 2013 CU2 or later on all Exchange 2013 servers in the organization.</li></ul>|
|Mixed Exchange 2010 and Exchange 2007 organization|Supported with the following minimum versions of Exchange: <ul><li>Update Rollup 10 for Exchange 2007 SP3 on all Exchange 2007 servers in the organization, including Edge Transport servers.<sup>1</sup></li><li>Exchange 2010 SP3 on all Exchange 2010 servers in the organization, including Edge Transport servers.<sup>2</sup></li><li>Exchange 2013 CU2 or later on all Exchange 2013 servers in the organization.</li></ul>|

<sup>1</sup>If you want to create an EdgeSync Subscription between an Exchange 2007 Hub Transport server and an Exchange 2013 SP1 Edge Transport server, you need to install Exchange 2007 SP3 Update Rollup 13 or later on the Exchange 2007 Hub Transport server.

<sup>2</sup>If you want to create an EdgeSync Subscription between an Exchange 2010 Hub Transport server and an Exchange 2013 SP1 Edge Transport server, you need to install Exchange 2010 SP3 Update Rollup 5 or later on the Exchange 2010 Hub Transport server.

## Mixed mode coexistence of Exchange 2013 and Exchange 2007 with Exchange 2010

If you have Active Directory sites with both Exchange 2010 and Exchange 2007 installed, follow the upgrade instructions from both Exchange 2010 and Exchange 2007, and perform the upgrade steps required by both.

## Overview of the upgrade process

To help you get an overview of the Exchange 2010 to Exchange 2013 upgrade process, we've gathered resources related to each key task in the following table. For specific step-by-step guidance, see [Checklist: Upgrade from Exchange 2010](checklist-upgrade-from-exchange-2010-exchange-2013-help.md).

|Task|Topic|
|---|---|
|Learn about Exchange 2013 roles and components|[What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md) <br><br> [Client Access server](client-access-server-exchange-2013-help.md) <p> [Mailbox server](mailbox-server-exchange-2013-help.md) <p> [Mail flow](mail-flow-exchange-2013-help.md) <p> [Unified Messaging](unified-messaging-exchange-2013-help.md)|
|Install Exchange 2013|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md) <br><br> [Install the Exchange 2013 Edge Transport role using the Setup wizard](install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md) (optional) <p> [Verify an Exchange 2013 installation](verify-an-exchange-2013-installation-exchange-2013-help.md)|
|Add digital certificates on the Client Access server|[Exchange 2013 Client Access server configuration](exchange-2013-client-access-server-configuration-exchange-2013-help.md) <br><br> [Digital certificates and SSL](digital-certificates-and-ssl-exchange-2013-help.md) <p> [Create a digital certificate request](create-a-digital-certificate-request-exchange-2013-help.md)|
|Configure Exchange-related virtual directories|[Default settings for Exchange virtual directories](default-settings-for-exchange-virtual-directories-exchange-2013-help.md)|
|Move mailboxes from Exchange 2010|[ilbox moves in Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)|
|Configure transport components|[Edge Subscriptions](edge-subscriptions-exchange-2013-help.md) (only necessary if you've installed an Edge Transport server) <br><br> [Mail routing](mail-routing-exchange-2013-help.md) <p> [Shadow redundancy](shadow-redundancy-exchange-2013-help.md) <p> [Delivery reports for administrators](delivery-reports-for-administrators-exchange-2013-help.md)|
|Configure and deploy UM|[Planning for Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md) <br><br> [Deploying voice mail and UM](deploying-voice-mail-and-um-exchange-2013-help.md)|
