---
title: 'Anti-spam agent logging: Exchange 2013 Help'
TOCTitle: Anti-spam agent logging
ms:assetid: dbd478d2-7993-4931-80db-5b2f7d4269bd
ms:mtpsurl: https://technet.microsoft.com/library/Bb124795(v=EXCHG.150)
ms:contentKeyID: 49287005
ms.topic: article
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about agent logging in Exchange 2013.
---

# Anti-spam agent logging

_**Applies to:** Exchange Server 2013_

Agent logs record the actions performed on a message by specific anti-spam agents in Microsoft Exchange Server 2013. Only the following agents can write information to the agent log:

- Connection Filtering agent

- Content Filter agent

- Edge Rules agent

- Recipient Filter agent

- Sender Filter agent

- Sender ID agent

> [!NOTE]
> The Connection Filtering agent and the Edge Rules agent aren't available on Mailbox servers.

The information written to the agent log depends on the agent, the SMTP event, and the action performed on the message.

You use the **Set-TransportService** cmdlet in the Exchange Management Shell to perform all agent log configuration tasks. The following options are available for the agent logs:

- Enable or disable agent logging. The default is enabled.

- Specify the location of the agent log files. The default value is %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

- Specify a maximum size for the individual agent log files. The default size is 10 megabytes (MB).

- Specify a maximum size for the directory that contains agent log files. The default size is 250 MB.

- Specify a maximum age for the agent log files. The default age is 7 days.

Exchange uses circular logging to limit the agent logs based on file size and file age to help control the hard disk space used by the log files.

## Overview of transport agents

Agents can only act upon messages at specific points in the SMTP command sequence used to transport the messages through the Transport service on a Mailbox server or an Edge Transport server. These access points in the SMTP command sequence are called _SMTP events_. Each agent has a priority value that can be assigned. However, the SMTP events must always occur in a specific order. Therefore, the agent priority depends on the SMTP event. If two agents can act on a message during the same SMTP event, the agent that has the highest priority will act on the message first.

The following table lists the SMTP events in order of occurrence and the agents that write information to the agent log in order of priority from highest to lowest for each SMTP event.

### SMTP events in order of occurrence and the agents that write information to the agent log in order of priority for each SMTP event

|SMTP event|Agent|
|---|---|
|**OnConnect**|Connection Filtering agent|
|**OnMailCommand**|Connection Filtering agent <br/><br/> Sender Filter agent|
|**OnRcptCommand**|Connection Filtering agent <br/><br/> Recipient Filter agent|
|**OnEndOfHeaders**|Connection Filtering agent <br/><br/> Sender ID agent <br/><br/> Sender Filter agent|
|**OnEndOfData**|Edge Rules agent <br/><br/> Content Filtering agent|

> [!NOTE]
> The Connection Filtering agent and the Edge Rules agent aren't available on Mailbox servers.

For more information about agents, SMTP events, and agent priority, see [Transport agents](transport-agents-exchange-2013-help.md).

## Structure of the agent log files

The agent logs exist in %ExchangeInstallPath%TransportRoles\\Logs\\Hub\\AgentLog.

The naming convention for the agent log files is AGENTLOG_yyyymmdd-nnnn_.log. The placeholders represent the following information:

- The placeholder _yyyymmdd_ is the Coordinated Universal Time (UTC) date that the log file was created. The placeholder _yyyy_ = year, _mm_ = month, and _dd_ = day.

- The placeholder _nnnn_ is an instance number that starts at the value of 1 for each day.

Information is written to the log file until the file size reaches its maximum specified value, and a new log file that has an incremented instance number is opened. This process is repeated throughout the day. Circular logging deletes the oldest log files when the agent log directory reaches its maximum specified size, or when a log file reaches its maximum specified age.

The agent log files are text files that contain data in the comma-separated value file (CSV) format. Each agent log file has a header that contains the following information:

- **\#Software**: Name of the software that created the agent log file. Typically, the value is Microsoft Exchange Server.

- **\#Version**: Version number of the software that created the agent log file. Currently, the value is 15.0.0.0.

- **\#Log-Type**: Log type value, which is Agent Log.

- **\#Date**: UTC date-time when the log file was created. The UTC date-time is represented in the ISO 8601 date-time format: _yyyy-mm-dd_T_hh:mm:ss.fff_Z, where _yyyy_ = year, _mm_ = month, _dd_ = day, T indicates the beginning of the time component, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.

- **\#Fields**: Comma delimited field names used in the agent log files.

## Information written to the agent log

The agent log stores each agent transaction on a single line in the log. The information stored on each line is organized by fields. These fields are separated by commas. The field name is generally descriptive enough to determine the type of information it contains. However, some of the fields may be blank. Or the type of information stored in the field may change based on the agent or the action performed on the message by the agent. The following table describes the fields used to classify each agent transaction.

### Fields used to classify each agent transaction

|Field name|Description|
|---|---|
|**Timestamp**|UTC date-time of the agent event. The UTC date-time is represented in the ISO 8601 date-time format: _yyyy-mm-dd_T_hh:mm:ss.fff_Z, where _yyyy_ = year, _mm_ = month, _dd_ = day, T indicates the beginning of the time component, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and Z signifies Zulu, which is another way to denote UTC.|
|**SessionId**|Unique SMTP session identifier. This identifier is represented as a 16-digit hexadecimal number.|
|**LocalEndpoint**|Local IP address and port number that accepted the message. SMTP sessions typically use port 25.|
|**RemoteEndpoint**|IP address and port number of the previous SMTP server that connected to this server to deliver the message. When Internet mail flows through an Edge Transport server in the perimeter network, the value of **RemoteEndpoint** in the agent log on the Mailbox server will be the IP address of the Edge Transport server. Even though the message is transmitted by SMTP, the port number used by the sending server will be a random number larger than 1,024.|
|**EnteredOrgFromIP**|IP address of the remote SMTP server that first connected to the Exchange organization to deliver the message. On an Edge Transport server, the value of **RemoteEndpoint** and **EnteredOrgFromIP** are the same. Anti-spam agents use the IP address in **EnteredOrgFromIP** to examine a message.|
|**MessageId**|Value of the `MessageID` header field. If this value is blank, the Exchange transport server assigns an arbitrary value, but only if the message is accepted. After a value is assigned, the value of `MessageID` is constant for the lifetime of the message.|
|**P1FromAddress**|Sender email address specified in `MAIL FROM` in the message envelope. This value is used to transport the message between SMTP messaging servers. This value serves as a comparison to the value of **P2FromAddresses** to determine whether the sender address in the message header is forged.|
|**P2FromAddresses**|Sender email address specified in the `From` header field or in the `Sender` header field in the message header.|
|**Recipient**|Email address of the recipients. Although the original message may contain multiple recipients, only one recipient is displayed per line in the agent log.|
|**NumRecipients**|Total number of recipients in the original message.|
|**Agent**|Name of the agent that took the action. The possible values are as follows: <ul><li>Content Filter agent</li><li>Recipient Filter agent</li><li>Sender Filter agent</li><li>Sender ID agent</li></ul>|
|**Event**|SMTP event where the action was taken by the agent. The value of **Event** depends on the agent. The SMTP events available to each agent are described in the first table earlier in this topic. The possible values for **Event** are as follows: <ul><li>OnConnect</li><li>OnEndOfHeaders</li><li>OnEndOfData</li><li>OnMailCommand</li><li>OnRcptCommand</li></ul>|
|**Action**|Action performed on the message by the agent. The possible values for **Action** are as follows: <ul><li>AcceptMessage</li><li>DeleteMessage</li><li>DeleteRecipients</li><li>Disconnect</li><li>QuarantineMessage</li><li>QuarantineRecipients</li><li>RejectAuthentication</li><li>RejectCommand</li><li>RejectConnection</li><li>RejectMessage</li><li>RejectRecipients</li></ul>|
|**SmtpResponse**|Enhanced SMTP response as defined in RFC 2034.|
|**Reason**|Reason for the action supplied by the agent.|
|**ReasonData**|Descriptive details for the action supplied by the agent.|

## Search the agent logs

You can use the **Get-AgentLog** cmdlet and the **Get-AntiSpamFilteringReport.ps1** script to search the agent logs.

The **Get-AntiSpamFilteringReport.ps1** script is located in `%ExchangeInstallPath%Scripts`. You need to run the script in the Shell from the Scripts folder. To change your location in the Shell to the Scripts folder, run the following command:

```powershell
Cd $env:ExchangeInstallPath\Scripts
```

To run the script in the Scripts folder, use the following syntax:

```powershell
.\Get-AntiSpamFilteringReport.ps1 -report <ReportValue> [<OptionalParameters>]
```

For details about using the script, run the following command:

```powershell
Get-Help -Detailed .\Get-AntiSpamFilteringReport.ps1
```
