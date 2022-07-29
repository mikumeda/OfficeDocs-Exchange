---
title: 'Queue filters: Exchange 2013 Help'
TOCTitle: Queue filters
ms:assetid: fbfbdcab-e0d2-4ed9-8f7f-e5fa2c87360d
ms:mtpsurl: https://technet.microsoft.com/library/Bb125237(v=EXCHG.150)
ms:contentKeyID: 49286856
ms.topic: article
description: Use queue filters to generate different views of queues.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Queue filters

_**Applies to:** Exchange Server 2013_

Filtering generates different views of queues. You use the queue properties as filter options. By specifying filter criteria, you can quickly locate queues and take action on them. The following scenarios are examples of how you might use queue filtering to manage mail flow:

- You receive a message from the Microsoft System Center Operations Manager that indicates that a queue length has exceeded the established threshold. You want to investigate whether a server-wide mail flow problem exists.

  You can create a filter to view all the queues that have a message count that exceeds what you consider typical. If a mail flow problem is indicated, you can select all the queues in the filter results and suspend the queues while you continue to investigate.

- You suspend several queues to investigate the cause of mail flow problems. You determine that the problem was caused by an incorrect connector configuration and is now fixed.

  You can create a filter to view all the queues that have a status of Suspended, and then select all the queues in the filter results and resume the queues.

## Queue properties to use when filtering queues

You can use the queue properties to create a filter and locate queues that meet specified criteria. You can create filters in Queue Viewer, or by using the _Filter_ parameter on the queue management cmdlets. Note that the queue management cmdlets support more filterable properties than the Queue Viewer. The following table lists the queue properties by which you can filter and the valid values for those properties.

|Queue Viewer queue property|Shell queue property|Description|
|---|---|---|
|n/a|`DeferredMessageCount`|This property identifies the number of messages that were returned to the Submission queue because of transient errors that were encountered during recipient resolution. For more information about deferred messages, see [Recipient resolution](recipient-resolution-exchange-2013-help.md).|
|**Delivery Type**|`DeliveryType`|The valid values for **DeliveryType** are explained in the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|
|n/a|`Identity`|This property is the identity of the queue in the form of _\<Server\>\\<Queue\>_. For more information see the "Queue identity" section in the [Queues](queues-exchange-2013-help.md) topic.|
|n/a|`IncomingRate`|This property is a calculated number that indicates how quickly messages are entering the queue. For more information, see "IncomingRate, OutgoingRate, and Velocity" section in the [Queues](queues-exchange-2013-help.md) topic.|
|**Last Error**|`LastError`|This property indicates the text string of the last error that was recorded for the queue.|
|**Last Retry Time**|`LastRetryTime`|This property indicates the date/time of the last connection attempt for a queue that has a status of `Retry`.|
|n/a|`LockedMessageCount`|This property is reserved for internal Microsoft use, and isn't used in on-premises Exchange 2013 organizations.|
|**Message Count**|`MessageCount`|This property indicates the number of messages in the queue.|
|n/a|`NextHopCategory`|This property designates the next hop of the queue as `Internal` or `External` and is based on the value of the **DeliveryType** property of the queue. For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|
|n/a|`NextHopConnector`|This property is the GUID of the next hop and is based on the value of the **DeliveryType** property of the queue. For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|
|**Next Hop Domain**|`NextHopDomain`|This property is the name of next hop and is based on the value of the **DeliveryType** property of the queue . For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|
|**Next Retry Time**|`NextRetryTime`|This property indicates the date/time of the next connection attempt for a queue that has a status of `Retry`.|
|n/a|`OutgoingRate`|This property is a calculated number that indicates how quickly messages are leaving the queue. For more information, see "IncomingRate, OutgoingRate, and Velocity" section in the [Queues](queues-exchange-2013-help.md) topic.|
|n/a|`RiskLevel`|This property is reserved for internal Microsoft use, and isn't used in on-premises Exchange 2013 organizations.|
|**Status**|`Status`|This property indicates the current queue status. A queue can have one of the following status values Active, Connecting, None, Suspended, Ready, or Retry. For more information, see the "Queue status" section in the [Queues](queues-exchange-2013-help.md) topic.|
|n/a|`TlsDomain`|This property contains the FQDN of the destination domain if the domain is configured for Domain Security.|
|n/a|`Velocity`|This property contains a calculated number that indicates how effectively the queue is draining. For more information, see "IncomingRate, OutgoingRate, and Velocity" section in the [Queues](queues-exchange-2013-help.md) topic.|
