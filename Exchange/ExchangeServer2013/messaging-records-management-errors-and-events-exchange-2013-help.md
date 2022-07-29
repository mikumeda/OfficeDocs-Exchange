---
title: 'Messaging records management errors and events: Exchange 2013 Help'
TOCTitle: Messaging records management errors and events
ms:assetid: 8bc3f5ae-403b-45af-86c1-b2fccab34e63
ms:mtpsurl: https://technet.microsoft.com/library/Bb310783(v=EXCHG.150)
ms:contentKeyID: 50873803
ms.reviewer: 
ms.topic: article
description: Messaging records management errors and events in Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Messaging records management errors and events

_**Applies to:** Exchange Server 2013_

Messaging records management (MRM) generates events that you can view in Event Viewer. This allows you to troubleshoot and verify the performance of the Managed Folder Assistant. Event Viewer tracks the following kinds of events in the following order, based on importance:

1. Error events
2. Warning events
3. Informational events

## MRM Errors and Events

The following tables provide lists of events that you can use to troubleshoot MRM. The logging types include the following:

- Events labeled as **LogAlways** are always logged individually.
- Events labeled as **LogPeriodic** are logged only once in any five-minute period, not every time they occur. This helps to prevent excessive log entries.

### MRM events in the Managed Folder Assistant category

|Event ID|Category|Event type|Logging|Value or description|
|---|---|---|---|---|
|10003|Managed Folder Assistant|Error|LogPeriodic|Could not get the server configuration object from Active Directory. _\<Exception details\>_. Check for domain controller network connectivity issues or incorrect DNS configuration.|
|10004|Managed Folder Assistant|Error|LogAlways|The retention policy for folder _\<folder\>_ in mailbox _\<mailbox\>_ will not be applied. The managed folder assistant is unable to process managed content setting _\<content setting\>_ for the managed folder _\<managed folder\>_. The RetentionAction is MoveToFolder but a destination folder was not specified. Please specify a destination folder.|
|10005|Managed Folder Assistant|Error|LogAlways|Retention policy will not be applied to folder _\<folder\>_ in mailbox _\<mailbox\>_. Unable to process Managed Content Setting _\<content setting\>_ for the Managed Folder _\<managed folder\>_. The RetentionAction is MoveToFolder but the destination folder _\<folder\>_ is the same as the source folder _\<folder\>_. Please specify a destination folder that is different from the source folder.|
|10009|Managed Folder Assistant|Error|LogAlways|The managed folder assistant skipped processing all databases on the local server because it could not read the audit log parameters from Active Directory. It will try again later in the schedule window. Current database: _\<database\>_|
|10010|Managed Folder Assistant|Error|LogAlways|The managed folder assistant skipped processing all databases on the local server because the audit log is enabled but the path to the audit log is missing in Active Directory. It will try again later in the schedule window. Current database: _\<database\>_|
|10011|Managed Folder Assistant|Error|LogAlways|The managed folder assistant could not configure the audit log. It will stop processing the current database: '%1'. It will try again later in the schedule window. Exception details: _\<details\>_|
|10012|Managed Folder Assistant|Error|LogAlways|The managed folder assistant did not write to the audit log. It will stop processing the current database: _\<database\>_. It will try to write to the audit log again later in the schedule window. Exception details: _\<details\>_|
|10017|Managed Folder Assistant|Error|LogAlways|An exception occurred in the Managed Folder Assistant while it was processing Mailbox: _\<mailbox\>_ Folder: Name: _\<folder name\>_ Id: _\<folder ID\>_ Item: Ids: _\<IDs\>_. Exception: _\<exception\>_.|

### MRM events in the Assistants category

|Event ID|Category|Event type|Logging|Value or description|
|---|---|---|---|---|
|9004|Assistants|Warning|LogAlways|Service _\<service\>_. _\<service\>_ failed to process mailbox _\<mailbox\>_. The following exception caused the failure: _\<exception\>_|
|9014|Assistants|Warning|LogAlways|Service _\<service\>_. Unable to process schedule changes. The following exception caused the failure: _\<exception\>_|
|9017|Assistants|Information|LogAlways|Service _\<service\>_. _\<service\>_ for database _\<database\>_ is entering a scheduled time window. There are _\<number\>_ mailboxes to process.|
|9018|Assistants|Information|LogAlways|Service _\<service\>_. _\<service\>_ for database _\<database\>_ is exiting a scheduled time window. _\<number\>_ out of _\<number\>_ mailboxes were successfully processed. _\<number\>_ mailboxes were skipped due to errors. _\<number\>_ mailboxes were processed separately. _\<number\>_ mailboxes were not processed due to insufficient time. <br/><br/> **Note**: The Managed Folder Assistant will resume where it left off the next time it runs.|
|9019|Assistants|Warning|LogPeriodic|Service _\<service\>_. Unable to save progress for _\<service\>_ on database _\<database\>_. (The assistant was unable to save where it stopped so that it could resume there when it restarts.) The following exception caused the failure: _\<exception\>_|
|9020|Assistants|Warning|LogAlways|Service _\<service\>_. _\<assistant name\>_ failed to start for database _\<database\>_. The following exception caused the failure: _\<exception\>_|
|9021|Assistants|Information|LogAlways|Service _\<service\>_. _\<service\>_ for database _\<database\>_ is processing an on-demand request. There are _\<number\>_ mailboxes to process.|
|9022|Assistants|Information|LogAlways|Service _\<service\>_. _\<service\>_ for database _\<database\>_ has finished an on-demand request. _\<number\>_ out of _\<number\>_ mailboxes were successfully processed. _\<number\>_ mailboxes were skipped due to errors.|
|9023|Assistants|Warning|LogAlways|Service _\<service\>_. _\<service\>_ failed to start time window processing on database _\<database\>_. The following exception caused the failure: _\<exception\>_|
|9025|Assistants|Information|LogAlways|Service _\<service\>_. _\<service\>_ skipped _\<number\>_ mailboxes on database _\<database\>_. Mailboxes: _\<mailboxes\>_|
|9026|Assistants|Warning|LogAlways|Service _\<service\>_. _\<service\>_ failed to start on-demand processing on database _\<database\>_. The following exception caused the failure: _\<exception\>_|
|9027|Assistants|Error|LogAlways|Service _\<service\>_. _\<service\>_ caused the process to terminate _\<number\>_ times while processing mailbox _\<mailbox\>_ on database _\<database\>_. This mailbox will no longer be processed in the requested time window or on-demand request. The following exception caused the failure: _\<exception\>_|
|9028|Assistants|Warning|LogAlways|Service _\<service\>_. _\<service\>_ caused the process to terminate _\<number\>_ times while processing mailbox _\<mailbox\>_ on database _\<database\>_. The following exception caused the failure: _\<exception\>_|
|9033|Assistants|Warning|LogAlways|Service _\<service\>_. _\<service\>_ for database _\<database\>_ received an on-demand request. However, there are no mailboxes to process.|
|9034|Assistants|Information|LogAlways|Service _\<service\>_ halted time based operations for managed folder assistant on database _\<database\>_.|
|9035|Assistants|Warning|LogAlways|Service _\<service\>_. _\<assistant name\>_ was unable to process _\<number\>_ mailboxes because insufficient time.|
|9037|Assistants|Error|LogAlways|Service _\<service\>_. An exception was encountered while processing a RPC. Method: _\<method\>_, Exception: _\<exception\>_|
