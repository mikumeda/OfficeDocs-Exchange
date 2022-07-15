---
title: 'Message tracking: Exchange 2013 Help'
TOCTitle: Message tracking
ms:assetid: bada2ea7-6d7c-4630-b7f1-67f56818f0ff
ms:mtpsurl: https://technet.microsoft.com/library/Bb124375(v=EXCHG.150)
ms:contentKeyID: 50646522
ms.reviewer: 
ms.topic: article
description: About the message tracking log in Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Message tracking in Exchange

_**Applies to:** Exchange Server 2013_

In Microsoft Exchange Server 2013, the message tracking log is a detailed record of all message activity as messages are transferred to and from the Transport service on Mailbox servers, mailboxes on Mailbox servers, and Edge Transport servers. You can use message tracking logs for message forensics, mail flow analysis, reporting, and troubleshooting.

In Exchange 2013, you can use the **Set-TransportService** cmdlet or the **Set-MailboxServer** cmdlet for all message tracking configuration tasks, because the Exchange 2013 Mailbox server holds the Transport service and the mailboxes. You can use either of these cmdlets to make the following message tracking configuration changes:

- Enable or disable message tracking. The default is enabled.
- Specify the location of the message tracking log files.
- Specify a maximum size for the individual message tracking log files. The default is 10 MB.
- Specify a maximum size for the directory that contains the message tracking log files: The default is 1000 MB.
- Specify maximum age for the message tracking log files: The default is 30 days.
- Enable or disable message subject logging in the message tracking logs. The default is enabled.

> [!NOTE]
> You can also use the Exchange admin center (EAC) to enable or disable message tracking, and to specify the location of the message tracking log files.

By default, Exchange uses circular logging to limit the message tracking logs based on file size and file age to help control the hard disk space used by the message tracking log files.

## Search the message tracking log

Message tracking logs contain vast amounts of data as messages move through an Exchange 2013 Mailbox server. When it comes to searching the message tracking logs, you have different options.

- **Get-MessageTrackingLog**: Administrators can use this cmdlet to search the message tracking log for information about messages using a wide range of filter criteria. For more information, see [Search message tracking logs](search-message-tracking-logs-exchange-2013-help.md).

- **Delivery reports for administrators**: Administrators can use the **Delivery reports** tab in the Exchange admin center (EAC) or the underlying **Search-MessageTrackingReport** and **Get-MesageTrackingReport** cmdlets to search the message tracking logs for information about messages sent by or received by a specific mailbox in the organization. For more information see [Delivery reports for administrators](delivery-reports-for-administrators-exchange-2013-help.md).

## Structure of the message tracking log files

By default, the message tracking log files exist in %ExchangeInstallPath%TransportRoles\\Logs\\MessageTracking.

The naming convention for log files in the message tracking log directory is `MSGTRK`_yyyymmdd-nnnn_`.log`, `MSGTRKMA`_yyyymmdd-nnnn_`.log`, `MSGTRKMD`_yyyymmdd-nnnn_`.log`, and `MSGTRKMS`*yyyymmdd-nnnn*`.log`. The different logs are used by the following services:

- **MSGTRK**: These logs are associated with the Transport service.

- **MSGTRKMA**: These logs are associated with the approvals and rejections used by moderated transport. For more information, see [Manage message approval](../ExchangeOnline/security-and-compliance/mail-flow-rules/manage-message-approval.md).

- **MSGTRKMD**: These logs are associated with messages delivered to mailboxes by the Mailbox Transport Delivery service.

- **MSGTRKMS**: These logs are associated with messages sent from mailboxes by the Mailbox Transport Submission service.

The placeholders in the log file names represent the following information:

- The placeholder _yyyymmdd_ is the coordinated universal time (UTC) date on which the log file was created. _yyyy_ = year, _mm_ = month, and _dd_ = day.

- The placeholder _nnnn_ is an instance number that starts at the value of 1 daily for each message tracking log file name prefix.

Information is written to each log file until the file size reaches its maximum specified value for each log file. Then, a new log file that has an incremented instance number is opened. This process is repeated throughout the day. The log file rotation functionality deletes the oldest log files when either of the following conditions is true:

- A log file reaches its maximum specified age.

- The message tracking log directory reaches its maximum specified size.

  > [!IMPORTANT]
  > The maximum size of the message tracking log directory is calculated as the total size of all log files that have the same name prefix. Other files that do not follow the name prefix convention are not counted in the total directory size calculation. Renaming old log files or copying other files into the message tracking log directory could cause the directory to exceed its specified maximum size.
  >
  > On Exchange 2013 Mailbox servers, the maximum size of the message tracking log directory is three times the specified value. Although the message tracking log files that are generated by the four different services have four different name prefixes, the amount and frequency of data written to the **MSGTRKMA** log files is negligible compared to the three other log file prefixes.

The message tracking log files are text files that contain data in the comma-separated value (CSV) format. Each message tracking log file has a header that contains the following information:

- **\#Software:**: Name of the software that created the message tracking log file. Typically, the value is Microsoft Exchange Server.

- **\#Version:**: Version number of the software that created the message tracking log file. Currently, the value is 15.0.0.0.

- **\#Log-Type:**: Log type value, which is Message Tracking Log.

- **\#Date:**: The UTC date-time when the log file was created. The UTC date-time is represented in the ISO 8601 date-time format: _yyyy-mm-dd_T_hh:mm:ss.fff_Z, where _yyyy_ = year, _mm_ = month, and _dd_ = day, T indicates the beginning of the time component, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.

- **\#Fields:**: Comma-delimited field names used in the message tracking log files.

## Fields in the message tracking log files

The message tracking log stores each message event on a single line in the log. The message event information is organized by fields, and these fields are separated by commas. The field name is generally descriptive enough to determine the type of information that it contains. However, some fields may be blank, or the type of information that is stored in the field may change based on the message event type and the type of message tracking log file where the event was recorded. General descriptions of the fields that are used to classify each message tracking event are explained in the following table.

|Field name|Description|
|---|---|
|**date-time**|The UTC date-time of the message tracking event. The UTC date-time is represented in the ISO 8601 date-time format: _yyyy-mm-dd_T_hh:mm:ss.fff_Z, where _yyyy_ = year, _mm_ = month, _dd_ = day, T indicates the beginning of the time component, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.|
|**client-ip**|The IPv4 or IPv6 address of the messaging server or messaging client that submitted the message.|
|**client-hostname**|The host name or FQDN of the messaging server or messaging client that submitted the message.|
|**server-ip**|The IPv4 or IPv6 address of the source or destination Exchange server.|
|**server-hostname**|The host name or FQDN of the destination server.|
|**source-context**|Extra information associated with the **source** field. For example, transport agent information.|
|**connector-id**|The name of the source or destination Send connector or Receive connector. For example, _ServerName_\\_ConnectorName_ or _ConnectorName_.|
|**source**|The Exchange transport component responsible for the message tracking event. The values found in this field are described in the Source values in the message tracking log section later in this topic.|
|**event-id**|The message event type. The event types are described in the Event types in the message tracking log section later in this topic.|
|**internal-message-id**|A message identifier assigned by the Exchange server currently processing the message. <br/><br/> A specific message's value of **internal-message-id** is different in the message tracking log of every Exchange server that's involved in the transmission of the message. An example value is `73014444033`.|
|**message-id**|The value of the **Message-Id:** header field found in the message header. If the **Message-Id:** header field does not exist or is blank, an arbitrary value is assigned. This value is constant for the lifetime of the message. For messages created in Exchange, the value is in the format `<GUID@ServerFQDN>`, including the angle brackets (`< >`). For example, `<4867a3d78a50438bad95c0f6d072fca5@mailbox01.contoso.com>`. Other messaging systems may use different syntax or values.|
|**network-message-id**|A unique message ID value that persists across copies of the message that may be created due to bifurcation or distribution group expansion. An example value is `1341ac7b13fb42ab4d4408cf7f55890f`.|
|**recipient-address**|The email addresses of the message's recipients. Multiple email addresses are separated by the semicolon character (;).|
|**recipient-status**|This field contains the recipient status for each recipient separated by the semicolon character (;). The status values are presented for the recipients in the same order as the values in the **recipient-address** field. Example status values include `250 2.1.5 Recipient OK` or `550 4.4.7 QUEUE.Expired;<ErrorText>`.|
|**total-bytes**|The size of the message that includes attachments, in bytes.|
|**recipient-count**|The number of recipients in the message.|
|**related-recipient-address**|This field is used with **EXPAND**, **REDIRECT**, and **RESOLVE** events to display other recipient email addresses associated with the message.|
|**reference**|This field contains additional information for specific types of events. For example: <br/><br/> **DSN**: Contains the report link, which is the **Message-Id** value of the associated delivery status notification (DSN) if a DSN is generated subsequent to this event. If this is a DSN message, the **Reference** field contains the **Message-Id** value of the original message for which this DNS was generated. <br/><br/> **EXPAND**: The Reference field contains the **related-recipient-address** value of the related messages. <br/><br/> **RECEIVE**: The Reference field may contain the **Message-Id** value of the related message if the message was generated by other processes, for example, journaling or Inbox rules. <br/><br/> **SEND**: The Reference field contains the **Internal-Message-Id** value of any DSN messages. <br/><br/> **THROTTLE**: The Reference field contains the reason why the message was throttled. <br/><br/> **TRANSFER**: The Reference field contains the Internal-Message-Id of the message that is being forked. <br/><br/> For messages generated by inbox rules, the **Reference** field contains the **Internal-Message-Id** value of the inbound message that caused the inbox rule to generate the outbound message. <br/><br/> For other types of events, the **Reference** field may contain the **Internal-Message-Id** value for forked messages. <br/><br/> For other types of events, the **Reference** field is usually blank.|
|**message-subject**|The message's subject found in the `Subject:` header field. The tracking of message subjects is controlled by the _MessageTrackingLogSubjectLoggingEnabled_ parameter in the **Set-TransportService** or **Set-MailboxServer** cmdlets. By default, message subject tracking is enabled.|
|**sender-address**|The email address specified in the `Sender:` header field, or the `From:` header field if `Sender:` is not present.|
|**return-path**|The return email address specified by `MAIL FROM:` in the message envelope. Although this field is never empty, it can have the null sender address value represented as `<>`.|
|**message-info**|Additional information about the message. For example: <ul><li>The message origination UTC date-time for **DELIVER** and **SEND** events. The origination date-time is the time when the message first entered the Exchange organization. The UTC date-time is represented in the ISO 8601 date-time format: _yyyy-mm-dd_T_hh:mm:ss.fff_Z, where _yyyy_ = year, _mm_ = month, _dd_ = day, T indicates the beginning of the time component, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.</li><li>Authentication errors. For example you may see the value `11a` and the type of authentication used when authentication errors occur.</li></ul>|
|**directionality**|The direction of the message. Example values include `Incoming`, `Undefined`, and `Originating`.|
|**tenant-id**|This field isn't used in on-premises Exchange 2013 organizations.|
|**original-client-ip**|The IPv4 or IPv6 address of the original client.|
|**original-server-ip**|The IPv4 or IPv6 address of the original server.|
|**custom-data**|This field contains data related to a specific event types. For example, the Transport Rule agent uses this field to record the GUID of the transport rule or DLP policy that acted on the message. For more information about these Transport Rule agent values, see the "Data logging" section in the [View DLP policy detection reports](view-dlp-policy-detection-reports-exchange-2013-help.md) topic.|

## Event types in the message tracking log

Various event types in the **event-id** field are used to classify the message events in the message tracking log. Some message events appear in only one type of message tracking log file, and some message events appear in all types of message tracking log files. The events types that are used to classify each message event are explained in the following table.

|Event name|Description|
|---|---|
|**AGENTINFO**|This event is used by transport agents to log custom data.|
|**BADMAIL**|A message submitted by the Pickup directory or the Replay directory that can't be delivered or returned.|
|**DEFER**|Message delivery was delayed.|
|**DELIVER**|A message was delivered to a local mailbox.|
|**DROP**|A message was dropped without a delivery status notification (also known as a DSN, bounce message, non-delivery report, or NDR). For example: <ul><li>Completed moderation approval request messages.</li><li>Spam messages that were silently dropped without an NDR.</li></ul>|
|**DSN**|A delivery status notification (DSN) was generated.|
|**DUPLICATEDELIVER**|A duplicate message was delivered to the recipient. Duplication may occur if a recipient is a member of multiple nested distribution groups. Duplicate messages are detected and removed by the information store.|
|**DUPLICATEEXPAND**|During the expansion of the distribution group, a duplicate recipient was detected.|
|**DUPLICATEREDIRECT**|An alternate recipient for the message was already a recipient.|
|**EXPAND**|A distribution group was expanded.|
|**FAIL**|Message delivery failed. Sources include **SMTP**, **DNS**, **QUEUE**, and **ROUTING**.|
|**HADISCARD**|A shadow message was discarded after the primary copy was delivered to the next hop. For more information, see [Shadow redundancy](shadow-redundancy-exchange-2013-help.md).|
|**HARECEIVE**|A shadow message was received by the server in the local database availability group (DAG) or Active Directory site.|
|**HAREDIRECT**|A shadow message was created.|
|**HAREDIRECTFAIL**|A shadow message failed to be created. The details are stored in the **source-context** field.|
|**INITMESSAGECREATED**|A message was sent to a moderated recipient, so the message was sent to the arbitration mailbox for approval. For more information, see [Manage message approval](/exchange/security-and-compliance/mail-flow-rules/manage-message-approval).|
|**LOAD**|A message was successfully loaded at boot.|
|**MODERATIONEXPIRE**|A moderator for a moderated recipient never approved or rejected the message, so the message expired. For more information about moderated recipients, see [Manage message approval](/exchange/security-and-compliance/mail-flow-rules/manage-message-approval).|
|**MODERATORAPPROVE**|A moderator for a moderated recipient approved the message, so the message was delivered to the moderated recipient.|
|**MODERATORREJECT**|A moderator for a moderated recipient rejected the message, so the message wasn't delivered to the moderated recipient.|
|**MODERATORSALLNDR**|All approval requests sent to all moderators of a moderated recipient were undeliverable, and resulted in non-delivery reports (NDRs).|
|**NOTIFYMAPI**|A message was detected in the Outbox of a mailbox on the local server.|
|**NOTIFYSHADOW**|A message was detected in the Outbox of a mailbox on the local server, and a shadow copy of the message needs to be created.|
|**POISONMESSAGE**|A message was put in the poison message queue or removed from the poison message queue.|
|**PROCESS**|The message was successfully processed.|
|**PROCESSMEETINGMESSAGE**|A meeting message was processed by the Mailbox Transport Delivery service.|
|**RECEIVE**|A message was received by the SMTP receive component of the transport service or from the Pickup or Replay directories (source: `SMTP`), or a message was submitted from a mailbox to the Mailbox Transport Submission service (source: `STOREDRIVER`).|
|**REDIRECT**|A message was redirected to an alternative recipient after an Active Directory lookup.|
|**RESOLVE**|A message's recipients were resolved to a different email address after an Active Directory lookup.|
|**RESUBMIT**|A message was automatically resubmitted from Safety Net. For more information, see [Safety Net](safety-net-exchange-2013-help.md).|
|**RESUBMITDEFER**|A message resubmitted from Safety Net was deferred.|
|**RESUBMITFAIL**|A message resubmitted from Safety Net failed.|
|**SEND**|A message was sent by SMTP between transport services.|
|**SUBMIT**|The Mailbox Transport Submission service successfully transmitted the message to the Transport service. For **SUBMIT** events, the **source-context** property contains the following details: <ul><li>**MDB**: The mailbox database GUID.</li><li>**Mailbox**: The mailbox GUID.</li><li>**Event**: The event sequence number.</li><li>**MessageClass**: The type of message. For example, `IPM.Note`.</li><li>**CreationTime**: Date-time of the message submission.</li><li>**ClientType**: For example, `User`, `OWA` ,or `ActiveSync`.</li></ul>|
|**SUBMITDEFER**|The message transmission from the Mailbox Transport Submission service to the Transport service was deferred.|
|**SUBMITFAIL**|The message transmission from the Mailbox Transport Submission service to the Transport service failed.|
|**SUPPRESSED**|The message transmission was suppressed.|
|**THROTTLE**|The message was throttled.|
|**TRANSFER**|Recipients were moved to a forked message because of content conversion, message recipient limits, or agents. Sources include **ROUTING** or **QUEUE**.|

## Source values in the message tracking log

The values in the **source** field in the message tracking log indicate the transport component that's responsible for the message tracking event. The following table describes the values of the **source** field.

|Source value|Description|
|---|---|
|**ADMIN**|The event source was human intervention. For example, an administrator used Queue Viewer to delete a message, or submitted message files using the Replay directory.|
|**AGENT**|The event source was a transport agent.|
|**APPROVAL**|The event source was the approval framework that's used with moderated recipients. For more information, see [Manage message approval](/exchange/security-and-compliance/mail-flow-rules/manage-message-approval).|
|**BOOTLOADER**|The event source was unprocessed messages that exist on the server at boot time. This is related to the **LOAD** event type.|
|**DNS**|The event source was DNS.|
|**DSN**|The event source was a delivery status notification (DSN). For example, a non-delivery report (NDR).|
|**GATEWAY**|The event source was a Foreign connector. For more information, see [Foreign connectors](foreign-connectors-exchange-2013-help.md).|
|**MAILBOXRULE**|The event source was an Inbox rule. For more information, see [Inbox rules](https://support.microsoft.com/office/edea3d17-00c9-434b-b9b7-26ee8d9f5622).|
|**MEETINGMESSAGEPROCESSOR**|The event source was the meeting message processor, which updates calendars based on meeting updates.|
|**ORAR**|The event source was an Originator Requested Alternate Recipient (ORAR). You can enable or disable support for ORAR on Receive connectors using the _OrarEnabled_ parameter on the **New-ReceiveConnector** or **Set-ReceiveConnector** cmdlets.|
|**PICKUP**|The event source was the Pickup directory. For more information, see [Pickup directory and Replay directory](pickup-directory-and-replay-directory-exchange-2013-help.md).|
|**POISONMESSAGE**|The event source was the poison message identifier. For more information about poison messages and the poison message queue, see [Queues](queues-exchange-2013-help.md)|
|**PUBLICFOLDER**|The event source was a mail-enabled public folder.|
|**QUEUE**|The event source was a queue.|
|**REDUNDANCY**|The event source was Shadow Redundancy. For more information, see [Shadow redundancy](shadow-redundancy-exchange-2013-help.md).|
|**ROUTING**|The event source was the routing resolution component of the categorizer in the Transport service.|
|**SAFETYNET**|The event source was Safety Net. For more information, see [Safety Net](safety-net-exchange-2013-help.md).|
|**SMTP**|The message was submitted by the SMTP send or SMTP receive component of the transport service.|
|**STOREDRIVER**|The event source was a MAPI submission from a mailbox on the local server.|

## Example entries in the message tracking log

An uneventful message sent between two users generates several entries in the message tracking log. You can see the results using the **Get-MessageTrackingLog** cmdlet. For more information, see [Search message tracking logs](search-message-tracking-logs-exchange-2013-help.md).

This is a condensed example of the message tracking log entries created when the user chris@contoso.com successfully sends a test message to the user michelle@contoso.com. Both users have mailboxes on the same server.

```console
EventId    Source      Sender            Recipients             MessageSubject
-------    ------      ------            ----------             --------------
NOTIFYMAPI STOREDRIVER                   {}
RECEIVE    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
SUBMIT     STOREDRIVER chris@contoso.com {michelle@contoso.com} test
HAREDIRECT SMTP        chris@contoso.com {michelle@contoso.com} test
RECEIVE    SMTP        chris@contoso.com {michelle@contoso.com} test
AGENTINFO  AGENT       chris@contoso.com {michelle@contoso.com} test
SEND       SMTP        chris@contoso.com {michelle@contoso.com} test
DELIVER    STOREDRIVER chris@contoso.com {michelle@contoso.com} test
```

## Security concerns for the message tracking log

No message content is stored in the message tracking log. By default, the subject line of an email message is stored in the message tracking log. You may want to disable message subject logging to comply with increased security or privacy requirements. Before you enable or disable message subject logging, make sure that you verify your organization's policy about revealing subject line information. For more information, see [Configure message tracking](configure-message-tracking-exchange-2013-help.md).
