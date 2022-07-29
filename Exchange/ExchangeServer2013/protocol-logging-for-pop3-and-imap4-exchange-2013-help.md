---
title: 'Protocol logging for POP3 and IMAP4: Exchange 2013 Help'
TOCTitle: Protocol logging for POP3 and IMAP4
ms:assetid: 212ed3d5-0c98-4346-a860-1cfcac5d73c4
ms:mtpsurl: https://technet.microsoft.com/library/Dd335141(v=EXCHG.150)
ms:contentKeyID: 50395394
ms.reviewer: 
ms.topic: article
manager: serdars
description: How to use protocol logging to review the POP3 and IMAP4 connections in your Exchange environment
ms.author: serdars
author: serdars
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Protocol logging for POP3 and IMAP4

_**Applies to:** Exchange Server 2013_

You can use protocol logging to review the POP3 and IMAP4 connections in your Exchange environment. This can be useful if you're troubleshooting issues related to POP3 or IMAP4 performance.

## Enabling POP3 and IMAP4 protocol logging

You can enable, disable, or change protocol logging using the Exchange Management Shell. If you enable protocol logging using the Shell, the default protocol logging settings will be used. In most cases, the default settings will be sufficient.

Alternatively, you can enable, disable, and modify protocol logging options by editing the Microsoft.Exchange.Pop3.exe.config and Microsoft.Exchange.Imap4.exe.config configuration files located on your Microsoft Exchange Server 2013 Client Access server. For more information about how to manage POP3 and IMAP4 protocol settings, see [Configure protocol logging for POP3 and IMAP4](configure-protocol-logging-for-pop3-and-imap4-exchange-2013-help.md).

## Reviewing the protocol log

The protocol log files are text files that contain data in the comma-separated value (CSV) file format. The protocol log stores each protocol event on a single line. The information stored on each line is organized by fields. These fields are separated by commas. The following table describes the fields that are used to classify each protocol event.

### Fields used to classify each protocol event

|Field name|Description|
|---|---|
|date-time|The date and time of the protocol event. The value is formatted as _yyyy-mm-ddhh:mm:ss.fffZ_, where _yyyy_ = year, _mm_ = month, _dd_ = day, _hh_ = hour, _mm_ = minute, _ss_ = second, _fff_ = fractions of a second, and _Z_ signifies Zulu. Zulu is another way to indicate Coordinated Universal Time (UTC).|
|connector-id|This field isn't used for POP3 and IMAP4 protocol logging.|
|session-id|A GUID that uniquely identifies the SMTP session that is associated with a protocol event.|
|sequence-number|A counter that starts at 0 and is incremented for each event in the same session.|
|local-endpoint|The local endpoint of a POP3 or IMAP4 session. This consists of an IP address and TCP port number, formatted as follows: _\<IP address\>_:_\<port\>_.|
|remote-endpoint|The remote endpoint of a POP3 or IMAP4 session. This consists of an IP address and TCP port number, formatted as follows: _\<IP address\>_:_\<port\>_.|
|event|A single character that represents the protocol event. The possible values for the event are as follows: <ul><li>`+`: Connect</li><li>-: Disconnect</li><li>`>`: Send</li><li>`<`: Receive</li><li>`*`: Information</li></ul>|
|data|Text information that's associated with the POP3 or IMAP4 event.|
|context|This field isn't used for POP3 and IMAP4 protocol logging.|
