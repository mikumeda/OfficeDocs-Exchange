---
title: 'Receive connector authentication mechanisms: Exchange 2013 Help'
TOCTitle: Receive connector authentication mechanisms
ms:assetid: 926424e1-83e3-4c4b-b2dd-bf814d81e877
ms:mtpsurl: https://technet.microsoft.com/library/JJ657472(v=EXCHG.150)
ms:contentKeyID: 49289352
ms.reviewer: 
ms.topic: article
description: About Receive connector authentication mechanisms in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Receive connector authentication mechanisms

_**Applies to:** Exchange Server 2013_

The Receive connector authentication mechanisms are the following:

|Authentication mechanism|Description|
|---|---|
|None|No authentication.|
|TLS|Advertise STARTTLS. Requires availability of a server certificate to offer TLS.|
|Integrated|NTLM and Kerberos (Integrated Windows authentication).|
|BasicAuth|Basic authentication. Requires an authenticated logon.|
|BasicAuthRequireTLS|Basic authentication over TLS. Requires a server certificate.|
|ExchangeServer|Exchange Server authentication (Generic Security Services application programming interface (GSSAPI) and Mutual GSSAPI).|
|ExternalAuthoritative|The connection is considered externally secured by using a security mechanism that's external to Exchange. The connection may be an Internet Protocol security (IPsec) association or a virtual private network (VPN). Alternatively, the servers may reside in a trusted physically controlled network. The `ExternalAuthoritative` authentication method requires the `ExchangeServers` permission group. This combination of authentication method and security group permits the resolution of anonymous sender email addresses for messages that are received through this connector.|

For more information about Receive Connector authentication mechanisms, see [New-ReceiveConnector](/powershell/module/exchange/New-ReceiveConnector).
