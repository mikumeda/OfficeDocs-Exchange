---
title: 'Receive connector permissions: Exchange 2013 Help'
TOCTitle: Receive connector permissions
ms:assetid: 31af7139-6823-411b-81b3-e42edd83ee6c
ms:mtpsurl: https://technet.microsoft.com/library/JJ673053(v=EXCHG.150)
ms:contentKeyID: 49289221
ms.reviewer: 
ms.topic: article
description: About Receive connector permissions in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: serdars
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Receive connector permissions

_**Applies to:** Exchange Server 2013_

The following table lists permission types and a description for each.

|Receive connector permission|Description|
|---|---|
|ms-Exch-SMTP-Submit|The session must be granted this permission or it will be unable to submit messages to this Receive connector. If a session doesn't have this permission, the MAIL FROM and AUTH commands will fail.|
|ms-Exch-SMTP-Accept-Any-Recipient|This permission allows the session to relay messages through this connector. If this permission isn't granted, only messages that are addressed to recipients in accepted domains are accepted by this connector.|
|ms-Exch-SMTP-Accept-Any-Sender|This permission allows the session to bypass the sender address spoofing check.|
|ms-Exch-SMTP-Accept-Authoritative-Domain-Sender|This permission allows senders that have e-mail addresses in authoritative domains to establish a session to this Receive connector.|
|ms-Exch-SMTP-Accept-Authentication-Flag|This permission allows Exchange 2003 servers to submit messages from internal senders. Exchange 2010 will recognize the messages as being internal. The sender can declare the message as trusted. Messages that enter your Exchange system through anonymous submissions will be relayed through your Exchange organization with this flag in an untrusted state.|
|ms-Exch-Accept-Headers-Routing|This permission allows the session to submit a message that has all received headers intact. If this permission isn't granted, the server will strip all received headers.|
|ms-Exch-Accept-Headers-Organization|This permission allows the session to submit a message that has all organization headers intact. Organization headers all start with **X-MS-Exchange-Organization-**. If this permission isn't granted, the receiving server will strip all organization headers.|
|ms-Exch-Accept-Headers-Forest|This permission allows the session to submit a message that has all forest headers intact. Forest headers all start with **X-MS-Exchange-Forest-**. If this permission isn't granted, the receiving server will strip all forest headers.|
|ms-Exch-Accept-Exch50|This permission allows the session to submit a message that contains the XEXCH50 command. This command is needed for interoperability with Exchange 2003. The XEXCH50 command provides data such as the spam confidence level (SCL) for the message.|
|ms-Exch-Bypass-Message-Size-Limit|This permission allows the session to submit a message that exceeds the message size restriction configured for the connector.|
|Ms-Exch-Bypass-Anti-Spam|This permission allows the session to bypass anti-spam filtering.|
