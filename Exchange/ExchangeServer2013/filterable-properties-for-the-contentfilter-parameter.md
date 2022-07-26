---
title: Filterable properties for the -ContentFilter parameter
TOCTitle: Filterable properties for the -ContentFilter parameter
ms:assetid: cf504a59-1938-489c-bb48-b27b2ac3234e
ms:mtpsurl: https://technet.microsoft.com/library/Ff601762(v=EXCHG.150)
ms:contentKeyID: 49895015
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Filterable properties for the -ContentFilter parameter in Exchange Server
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Filterable properties for the -ContentFilter parameter

_**Applies to:** Exchange Server 2013_

This topic lists the filterable properties for the _ContentFilter_ parameter. The _ContentFilter_ parameter is used to export messages to a .pst file that match the filter. The _ContentFilter_ parameter is used in the [New-MailboxExportRequest](/powershell/module/exchange/New-MailboxExportRequest) cmdlet.

## Filterable properties

Many of the properties for the _ContentFilter_ parameter accept wildcard characters. If you use a wildcard character, use the **-like** operator instead of the **-eq** operator. The **-like** operator is used to find pattern matches in rich types, such as strings, whereas the **-eq** operator is used to find an exact match.

The following table contains a list of the filterable properties for the _ContentFilter_ parameter. This table lists the name of the property, a description, the acceptable values, and a syntax example. For more information about OPATH filters, see [Recipient filters in Exchange PowerShell commands - Additional OPATH syntax information](/powershell/exchange/recipient-filters#additional-opath-syntax-information).

|Property|Description|Values|Example syntax|
|---|---|---|---|
|All|This property returns all messages that have a particular string in any of the indexed properties. For example, use this property if you want to export all messages that have "Ayla" as the recipient, the sender, or have the name mentioned in the message body.|String <br/><br/> Wildcard|`-ContentFilter "All -like '*Ayla*'"`|
|Attachment|This property returns messages that have the specified string in the content of an attachment or in the attachment's file name.|String <br/><br/> Wildcard|`-ContentFilter "Attachment -like '*.jpg'"`|
|BCC|This property returns sent messages that have the specified recipient in the Bcc field.|Display name <br/><br/> Alias <br/><br/> SMTP address <br/><br/> LegacyDN <br/><br/> Wildcard|`-ContentFilter "(BCC -eq 'ayla@contoso.com') -or (BCC -eq 'tony@contoso.com')"`|
|Body|This property returns messages that have the specified string within the message body.|String <br/><br/> Wildcard|`-ContentFilter "Body -like '*prospectus*'"`|
|Category|This property returns messages that have a matching category. Categories are set by users or Inbox rules.|String <br/><br/> Wildcard|`-ContentFilter "Category -like '*Blue*'"`|
|CC|This property returns sent messages that have the specified recipient in the Cc field.|Display name <br/><br/> Alias <br/><br/> SMTP address <br/><br/> LegacyDN <br/><br/> Wildcard|`-ContentFilter "(CC -eq 'ayla@contoso.com') -or (CC -eq 'tony@contoso.com')"`|
|Expires|This property returns messages that have a specified expiration time stamp.|Date-Time stamp|`-ContentFilter "Expires -lt '01/01/2013'"`|
|HasAttachment|This property returns messages with or without attachments.|Boolean <br/><br/> `$true` or `$false`|`-ContentFilter "HasAttachment -eq $true"`|
|Importance|This property returns messages that have a specified importance level.|0 or "Low" <br/><br/> 1 or "Normal" <br/><br/> 2 or "High"|`-ContentFilter "Importance -eq 'high'"` <br/><br/> `-ContentFilter "Importance -eq 2"`|
|IsFlagged|This property returns messages that have been flagged by the user or Inbox rule.|Boolean <br/><br/> `$true` or `$false`|`-ContentFilter "IsFlagged -eq $true"`|
|IsRead|This property returns messages that have been read or not read by the user.|Boolean <br/><br/> `$true` or `$false`|`-ContentFilter "IsRead -eq $true"`|
|MessageKind|This property returns messages that are of the specified type.|Calendar <br/><br/> Contact <br/><br/> Doc <br/><br/> Email <br/><br/> Fax <br/><br/> InstantMessage <br/><br/> Journal <br/><br/> Note <br/><br/> Post <br/><br/> RSSFeed <br/><br/> Task <br/><br/> Voicemail|`-ContentFilter "MessageKind -eq 'Calendar'"` <br/><br/> `-ContentFilter "MessageKind -ne 'Email'"`|
|MessageLocalee|This property returns messages that are of the specified locale.|CultureInfo|`-ContentFilter "MessageLocale -ne 'en-US'"` <br/><br/> `-ContentFilter "MessageLocale -eq 'tr-TR'"`|
|Participants|This property returns messages that have the specified recipient in the To, Bcc, or Cc fields.|Display name <br/><br/> Alias <br/><br/> SMTP address <br/><br/> LegacyDN <br/><br/> Wildcard|`-ContentFilter "(Participants -eq 'ayla@contoso.com') -or (Participants -eq 'tony@contoso.com')"`|
|PolicyTag|This property returns messages that have a policy tag. The Exchange store persists policy tags as GUIDs. Therefore, the string can contain either an explicit GUID value, which is then searched by the PR_POLICY_TAG, or a wildcard string. <br/><br/> If the supplied value isn't a GUID, the command uses Active Directory information to resolve names to GUIDs.|String <br/><br/> Wildcard|`-ContentFilter "PolicyTag -ne '00000000-0000-0000-0000-000000000000'"`|
|Received|This property returns messages that were received with the specified Received time stamp.|Date-Time stamp|`-ContentFilter "Received -lt '01/01/2013 9:00'"` <br/><br/> `-ContentFilter "(Received -lt '01/01/2013') -and (Received -gt '01/01/2012')"`|
|Sender|This property returns messages that were received from the specified sender.|Display name <br/><br/> Alias <br/><br/> SMTP address <br/><br/> LegacyDN <br/><br/> Wildcard|`ContentFilter "Sender -eq 'tony'"`|
|Sent|This property returns messages that were sent with the specified Sent time stamp.|Date-Time stamp|`-ContentFilter "Sent -lt '01/01/2013 9:00'"` <br/><br/> `-ContentFilter "(Sent -lt '01/01/2013') -and (Sent -gt '01/01/2012')"`|
|Size|This property returns messages that are of a specific size.|B (bytes) <br/><br/> KB (kilobytes) <br/><br/> MB (megabytes)|`-ContentFilter "Size -gt '10KB'"`|
|Subject|This property returns messages that have the specified string within the subject of the message.|String <br/><br/> Wildcard|`-ContentFilter "Subject -like '*meeting*'"`|
|To|This property returns sent messages that have the specified recipient in the To field.|Display name <br/><br/> Alias <br/><br/> SMTP address <br/><br/> LegacyDN <br/><br/> Wildcard|`-ContentFilter "To -eq 'aylakol'"`|
