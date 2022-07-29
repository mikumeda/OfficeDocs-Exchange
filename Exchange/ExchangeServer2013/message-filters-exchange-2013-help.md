---
title: 'Message filters: Exchange 2013 Help'
TOCTitle: Message filters
ms:assetid: 8e6187c1-76f0-49da-bc24-2ab57cfb3c2c
ms:mtpsurl: https://technet.microsoft.com/library/Bb123714(v=EXCHG.150)
ms:contentKeyID: 49286849
ms.topic: article
description: Configure filter criteria.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Message filters

_**Applies to:** Exchange Server 2013_

Filtering generates different views of the messages in queues. By specifying filter criteria, you can quickly locate messages and take action on them. When an email message is sent to multiple recipients, the message may be located in multiple queues. When you filter by message properties, you can locate messages across all queues. The following scenarios are examples of how you might use message filtering to manage mail flow:

- The Submission queue on the Mailbox server or Edge Transport server that receives email from the Internet has a high volume of messages that are queued for delivery. Many of the messages have the same subject. Therefore, you suspect that spam is being sent to your organization. You can create a filter to view all the messages that meet the subject criteria. If you determine that the messages are spam, you can select them all and delete them from the delivery queue without sending an NDR.

- A user reports that mail flow is slow. You examine the queues and see that many messages that have random subjects appear to be coming from a single domain. You can create a filter to view all the queued messages from that domain. If you determine that the messages are spam, you can select them all and delete them from the queues without sending an NDR.

## Message properties as filters

You can use message properties to create a filter and locate messages that meet specified criteria. You can create filters in Queue Viewer, or by using the _Filter_ parameter on the message management cmdlets. Note that the message management cmdlets support more filterable properties than the Queue Viewer. The following table lists the message properties by which you can filter and the values that are associated with those properties.

### Message properties to use when filtering messages

|Queue Viewer message property|Shell message property|Description|
|---|---|---|
|**Date Received**|`DateReceived`|The date/time when the message was placed in the queue.|
|n/a|`DeferReason`|This property identifies why the message was deferred. If the message wasn't deferred, this property has the value `None`. A deferred message is returned to the Submission queue because of transient errors that were encountered during recipient resolution. For more information about deferred messages, see [Recipient resolution](recipient-resolution-exchange-2013-help.md). The possible values are: <ul><li>`AD Transient Failure During Content Conversion`</li><li>`AD Transient Failure During Resolve`</li><li>`Agent`</li><li>`Ambiguous Recipient`</li><li>`Loop Detected`</li><li>`Marked As Retry Delivery If Rejected`</li><li>`Rerouted By Store Driver`</li><li>`Storage Transient Failure During Content Conversion`</li><li>`Transient Failure`</li><li>`Target Site Inbound Mail Disabled`</li><li>`Recipient Thread Limit Exceeded`</li><li>`Transient Attribution Failure`</li><li>`Transient Accepted Domains Load Failure`</li></ul>|
|**Expiration Time**|`ExpirationTime`|This property contains the date/time when the message will expire and be deleted from the queue if the message can't be delivered.|
|**From Address**|`FromAddress`|This property contains the SMTP address of the sender.|
|n/a|`Identity`|This property is the identity of the message in the form of _\<Server\>\\<Queue\>\&lt;MessageInteger\>_. For more information see the "Message identity" section in the [Queues](queues-exchange-2013-help.md) topic.|
|**Internet Message ID**|`InternetMessageId`|This property contains the value of the `Message-ID:` header field that's located in the message header. The value is expressed as an email address that contains a GUID and the FQDN the sending SMTP server. For example: <br/><br/> `<67D754D6103DC4FB3BA6BC7205DACABA61231@mailbox01.contoso.com>`|
|**Last Error**|`LastError`|This property contains the text of the last error that was recorded for a message. For example, `A matching connector cannot be found to route the external recipient`.|
|n/a|`MessageLatency`|This property contains the amount of time elapsed between when the message first entered the Submission queue on the server, and when the message was placed in the queue. The value uses the syntax _hh:mm:ss.ff_, where _hh_ = hour, _mm_ = minute, _ss_ = second, and _ff_ = fractions of a second.|
|**Message Source Name**|`MessageSourceName`|This property contains a text string that indicates the name of the transport component that submitted the message to the queue. For example, if the message came in through a Receive connector, the value is: `SMTP:`_\<ConnectorName\>_. If the message is a delivery status notification (DSN), the value is `DSN`.|
|n/a|`Priority`|This property contains the priority of the message that's assigned by the user in Outlook or Outlook Web App. The possible values are `Low`, `Normal`, and `High`. For more information, see [Priority queuing](priority-queuing-exchange-2013-help.md).|
|**Queue ID**|`Queue`|This property is the identity of the queue that holds the message. The queue identity uses the syntax _\<Server\>\\<Queue\>_. For more information, see the "Queue identity" section in the [Queues](queues-exchange-2013-help.md) topic.|
|n/a|`RetryCount`|This property identifies the number of times that delivery of the message to the destination was tried, either automatically or manually.|
|**SCL**|`SCL`|The value of the spam confidence level (SCL) property specifies the SCL of the message. Valid SCL entries are integers from 0 through 9. An empty SCL property value indicates that the message hasn't been processed by the Content Filter agent. <br/><br/> This property contains the spam confidence level (SCL) value of the message. Valid SCL entries are integers from 0 through 9 and -1. For more information, see [Spam Confidence Level Threshold](spam-confidence-level-threshold-exchange-2013-help.md).|
|**Size (KB)**|`Size`|This property indicates the size of the message.|
|**Source IP**|`SourceIP`|This property contains the IP address of the server that submitted the message to the Exchange server that holds the message in the queue. The address could be the IP address of a remote SMTP server, or the IP address of the local Exchange server.|
|**Status**|`Status`|This property indicates the current message status. A message can have one of the following status values: <ul><li>`Active`</li><li>`Locked`</li><li>`None`</li><li>`Pending Remove`</li><li>`Pending Suspend`</li><li>`Ready`</li><li>`Retry`</li><li>`Suspended`</li><li> <p> For more information, see the "Message properties" section in the [Queues](queues-exchange-2013-help.md) topic.|
|**Subject**|`Subject`|This property indicates the subject of a message that's found in the `Subject:` header field in the message header.|
