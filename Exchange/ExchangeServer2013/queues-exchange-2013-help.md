---
title: 'Queues: Exchange 2013 Help'
TOCTitle: Queues
ms:assetid: e7ad0ba5-3789-4a2b-9825-6bb1b321609c
ms:mtpsurl: https://technet.microsoft.com/library/Bb125022(v=EXCHG.150)
ms:contentKeyID: 50646240
ms.reviewer: 
ms.topic: article
description: About queues in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Queues

_**Applies to:** Exchange Server 2013_

A _queue_ is a temporary holding location for messages that are waiting to enter the next stage of processing or delivery to a destination. Each queue represents a logical set of messages that the Exchange server processes in a specific order. In Microsoft Exchange Server 2013, queues hold messages before, during and after delivery. Queues exist on Mailbox servers and Edge Transport servers. Mailbox servers and Edge Transport servers are called _transport servers_ throughout this topic.

Like the previous versions of Exchange, Exchange 2013 uses a single Extensible Storage Engine (ESE) database for queue storage.

You can manage queues and the messages in queues using the Exchange Management Shell and Queue Viewer in the Exchange Toolbox. You can use these interfaces to view the status and contents of queues and detailed message properties. You can also use these interfaces to perform actions that modify queues or the messages in the queues.

## Types of queues

The following types of queues are used in Exchange 2013:

- **Persistent queues**: _Persistent queues_ are queues that exist on every transport server in every Exchange organization. Like previous versions of Exchange, there are three persistent queues in Exchange 2013:

  - **Submission queue**: The Submission queue is used by the categorizer to gather all messages that have to be resolved, routed, and processed by transport agents on the transport server. All messages that are received by a transport server enter processing in the Submission queue. On Mailbox servers, messages are submitted through a Receive connector, the Pickup or Replay directories, or the Mailbox Transport Submission service. On Edge Transport servers, messages are typically submitted through a Receive connector, but the Pickup and Replay directories are also available.

    The categorizer retrieves messages from this queue and, among other things, determines the location of the recipient and the route to that location. After categorization, the message is moved to a delivery queue or to the Unreachable queue. Each transport server has only one Submission queue. Messages that are in the Submission queue can't be in other queues at the same time. For more information about the categorizer and the transport pipeline, see [Mail flow](mail-flow-exchange-2013-help.md).

  - **Unreachable queue**: The Unreachable queue contains messages that can't be routed to their destinations. Typically, an unreachable destination is caused by configuration changes that have modified the routing path for delivery. Regardless of destination, all messages that have unreachable recipients reside in this queue. Each transport server has only one Unreachable queue.

    Messages in the Unreachable queue are automatically resubmitted when a routing change is detected. So, after the condition or configuration error caused the messages to enter the Unreachable queue is repaired, you don't need to take additional action to move the messages out of the Unreachable queue for delivery.

    The Unreachable queue is typically empty. If the Unreachable queue contains no messages it doesn't appear in Queue Viewer or **Get-Queue** results.

  - **Poison message queue**: The poison message queue is a special queue that's used to isolate messages that are determined to be harmful to the Exchange 2013 system after a transport server or service failure. The messages may be genuinely harmful in their content and format. Alternatively, they may be the results of a poorly written agent that has caused the Exchange server to fail when it processed the supposedly bad messages.

    The poison message queue is typically empty. If the poison message queue contains no messages it doesn't appear in Queue Viewer or **Get-Queue** results. The messages in the poison message queue are never automatically resumed or expired. Messages remain in the poison message queue until they're manually resumed or removed by an administrator.

- **Delivery queues**: Delivery queues hold messages that are being delivered to any local or remote destinations by using SMTP. All messages are transmitted between Exchange servers by using SMTP. Non-SMTP destinations also use delivery queues if the destination is serviced by a Delivery Agent connector. . Each delivery queue contains messages that are being routed to the same destination. It's practically inevitable that multiple delivery queues will exist on a transport server. Delivery queues are dynamically created when they're required and are automatically deleted when the queue is empty and the expiration time has passed. The queue expiration time is controlled by the _QueueMaxIdleTime_ parameter on the **Set-TransportService** cmdlet. The default value is three minutes.

- **Shadow queues**: Shadow queues hold redundant copies of a message while the message is in transit. For more information, see [Shadow redundancy](shadow-redundancy-exchange-2013-help.md).

- **Safety Net**: Safety Net retains copies of messages that were successfully delivered by the transport server. Although it's not accessible by queue management tools, Safety Net is just another queue in the queue database. For more information, see [Safety Net](safety-net-exchange-2013-help.md).

## Queue database files

All the different queues are stored in a single ESE database. By default, this queue database is located on the transport server at `%ExchangeInstallPath%TransportRoles\data\Queue`.

Like any ESE database, the queue database uses log files to accept, track, and maintain data. To enhance performance, all message transactions are written first to log files and memory, and then to the database file. The checkpoint file tracks the transaction log entries that have been committed to the database. During an ordinary shutdown of the Microsoft Exchange Transport service, uncommitted database changes that are found in the transaction logs are always committed to the database.

Circular logging is used for the queue database. This means that the history of committed transactions that are found in the transaction logs isn't maintained. Any transaction logs that are older than the current checkpoint are immediately and automatically deleted. Therefore, the transaction logs can't be replayed for queue database recovery from backup.

Exchange 2013 uses _generation tables_ for storage and clean-up of messages in the queue database. Instead of processing and deleting individual message records from one large table, the queue database stores messages in time-based tables, and only deletes the entire table after all the messages in the table have been successfully processed. For example, all messages queued from 1:00 PM to 2:00 PM, regardless of the queue or destination, are stored in the `1p-2p_msgs` table. At 2:00 PM, new messages are stored in the `2p-3p_msgs` table. At 4:00 PM, a new table named `4p-5p_msgs` is created, and the entire `1p-2p_msgs` table is deleted, but only if all messages in the table have been successfully processed. This approach of deleting entire messages tables instead of individual messages helps improves the I/O performance of the drive that holds the queue database.

The following table lists the files that constitute the queue database.

### Files that constitute the queue database

|File|Description|
|---|---|
|Mail.que|This queue database file stores all the queued messages.|
|Tmp.edb|This temporary database file is used to verify the queue database schema on startup.|
|Trn_.log|This transaction log records all changes to the queue database. Changes to the database are first written to the transaction log and then committed to the database. Trn.log is the current active transaction log file. Trntmp.log is the next provisioned transaction log file that's created in advance. If the existing Trn.log transaction log file reaches its maximum size, Trn.log is renamed to Trn_nnnn_.log, where _nnnn_ is a sequence number. Trntmp.log is then renamed Trn.log and becomes the current active transaction log file.|
|Trn.chk|This checkpoint file tracks the transaction log entries that have been committed to the database. This file is always in the same location as the mail.que file.|
|Trnres00001.jrs <br/><br/> Trnres00002.jrs|These reserve transaction log files act as placeholders. They're only used when the hard disk that contains the transaction log runs out of space to stop the queue database cleanly.|

## Options for configuring the queue database

You configure the queue database by adding or modifying keys in the `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML application configuration file. This file is associated with the Microsoft Exchange Transport service. Changes you make to the EdgeTransport.exe.config file take effect after you restart the Microsoft Exchange Transport service.

The `<appSettings>` section of the EdgeTransport.exe.config file is where you can add new keys or modify existing keys. If a specific key doesn't exist, you can add it manually to change its value.

The keys for the queue database that are available in the EdgeTransport.exe.config file are described in the following table.

### Message queue database keys that are available in the EdgeTransport.exe.config file

|Key|Default value|Description|
|---|---|---|
|_QueueDatabaseBatchSize_|40|This key specifies the number of database I/O operations that can be grouped together before they're executed. By default, this key doesn't exist in the EdgeTransport.exe.config file.|
|_QueueDatabaseBatchTimeout_|100|This key specifies the maximum time in milliseconds that the database will wait for multiple database I/O operations to group before it executes them. The database I/O operations are executed without waiting for any more if the following conditions are true: <ul><li>The number of database I/O operations that's specified by the _QueueDatabaseBatchSize_ key hasn't been reached.</li><li>The time specified by the _QueueDatabaseBatchTimeout_ key has passed.</li></ul> <p> By default, this key doesn't exist in the EdgeTransport.exe.config file.|
|_QueueDatabaseMaxConnections_|4|This key specifies the number of ESE database connections that can be open.|
|_QueueDatabaseLoggingBufferSize_|5 MB|This key specifies the memory that's used to cache the transaction records before they're written to the transaction log file.|
|_QueueDatabaseLoggingFileSize_|5 MB|This key specifies the maximum size of a transaction log file. When the maximum log file size is reached, a new log file is opened.|
|_QueueDatabaseLoggingPath_|`%ExchangeInstallPath%TransportRoles\data\Queue`|This key specifies the default directory for the queue database log files. For instructions on how to change the location of the queue database, see [Change the location of the queue database](change-the-location-of-the-queue-database-exchange-2013-help.md).|
|_QueueDatabaseMaxBackgroundCleanupTasks_|32|This key specifies the maximum number of background cleanup work items that can be queued to the database engine thread pool at any time.|
|_QueueDatabaseOnlineDefragEnabled_|True|The key enables or disables scheduled online defragmentation of the mail queue database. By default, this key doesn't exist in the EdgeTransport.exe.config file.|
|_QueueDatabaseOnlineDefragSchedule_|`1:00:00` or 1:00 A.M.|This key specifies the time of day in 24 hour format to start the online defragmentation of the mail queue database. To specify a value, enter the value as a time: _hh:mm:ss_, where _h_ = hours, _m_ = minutes, and _s_ = seconds.|
|_QueueDatabaseOnlineDefragTimeToRun_|`3:00:00` or 3 hours|This key specifies the length of time the online defragmentation task is allowed to run. Even if the defragmentation task doesn't finish in the time specified, the queue database is left in a consistent state. To specify a value, enter the value as a time span: _hh:mm:ss_, where _h_ = hours, _m_ = minutes, and _s_ = seconds.|
|_QueueDatabasePath_|`%ExchangeInstallPath%TransportRoles\data\Queue`|This key specifies the default directory for the queue database files. For instructions on how to change the location of the queue database, see [Change the location of the queue database](change-the-location-of-the-queue-database-exchange-2013-help.md).|

> [!NOTE]
> Any customized per-server settings you make in Exchange XML application configuration files, for example, web.config files on Client Access servers or the EdgeTransport.exe.config file on Mailbox servers, will be overwritten when you install an Exchange Cumulative Update (CU). Make sure that you save this information so you can easily re-configure your server after the install. You must re-configure these settings after you install an Exchange CU.

## Queue properties

A queue has many properties that describe the purpose and status of the queue. Some queue properties are applied to the queue when the queue is created, and don't change. Other properties contain status size, time, or other indicators that are updated frequently.

## NextHopSolutionKey

The routing component of the categorizer in the Microsoft Exchange Transport service selects the destination for a message, and this destination is used to create the delivery queue. The destination is stamped on every recipient as the **NextHopSolutionKey** attribute. Every unique value of the **NextHopSolutionKey** attribute corresponds to a separate delivery queue.

The **NextHopSolutionKey** attribute contains the following fields:

- **DeliveryType**: The value of this field represents the results of the categorization of the message, and how the Transport service intends to transmit the message to the next hop, which could be the ultimate destination of the message, or an intermediate hop along the way. The Transport service uses a predefined list of values for **DeliveryType** based on the target routing destination or delivery group.

- **NextHopDomain**: This field uses specific values based on the value of the **DeliveryType** field. For delivery queues, the value of this field is effectively the name of the queue. The value of **NextHopDomain** isn't always a domain name. For example, the value could be the name of the target Active Directory site or database availability group (DAG). Think of this field as the next hop name, where the value is the name of the routing destination or the target delivery group.

- **NextHopConnector**: This field uses specific values based on the value of the **DeliveryType** field. The value is always expressed as a GUID. If this field isn't used, the value is a GUID with all zeroes. The value of **NextHopConnector** isn't always the GUID of a connector. For example, the value could be the GUID of the target Active Directory site or DAG. Think of this field as the next hop GUID, where the value is the GUID of the routing destination or the target delivery group.

Exchange 2013 also adds the **NextHopCategory** property to the queue based on the value of **DeliveryType**. The value of **NextHopCategory** is `External` or `Internal`. The value `External` indicates the next hop of the queue is outside the Exchange organization. The value `Internal` indicates the next hop of the queue is inside the Exchange organization. Note that a message for an external recipient may require one or more internal hops before the message is delivered externally.

The values of **DeliveryType**, **NextHopCategory**, **NextHopDomain** and **NextHopConnector** are described in the following table.

|Delivery Type in Queue Viewer|DeliveryType in the Shell|Description|NextHopCategory|NextHopDomain|NextHopConnector|
|---|---|---|---|---|---|
|**Delivery Agent**|**DeliveryAgent**|The queue holds messages for delivery to recipients in a non-SMTP address space. The messages are delivered by using a Delivery Agent connector that's configured on the local server.|External|This value is the destination address space that's configured on the Delivery Agent connector.|This value is he GUID of the Delivery Agent connector. For example, `4520e633-d83d-411a-bbe4-6a84648674ee`.|
|**DnsConnectorDelivery**|**DnsConnectorDelivery**|The queue holds messages for delivery to recipients in an SMTP address space. The messages are delivered by using a Send connector that's configured on the local server. The Send connector is configured to use DNS routing.|External|This value is the destination address space that's configured on the Send connector. For example, `contoso.com`.|This value is the GUID of the Send connector. For example, `4520e633-d83d-411a-bbe4-6a84648674ee`.|
|**NonSmtpGatewayDelivery**|**NonSmtpGatewayDelivery**|The queue holds messages for delivery to recipients in a non-SMTP address space. The messages are delivered by using a Foreign connector that's configured on the local server.|External|This value is the destination address space that's configured on the Foreign connector.|This value is the GUID of the Foreign connector. For example, `4520e633-d83d-411a-bbe4-6a84648674ee`.|
|**SmartHostConnectorDelivery**|**SmartHostConnectorDelivery**|The queue holds messages for delivery to recipients in an SMTP address space. The messages are delivered by using a Send connector that's configured on the local server. The Send connector is configured to use smart host routing.|External|This value is the list of smart hosts that are configured on the Send connector. Smart hosts can be configured as FQDNs, IP addresses or both. The values can be one of the following: <ul><li>**FQDN**: The syntax is `<FQDN1,FQDN2,...>`. For example, `smarthost01.contoso.com` or `smarthost01.contoso.com,smarthost02.fabrikam.com`.</li><li>**IP address**: The syntax is `<[IPAddress1],[IPAddress2],...>`. For example, `[10.10.10.100]` or `[10.10.10.100],[10.10.10.101]`.</li><li>**FQDN and IP address**: The syntax is `<[IPAddress1],FQDN1,...>`, and depends on how the smart hosts are listed on the Send connector. For example, `[172.17.17.7],relay.tailspintoys.com` or `mail.contoso.com,[192.168.1.50]`.</li></ul>|This value is the GUID of the Send connector. For example, `4520e633-d83d-411a-bbe4-6a84648674ee`.|
|**SMTP Delivery to Mailbox**|**SmtpDeliveryToMailbox**|The queue holds messages for delivery to Exchange 2013 mailbox recipients. The destination mailbox database is in one of the following locations: <ul><li>The local Exchange 2013 Mailbox server.</li><li>An Exchange 2013 Mailbox server in the same DAG.</li><li>An Exchange 2013 Mailbox server in the same Active Directory site in non-DAG environments.</li></ul>|Internal|This value is the name of the destination mailbox database. For example, `Mailbox Database 0471695037`.|This value is the GUID of the target mailbox database. For example, `6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123`.|
|**SMTP Relay to Send Connector Source Servers**|**SmtpRelayToConnectorSourceServers**|The queue holds messages for delivery to SMTP or non-SMTP recipients. The messages are delivered by using a Send connector, Delivery Agent connector, or Foreign connector that's configured on a remote transport server. The remote transport server could be an Exchange 2013 Mailbox server, or an Exchange 2007 or Exchange 2010 Hub Transport server from a previous version of Exchange. The remote server could be located in the local Active Directory site, or in a remote Active Directory site.|Internal|This value is the name of the destination Send connector, Delivery Agent connector, or Foreign connector. For example, `Contoso.com Send Connector`.|This value is the GUID of the destination Send connector, Delivery Agent connector, or Foreign connector. For example, `4520e633-d83d-411a-bbe4-6a84648674ee`.|
|**SMTP Relay to Database Availability Group**|**SmtpRelayToDag**|The queue holds messages for delivery to Exchange 2013 mailbox recipients, where the destination mailbox database is located in a remote DAG. The remote DAG could be in the local Active Directory site, or a remote Active Directory site.|Internal|This value is the name of the destination DAG. For example, `DAG1`.|This value is the GUID of the destination DAG. For example, `6dcb5a1e-0a88-4fc9-b8f9-634c34b1a123`|
|**SMTP Relay to Mailbox Delivery Group**|**SmtpRelayToMailboxDeliveryGroup**|The queue holds messages for delivery to legacy mailbox recipients, where the destination mailbox is on an Exchange 2007 or Exchange 2010 Mailbox server. The message is related to a Hub Transport server that's running the same version of Exchange as the destination mailbox. The destination Hub Transport server could be in the local Active Directory site, or a remote Active Directory site.|Internal|The queue name uses the syntax: `Site:&lt;ADSiteName&gt;;Version:&lt;ExchangeVersion>`, where _\<ADSiteName\>_ is the name of the destination Active Directory site, and _\<ExchangeVersion\>_ is the version of Exchange on the Mailbox server.|This value is blank.|
|**SMTP Relay to Remote Active Directory Site**|**SmtpRelayToRemoteActiveDirectorySite**|The queue holds messages for delivery to a remote destination, and the routing topology requires the message to be routed through a specific Active Directory site. The site is an intermediate hop on the way to the final destination. This situation occurs under the following circumstances: <ul><li>The message needs to be routed through a hub site.</li><li>The message requires delivery through a Send connector that's configured on an Edge Transport server that's subscribed to a remote Active Directory site.</li></ul>|Internal|This value is the target Active Directory site name. For example, `NorthAmericanSite`.|This value is the GUID of the target Active Directory site. For example, `bfd6c3df-5b65-8bfb-53f1f2c0d55c`.|
|**SMTP Relay to Specified Exchange Servers**|**SmtpRelayToServers**|The queue holds messages for delivery to a distribution group that's configured for a specific expansion server. The expansion could be an Exchange 2013 Mailbox server, or an Exchange 2007 or Exchange 2010 Hub Transport server. The server could be in the local Active Directory site, or in a remote Active Directory site.|Internal|This value is the FQDN of the target expansion server. For example, `mailbox01.contoso.com`.|This value is `00000000-0000-0000-0000-000000000000`.|
|**SMTP Relay in Active Directory Site to Edge Transport Server**|**SmtpRelayWithinAdSiteToEdge**|The queue holds messages for delivery to an SMTP address space. The messages are delivered by using a Send connector that's configured on an Edge Transport server that's subscribed to the local Active Directory site.|Internal|This value is the name of the Send connector that sends outbound Internet mail from the organization to the Internet. This Send connector is automatically created by the Edge subscription, and is named `EdgeSync - &lt;ADSiteName&gt; to Internet`. _\<ADSiteName\>_ is the name of the local Active Directory site to which the Edge Transport server is subscribed.|This value is the GUID of the Send connector. For example, `4520e633-d83d-411a-bbe4-6a84648674ee`.|
|**Heartbeat**|**Heartbeat**|This value is reserved for internal Microsoft use. For more information about heartbeat, see [Shadow redundancy](shadow-redundancy-exchange-2013-help.md).|n/a|n/a|n/a|
|**Shadow Redundancy**|**ShadowRedundancy**|The queue holds messages in a shadow queue. A shadow queue holds redundant copies messages in transit in case the primary messages aren't successfully delivered. For more information, see [Shadow redundancy](shadow-redundancy-exchange-2013-help.md).|Internal|This value is the FQDN of the primary server for which the shadow queue is holding redundant copies of the primary messages. For example, `mailbox01.contoso.com`.|This value is `00000000-0000-0000-0000-000000000000`.|
|**Undefined**|**Undefined**|This value is used only on the Submission queue and the poison message queue.|Internal|For the Submission queue, this value is `Submission`. For the poison message queue, this value is `Poison Message`.|This value is `00000000-0000-0000-0000-000000000000`.|
|**Undreachable**|**Unreachable**|This value is used only on the Unreachable queue.|Internal|This value is `Unreachable Domain`.|This value is `00000000-0000-0000-0000-000000000000`.|

Note that Exchange 2013 supports legacy values of **DeliveryType** for backwards compatibility with previous versions of Exchange. These values are available in Queue Viewer and the Shell, but they aren't used by Exchange 2013. These legacy **DeliveryType** values are:

- **MapiDelivery**: The queue holds messages for delivery by an Exchange 2007 or Exchange 2010 Hub Transport server to a mailbox on an Exchange 2007 or Exchange 2010 Mailbox server in the local Active Directory site.
- **SmtpRelayWithinAdSite**: The queue holds messages for delivery by an Exchange 2007 or Exchange 2010 Hub Transport server to another Hub Transport server in the same Active Directory site. The destination Hub Transport server can be the source server for a connector, or a distribution group expansion server.
- **SmtpRelaytoTiRg**: The queue holds messages for delivery by an Exchange 2007 or Exchange 2010 Hub Transport server to an Exchange Server 2003 routing group. The destination server can be the source server for a connector, a distribution group expansion server, or an Exchange 2003 bridgehead server.

## IncomingRate, OutgoingRate, and Velocity

Exchange 2013 measures the rate of messages entering and leaving a queue and stores these values in queue properties. You can use these rates as an indicator of queue and transport server health. The properties are:

- **IncomingRate**: This property is the rate that messages are entering the queue.

  This value is calculated from the number of messages entering the queue every 5 seconds averaged over the last 60 seconds. The formula can be expressed as `(i1+i2+i3+i4+i5+i6)/6`, where i*n_ = the number of incoming messages in 5 seconds.

- **OutgoingRate**: This property is the rate that messages are leaving the queue.

  This value is calculated from the number of messages leaving the queue every 5 seconds averaged over the last 60 seconds. The formula can be expressed as `(o1+o2+o3+o4+o5+o6)/6`, where o*n_ = the number of outgoing messages in 5 seconds.

- **Velocity**: This property is the drain rate of the queue, and is calculated by subtracting the value of **IncomingRate** from the value of **OutgoingRate**.

  If the value of **Velocity** is greater than 0, messages are leaving the queue faster than they are entering the queue.

  If the value of **Velocity** is equals 0, messages are leaving the queue as fast as they are entering the queue. This is also the value you'll see when the queue is inactive.

  If the value of **Velocity** is less than 0, messages are entering the queue faster than they are leaving the queue.

At a basic level, a positive value of **Velocity** indicates a healthy queue that's efficiently draining, and a negative value of **Velocity** indicates a queue that isn't efficiently draining. However, you also need to consider the values of the **IncomingRate**, **OutgoingRate**, and **MessageCount** properties, as well as the magnitude of the **Velocity** value for the queue. For example, a queue that has a large negative value of **Velocity**, a large **MessageCount** value, a small **OutgoingRate** value, and a large **IncominRate** value are accurate indicators that the queue isn't draining properly. However, a queue with a negative **Velocity** value that's very close to zero that also has very small values for **IncomingRate**, **OutgoingRate**, and **MessageCount** doesn't indicate a problem with the queue.

## Queue status

The current status of a queue is stored in the **Status** property of the queue. A queue can have one of the following status values:

- **Active**: The queue is actively transmitting messages.
- **Connecting**: The queue is in the process of connecting to the next hop.
- **Ready**: The queue recently transmitted messages, but the queue is now empty.
- **Retry**: The last automatic or manual connection attempt failed, and the queue is waiting to retry the connection.
- **Suspended**: The queue has been manually suspended by an administrator to prevent message delivery. New messages can enter the queue, and messages that are in the act of being transmitted to the next hop will finish delivery and leave the queue. Otherwise, messages won't leave the queue until the queue is manually resumed by an administrator. Note that suspending a queue doesn't change the status of the individual messages in the queue.

  You can suspend a queue that has a status of Active or Retry. You can also suspend the Unreachable queue and the Submission queue.

  If you suspend the Unreachable queue, messages won't be automatically resubmitted to the categorizer when configuration updates are detected. To automatically resubmit these messages, you need to manually resume the Unreachable queue. If you suspend the Submission queue, messages won't be picked up by the categorizer until the queue is resumed.

## Other queue properties

There are other queue properties that are self-explanatory. You use most of the queue properties as filter options. By specifying filter criteria, you can quickly locate queues and take action on them. For a complete description of the filterable queue properties, see [Queue filters](queue-filters-exchange-2013-help.md).

An important queue property that's also worth mentioning here is the **MessageCount** property that shows how many messages are in a queue. This property is an important indicator of queue health. For example, a delivery queue that contains a large number of messages that continues to grow and never decreases could indicate a routing or transport pipeline issue that requires your attention.

## Message properties

A message in a queue has many properties. Many of the properties reflect the information that was used to create the message. Some of the messages status and information properties are heavily influenced by corresponding properties on the queue. However, an individual message may have a different value than the corresponding property of the queue. Other properties contains status, time, or other indicators that are updated frequently.

## Message status

The current status of a message is stored in the **Status** property of the message. A message can have one of the following status values:

- **Active**: If the message is in a delivery queue, the message is being delivered to its destination. If the message is in the Submission queue, the message is being processed by the categorizer.
- **Locked**: This value is reserved for internal Microsoft use, and isn't used in on-premises Exchange organizations.
- **PendingRemove**: The message was deleted by the administrator, but the message was already in the act of being transmitted to the next hop. The message will be deleted if the delivery ends in an error that causes the message to reenter the queue. Otherwise, delivery will continue.
- **PendingSuspend**: The message was suspended by the administrator, but the message was already in the act of being transmitted to the next hop.. The message will be suspended if the delivery ends in an error that causes the message to reenter the queue. Otherwise, delivery will continue.
- **Ready**: The message is waiting in the queue and is ready to be processed.
- **Retry**: The last automatic or manual connection attempt for the queue in which this message is located failed. The message is waiting for the next automatic queue connection retry.
- **Suspended**: The message was manually suspended by the administrator. All messages in the poison message queue are in a permanently suspended state.

## Other message properties

There are other message properties that are self-explanatory. You can use most of the message properties as filter options. By specifying filter criteria, you can quickly locate messages and take action on them. For a complete description of the filterable message properties, see [Message filters](message-filters-exchange-2013-help.md).

## Manage queues and messages in queues

Queue Viewer and virtually all of the queue and message management cmdlets are restricted to a single Exchange server. You can view or operate on individual queues or messages, or multiple queues or messages, but only on a specific server.

Exchange 2013 introduces the **Get-QueueDigest** cmdlet that provides a high-level, aggregate view of the state of queues on all servers within a specific scope, for example, a DAG, an Active Directory site, a list of servers, or the entire Active Directory forest. Note that queues on a subscribed Edge Transport server in the perimeter network aren't included in the results. Also, **Get-QueueDigest** is available on an Edge Transport server, but the results are restricted to queues on the Edge Transport server.

> [!NOTE]
> By default, the **Get-QueueDigest** cmdlet displays delivery queues that contain ten or more messages, and the results are between one and two minutes old. For instructions on how to change these default values, see [Configure Get-QueueDigest](configure-get-queuedigest-exchange-2013-help.md).

The following table describes the management tasks you can perform on queues or messages in queues.

|Task|Description|Tool to use|Instructions|
|---|---|---|---|
|View and filter queues on a server|This action displays one or more queues on a transport server. You can use the results to take action on the queues.|Queue Viewer or the **Get-Queue** cmdlet.|[Manage queues](manage-queues-exchange-2013-help.md)|
|View and filter queues on specific servers in specific DAGs, specific Active Directory sites, or in the whole Active Directory forest.|This action displays a summary view of queues across a defined scope (servers, DAGs, Active Directory sites, or the entire Active Directory forest).|**Get-QueueDigest** cmdlet only|[Manage queues](manage-queues-exchange-2013-help.md)|
|Suspend queues|This action temporarily prevents delivery of messages that are currently in the queue. The queue continues to accept new messages, but no messages leave the queue.|Queue Viewer or the **Suspend-Queue** cmdlet.|[Manage queues](manage-queues-exchange-2013-help.md)|
|Resume queues|This action reverses the effect of the suspend queue action and enables delivery of queued messages to resume.|Queue Viewer or the **Resume-Queue** cmdlet.|[Manage queues](manage-queues-exchange-2013-help.md)|
|Retry queues|This action immediately tries to connect to the next hop. Without manual intervention, when the connection to the next hop fails, the connection is attempted a specific number of times after a specific time interval between each attempt. <br/><br/> Whether the connection attempt is manual or automatic, any connection attempt resets the next retry time. For more information, see [Message retry, resubmit, and expiration intervals](message-retry-resubmit-and-expiration-intervals-exchange-2013-help.md).|Queue Viewer or the **Retry-Queue** cmdlet.|[Manage queues](manage-queues-exchange-2013-help.md)|
|Resubmit messages in queues|This action causes the messages in the queue to be resubmitted to the Submission queue and to go back through the categorization process.|**Retry-Queue** with the _Resubmit_ parameter <br/><br/> Note that you can use Queue Viewer to resubmit messages, but only from the poison message queue. To resubmit a message in poison message, you resume the message in Queue Viewer, or by using the **Resume-Message** cmdlet.|[Manage queues](manage-queues-exchange-2013-help.md)|
|Suspend messages in queues|This action temporarily prevents delivery of a message. You can use the suspend message action to prevent delivery of a message to all the recipients in a specific queue or to all recipients in all queues.|Queue Viewer or the **Suspend-Message** cmdlet.|[Manage messages in queues](manage-messages-in-queues-exchange-2013-help.md)|
|Resume messages in queues|This action reverses the effect of the suspend message action and enables delivery of queued messages to resume. You can use the resume message action to resume delivery of a message to all the recipients in a specific queue or to all recipients in all queues.|Queue Viewer or the **Resume-Message** cmdlet.|[Manage messages in queues](manage-messages-in-queues-exchange-2013-help.md)|
|Remove messages from queues|This action permanently prevents delivery of a message. You can use the remove message action to prevent delivery of a message to any recipients in a specified queue or to all recipients in all queues. You can also configure the remove message action to send a non-delivery report (NDR) to the sender when the message is removed.|Queue Viewer or the **Remove-Message** cmdlet.|[Manage messages in queues](manage-messages-in-queues-exchange-2013-help.md)|
|Export messages from queues|This action copies a message to the file path that you specify. The messages aren't deleted from the queue, but a copy of the message is saved to a file location. This enables administrators or officials in an organization to later examine the messages. Before you export a message, you need to suspend the message in the queue so that typical delivery doesn't continue during the export process.|**Export-Message** cmdlet only.|[Export messages from queues](export-messages-from-queues-exchange-2013-help.md)|
