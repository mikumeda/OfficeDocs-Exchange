---
title: 'Anti-spam stamps: Exchange 2013 Help'
TOCTitle: Anti-spam stamps
ms:assetid: 28d3a5c2-8509-4b25-9876-763536e77c27
ms:mtpsurl: https://technet.microsoft.com/library/Aa996878(v=EXCHG.150)
ms:contentKeyID: 49248677
description: Anti-spam stamps help you diagnose spam-related problems in Microsoft Exchange
ms.topic: article
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Anti-spam stamps

_**Applies to:** Exchange Server 2013_

Anti-spam stamps help you diagnose spam-related problems by applying diagnostic metadata, or stamps, such as sender-specific information, puzzle validation results, and content filtering results, to messages as they pass through the anti-spam features that filter inbound messages from the Internet. There are three anti-spam stamps: the phishing confidence level stamp, the spam confidence level stamp, and the Sender ID stamp.

You can use anti-spam stamps as diagnostic tools to determine what actions to take on false-positives and on suspected spam messages that individuals receive in their mailboxes.

> [!NOTE]
> On November 1, 2016, Microsoft stopped producing spam definition updates for the SmartScreen filters in Exchange and Outlook. The existing SmartScreen spam definitions will be left in place, but their effectiveness will likely degrade over time. For more information, see <A href="https://techcommunity.microsoft.com/t5/exchange-team-blog/deprecating-support-for-smartscreen-in-outlook-and-exchange/ba-p/605332">Deprecating support for SmartScreen in Outlook and Exchange</A>.

## Viewing anti-spam stamps

You can view anti-spam stamps by using Microsoft Outlook. For more information, see [View anti-spam stamps in Outlook](view-anti-spam-stamps-in-outlook-exchange-2013-help.md).

## Understanding the anti-spam report

The anti-spam report is a summary report of the anti-spam filter results that have been applied to an email message. The Content Filter agent applies this stamp to the message envelope in the form of an X-header as follows.

```powershell
X-MS-Exchange-Organization-Antispam-Report: DV:<DATVersion>;CW:CustomList;PCL:PhishingVerdict <verdict>;P100:PhishingBlock;PP:Presolve;SID:SenderIDStatus <status>;TIME:<SendReceiveDelta>;MIME:MimeCompliance
```

The following table describes the filter information that can appear in an anti-spam report.

> [!NOTE]
> The anti-spam report only displays information from the filters that were applied to the specific message. An anti-spam report doesn't usually contain all the information listed in the following table. For example, you may receive the following anti-spam report: `DV:3.1.3924.1409;SID:SenderIDStatus Fail;PCL:PhishingLevel SUSPICIOUS;CW:CustomList;PP:Presolved;TIME:TimeBasedFeatures`.

### Filter information in an anti-spam report

|Stamp|Description|
|---|---|
|SID|The Sender ID (SID) stamp is based on the sender policy framework (SPF) that authorizes the use of domains in email. The SPF is displayed in the message envelope as `Received-SPF`. The Sender ID evaluation process generates a Sender ID status for the message. This status can be returned as one of the following values: <ul><li>**Pass**: Both the IP address and Purported Responsible Address (PRA) passed the Sender ID verification check.</li><li>**Neutral**: Published Sender ID data is explicitly inconclusive.</li><li>**Soft fail**:The IP address for the PRA may be in the not permitted set.</li><li>**Fail**: The IP Address is not permitted; no PRA is found in the incoming mail or the sending domain does not exist.</li><li>**None**: No published SPF data exists in the sender's DNS.</li><li>**TempError**: A temporary DNS failure occurred, such as an unavailable DNS server.</li><li>**PermError**: The DNS record is invalid, such as an error in the record format.</li></ul> <p> The Sender ID stamp is displayed as an X-Header in the message envelope as follows: `X-MS-Exchange-Organization-SenderIdResult:<status>` <p> For more information about Sender ID, see [Sender ID](sender-id-exchange-2013-help.md).|
|DV|The DAT version (DV) stamp indicates the version of the spam definition file that was used when scanning the message.|
|SA|The signature action (SA) stamp indicates that the message was either recovered or deleted because of a signature that was found in the message.|
|SV|The signature DAT version (SV) stamp indicates the version of the signature file that was used when scanning the message.|
|PCL|The phishing confidence level (PCL) stamp displays the rating of the message based on its content and is applied when the message is processed by the Content Filter agent. This status can be returned as one of the following values: <ul><li>**Neutral**: The message's content isn't likely to be phishing.</li><li>**Suspicious**: The message's content is likely to be phishing.</li></ul> <p> The PCL value can range from 1 through 8: <ul><li>A PCL rating from 1 through 3 returns a status of `Neutral`. This means that the message's content isn't likely to be phishing.</li><li>A PCL rating from 4 through 8 returns a status of `Suspicious`. This means that the message is likely to be phishing.</li></ul> <p> The values are used to determine what action Outlook takes on messages. Outlook uses the PCL stamp to block the content of suspicious messages. <p> The PCL stamp is displayed as an X-header in the message envelope as follows: `X-MS-Exchange-Organization-PCL:<status>`|
|SCL|The spam confidence level (SCL) stamp of the message displays the rating of the message based on its content. The Content Filter agent uses Microsoft SmartScreen technology to assess the contents of a message and to assign an SCL rating to each message. <p> The SCL value is from 0 through 9, where 0 is considered less likely to be spam, and 9 is considered more likely to be spam. The actions that Exchange and Outlook take depend on your SCL threshold settings. <p> The SCL stamp is displayed as an X-header in the message envelope as follows: `X-MS-Exchange-Organization-SCL:<status>` <p> For more information about SCL thresholds and actions, see [Spam Confidence Level Threshold](spam-confidence-level-threshold-exchange-2013-help.md).|
|CW|The custom weight (CW) stamp of a message indicates that the message contains an unapproved word or phrase and that the SCL value, or weight, of that unapproved word or phrase was applied to the final SCL score: <ul><li>Unapproved phrases, or Block phrases, have maximum weight and change the SCL score to 9.</li><li>Approved words or phrases, or Allow phrases, have minimum weight and change the SCL score to 0.</li></ul> <p> For more information about how to add approved and unapproved words or phrases to the Content Filtering agent, see [Manage content filtering](manage-content-filtering-exchange-2013-help.md).|
|PP|The presolved puzzle (PP) stamp indicates that if a sender's message contains a valid, solved computational postmark, based on Outlook E-mail Postmark validation functionality, it's unlikely that the sender is a malicious sender. In this case, the Content Filter agent would reduce the SCL rating. <p> The Content Filter agent doesn't change the SCL rating if the E-mail Postmark validation feature is enabled and either of the following conditions is true: <ul><li>An inbound message doesn't contain a computational postmark header.</li><li>The computational postmark header isn't valid.</li></ul> <p> For more information about the postmark validation feature, see [Content filtering](content-filtering-exchange-2013-help.md).|
|TIME:TimeBasedFeatures|The TIME stamp indicates that there was a significant time delay between the time that the message was sent and the time that the message was received. The TIME stamp is used to determine the final SCL rating for the message.|
|MIME:MIMECompliance|The MIME stamp indicates that the email message isn't MIME compliant.|
|P100:PhishingBlock|The P100 stamp indicates that the message contains a URL that's present in a phishing definition file.|
|IPOnAllowList|The IPOnAllowList stamp indicates that the sender's IP address is on the IP Allow list. For more information about the IP Allow list, see [Understanding Connection Filtering](/previous-versions/office/exchange-server-2010/bb124320(v=exchg.141)).|
|MessageSecurityAntispamBypass|The MessageSecurityAntispamBypass stamp indicates that the message wasn't filtered for content and that the sender has been granted permission to bypass the anti-spam filters.|
|SenderBypassed|The SenderBypassed stamp indicates that the Content Filter agent doesn't process any content filtering for messages that are received from this sender. For more information, see [Manage content filtering](manage-content-filtering-exchange-2013-help.md).|
|AllRecipientsBypassed|The AllRecipientsBypassed stamp indicates that one of the following conditions was met for all recipients listed in the message: <ul><li>The _AntispamBypassedEnabled_ parameter on the recipient's mailbox is set to `$true`. This is a per-recipient setting that can only be set by an administrator using the **Set-Mailbox** cmdlet.</li><li>The message sender is in the recipient's Outlook Safe Senders List. For more information about the Safe Senders List, see [Manage safelist aggregation](manage-safelist-aggregation-exchange-2013-help.md).</li><li>The Content Filter agent doesn't process any content filtering for messages that are sent to this recipient. For more information about recipient exceptions, see [Manage content filtering](manage-content-filtering-exchange-2013-help.md).</li></ul>|
