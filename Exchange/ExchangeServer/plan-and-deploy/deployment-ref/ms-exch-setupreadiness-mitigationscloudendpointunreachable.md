---
ms.localizationpriority: medium
description:  Mitigations Cloud endpoint is not reachable
ms.topic: reference
author: JoanneHendrickson
ms.custom:
- ms-exch-setupreadiness-KB2999226NotInstalled
ms.author: jhendr
ms.reviewer:
title: Mitigations Cloud endpoint is not reachable
ms.collection: exchange-server
f1.keywords:
- CSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars
---

# Mitigations Cloud endpoint is not reachable

::: moniker range="exchserver-2016"

Microsoft Exchange Server 2016 setup displayed this warning because the setup failed to connect to the Mitigation Service Cloud endpoint from the local computer.

Exchange 2016 setup (for September 2021 CU and later versions) installs the Exchange Emergency Mitigation (EM) Service. The EM Service checks for available mitigations every hour before downloading and applying them.

::: moniker-end

::: moniker range="exchserver-2019"
Microsoft Exchange Server 2019 setup displayed this warning because the setup failed to connect to the Mitigation Service Cloud endpoint from the local computer.

Exchange 2019 setup (for September 2021 CU and later versions) installs the Exchange Emergency Mitigation (EM) Service. The EM Service checks for available mitigations every hour before downloading and applying them.

::: moniker-end

The functionality to check and download mitigations requires outbound connectivity to the Mitigation Service Cloud endpoint. Without this connectivity, the EM service can’t function, which can pose a security risk.

For the EM service to function correctly, admins needs to enable connectivity with the following endpoint from the computer on which Exchange Server is installed.

<br>

****

|Required|Address|Port|
|---|---|---|---|
|Yes|officeclient.microsoft.com/*|443|
|

**Having problems?** Ask for help in the Exchange forums. Visit the forums at: [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).
