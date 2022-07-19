---
title: "Can't install Exchange 2013 in a forest containing Exchange 2000 or Exchange 2003 servers"
TOCTitle: Can't install Exchange 2013 in a forest containing Exchange 2000 or Exchange 2003 servers.
ms:assetid: a115b182-cbd2-4d31-aa0e-375240939301
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.setupreadiness.exchange2000or2003presentinorg(v=EXCHG.150)
ms:contentKeyID: 49090987
ms.topic: article
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about the 'Can't install Exchange 2013 in a forest containing Exchange 2000 or Exchange 2003 servers' error.
---

# Can't install Exchange 2013 in a forest containing Exchange 2000 or Exchange 2003 servers

_**Applies to:** Exchange Server 2013_

Microsoft Exchange Server 2013 can't continue because one or more computers running Exchange 2000 Server or Exchange Server 2003 were found in the Active Directory forest. Before you can install Exchange 2013, all Exchange 2000 and Exchange 2003 servers must be removed from the forest. Mailboxes, public folders, and all other Exchange objects or components must be upgraded to either Exchange Server 2007 or Exchange Server 2010. You can't upgrade from Exchange 2000 or Exchange 2003 directly to Exchange 2013.

The path you need to follow to install Exchange 2013 in your organization depends on the version of Exchange you currently have installed in your forest. See the following table for more information.

|If you have the following installed in your organization|You must take this path to upgrade to Exchange 2013|
|---|---|
|Exchange 2000|<ol><li>Install Exchange 2007 into your Exchange 2000 organization.</li><li>Configure Exchange 2007 and Exchange 2000 coexistence.</li><li>Migrate Exchange 2000 mailboxes, public folders, and other components to Exchange 2007.</li><li>Decommission and remove all Exchange 2000 servers.</li><li>Install Exchange 2013 into your Exchange 2007 organization.</li><li>Configure Exchange 2013 and Exchange 2007 coexistence.</li><li>Migrate Exchange 2007 mailboxes, public folders, and other components to Exchange 2013.</li><li>Decommission and remove all Exchange 2007 servers.</li></ol> <p> For more information, see [Upgrading to Exchange 2007](/previous-versions/office/exchange-server-2007/bb124008(v=exchg.80)) and [Upgrade from Exchange 2007 to Exchange 2013](upgrade-from-exchange-2007-to-exchange-2013-exchange-2013-help.md).|
|Exchange 2003|<ol><li>Install Exchange 2010 into your Exchange 2003 organization.</li><li>Configure Exchange 2010 and Exchange 2003 coexistence.</li><li>Migrate Exchange 2003 mailboxes, public folders, and other components to Exchange 2010.</li><li>Decommission and remove all Exchange 2003 servers.</li><li>Install Exchange 2013 into your Exchange 2010 organization.</li><li>Configure Exchange 2013 and Exchange 2010 coexistence.</li><li>Migrate Exchange 2010 mailboxes, public folders, and other components to Exchange 2013.</li><li>Decommission and remove all Exchange 2010 servers.</li></ol> <p> For more information, see [Exchange 2003 - Planning Roadmap for Upgrade and Coexistence](/previous-versions/office/exchange-server-2010/aa998186(v=exchg.141)) and [Upgrade from Exchange 2010 to Exchange 2013](upgrade-from-exchange-2010-to-exchange-2013-exchange-2013-help.md).|

When upgrading to Exchange 2013 or later, you can use the Exchange Deployment Assistant to help complete your deployment. For more information, see [Exchange Deployment Assistant](https://assistants.microsoft.com/).

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

Did you find what you're looking for? Please take a minute to [send us feedback](mailto:exsetuphelpfeedback@microsoft.com?subject=exchange%202013%20setup%20help%20feedback) about the information you were hoping to find.
