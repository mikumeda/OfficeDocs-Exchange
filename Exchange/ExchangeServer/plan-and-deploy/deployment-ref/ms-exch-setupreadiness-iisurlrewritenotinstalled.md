---
ms.localizationpriority: medium
description: IIS URL Rewrite Module not installed
ms.topic: reference
author: JoanneHendrickson
ms.custom:
- ms.exch.setupreadiness.ForestLevelNotWin2003Native
ms.author: jhendr
ms.reviewer:
title: IIS URL Rewrite Module not installed
ms.collection: exchange-server
f1.keywords:
- CSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---
# IIS URL Rewrite Module not installed

::: moniker range="exchserver-2016"

Microsoft Exchange Server 2016 setup can't continue because the local computer requires additional software to be installed.

Exchange 2016 setup (for September 2021 CU and later versions) requires **IIS URL Rewrite Module 2.1** to be installed on the computer before installation can continue.

::: moniker-end

::: moniker range="exchserver-2019"

Microsoft Exchange Server 2019 setup can't continue because the local computer requires additional software to be installed.

Exchange 2019 setup (for September 2021 CU and later versions) requires **IIS URL Rewrite Module 2.1** to be installed on the computer before installation can continue.

::: moniker-end

1. Download and install:  [URL Rewrite Module version 2.1](https://www.iis.net/downloads/microsoft/url-rewrite). Choose the x64 installer of any language.
2. Select **retry** on the **Readiness Checks page**.

> [!NOTE]
> If this update requires a reboot to complete installation, you'll need to exit the Exchange 2016 setup, reboot, and then start Setup again.

> [!IMPORTANT]
> If the URL Rewrite Module is uninstalled after setup, it may lead to unresponsive ECP/OWA.

## Having problems?

Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).
