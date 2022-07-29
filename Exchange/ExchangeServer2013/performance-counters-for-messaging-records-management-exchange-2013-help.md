---
title: 'Performance counters for messaging records management: Exchange 2013 Help'
TOCTitle: Performance counters for messaging records management
ms:assetid: b59def6f-4249-4e0c-8057-8ae6eb7c5676
ms:mtpsurl: https://technet.microsoft.com/library/Bb310790(v=EXCHG.150)
ms:contentKeyID: 50873808
ms.topic: article
description: Performance counters for messaging records management.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Performance counters for messaging records management

_**Applies to:** Exchange Server 2013_

The performance counters in this topic monitor the Managed Folder Assistant as it implements messaging records management (MRM) for Microsoft Exchange Server 2010. Because running the Managed Folder Assistant is a resource-intensive process, you should run it only when your server can tolerate the additional load. You should also monitor server performance when the Managed Folder Assistant is running. In addition to the performance counters listed in this topic, you may also want to monitor additional performance counters that monitor items such as disk performance and CPU usage.

For more information about monitoring computers running MRM, see [Monitoring messaging records management](monitoring-messaging-records-management-exchange-2013-help.md).

## Performance Counters for MRM

The following table describes performance counters for MRM.

|Performance counter|Performance object|Description|
|---|---|---|
|Average Mailbox Processing Time In Seconds|MSExchange Assistants|Counts the average processing time of mailboxes for time-based assistants.|
|Mailboxes Processed|MSExchange Assistants|Counts the number of mailboxes processed by time-based assistants since the service started.|
|Mailboxes processed/sec|MSExchange Assistants|Determines the rate of mailboxes processed by time-based assistants per second.|
|Items Deleted but Recoverable|MSExchange Managed Folder Assistant|Counts the number of items deleted by the Managed Folder Assistant since the start of the most recent schedule interval. (The items are still recoverable through the Recoverable Items folder.) The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes that you specified for processing. This counter is reset to zero at the start of each schedule interval.|
|Items Journaled|MSExchange Managed Folder Assistant|Counts the number of items journaled by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the current work cycle and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each work cycle.|
|Items Marked as Past Retention Date|MSExchange Managed Folder Assistant|Counts the number of items marked as past their retention date by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each schedule interval.|
|Items Moved|MSExchange Managed Folder Assistant|Counts the number of items moved by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each schedule interval.|
|Items Permanently Deleted|MSExchange Managed Folder Assistant|Counts the number of items permanently deleted by the Managed Folder Assistant since the beginning of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the beginning of each schedule interval.|
|Items Subject to Retention Policy|MSExchange Managed Folder Assistant|Counts the number of items subject to retention policy by the Managed Folder Assistant since the start of the most recent schedule interval. The number includes items in the mailboxes scheduled for processing during the schedule interval and items in any mailboxes you specified for processing. This counter is reset to zero at the start of each schedule interval. This counter is the sum of the following four expiration-related counters: <ul><li>Items Journaled</li><li>Items Marked as Past Retention Date</li><li>Items Moved</li><li>Items Permanently Deleted</li></ul>|
|TotalSizeItemsExpired - Size of Items subject to Retention Policy (In Bytes)|MSExchange Managed Folder Assistant|Indicates the total size of items expired by the Managed Folder Assistant (SoftDelete, HardDelete, MoveToArchive). <br/><br/> The following items are included: <ul><li>Messages subject to deletion or move to a managed custom folder by a managed folder mailbox policy</li><li>Messages subject to deletion or move to archive by the user's retention policy</li><li>Messages expired by dumpster policy</li><li>Messages cleaned up by system cleanup tags</li></ul> <p> This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.|
|TotalSizeItemsSoftDeleted - Size of Items Deleted but Recoverable (In Bytes)|MSExchange Managed Folder Assistant|Indicates the total size of items soft deleted by the Managed Folder Assistant. <br/><br/> The following items are included: <ul><li>Messages soft deleted by a managed folder mailbox policy</li><li>Messages soft deleted by a retention policy</li></ul> <p> This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.|
|TotalSizeItemsPermanentlyDeleted - Size of Items Permanently Deleted (In Bytes)|MSExchange Managed Folder Assistant|Indicates the total size of items soft deleted by the Managed Folder Assistant. <br/><br/> The following items are included: <ul><li>Messages hard deleted by a managed folder mailbox policy</li><li>Messages hard deleted by a retention policy</li><li>Messages hard deleted by the Recoverable Items policy</li></ul> <p> This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.|
|TotalSizeItemsMoved - Size of Items Moved because of an Archive policy tag (In Bytes)|MSExchange Managed Folder Assistant|Indicates the total size of items moved to a folder or moved to archive by the Managed Folder Assistant. <br/><br/> The following items are included: <ul><li>Messages moved to a managed custom folder by a managed folder mailbox policy</li><li>Messages moved to the personal archive by a retention policy</li></ul> <p> This counter is reset to zero at every work cycle checkpoint of the Managed Folder Assistant work cycle.|
|TotalItemsWithPersonalTag - Items stamped with Personal Tag (Expiry or Archive)|MSExchange Managed Folder Assistant|Indicates the number of times a user tags items with a personal tag. <br/><br/> This includes both Deletion and Archive tags. <br/><br/> For example: <ul><li>An item is tagged with a personal tag.</li><li>An item with a personal tag is retagged with another personal tag.</li></ul> <p> If a folder is tagged with a personal tag, the counter is incremented by the total number of items in the folder.|
|TotalItemsWithDefaultTag - Items stamped with Default Tag (Expiry or Archive)|MSExchange Managed Folder Assistant|Indicates the number of items assigned a default policy tag (DPT) based on a user action, for example, when a user selects a message with a personal tag and selects **Use folder policy**. <br/><br/> If a new user is assigned a retention policy with a DPT, the counter is incremented by the number of items that will be assigned the DPT because of the retention policy. <br/><br/> **Note**: If a user has a retention policy with a DPT, new messages that arrive through transport get a default tag, and this isn't tracked by this counter.|
|TotalItemsWithSystemCleanupTag - Items stamped with System Cleanup Tag|MSExchange Managed Folder Assistant|Indicates the number of items tagged with the system cleanup tag. This includes mailbox metadata items that aren't visible to users.|
|TotalItemsExpiredByDefaultExpiryTag - Items expired because of a default Expiry Tag|MSExchange Managed Folder Assistant|Indicates the number of items expired (soft or hard deleted) by the Managed Folder Assistant because of any non-personal (default or system) tag in a retention policy. <br/><br/> This doesn't include the items expired by Recoverable Items clean up or system clean up.|
|TotalItemsExpiredByPersonalExpiryTag - Items expired because of a personal Expiry Tag|MSExchange Managed Folder Assistant|Indicates the number of items expired (soft or hard deleted) by the Managed Folder Assistant because of a personal tag in the retention policy.|
|TotalItemsMovedByDefaultArchiveTag - Items moved because of a default Archive Tag|MSExchange Managed Folder Assistant|Indicates the number of items moved to the archive by the Managed Folder Assistant because of any non-personal (default or system) archive tag in a retention policy. <br/><br/> This doesn't include the items moved to the Recoverable Items folder in archive by Recoverable Items cleanup.|
|TotalItemsMovedByPersonalArchiveTag - Items Moved because of an Archive Tag|MSExchange Managed Folder Assistant|Indicates the number of items moved to the archive by the Managed Folder Assistant because of a personal archive tag in a retention policy.|
|TotalMovedDumpsterItems - Mailbox Dumpsters Moved Items|MSExchange Managed Folder Assistant|Indicates the number of items moved to the Recoverable Items folder in the archive by Recoverable Items cleanup.|
