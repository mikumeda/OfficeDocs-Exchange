---
title: 'Priority queuing: Exchange 2013 Help'
TOCTitle: Priority queuing
ms:assetid: 6edbd826-fe55-435b-9c63-48e6365c3d09
ms:mtpsurl: https://technet.microsoft.com/library/Bb691107(v=EXCHG.150)
ms:contentKeyID: 50646236
ms.reviewer: 
ms.topic: article
description: Priority queuing in Exchange Server 2013 enables the sender-defined priority of a message to influence the message processing by the Transport service on the Mailbox server
manager: serdars
ms.author: serdars
author: serdars
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Priority queuing

_**Applies to:** Exchange Server 2013_

_Priority queuing_ is a feature of Microsoft Exchange Server 2013 that enables the sender-defined priority of a message to influence the processing of the message by the Transport service on the Mailbox server.

The message priority is assigned by the sender in Microsoft Outlook when the sender creates and sends the message. The sender can set any of the following message priority values in Outlook:

- Low importance
- Normal importance
- High importance

The default priority for a message created in Outlook or Outlook Web App is Normal priority. The message priority is stored in the `X-Priority` header field in the message header.

Every message sent or received in an Exchange 2013 organization must be categorized by the Transport service on a Mailbox server before it can be routed and delivered. The categorizer in the Transport service on a Mailbox server picks up one message at a time from the Submission queue and performs recipient resolution, routing resolution, and content conversion on the message before putting the message in a delivery queue. For more information, see [Mail flow](mail-flow-exchange-2013-help.md).

Delivery queues are dynamically created based on the destination of a message. For more information, see [Queues](queues-exchange-2013-help.md).

All messages that have the same destination are put in the same delivery queue. Priority queuing affects the transmission of messages from a delivery queue to the destination messaging server. When priority queuing is enabled, High priority messages are transmitted to their destinations before Normal priority messages, and Normal priority messages are transmitted to their destinations before Low priority messages. The prioritized delivery of messages based on the message priority can help you define specific service level agreement (SLA) requirements for message delivery times.

## Options for configuring priority queuing

Support for priority queuing is controlled by keys in the `%ExchangeInstallPath%bin\EdgeTransport.exe.config` XML application configuration file. For instructions on how to configure priority queuing, see [Enable and configure priority queuing](enable-and-configure-priority-queuing-exchange-2013-help.md).

The following table explains each key in more detail.

### Priority queuing keys in the EdgeTransport.exe.config file

|Key|Default value|Description|
|---|---|---|
|_PriorityQueuingEnabled_|`false`|This key enables or disables priority queuing in the Transport service on the Mailbox server. Valid input for this key is `true` or `false`. <br/><br/> When this key is `false`, priority queuing is disabled, and all the priority queuing message limits that exist in the EdgeTransport.exe.config file are ignored.|
|_MaxHighPriorityMessageSize_|`250KB`|This key specifies the maximum allowed size of a High priority message. If a High priority message is larger than the value specified by this key, the message is automatically downgraded from High priority to Normal priority. <br/><br/> The value of this key should be significantly less than the value of the _MaxSendMessageSize_ parameter on the **Set-TransportConfig** cmdlet. The default value of this parameter is `10 MB`. The difference in these two values helps ensure consistent and predictable delivery times for High priority messages. <br/><br/> When you enter a value, qualify the value with one of the following units: <ul><li>KB (kilobytes)</li><li>MB (megabytes)</li></ul>|
|_LowPriorityDelayNotificationTimeout_ <br/><br/> _NormalPriorityDelayNotificationTimeout_ <br/><br/> _HighPriorityDelayNotificationTimeout_|**Low**: `8:00:00` (8 hours) <br/><br/> **Normal**: `4:00:00` (4 hours) <br/><br/> **High**: `00:30:00` (30 minutes)|These keys specify the timeout interval for delay delivery status notification (DSN) messages based on the message priority. <br/><br/> After each message delivery failure, the Transport service generates a delay DSN message and queues it for delivery to the sender of the undeliverable message. This delay DSN message is sent only after a specified delay notification time-out interval, and only if the failed message wasn't successfully delivered during that time. This delay prevents the sending of unnecessary delay DSN messages that may be caused by temporary message transmission failures. <br/><br/> To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.|
|_LowPriorityMessageExpirationTimeout_ <br/><br/> _NormalPriorityMessageExpirationTimeout_ <br/><br/> _HighPriorityMessageExpirationTimeout_|**Low**: `2.00:00:00` (2 days) <br/><br/> **Normal**: `2.00:00:00` (2 days) <br/><br/> **High**: `8:00:00` (8 hours)|These keys specify the maximum length of time that the Transport service tries to deliver a failed message. If the message can't be successfully delivered before the expiration time-out interval has passed, a non-delivery report (NDR) that contains the original message or the message headers is delivered to the sender. <br/><br/> To specify a value, enter it as a time span: dd.hh:mm:ss where d = days, h = hours, m = minutes, and s = seconds.|
|_MaxPerDomainLowPriorityConnections_ <br/><br/> _MaxPerDomainNormalPriorityConnections_ <br/><br/> _MaxPerDomainHighPriorityConnections_|**Low**: 2 <br/><br/> **Normal**: 15 <br/><br/> **High**: 3|These keys specify the maximum number of connections that the Transport service can have open to any single remote domain. The outgoing connections to remote domains occur by using the delivery queues and Send connectors that exist on the Mailbox server. <br/><br/> The sum these three keys should be less than or equal to the value of the _MaxPerDomainOutboundConnections_ parameter on the **Set-TransportService** cmdlet. The default value of this parameter is `20`.|

## How priority queuing affects other message limits on Mailbox servers

All messages that pass through the Transport service are subject to a variety of message retry, resubmit, and expiration limits. For more information, see [Message size limits](message-size-limits-exchange-2013-help.md).

Some message limits available in the **Set-TransportService** cmdlet have corresponding priority queuing message limits available in the EdgeTransport.exe.config application configuration file. The following table shows these corresponding message limits.

### Message limits in the Set-TransportService cmdlet that correspond to priority queuing message limits in the EdgeTransport.exe.config file

|Source|Parameter or key|Default value|
|---|---|---|
|**Set-TransportService**|_DelayNotificationTimeOut_|`4:00:00` (4 hours)|
|EdgeTransport.exe.config|_NormalPriorityDelayNotificationTimeout_|`4:00:00` (4 hours)|
|**Set-TransportService**|_MessageExpirationTimeOut_|`2.00:00:00` (2 days)|
|EdgeTransport.exe.config|_NormalPriorityMessageExpirationTimeout_|`2.00:00:00` (2 days)|

When priority queuing is disabled, all the priority queuing message limits that exist in the EdgeTransport.exe.config configuration file are ignored. All the message limits on the **Set-TransportService** cmdlet apply to all messages that travel through the Transport service on the Mailbox server.

When priority queuing is enabled, the priority queuing message limits in the EdgeTransport.exe.config configuration file override the corresponding message limits in the **Set-TransportService** cmdlet. All other message limits in the **Set-TransportService** cmdlet still apply to Low priority, Normal priority, and High priority messages that travel through the Transport service on the Mailbox server.

## User Settings for Priority Queuing

The **Set-Mailbox** cmdlet has the _DowngradeHighPriorityMessagesEnabled_ parameter. The default value is `$false`. When this parameter is set to `$true`, any High priority messages sent from the mailbox are automatically downgraded to Normal priority.
