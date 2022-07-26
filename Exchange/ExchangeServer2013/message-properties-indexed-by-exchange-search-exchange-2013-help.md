---
title: 'Message properties indexed by Exchange Search: Exchange 2013 Help'
TOCTitle: Message properties indexed by Exchange Search
ms:assetid: a9754dc1-44aa-4076-8b59-a5d39246d5b0
ms:mtpsurl: https://technet.microsoft.com/library/JJ983804(v=EXCHG.150)
ms:contentKeyID: 51407271
ms.reviewer: 
ms.topic: article
description: Message properties that Exchange Search indexes
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Message properties indexed by Exchange Search

_**Applies to:** Exchange Server 2013_

Exchange Search indexes many item properties, including sender, recipients, message body, and attachments for email messages.

## Properties indexed by Exchange Search

The following table includes a list of all item properties indexed by Exchange Search.

|Property|Type|Queryable|Searchable|Retrievable|
|---|---|:---:|:---:|:---:|
|Account|String|Yes|Yes|No|
|Assistantname|String|Yes|Yes|No|
|Attachment|String|Yes|Yes|No|
|Attachmentfilenames|String|Yes|Yes|No|
|Attachmentmetaproperties|String|No|Yes|No|
|Attachmentcount|Integer|No|No|Yes|
|Bcc|String|Yes|Yes|No|
|Body|String|Yes|Yes|No|
|Businessaddress|String|Yes|Yes|No|
|Businessmainphone|String|Yes|Yes|No|
|Businessphonenumber|String|Yes|Yes|No|
|Carphonenumber|String|Yes|Yes|No|
|Category|String|Yes|Yes|No|
|Cc|String|Yes|Yes|No|
|Companyname|String|Yes|Yes|No|
|Compositeitemid|String|No|No|Yes|
|Conversationid|Integer|No|No|Yes|
|Conversationtopic|String|Yes|Yes|No|
|Departmentname|String|Yes|Yes|No|
|Displayname|String|Yes|Yes|No|
|Displaynameprefix|String|Yes|Yes|No|
|Documentid|Integer|Yes|No|Yes|
|Emailaddress|String|Yes|Yes|No|
|Emaildisplayname|String|Yes|Yes|No|
|Emailoriginaldisplayname|String|Yes|Yes|No|
|Errorcode|Integer|Yes|No|Yes|
|Fileas|String|Yes|Yes|No|
|Firstname|String|Yes|Yes|No|
|Folderid|String|Yes|No|No|
|From|String|Yes|Yes|No|
|Homeaddress|String|Yes|Yes|No|
|Homephone|String|Yes|Yes|No|
|Importance|Integer|Yes|No|No|
|Ispartiallyprocessed|Boolean|Yes|No|Yes|
|Ispermanentfailure|Boolean|Yes|No|Yes|
|Itemclass|String|Yes|No|No|
|Kind|String|Yes|Yes|No|
|Lastattempttime|DateTime|Yes|No|Yes|
|Lastname|String|Yes|Yes|No|
|Mailboxguid|String|Yes|No|Yes|
|Manager|String|Yes|Yes|No|
|Meetinglocation|String|Yes|Yes|No|
|Middlename|String|Yes|Yes|No|
|Mobilephonenumber|String|Yes|Yes|No|
|Nickname|String|Yes|Yes|No|
|Officelocation|String|Yes|Yes|No|
|Otheraddress|String|Yes|Yes|No|
|Participants|String|Yes|Yes|No|
|Primarytelephonenumber|String|Yes|Yes|No|
|Received|DateTime|Yes|No|No|
|Receivedby|String|Yes|Yes|No|
|Receivedrepresenting|String|Yes|Yes|No|
|Recipients|String|Yes|Yes|No|
|Sent|DateTime|Yes|No|No|
|Sharinginfo|String|Yes|No|No|
|Size|Integer|Yes|No|No|
|Subject|String|Yes|Yes|No|
|Tasktitle|String|Yes|Yes|No|
|Title|String|Yes|Yes|No|
|To|String|Yes|Yes|No|
|Umaudionotes|String|Yes|Yes|No|
|Watermark|Integer|No|No|Yes|
|Yomicompanyname|String|Yes|No|Yes|
|Yomifirstname|String|Yes|Yes|No|
|Yomilastname|String|Yes|Yes|No|

**Notes about indexed properties**:

- **Queryable properties** can be used in AQS queries by search clients such as Outlook Web App in `property:value` pairs, for example, `from:bsuneja@cotoso.com`. A subset of the queryable properties listed in the previous table can also be used in search queries for In-Place eDiscovery. For a list of these properties, see [In-Place eDiscovery in Exchange 2013](in-place-ediscovery-exchange-2013-help.md).

- **Searchable properties** are properties that can't be specified in `property:value` pairs, but a keyword search returns the value if found in any searchable property. For example, you can't use `body:Contoso` to search for the string `contoso` in the message body only. However, a search for that string will return all items where the property is found in any searchable property.

- **Retrievable properties** such as `documenteid` and `ispartiallyprocessed` are returned with every search.
