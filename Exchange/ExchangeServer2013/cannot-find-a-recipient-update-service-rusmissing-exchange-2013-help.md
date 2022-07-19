---
title: 'Cannot find a recipient update service_RUSMissing: Exchange 2013 Help'
TOCTitle: Cannot find a recipient update service_RUSMissing
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 46629034
ms.topic: article
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about the 'Cannot find a recipient update service\_RUSMissing' error.
---

# Cannot find a recipient update service\_RUSMissing

_**Applies to:** Exchange Server 2013_

The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

Microsoft® Exchange Server 2007 or Exchange Server 2010 setup cannot continue because the Recipient Update Service (RUS) responsible for a domain in the existing Exchange organization cannot be found.

Microsoft Exchange setup requires that each domain in the existing Exchange organization have an instance of the Recipient Update Service.

If an instance of the Recipient Update Service is missing for a domain, new user objects created in the domain will not receive e-mail addresses issued to them.

To resolve this issue, verify that an instance of the Recipient Update Service exists for each domain and create an instance of the Recipient Update Service for the domains that do not have one and then rerun Microsoft Exchange setup.

|To create a Recipient Update Service instance for a domain|
|---|
|<ol><li>Open Exchange System Manager.</li><li>Expand **Recipients**.</li><li>Right-click the **Recipient Update Services** node, click **New**, and then click **Recipient Update Service**.</li><li>In the New Object window, click **Browse** to locate the name of the domain.</li><li>Select the name of the domain and then click **OK**.</li><li>In the New Object window, click **Next**, and then **Finish**.</li></ol>|
