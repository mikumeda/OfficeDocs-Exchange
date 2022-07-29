---
title: 'One or more Active Directory Connector servers were found'
TOCTitle: One or more Active Directory Connector servers were found_ADCFound
ms:assetid: a874f51f-09a2-4a76-9695-d61fb1ee6c1c
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.setupreadiness.adcfound(v=EXCHG.150)
ms:contentKeyID: 46629070
ms.reviewer: 
ms.topic: article
description: "Exchange Setup can't continue: Active Directory Connector servers found"
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# One or more Active Directory Connector servers were found\_ADCFound

_**Applies to:** Exchange Server 2013_

The content in this topic hasn't been updated for Microsoft Exchange Server 2013. While it hasn't been updated yet, it may still be applicable to Exchange 2013. If you still need help, check out the community resources below.

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

Microsoft Exchange Server 2007 and Exchange Server 2010 setup cannot continue because one or more Active Directory Connectors (ADC) have been found in the current Microsoft Exchange environment.

ADC replicates objects from Exchange Server version 5.5 to the Active Directory directory service in a mixed mode Microsoft Exchange environment and is not supported by Exchange 2007 or Exchange 2010.

Exchange 2007 or Exchange 2010 setup requires that all ADC components be removed.

To resolve this issue, remove all ADC components, and rerun Exchange 2007 or Exchange 2010 setup.

|To remove Active Directory Connector components|
|---|
|<ol><li>To disable the ADC service on the server that is running the ADC service, right-click **My Computer** on the desktop, and then click **Manage**.</li><li>Expand the **Services and Applications** node, and then click the **Services** node.</li><li>In the right pane, right-click **Microsoft Active Directory Connector** and then click **Properties**.</li><li>Change the **Startup Type** to **Disabled**. The next time that the computer starts, the ADC service will not start.</li><li>Click **Apply**, and then click **OK**.</li><li>To uninstall the ADC service, use the Active Directory Installation Wizard on the Microsoft Exchange 2000 Server or Microsoft Exchange Server 2003 CD. Open the \ADC\I386 folder and double-click the Setup.exe program. Follow the prompts to **Remove All** ADC service components. <br/><br/> **Important**: You must complete step 6 and **Remove All** ADC components to resolve this issue. It is insufficient to disable the ADC service.</li></ol>|
