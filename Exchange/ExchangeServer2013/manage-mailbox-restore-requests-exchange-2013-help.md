---
title: 'Manage mailbox restore requests: Exchange 2013 Help'
TOCTitle: Manage mailbox restore requests
ms:assetid: 8e668a52-c601-4d96-a51c-ab60267e1321
ms:mtpsurl: https://technet.microsoft.com/library/JJ863437(v=EXCHG.150)
ms:contentKeyID: 50387723
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: How to manage mailbox restore requests in Microsoft Exchange 2013
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Manage mailbox restore requests

_**Applies to:** Exchange Server 2013_

Mailbox restore requests are used to restore disconnected mailboxes. A disconnected mailbox is a mailbox in an Exchange mailbox database that isn't associated with an Active Directory user account. Mailboxes become disconnected when they're disabled, deleted, or moved to another database. For more information, see [Disconnected mailboxes](disconnected-mailboxes-exchange-2013-help.md).

Disconnected mailboxes remain in the mailbox database for the duration specified in the deleted mailbox retention settings for the mailbox database. By default, disconnected mailboxes are retained for 30 days. During this retention period, the contents of a deleted mailbox can be restored (copied) to an existing mailbox. This topic describes how to use the Shell to manage mailbox restore requests.

For additional management tasks related to disconnected mailboxes, see the following topics:

- [Disable or delete a mailbox](disable-or-delete-a-mailbox-exchange-2013-help.md)
- [Connect a disabled mailbox](connect-a-disabled-mailbox-exchange-2013-help.md)
- [Connect or restore a deleted mailbox](connect-or-restore-a-deleted-mailbox-exchange-2013-help.md)
- [Restore a soft-deleted mailbox](restore-a-soft-deleted-mailbox-exchange-2013-help.md)
- [Permanently delete a mailbox](permanently-delete-a-mailbox-exchange-2013-help.md)

## What do you need to know before you begin?

- Estimated time to complete each procedure: 2 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Mailbox restore request" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

- The procedures in this topic can only be performed in the Shell. You can't use the EAC to manage mailbox restore requests.

- To display the value of the _Identity_ property for all mailbox restore requests, run the following command.

  ```powershell
  Get-MailboxRestoreRequest | Format-Table Identity
  ```

    You can use this identity value to specify a specific mailbox restore request when you're performing the procedures in this topic.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-2013-help.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

## Use the Shell to view restore request properties

You can view the properties of a mailbox restore request, which provide you with basic information about the status of a mailbox restore request.

To display a list and the value of the _Identity_ property for all mailbox restore requests, run the following command.

```powershell
Get-MailboxRestoreRequest | Format-Table Identity
```

You can use the identity to get information about specific mailbox restore requests.

This example returns the status of the restore request "Pilar Pinilla \\MailboxRestore" using the _Identity_ parameter.

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore"
```

This example returns all information for the second restore request for the Pilar Pinilla target mailbox.

```powershell
Get-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1" | Format-List
```

This example returns the status of restore requests being restored from the source database MBD01.

```powershell
Get-MailboxRestoreRequest -SourceDatabase MBD01
```

This example returns all restore requests that are currently in progress.

```powershell
Get-MailboxRestoreRequest -Status InProgress
```

Other useful status states include `Queued`, `Completed`, `Suspended`, and `Failed`.

This example returns all restore requests that have been suspended.

```powershell
Get-MailboxRestoreRequest -Suspend $true
```

If the command returns an error, verify that you're using the correct syntax and identity. In some cases, the cmdlet may be successful and not return any results. For example, if you've submitted a mailbox restore request and run the command `Get-MailboxRestoreRequest -Status InProgress` and no results are returned, then none of the restore requests are currently running.

For detailed syntax and parameter information, see [Get-MailboxRestoreRequest](/powershell/module/exchange/Get-MailboxRestoreRequest).

## Get-MailboxRestoreRequest Output

By default, the **Get-MailboxRestoreRequest** cmdlet returns the name of the request, the target mailbox to which data is being restored, and the status of the request. The following table lists useful information returned if you pipe the cmdlet to the **Format-List** cmdlet.

|Value|Description|
|---|---|
|`SourceDatabase`|Specifies the database that contains the disconnected mailbox that's being restored.|
|`TargetMailbox`|Specifies the mailbox into which data is being restored.|
|`Name`|Specifies the name of the request.|
|`RequestQueue`|Specifies the database on which the Microsoft Exchange Mailbox Replication service (MRS) stores the detailed status of the request.|
|`Status`|Specifies the status of the request.|
|`Suspend`|Specifies whether the request is suspended. A mailbox restore can be suspended when it's created using the **New-MailboxRestoreRequest** cmdlet with the _Suspend_ parameter. It can also be suspended if the mailbox restore operation fails or by an administrator using the **Suspend-MailboxRestoreRequest** cmdlet.|
|`Identity`|Specifies the identity of the request. This identity is a combination of the target mailbox name and the request name.|

## Use the Shell to view restore request statistics

You can view the statistics of a mailbox restore request, which provide you with detailed information that can be used for troubleshooting purposes.

This example returns the default statistics for the restore request danp\\MailboxRestore1. By default, the information returned includes name, mailbox, status, and percentage complete.

```powershell
Get-MailboxRestoreRequestStatistics -Identity danp\MailboxRestore1
```

This example returns the statistics for Dan Park's mailbox and exports the report to a .csv file.

```powershell
Get-MailboxRestoreRequestStatistics -Identity "Dan Park\MailboxRestore" | Export-CSV \\SERVER01\RestoreRequest_Reports\DanPark_Restorestats.csv
```

This example returns additional information about the restore request for Pilar Pinilla's mailbox using the _IncludeReport_ parameter and piping the results to the **Format-List** cmdlet.

```powershell
Get-MailboxRestoreRequestStatistics -Identity "Pilar Pinilla\MailboxRestore" -IncludeReport | Format-List
```

This example returns additional information for all restore requests that have a status of `Failed` using the _IncludeReport_ parameter, and then saves the information to the file AllRestoreReports.txt in the location where the command is being run.

```powershell
Get-MailboxRestoreRequest -Status Failed | Get-MailboxRestoreRequestStatistics -IncludeReport | Format-List > AllRestoreReports.txt
```

For detailed syntax and parameter information, see [Get-MailboxRestoreRequestStatistics](/powershell/module/exchange/Get-MailboxRestoreRequestStatistics) and [Get-MailboxRestoreRequest](/powershell/module/exchange/Get-MailboxRestoreRequest).

## Get-MailboxRestoreRequestStatistics Output

By default, the [Get-MailboxRestoreRequestStatistics](/powershell/module/exchange/Get-MailboxRestoreRequestStatistics) cmdlet returns the name of the request, the status of the request, the alias of the target mailbox, and the percentage completed. The following table lists other useful information returned if you pipeline the cmdlet to the **Format-List** cmdlet.

|Value|Description|
|---|---|
|`Name`|Specifies the name of the request.|
|`Status`|Specifies the status of the request.|
|`StatusDetail`|Specifies more details about the request status. For example, if the `Status` value returns `InProgress`, the `StatusDetail` value would return the specific stages for the `InProgress` status, such as `CreatingFolderHierarchy` and `CopyingMessages`.|
|`SyncStage`|Specifies how far along the request is through the restore process.|
|`Suspend`|Specifies whether the restore request is suspended. This value is `true` in the following scenarios: <ul><li>MRS stopped or is in the process of stopping the request due to a failure.</li><li>An administrator suspended the request.</li></ul>|
|`SourceExchangeGuid`|Specifies the GUID of the source mailbox from which data is being restored.|
|`SourceRootFolder`|Specifies the name of the root folder in the source mailbox hierarchy from which data is being restored. If this value is blank, data is restored from the folder Top of Information Store.|
|`SourceDatabase`|Specifies the name of the database on which the source mailbox is located.|
|`MailboxRestoreFlags`|Specifies that the mailbox being restored is either `Disabled` or `Soft-Deleted`.|
|`TargetAlias`|Specifies the alias of the target mailbox.|
|`TargetIsArchive`|Specifies whether the mailbox is being restored into an archive.|
|`TargetExchangeGuid`|Specifies the GUID of the target mailbox.|
|`TargetRootFolder`|Specifies the name of the root folder in the target mailbox hierarchy to which data is being restored. If this value is blank, data is restored to the folder Top of Information Store.|
|`TargetDatabase`|Specifies the name of the database on which the target mailbox is located.|
|`TargetMailboxIdentity`|Specifies the identity of the target mailbox.|
|`IncludeFolders`|Specifies the list of folders to include during the restore. If this value is blank, no folders were specified when the request was created, and all folders will be restored to the mailbox (unless the _ExcludeFolders_ parameter is used to exclude specific folders).|
|`ExcludeFolders`|Specifies the list of folders to exclude during the restore. If this value is blank, no folders were specified when the request was created, and all folders will be restored to the mailbox (unless the _IncludeFolders_ parameter is used to include specific folders).|
|`ExcludeDumpster`|Specifies whether the Recoverable Items folder was excluded when the request was created.|
|`ConflictResolutionOption`|Specifies the action for MRS to take if there are matching messages in the target and source folders.|
|`AssociatedMessagesCopyOption`|Specifies whether the associated messages are copied when the request is processed. Associated messages are special messages that contain hidden data with information about rules, views, and forms.|
|`BadItemLimit`|Specifies the number of bad items that MRS will skip if the request encounters corrupted messages.|
|`BadItemsEncountered`|Specifies the number of corrupted messages encountered by the command. If the _BadItemsEncountered_ value is greater than the _BadItemLimit_ value, the request fails.|
|`QueuedTimeStamp`|Specifies the date and time at which the request was initiated to MRS.|
|`StartTimeStamp`|Specifies the date and time at which MRS started processing the restore request.|
|`LastUpdateTimeStamp`|Specifies the date and time at which the last change was made to the request. The change may have been made by an administrator or by MRS.|
|`SuspendTimeStamp`|Specifies the date and time at which the request was suspended.|
|`OverallDuration`|Specifies the amount of time it took to complete the request. If the request is in a `Failed` state, this value specifies the amount of time between the request being initiated and the request failing. If the request isn't complete, this value specifies the amount of time between the request being initiated and the **Get-MailboxRestoreRequestStatistics** cmdlet being run.|
|`TotalSuspendedDuration`|Specifies the amount of time the request was in the `Suspended` state.|
|`TotalFailedDuration`|Specifies the amount of time the request was in the `Failed` state.|
|`TotalQueuedDuration`|Specifies the amount of time the request was in the `Queued` state.|
|`TotalInProgressDuration`|Specifies the amount of time the request was in the `In Progress` state.|
|`TotalStalledDueToHADuration`|Specifies the amount of time the request was stalled due to high availability.|
|`MRSServerName`|Specifies the name of the Client Access server that processed the request.|
|`EstimatedTransferSize`|Specifies the total file size that was restored or the file size that MRS expects to restore if the request is in the `In Progress` state.|
|`EstimatedTransferItemCount`|Specifies the number of items that were restored or the number of items that MRS expects to restore if the request is in the `In Progress` state.|
|`BytesTransferredPerMinute`|Specifies the average number of bytes that have been transferred per minute.|
|`ItemsTransferred`|Specifies the number of items that have been transferred.|
|`PercentComplete`|Specifies the percentage of the request that has been completed.|
|`CompletedRequestAgeLimit`|Specifies how long a completed restore request will be retained before it's deleted. The default is 30 days.|
|`PositionInQueue`|If the request hasn't started, this value specifies the request's position in the queue.|
|`FailureCode`|If there is a failure, this value specifies the failure code.|
|`FailureType`|If there is a failure, this value specifies the failure type.|
|`FailureSide`|If there is a failure, this value specifies whether the failure occurred on the target mailbox or the source mailbox.|
|`Message`|If there is a failure, this value specifies the failure message. This value can also specify the suspend comment.|
|`FailureTimestamp`|If the request failed, this value specifies the date and time at which the request failed.|
|`FailureContext`|If the request failed, this value specifies information about the action being performed at the time of failure.|
|`ValidationMessage`|If the request isn't valid, this value specifies the reason.|
|`RequestQueue`|Specifies the database on which MRS stores the detailed status of the request.|
|`Identity`|Specifies the identity of the request.|
|`Report`|If you used the _IncludeReport_ parameter, this value specifies information that can be used to troubleshoot the request.|

Run the **Get-MailboxRestoreRequestStatistics** cmdlet to verify that you can view the statistics for mailbox restore requests. If the cmdlet returns an error, verify that you're using the correct identity for the restore request.

## Use the Shell to change restore request properties

If a mailbox restore request fails, you can use the **Set-MailboxRestoreRequest** cmdlet to change the request's properties to try to recover from the failure.

This example specifies that the restore request MailboxRestore1 for Debra Garcia's mailbox skips 10 corrupted mailbox items.

```powershell
Set-MailboxRestoreRequest -Identity "Debra Garcia\MailboxRestore1" -BadItemLimit 10
```

This example specifies that the restore request MailboxRestore1 for Florence Flipo's mailbox skips 100 corrupted items. Because the _BadItemLimit_ value is greater than 50, the _AcceptLargeDataLoss_ parameter must be specified.

```powershell
Set-MailboxRestoreRequest -Identity "Florence Flipo\MailboxRestore1" -BadItemLimit 100 -AcceptLargeDataLoss
```

For detailed syntax and parameter information, see [Set-MailboxRestoreRequest](/powershell/module/exchange/Set-MailboxRestoreRequest).

### How do you know you've successfully changed the properties of a restore request?

To verify that you've successfully changed the properties of a restore request, run the **Get-MailboxRestoreRequestStatistics** cmdlet to display the revised properties for the restore request. If the restore request was successfully created, the _Status_ property will have a value of `Queued`, `InProgress`, or `Completed`. After the restore request is completed, the contents of the soft-deleted mailbox will appear in the target mailbox.

For detailed syntax and parameter information, see [Get-MailboxRestoreRequestStatistics](/powershell/module/exchange/Get-MailboxRestoreRequestStatistics).

## Use the Shell to suspend a restore request

You can suspend a restore request any time after the request was created but before the request reaches the status of `Completed`. See Use the Shell to resume a restore request later in this topic for the command syntax to resume the restore request using the [Resume-MailboxRestoreRequest](/powershell/module/exchange/Resume-MailboxRestoreRequest) cmdlet.

This example suspends the restore request MailboxRestore1 for Pilar Pinilla's mailbox.

```powershell
Suspend-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

This example suspends all restore requests in progress by first retrieving all requests that have a status of `InProgress`, and then piping the output to the **Suspend-MailboxRestoreRequest** cmdlet and including the suspend comment "Resume after FY13Q2 Maintenance."

```powershell
Get-MailboxRestoreRequest -Status InProgress | Suspend-MailboxRestoreRequest -SuspendComment "Resume after FY13Q2 Maintenance"
```

For detailed syntax and parameter information, see [Suspend-MailboxRestoreRequest](/powershell/module/exchange/Suspend-MailboxRestoreRequest).

### How do you know you've successfully suspended a mailbox restore request?

To verify that you've successfully suspended a mailbox restore request, run the following command.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

If the value of the _Suspend_ property equals `True`, the restore request was successfully suspended. Also, a value of `Suspended` for the _Status_ property indicates that the restore request was suspended.

## Use the Shell to resume a restore request

Use the **Resume-MailboxRestoreRequest** cmdlet to resume a restore request that failed or was suspended.

This example resumes the restore request Pilar Pinilla\\MailboxRestore1.

```powershell
Resume-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

This example resumes all restore requests that have a status of Failed.

```powershell
Get-MailboxRestoreRequest -Status Failed | Resume-MailboxRestoreRequest
```

For detailed syntax and parameter information, see [Resume-MailboxRestoreRequest](/powershell/module/exchange/Resume-MailboxRestoreRequest).

### How do you know you've successfully resumed a restore request?

To verify you've successfully resumed a restore request, run the following command.

```powershell
Get-MailboxRestoreRequest <identity> | Format-List Suspend,Status
```

If the value of the _Suspend_ property equals `False`, the restore request successfully resumed. Also, a value of `InProgress` for the _Status_ property indicates that the restore request resumed.

## Use the Shell to remove a restore request

You can use the **Remove-MailboxRestoreRequest** cmdlet to remove mailbox restore requests. If you remove a restore request after mailbox data begins being copied to the target mailbox, the mailbox data that's copied remains in the target mailbox.

> [!NOTE]
> As previously stated, completed restore requests are retained for 30 days by default before they're automatically deleted.

This example removes the restore request Pilar Pinilla\\MailboxRestore1.

```powershell
Remove-MailboxRestoreRequest -Identity "Pilar Pinilla\MailboxRestore1"
```

This example removes all restore requests that have the status of Completed.

```powershell
Get-MailboxRestoreRequest -Status Completed | Remove-MailboxRestoreRequest
```

This example cancels the restore request by using the _RequestGuid_ parameter for a request stored on MBXDB01. The parameter set that requires the _RequestGuid_ and _RequestQueue_ parameters is used only for Microsoft Replication Service debugging purposes. You should use this parameter set only if instructed by Microsoft Customer Service and Support.

```powershell
Remove-MailboxRestoreRequest -RequestQueue MBXDB01 -RequestGuid 25e0eaf2-6cc2-4353-b83e-5cb7b72d441f
```

For detailed syntax and parameter information, see [Remove-MailboxRestoreRequest](/powershell/module/exchange/Remove-MailboxRestoreRequest).

### How do you ou've successfully removed a mailbox restore request?

To verify that you've successfully removed a mailbox restore request, run the following command.

```powershell
Get-MailboxRestoreRequest -Identity <identity of removed restore request>
```

The command will return an error stating that the restore request doesn't exist.

You can also run the **Get-MailboxRestoreRequest** cmdlet. If a restore request was successfully removed, it won't be included in the results.
