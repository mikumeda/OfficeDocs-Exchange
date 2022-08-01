---
title: 'Mailbox audit logging: Exchange 2013 Help'
TOCTitle: Mailbox audit logging
ms:assetid: 29b67d58-eef9-4ad4-863f-562405ea8794
ms:mtpsurl: https://technet.microsoft.com/library/Ff459237(v=EXCHG.150)
ms:contentKeyID: 49300455
ms.reviewer: 
ms.topic: article
description: About Mailbox audit logging in Exchange 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Mailbox audit logging

_**Applies to:** Exchange Server 2013_

Because mailboxes can contain sensitive, high business impact (HBI) information and personally identifiable information (PII), it's important that you track who logs on to the mailboxes in your organization and what actions are taken. It's especially important to track access to mailboxes by users other than the mailbox owner. These users are referred to as _delegate users_.

By using _mailbox audit logging_, you can log mailbox access by mailbox owners, delegates (including administrators with full access permissions to mailboxes), and administrators.

When you enable audit logging for a mailbox, you can specify which user actions (for example, accessing, moving, or deleting a message) will be logged for a logon type (administrator, delegate user, or owner). Audit log entries also include important information such as the client IP address, host name, and process or client used to access the mailbox. For items that are moved, the entry includes the name of the destination folder.

## Mailbox audit logs

Mailbox audit logs are generated for each mailbox that has mailbox audit logging enabled. Log entries are stored in the Recoverable Items folder in the audited mailbox, in the Audits subfolder. This ensures that all audit log entries are available from a single location, regardless of which client access method was used to access the mailbox or which server or workstation an administrator used to access the mailbox audit log. If you move a mailbox to another Mailbox server, the mailbox audit logs for that mailbox are also moved because they're located in the mailbox.

By default, mailbox audit log entries are retained in the mailbox for 90 days and then deleted. You can modify this retention period by using the _AuditLogAgeLimit_ parameter with the [Set-Mailbox](/powershell/module/exchange/Set-Mailbox) cmdlet. If a mailbox is on In-Place Hold or Litigation Hold, audit log entries are only retained until the audit log retention period for the mailbox is reached. To retain audit log entries longer, you have to increase the retention period by changing the value for the _AuditLogAgeLimit_ parameter. You can also export audit log entries before the retention period is reached. For more information, see:

- [Export mailbox audit logs](../ExchangeOnline/security-and-compliance/exchange-auditing-reports/export-mailbox-audit-logs.md)
- [Create a mailbox audit log search](create-a-mailbox-audit-log-search-exchange-2013-help.md)

## Enabling mailbox audit logging

Mailbox audit logging is enabled per mailbox. Use the **Set-Mailbox** cmdlet to enable or disable mailbox audit logging. For details, see [Enable or disable mailbox audit logging for a mailbox](enable-or-disable-mailbox-audit-logging-for-a-mailbox-exchange-2013-help.md).

When you enable mailbox audit logging for a mailbox, access to the mailbox and certain administrator and delegate actions are logged by default. To log actions taken by the mailbox owner, you must specify which owner actions should be audited.

## Mailbox actions logged by mailbox audit logging

The following table lists the actions logged by mailbox audit logging, including the logon types for which the action can be logged.

|Action|Description|Administrator|Delegate|Owner|
|---|---|---|---|---|
|Copy|An item is copied to another folder.|Yes|No|No|
|Create|An item is created in the Calendar, Contacts, Notes, or Tasks folder in the mailbox; for example, a new meeting request is created. Note that message or folder creation isn't audited.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes|
|FolderBind|A mailbox folder is accessed.|Yes<sup>\*</sup>|Yes<sup>\*\*</sup>|No|
|HardDelete|An item is deleted permanently from the Recoverable Items folder.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes|
|MessageBind|An item is accessed in the reading pane or opened.|Yes|No|No|
|Move|An item is moved to another folder.|Yes<sup>\*</sup>|Yes|Yes|
|MoveToDeletedItems|An item is moved to the Deleted Items folder.|Yes<sup>\*</sup>|Yes|Yes|
|SendAs|A message is sent using Send As permissions.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Not applicable|
|SendOnBehalf|A message is sent using Send on Behalf permissions.|Yes<sup>\*</sup>|Yes|Not applicable|
|SoftDelete|An item is deleted from the Deleted Items folder.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes|
|Update|An item's properties are updated.|Yes<sup>\*</sup>|Yes<sup>\*</sup>|Yes|

<sup>\*</sup> Audited by default if auditing is enabled for a mailbox.

<sup>\*\*</sup> Entries for folder bind actions performed by delegates are consolidated. One log entry is generated for individual folder access within a time span of 24 hours.

If you no longer require certain types of mailbox actions to be audited, you should modify the mailbox's audit logging configuration to disable those actions. Existing log entries aren't purged until the age limit for audit log entries is reached.

## Searching mailbox audit log entries

You can use the following methods to search mailbox audit log entries:

- **Synchronously search a single mailbox**: You can use the [Search-MailboxAuditLog](/powershell/module/exchange/Search-MailboxAuditLog) cmdlet to synchronously search mailbox audit log entries for a single mailbox. The cmdlet displays search results in the Exchange Management Shell window. For details, see [Search the mailbox audit log for a mailbox](search-the-mailbox-audit-log-for-a-mailbox-exchange-2013-help.md).

- **Asynchronously search one or more mailboxes**: You can create a mailbox audit log search to asynchronously search mailbox audit logs for one or more mailboxes, and then have the search results sent to a specified email address. The search results are sent as an XML attachment. To create the search, use the [New-MailboxAuditLogSearch](/powershell/module/exchange/New-MailboxAuditLogSearch) cmdlet. For details, see [Create a mailbox audit log search](create-a-mailbox-audit-log-search-exchange-2013-help.md).

- **Use auditing reports in the Exchange admin center (EAC)**: You can use the **Auditing** tab in the EAC to run a non-owner mailbox access report or export entries from the mailbox audit log. For details, see:

  - [Run a non-owner mailbox access report](../ExchangeOnline/security-and-compliance/exchange-auditing-reports/non-owner-mailbox-access-report.md)
  - [Export mailbox audit logs](../ExchangeOnline/security-and-compliance/exchange-auditing-reports/export-mailbox-audit-logs.md)

## Mailbox audit log entries

The following table describes the fields logged in a mailbox audit log entry.

|Field|Populated with|
|---|---|
|**Operation**|One of the following actions: <ul><li>Copy</li><li>Create</li><li>FolderBind</li><li>HardDelete</li><li>MessageBind</li><li>Move</li><li>MoveToDeletedItems</li><li>SendAs</li><li>SendOnBehalf</li><li>SoftDelete</li><li>Update</li></ul>|
|**OperationResult**|One of the following results: <ul><li>Failed</li><li>PartiallySucceeded</li><li>Succeeded</li></ul>|
|**LogonType**|Logon type of the user who performed the operation. Logon types include: <ul><li>Owner</li><li>Delegate</li><li>Admin</li></ul>|
|**DestFolderId**|Destination folder GUID for move operations.|
|**DestFolderPathName**|Destination folder path for move operations.|
|**FolderId**|Folder GUID.|
|**FolderPathName**|Folder path.|
|**ClientInfoString**|Details that identify which client or Exchange component performed the operation.|
|**ClientIPAddress**|Client computer IP address.|
|**ClientMachineName**|Client computer name.|
|**ClientProcessName**|Name of the client application process.|
|**ClientVersion**|Client application version.|
|**InternalLogonType**|Logon type of the user who performed the operation. Logon types include: <ul><li>Owner</li><li>Delegate</li><li>Admin</li></ul>|
|**MailboxOwnerUPN**|Mailbox owner user principal name (UPN).|
|**MailboxOwnerSid**|Mailbox owner security identifier (SID).|
|**DestMailboxOwnerUPN**|Destination mailbox owner UPN, logged for cross-mailbox operations.|
|**DestMailboxOwnerSid**|Destination mailbox owner SID, logged for cross-mailbox operations.|
|**DestMailboxOwnerGuid**|Destination mailbox owner GUID.|
|**CrossMailboxOperation**|Information about whether the operation logged is a cross-mailbox operation (for example, copying or moving messages between mailboxes).|
|**LogonUserDisplayName**|Display name of user who is logged on.|
|**DelegateUserDisplayName**|Delegate user display name.|
|**LogonUserSid**|SID of user who is logged on.|
|**SourceItems**|ItemID of mailbox items on which the logged action is performed (for example, move or delete). For operations performed on a number of items, this field is returned as a collection of items.|
|**SourceFolders**|Source folder GUID.|
|**ItemId**|Item ID.|
|**ItemSubject**|Item subject.|
|**MailboxGuid**|Mailbox GUID.|
|**MailboxResolvedOwnerName**|Mailbox user resolved name in the format _DOMAIN_\_SamAccountName_.|
|**LastAccessed**|Time when the operation was performed.|
|**Identity**|Audit log entry ID.|

## More information

- **Administrator access to mailboxes**: Mailboxes are considered to be accessed by an administrator only in the following scenarios:

  - [In-Place eDiscovery](../ExchangeOnline/security-and-compliance/in-place-ediscovery/in-place-ediscovery.md) is used to search a mailbox.
  - The [New-MailboxExportRequest](/powershell/module/exchange/New-MailboxExportRequest) cmdlet is used to export a mailbox.
  - [Microsoft Exchange Server MAPI Client and Collaboration Data Objects](https://www.microsoft.com/download/details.aspx?id=39045) is used to access the mailbox.

- **Bypassing mailbox auditing logging**: Mailbox access by authorized automated processes such as accounts used by third-party tools or accounts used for lawful monitoring can create a large number of mailbox audit log entries and may not be of interest to your organization. You can configure such accounts to bypass mailbox audit logging. For details, see [Bypass a user account from mailbox audit logging](bypass-a-user-account-from-mailbox-audit-logging-exchange-2013-help.md).

- **Logging mailbox owner actions**: For mailboxes such as the Discovery Search Mailbox, which may contain more sensitive information, consider enabling mailbox audit logging for mailbox owner actions such as message deletion.
