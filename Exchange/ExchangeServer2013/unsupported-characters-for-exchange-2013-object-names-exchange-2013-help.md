---
title: 'Unsupported characters for Exchange 2013 object names: Exchange 2013 Help'
TOCTitle: Unsupported characters for Exchange 2013 object names
ms:assetid: 76fa4e23-f0f6-473b-9227-70ded907578f
ms:mtpsurl: https://technet.microsoft.com/library/Dn169553(v=EXCHG.150)
ms:contentKeyID: 53875525
ms.reviewer: 
ms.topic: article
description: Unsupported characters for Microsoft Exchange object names
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Unsupported characters for Exchange 2013 object names

_**Applies to:** Exchange Server 2013_

This article describes characters that you can't use in object or component names in Exchange 2013. When you create names for objects or components in Exchange 2013, the names can't contain unsupported characters, even though you may be able to create an object using an unsupported character. Also, if you try to import or connect to objects whose names contain unsupported characters, you may receive an error message or experience unexpected behavior.

## Unsupported characters

The following table lists characters that aren't supported for use in the names of Exchange-related objects or components. The table also lists the scenario in which problems may occur if unsupported characters are used. Note that there is a maximum length of 64 characters for each object listed in the table.

|Exchange object or component|Exchange scenario|Unsupported characters|
|---|---|---|
|Email domain name|Simple Mail Transfer Protocol (SMTP) connector|`~ ! @ # $ % ^ & * ( ) + = { } | [ ] \ : " ; < > , . ? /`|
|Host name of connector address space|Mail flow|`..` (two periods)|
|Host name for Exchange servers|SMTP|`_` (underscore)|
|Organization or site name|Running the Setup program or moving mailboxes|`~ ! @ # $ % ^ & * ( ) _ + = { } | [ ] \ : " ; '  < > , . ? /`|
|Organization internal directory name|Directory|`~ ! @ # $ % ^ & * ( ) _ + = { } | [ ] \ : " ; '  < > , . ? /`|
|Public folder tree name|Viewing and creating the public folder|`: ;`|
|Recipient name|SMTP|`' "`|
|Recipient policy SMTP address|Viewing the public folder hierarchy|`~ ! @ # $ % ^ & * ( ) + = { } | [ ] \ : " ; < > , . ? /`|
|Recipient policy SMTP address host name|Mail flow|`..` (two periods)|
|Site internal directory name|Viewing the public folder hierarchy|`? ( ) *`|
|Smart host name|SMTP|Leading or trailing spaces|
