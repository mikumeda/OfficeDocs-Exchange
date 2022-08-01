---
ms.topic: article
description: This article describes the queues new to Mailbox and Edge Transport servers in Microsoft Exchange Server 2013.
title: 'Use the Exchange Management Shell to manage queues: Exchange 2013 Help'
TOCTitle: Use the Exchange Management Shell to manage queues
ms:assetid: 5433c1d3-ad2e-4f82-b50d-b67964b32f26
ms:mtpsurl: https://technet.microsoft.com/library/Aa998047(v=EXCHG.150)
ms:contentKeyID: 50646233
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Use the Exchange Management Shell to manage queues

_**Applies to:** Exchange Server 2013_

As in previous versions of Exchange, you can use the Exchange Management Shell in Microsoft Exchange Server 2013 to view information about queues and the messages in those queues, and to perform management actions on queues and messages. In Exchange 2013, queues exist on Mailbox servers and Edge Transport servers. This topic refers to these servers as _transport servers_.

When you use the Shell to view and manage queues and messages in queues on transport servers, it's important to understand how to identify the queues or messages you want to manage. Typically, transport servers contain a large number of queues and messages to be delivered. You use the filtering parameters that are available on the queue and message management cmdlets to identify the queues or messages that you want to view or manage.

Note that you can also use Queue Viewer in the Exchange Toolbox to manage queues and messages in queues. However, the queue and message viewing cmdlets support more filterable properties and filter options than Queue Viewer. For more information about using Queue Viewer, see [Queue Viewer](queue-viewer-exchange-2013-help.md).

## Queue filtering parameters

The following table describes the filtering parameters that are available on the queue management cmdlets.

|Cmdlet|Filtering parameters|Comments|
|---|---|---|
|**Get-Queue**|_Identity_ <br/><br/> _Filter_ <br/><br/> _Include_ <br/><br/> _Exclude_|You can't use the _Identity_ parameter in the same command with the _Filter_ parameters. You can use the _Include_ and _Exclude_ parameters with the _Filter_ parameter in the same command.|
|**Resume-Queue** <br/><br/> **Retry-Queue** <br/><br/> **Suspend-Queue**|_Identity_ <br/><br/> _Filter_|You need to use either the _Identity_ parameter or the _Filter_ parameter, but you can't use both in the same command.|
|**Get-QueueDigest**|_Server_ <br/><br/> _Dag_ <br/><br/> _Site_ <br/><br/> _Forest_ <br/><br/> _Filter_|You need to use the _Server_, _Dag_, _Site_, or _Forest_ parameter, but you can't use any of them together in the same command. You can use the _Filter_ parameter with any of the other filtering parameters.|

Note that a _Server_ parameter is available on all queue management cmdlets. On the **Get-QueueDigest** cmdlet, the _Server_ parameter is a scope parameter that specifies the server or servers where you want to view summary information about queues. On all other queue management cmdlets, you use the _Server_ parameter to connect to a specific server, and run the queue management commands on that server. You can use the _Server_ parameter with or without the _Filter_ parameter, but you can't use the _Server_ parameter with the _Identity_ parameter. You use the transport server's hostname or FQDN with the _Server_ parameter.

## Queue identity

The _Identity_ parameter on the queue management cmdlets identifies a specific queue. When you use the _Identity_ parameter, you can't specify any other queue filtering parameters, because you've already uniquely identified the queue. The _Identity_ parameter uses the basic syntax _\<Server\>_\\_\<Queue\>_.

The _\<Server\>_ placeholder is the hostname or FQDN of the Exchange server, for example `mailbox01` or `mailbox01.contoso.com`. If you omit the _\<Server\>_ qualifier, the local server is implied.

The \<_Queue_\> placeholder accepts one of the following values:

- **Persistent queue name**: Persistent queues have unique, consistent names on all Mailbox or Edge Transport servers. The persistent queue names are:

  - **Submission**: This queue contains messages waiting to be processed by the categorizer.
  - **Unreachable**: This queue contains messages that can't be routed. This queue doesn't exist until messages are placed in it.
  - **Poison**: This queue contains messages that are determined to be harmful to the Exchange server. This queue doesn't exist until messages are placed in it.

- **Delivery queue name**: The name of a delivery queue is the value of the **NextHopDomain** property of the queue. For example, the queue name could be the address space of a Send connector, the name of an Active Directory site, or the name of a DAG. For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.

- **Queue integer**: Delivery queues and shadow queues are assigned a unique integer value in the queue database. However, you need to run the **Get-Queue** cmdlet to find the integer value for the queue in the **Identity** or **QueueIdentity** properties.

- **Shadow queue name**: A shadow queue uses the syntax `Shadow\`_\<QueueInteger\>_

The following table summarizes the syntax you can use with _Identity_ parameter on the queue management cmdlets. In all values, _\<Server\>_ is the hostname or FQDN of the server.

### Queue identity formats

|Identity parameter value|Description|
|---|---|
|`<Server>\<PersistentQueueName>` or `<PersistentQueueName>`|A persistent queue on the specified server or the local server. <br/><br/> _\<PersistentQueueName\>_ is `Submission`, `Unreachable`, or `Poison`.|
|`<Server>\<NextHopDomain>` or `<NextHopDomain>`|A delivery queue on the specified server or the local server. <br/><br/> _\<NextHopDomain\>_ is a routing destination or delivery group for the messages in the queue. For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|
|`<Server>\<QueueInteger>` or `<QueueInteger>`|A delivery queue on the specified server or the local server. <br/><br/> _\<QueueInteger\>_ is the unique integer value of the queue that's displayed in the **Identity** property of the **Get-Queue** cmdlet.|
|`<Server>\Shadow\<QueueInteger>` or `Shadow\<QueueInteger>`|A shadow queue on the specified server or the local server.|
|`<Server>\*` or `*`|All queues on the specified server or the local server. Note that these values can only be used with the **Get-Queue** cmdlet.|

## Queue Filter parameter

You can use the _Filter_ parameter on the all of the queue management cmdlets to specify the queues you want to view or manage based on the properties of the queues. The _Filter_ parameter creates an expression with comparison operators that restricts the queue operation to queues that meet the filter criteria. You can use the `-and` logical operator to specify multiple conditions that the results must match.

For a complete list of queue properties you can use with the _Filter_ parameter, see [Queues](queues-exchange-2013-help.md).

For a list of comparison operators you can use with the _Filter_ parameter, see the Comparison operators to use when filtering queues or messages section in this topic.

For examples of procedures that use the _Filter_ parameter to view and manage queues, see [Manage queues](manage-queues-exchange-2013-help.md).

## Include and Exclude parameters

Exchange 2013 has the _Include_ and _Exclude_ parameters available on the `Get-Queue` cmdlet. You can use these parameters individually, together, and with the _Filter_ parameter to fine-tune your queue results on the local or specified transport server. For example, you can:

- Exclude empty queues from the results.
- Exclude queues to external destinations from the results.
- Include queues that have a specific value of **DeliveryType** in the results.

The _Include_ and _Exclude_ parameters use the following queue properties to filter queues:

|Value|Description|Shell code example|
|---|---|---|
|`DeliveryType`|This value includes or excludes queues based on the **DeliveryType** property. You can specify multiple values separated by commas. The valid values for **DeliveryType** are explained in the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|This example returns all delivery queues on the local server where the next hop is a Send connector on the local server that's configured for smart host routing: <br/><br/> `Get-Queue -Include SmartHostConnectorDelivery`|
|`Empty`|This value includes or excludes empty queues. Empty queues have the value `0` in the **MessageCount** property.|This example returns all queues on the local server that contain messages <br/><br/> `Get-Queue -Exclude Empty`|
|`External`|This value includes or excludes queues that have the value `External` in the **NextHopCategory** property. <br/><br/> External queues always have one of the following values for **DeliveryType**: <ul><li>`DeliveryAgent`</li><li>`DnsConnectorDelivery`</li><li>`NonSmtpGatewayDelivery`</li><li>`SmartHostConnectorDelivery`</li></ul><p>For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|This example returns all internal queues on the local server <br/><br/> `Get-Queue -Exclude External`|
|`Internal`|This value includes or excludes queues that have the value `Internal` in the **NextHopCategory** property. For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.|This example returns all internal queues on the local server. <br/><br/> `Get-Queue -Include Internal`|

Note that you can duplicate the functionality of the _Include_ and _Exclude_ parameters by using the _Filter_ parameter. For example, the command `Get-Queue -Exclude Empty` yields the same result as `Get-Queue -Filter "MessageCount -gt 0"`. However, the syntax of the _Include_ and _Exclude_ parameters is simpler and easier to remember.

## Get-QueueDigest

Exchange 2013 adds a new queue cmdlet named **Get-QueueDigest**. This cmdlet allows you to view information about some or all of the queues in your Exchange organization by using a single command. Specifically, the **Get-QueueDigest** cmdlet allows you to view information about queues based on their location on servers, in DAGs, in Active Directory sites, or in the whole Active Directory forest. Note that queues on a subscribed Edge Transport server in the perimeter network aren't included in the results. Also, **Get-QueueDigest** is available on an Edge Transport server, but the results are restricted to queues on the Edge Transport server.

> [!NOTE]
> By default, the **Get-QueueDigest** cmdlet displays delivery queues that contain ten or more messages, and the results are between one and two minutes old. For instructions on how to change these default values, see [Configure Get-QueueDigest](configure-get-queuedigest-exchange-2013-help.md).

The filtering and sorting parameters that are available with the **Get-QueueDigest** cmdlet are described in the following table.

|Parameter|Description|
|---|---|
|_Dag_, _Server_, or _Site_|These parameters are mutually exclusive, and set the scope for the cmdlet. You need to specify one of these parameters or the _Forest_ switch. Typically, you would use the name of the server, DAG or Active Directory site, but you can use any value that uniquely identifies the server, DAG, or site. You can specify multiple servers, DAGs, or sites separated by commas.|
|_Forest_|This switch is required if you aren't using the _Dag_, _Server_, or _Site_ parameters. You don't specify a value with this switch. By using this switch, you get queues from all Exchange 2013 Mailbox servers in the Active Directory forest. You can't use the _Forest_ switch to view queues in remote Active Directory forests.|
|_DetailsLevel_|This parameter accepts the values `None`, `Normal`, and `Verbose`. The default value is `Normal`. When you use the value `None`, the queue name is omitted from the **Details** column in the results.|
|_Filter_|This parameter allows you to filter queues based on the queue properties. You can use any of the filterable queue properties as described in the [Queue filters](queue-filters-exchange-2013-help.md) topic.|
|_GroupBy_|This parameter groups the queue results. You can group the results by one of the following properties: <ul><li>DeliveryType</li><li>LastError</li><li>NextHopCategory</li><li>NextHopDomain</li><li>NextHopKey</li><li>Status</li><li>ServerName</li></ul><p>By default, the results are grouped by `NextHopDomain`. For information about these queue properties, see [Queue filters](queue-filters-exchange-2013-help.md).|
|_ResultSize_|This parameter limits the queue results to the value you specify. The queues are sorted in descending order based on the number of messages in the queue, and grouped by the value specified by the _GroupBy_ parameter. The default value is 1000. This means that by default, the command displays the top 1000 queues grouped by **NextHopDomain**, and sorted by the queues containing the most messages to the queues containing the least messages.|
|_Timeout_|The parameter specifies the number of seconds before the operation times out. The default value is `00:00:10` or 10 seconds.|

This example returns all non-empty external queues on the Exchange 2013 Mailbox servers named Mailbox01,Mailbox02, and Mailbox03.

```powershell
Get-QueueDigest -Server Mailbox01,Mailbox02,Mailbox03 -Include External -Exclude Empty
```

## Message filtering parameters

The following table describes the filtering parameters that are available on the message management cmdlets.

|Cmdlet|Filtering parameters|Comments|
|---|---|---|
|**Get-Message**|_Identity_ <br/><br/> _Filter_ <br/><br/> _Queue_|All filtering parameters are mutually exclusive, and you can use them together in the same command.|
|**Remove-Message** <br/><br/> **Resume-Message** <br/><br/> **Suspend-Message**|_Identity_ <br/><br/> _Filter_|You need to use either the _Identity_ parameter or the _Filter_ parameter, but you can't use both in the same command.|
|**Export-Message**|_Identity_|The _Identity_ parameter is required.|

Note that a _Server_ parameter is available on all message management cmdlets except for the **Export-Message** cmdlet. You use the _Server_ parameter to connect to a specific server, and run the message management commands on that server. You can use the _Server_ parameter with or without the _Filter_ parameter, but you can't use the _Server_ parameter with the _Identity_ parameter. You use the transport server's hostname or FQDN with the _Server_ parameter.

## Message identity

The _Identity_ parameter on the message management cmdlets identifies a specific message in one or more queues. When you use the _Identity_ parameter, you can't specify any other message filtering parameters, because you've already uniquely identified the message. The _Identity_ parameter uses the basic syntax _\<Server\>_\\_\<Queue\>_\\_\<MessageInteger\>_.

The _\<Server\>_ placeholder is the hostname or FQDN of the Exchange server, for example `mailbox01` or `mailbox01.contoso.com`. If you omit the _\<Server\>_ qualifier, the local server is implied.

The \<_Queue_\> placeholder accepts the identity of the queue as described in the "Queue identity" section in this topic. For example, you can use the persistent queue name, the **NextHopDomain** value, or the unique integer value of the queue in the queue database.

The _\<MessageInteger\>_ placeholder represents the unique integer value that's assigned to the message when it first enters the queue database on the server. If the message is sent to multiple recipients that require multiple queues, all copies of the message in all queues in the queue database have the same integer value. However, you need to run the **Get-Message** cmdlet to find the integer value for the message in the **Identity** or **MessageIdentity** properties.

The following table summarizes the syntax you can use with _Identity_ parameter on the message management cmdlets. In all values, _\<Server\>_ is the hostname or FQDN of the server.

### Message identity formats

|Identity parameter value|Description|
|---|---|
|`<Server>\<Queue>\<MessageInteger>` or `<Queue>\<MessageInteger>`|A message in a specific queue on the specified server or the local server. <br/><br/> _\<MessageInteger\>_ is the unique integer value of the message that's displayed in the **Identity** property of the **Get-Message** cmdlet. <br/><br/> _\<Queue\>_ represents one of the following values: <ul><li>**Persistent queue name**   The value `Submission`, `Unreachable`, or `Poison`.</li><li>**Delivery queue name**   The value of the **NextHopDomain** property of the queue, which is effectively the name of the queue. This value could be a routing destination or a delivery group. For more information, see the "NextHopSolutionKey" section in the [Queues](queues-exchange-2013-help.md) topic.</li><li>**Queue integer**   The unique integer value of the delivery queue or shadow queue that's displayed in the **Identity** property of the **Get-Message** or **Get-Queue** cmdlets.</li><li>**Shadow queue identity**   The shadow queue identity uses the syntax `Shadow\<QueueInteger>`.</li></ul>|
|`<Server>\*\<MessageInteger>` or `*\<MessageInteger>` or `<MessageInteger>`|All copies of the message in all queues in the queue database on the specified server or the local server.|

## Message Filter parameter

You can use the _Filter_ parameter on the **Get-Message**, **Remove-Message**, **Resume-Message**, and **Suspend-Message** cmdlets to specify the messages you want to view or manage based on the properties of the messages. The _Filter_ parameter creates an expression with comparison operators that restricts the message operation to messages that meet the filter criteria. You can use the `-and` logical operator to specify multiple conditions that the results must match.

For a complete list of message properties you can use with the _Filter_ parameter, see [Queues](queues-exchange-2013-help.md).

For a list of comparison operators you can use with the _Filter_ parameter, see the Comparison operators to use when filtering queues or messages section in this topic.

For examples of procedures that use the _Filter_ parameter to view and manage messages, see [Manage queues](manage-queues-exchange-2013-help.md).

## Queue parameter

The _Queue_ parameter is used only with the **Get-Message** cmdlet. You can use this parameter to get all messages in a specific queue, or all messages from multiple queues by using the wildcard character (\*).When you use the _Queue_ parameter, use the queue identity format _\<Server\>_\\_\<Queue\>_ as described in the "Queue identity" section in this topic.

## Comparison operators to use when filtering queues or messages

When you create a queue or message filter expression by using the _Filter_ parameter, you need to include an comparison operator for the property value to match. The following table shows the comparison operators that you can use in a filter expression and how each operator functions. For all operators, the values compared aren't case sensitive.

### Comparison operators

|Operator|Function|Shell code example|
|---|---|---|
|`-eq`|This operator is used to specify that the results must exactly match the property value that's supplied in the expression.|To display a list of all queues that have a status of Retry: <br/><br/> `Get-Queue -Filter "Status -eq 'Retry'"` <br/><br/> To display a list of all messages that have a status of Retry: <br/><br/> `Get-Message -Filter "Status -eq 'Retry'"`|
|`-ne`|This operator is used to specify that the results shouldn't match the property value that's supplied in the expression.|To display a list of all queues that don't have a status of Active: <br/><br/> `Get-Queue -Filter "Status -ne 'Active'"` <br/><br/> To display a list of all messages that don't have a status of Active: <br/><br/> `Get-Message -Filter "Status -ne 'Active'"`|
|`-gt`|This operator is used with properties where the value is expressed as an integer or date/time. The filter results only include queues or messages where the value of the specified property is greater than the value that's supplied in the expression.|To display a list of queues that currently contain more than 1,000 messages: <br/><br/> `Get-Queue -Filter "MessageCount -gt 1000"` <br/><br/> To display a list of messages that currently have a retry count that's more than 3: <br/><br/> `Get-Message -Filter "RetryCount -gt 3"`|
|`-ge`|This operator is used with properties where the value is expressed as an integer or date/time. The filter results only include queues or messages where the value of the specified property is greater than or equal to the value that's supplied in the expression.|To display a list of queues that currently contain 1,000 or more messages: <br/><br/> `Get-Queue -Filter "MessageCount -ge 1000"` <br/><br/> To display a list of messages that currently have a retry count that's 3 or more: <br/><br/> `Get-Message -Filter "RetryCount -ge 3"`|
|`-lt`|This operator is used with properties where the value is expressed as an integer or date/time. The filter results only include queues or messages where the value of the specified property is less than the value that's supplied in the expression.|To display a list of queues that currently contain less than 1,000 messages: <br/><br/> `Get-Queue -Filter "MessageCount -lt 1000"` <br/><br/> To display a list of messages that have an SCL that's less than 6: <br/><br/> `Get-Message -Filter "SCL -lt 6"`|
|`-le`|This operator is used with properties where the value is expressed as an integer or date/time. The filter results only include queues or messages where the value of the specified property is less than or equal to the value supplied in the expression.|To display a list of queues that currently contain 1,000 or fewer messages: <br/><br/> `Get-Queue -Filter "MessageCount -le 1000"` <br/><br/> To display a list of messages that have an SCL that's 6 or less: <br/><br/> `Get-Message -Filter "SCL -le 6"`|
|`-like`|This operator is used with properties where the value is expressed as a text string. The filter results only include queues or messages where the value of the specified property contains the text string that's supplied in the expression. You can include the wildcard character (*) in a **-like** expression that's applied to a text string field, but not with a field that has the enumeration type.|To display a list of delivery queues that have a destination to any SMTP domain that ends in Contoso.com: <br/><br/> `Get-Queue -Filter "Identity -like '*contoso.com'"` <br/><br/> To display a list of messages that have a subject that contains the text "payday loan": <br/><br/> `Get-Messages -Filter "Subject -like '*payday loan*'"`|

You can specify a filter that evaluates multiple expressions by using the **-and** comparison operator. The queues or messages must meet all conditions of the filter to be included in the results.

This example displays a list of queues that have a destination to any SMTP domain name that ends in Contoso.com and that currently contain more than 500 messages.

```powershell
Get-Queue -Filter "Identity -like '*contoso.com*' -and MessageCount -gt 500"
```

This example displays a list of messages that are sent from any email address in the contoso.com domain that have an SCL that's greater than 5.

```powershell
Get-Message -Filter "FromAddress -like '*Contoso.com*' -and SCL -gt 5"
```

## Advanced paging parameters

Depending on current mail flow, queries against queues and messages can return a large set of objects. You can use the advanced paging parameters to control how query results are retrieved and displayed.

When you use the Shell to view queues and the messages in the queues, your query retrieves one page of information at a time. The advanced paging parameters control the size of the result set and can also be used to sort the results. All advanced paging parameters are optional and can be combined with any one of the parameter sets that can be used with the **Get-Queue** and **Get-Message** cmdlets. If you don't specify any advanced paging parameters, the query returns the results in ascending order of identity.

By default, when a sort order is specified, the message identity property is always included and is sorted in an ascending order. This is the default ordering relationship. The message identity property is included because the other properties that can be included in a sort order aren't unique. By explicitly including the message identity property in the sort order, you can specify that the results display the message identity sorted in descending order.

You can use the _BookmarkIndex_ and _BookmarkObject_ parameters to mark a position in the sorted result set. If the bookmark object no longer exists when the next page of results is retrieved, the default ordering relationship makes sure that the result set starts with the closest object to the bookmark. The closest object depends on the specified sort order.

The following table describes the advanced paging parameters.

|Parameter|Description|
|---|---|
|_BookmarkIndex_|This parameter specifies the position in the result set where the displayed results start. The value of this parameter is a 1-based index in the total result set. If the value is less than or equal to zero, the first complete page of results is returned. If the value is set to `Int.MaxValue`, the last complete page of results is returned.|
|_BookmarkObject_|This parameter specifies the object in the result set where the displayed results start. If you specify a bookmark object, that object is used as the point to start the search. The rows before or after that object, depending on the value of the _SearchForward_ parameter, are retrieved. You can't combine the _BookmarkObject_ parameter and the _BookmarkIndex_ parameter in a single query.|
|_IncludeBookmark_|This parameter specifies whether to include the bookmark object in the result set. By default, the value is set to `$true` and the bookmark object is included. You may run a query for a limited result size, and then specify the last item in that result set as the bookmark for the next query. In this case, you may want to set _IncludeBookmark_ to `$false` so that the object isn't included in both result sets.|
|_ResultSize_|This parameter specifies the number of results to display per page. If you don't specify a value, the default result size of 1,000 objects is used. Exchange limits the result set to 250,000.|
|_ReturnPageInfo_|This parameter is a hidden parameter. It returns information about the total number of results and the index of the first object of the current page. The default value is `$false`.|
|_SearchForward_|This parameter specifies whether to search forward or backward in the result set. This parameter doesn't affect the order in which the result set is returned. It determines the direction of search relative to the bookmark index or object. If no bookmark index or object is specified, the _SearchForward_ parameter determines whether the search starts from the first or last object in the result set. <br/><br/> The default value for this parameter is `$true`. If the this parameter is set to `$true` and a bookmark is specified, the query searches forward from that bookmark. If you use this configuration and there are no results beyond the bookmark, the query returns the last full page of results. <br/><br/> If the _SearchForward_ parameter is set to `$false` and a bookmark is specified, the query searches backward from that bookmark. If you use this configuration and there is less than a full page of results beyond the bookmark, the query returns the first full page of results.|
|_SortOrder_|This parameter specifies an array of message properties used to control the sort order of the result set. The sort order properties are specified in descending order of precedence. Each property is separated by a comma and appended with a plus sign (+) to sort in ascending order, or a minus sign (-) to sort in descending order. <br/><br/> If an explicit sort order isn't specified by using this parameter, the records that match the query are displayed and sorted by the Identity field for the respective object type. The results are always sorted by identity in ascending order when a sort order isn't explicitly specified.|

The following code example shows how to use the advanced paging parameters in a query. In this example, the command connects to the specified server and retrieves a result set that contains 500 objects. The results are displayed in a sorted order, first in ascending order by sender address, and then in descending order of message size.

```powershell
Get-Message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size
```

If you want to view successive pages, you can set a bookmark for the last object retrieved in a result set and run an additional query. You need to use the scripting capabilities of the Shell to perform this procedure.

The following example uses scripting to retrieve the first page of results, sets the bookmark object, excludes the bookmark object from the result set, and then retrieves the next 500 objects on the specified server.

1. Open the Shell and type the following command to retrieve the first page of results.

    ```powershell
    $Results=Get-message -Server mailbox01.contoso.com -ResultSize 500 -SortOrder +FromAddress,-Size
    ```

2. To set the bookmark object, type the following command to save the last element of the first page to a variable.

    ```powershell
    $temp=$results[$results.length-1]
    ```

3. To retrieve the next 500 objects on the specified server and to exclude the bookmark object, type the following command.

    ```powershell
    Get-message -Server mailbox01.contoso.com -BookmarkObject:$temp -IncludeBookmark $False -ResultSize 500 -SortOrder +FromAddress,-Size
    ```
