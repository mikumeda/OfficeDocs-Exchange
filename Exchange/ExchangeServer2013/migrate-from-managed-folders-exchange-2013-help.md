---
title: 'Migrate from managed folders: Exchange 2013 Help'
TOCTitle: Migrate from managed folders
ms:assetid: 6796a79d-501e-4216-9370-77965bc5835d
ms:mtpsurl: https://technet.microsoft.com/library/Dd298032(v=EXCHG.150)
ms:contentKeyID: 51439480
ms.reviewer: 
ms.topic: article
description: How to migrate from managed folders in Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Migrate from managed folders

_**Applies to:** Exchange Server 2013_

In Microsoft Exchange Server 2013, messaging records management (MRM) is performed by using retention tags and retention policies. A retention policy is a group of retention tags that can be applied to a mailbox. For more details, see [Retention tags and retention policies](../ExchangeOnline/security-and-compliance/messaging-records-management/retention-tags-and-policies.md). Managed folders, the MRM technology introduced in Exchange Server 2007, aren't supported.

A mailbox that has a managed folder mailbox policy applied can be migrated to use a retention policy. To do so, you must create retention tags that are equivalent to the managed folders linked to the user's managed folder mailbox policy.

> [!IMPORTANT]
> Before you migrate from managed folders to retention policies in your production environment, we recommend that you test the process in a test environment.

> [!TIP]
> You can place mailboxes on retention hold to halt processing of retention policies or managed folder mailbox policies. Placing mailboxes on retention hold can be helpful in migration scenarios to avoid deleting messages or moving them to archive until new policy settings have been tested on test mailboxes or a small number of production mailboxes. For details, see [Place a mailbox on retention hold](mailbox-retention-hold-exchange-2013-help.md).

For other management tasks related to MRM, see [Messaging Records Management Procedures](/office365/securitycompliance/inactive-mailboxes-in-office-365).

## Comparing retention tags to managed folders

Unlike managed folders, which require users to move items to a managed folder based on retention settings, retention tags can be applied to a folder or an individual item in the mailbox. This process has minimal impact on the user's workflow and email organization methods. When a folder has retention tags applied, all items in that folder inherit the retention settings. Users can further specify retention settings by applying different retention tags to individual items in that folder.

Managed folders support different managed content settings for a folder, each with a different message class (such as email items or calendar items). Retention tags don't require a separate managed content settings object because the retention settings are specified in the tag's properties. It isn't supported to create retention tags for particular message classes, with the exception of a default policy tag (DPT) for voicemail messages. Retention tags also don't allow you to use journaling performed by the Managed Folder Assistant.

> [!NOTE]
> Journal rules, which are used to send copies of messages with a journal report to a journaling mailbox, are enforced in the transport pipeline by the Journaling agent and are independent of MRM. For more details, see [Journaling](journaling-exchange-2013-help.md).

The following table compares the MRM functionality available when using retention tags or managed folders.

### Retention tags vs. managed folders

|Functionality|Retention tags|Managed folders|
|---|---|---|
|Specify retention settings for default folders (such as Inbox)|Use retention policy tags (RPTs)|Use managed default folders|
|Specify retention settings for entire mailbox|Use a default policy tag (DPT)|Use managed default folders|
|Use retention settings for custom folders|Use personal tags|Using managed custom folders|
|Require managed content settings|No (retention settings included in a retention tag)|Yes|
|Use retention settings for different message classes (such as e-mail messages, voice mail, or calendar items)|No|Yes|
|Support the Move To Archive action, which moves items to the user's archive mailbox|Yes|No|
|Support the Move To Managed Folder action|No|Yes|
|Allow journaling using the Managed Folder Assistant|No|Yes|
|Policy applied to user|Retention policy|Managed folder mailbox policy|
|Maximum number of policies that can be applied to a mailbox user|1|1|
|Processed by the Managed Folder Assistant|Yes|Yes|
|Client support|Microsoft Outlook 2010 and Office Outlook Web App|Outlook 2010, Office Outlook 2007, and Outlook Web App|

## What do you need to know before you begin?

- Estimated time to complete: 20 minutes.

- Procedures in this topic require specific permissions. See each procedure for its permissions information.

- You can't use the Exchange admin center (EAC) to create retention tags based on retention policies.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-2013-help.md).

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

## Migrate mailbox users from managed folders

The following are general steps for migrating users from this managed folder mailbox policy to a retention policy. Each step is detailed later in this topic:

1. Gather information about managed folder mailbox policies applied to all Exchange 2010 and Exchange 2007 mailboxes, managed folders in each policy and managed content settings for each managed folder. You can use the EMC or the Shell on an Exchange 2010 or Exchange 2007 server to obtain this information.

2. Create retention tags for the migration.

3. Create a retention policy and link the newly created retention tags to the policy.

4. Remove the managed folder mailbox policy and then apply the retention policy to user mailboxes.

    > [!IMPORTANT]
    > After you apply the retention policy to a user and the Managed Folder Assistant runs, the managed folders in the user's mailbox become unmanaged.

For the following procedures, Contoso mailboxes have a managed folder mailbox policy applied containing the following managed folders.

### Managed folders for Contoso

|Managed folder|Managed content settings|Retention enabled|Retention age|Retention action|
|---|---|---|---|---|
|Corp-DeletedItems|CS-Corp-DeletedItems|Yes|30 days|Delete and Allow Recovery|
|Corp-SentItems|CS-Corp-SentItems|Yes|1,825 days|Move to Deleted Items|
|Corp-JunkMail|CS-Corp-JunkMail|Yes|30 days|Permanently Delete|
|Corp-EntireMailbox|CS-Corp-EntireMailbox|Yes|365 days|Move to Deleted Items|
|30 Days|CS-30Days|Yes|30 days|Move to Deleted Items|
|5 Years|CS-5Years|Yes|1,825 days|Move to Deleted Items|
|Never Expire|CS-NeverExpire|No|365 days|Not applicable|

## Step 1: Create retention tags for the migration

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

There are two methods you can use for this step:

- **Create retention tags based on the managed folders and their corresponding managed content settings**: With this method, you use the **New-RetentionPolicyTag** cmdlet with the _ManagedFolderToUpgrade_ parameter. When you specify this parameter, the corresponding retention tag is automatically applied to the managed folder.

    > [!IMPORTANT]
    > If the managed folder you want to port has multiple managed content settings for different message classes, only one retention tag is created, and the highest retention age of all the managed content settings is used as the retention age for the ported tag, irrespective of the message class of the managed content settings.<BR>For example, review the following managed content settings for the managed folder Corp-DeletedItems.

- **Create retention tags by manually specifying the retention settings**: With this method, you use the **New-RetentionPolicyTag** cmdlet without the _ManagedFolderToUpgrade_ parameter. When you don't specify this parameter, any retention policy tags you add to the policy are applied to the default folders, and the default policy tag is applied to the entire mailbox. However, any personal tags you add to the policy aren't automatically applied to the managed folders.

> [!NOTE]
> If you are in a mixed environment with Exchange 2013 and Exchange 2010 servers, you can use the **Port Managed Folder** wizard in the Exchange Management Console (EMC) on an Exchange 2010 server to easily port managed folder and corresponding managed content setting to retention tags.

### Create retention tags based on managed folders

This example creates retention tags based on the corresponding managed content settings shown in the Contoso managed folder mailbox policy.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -ManagedFolderToUpgrade Corp-DeletedItems
New-RetentionPolicyTag Corp-SentItems -ManagedFolderToUpgrade Corp-SentItems
New-RetentionPolicyTag Corp-JunkMail -ManagedFolderToUpgrade Corp-JunkMail
New-RetentionPolicyTag Corp-EntireMailbox -ManagedFolderToUpgrade Corp-EntireMailbox
New-RetentionPolicyTag 30Days -ManagedFolderToUpgrade 30Days
New-RetentionPolicyTag 5Years -ManagedFolderToUpgrade 5Years
New-RetentionPolicyTag NeverExpire -ManagedFolderToUpgrade NeverExpire
```

For detailed syntax and parameter information, see [New-RetentionPolicyTag](/powershell/module/exchange/New-RetentionPolicyTag).

### Create retention tags manually

> [!NOTE]
> You can also use the EAC to create retention tags manually (not based on settings in managed folders). For details, see [Create a Retention Policy](create-a-retention-policy-exchange-2013-help.md).

This example creates retention tags based on the managed folders and corresponding managed content settings shown in the Contoso managed folder mailbox policy. The retention settings are specified manually without using the _ManagedFolderToUpgrade_ parameter.

```powershell
New-RetentionPolicyTag Corp-DeletedItems -Type DeletedItems -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction DeleteAndAllowRecovery
New-RetentionPolicyTag Corp-SentItems -Type SentItems -RetentionEnabled $true -AgeLimitforRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag Corp-JunkMail -Type JunkMail -RetentionEnabled $true -AgeLimitforRetention 30 -RetentionAction PermanentlyDelete
New-RetentionPolicyTag Corp-EntireMailbox -Type All -RetentionEnabled $true -AgeLimitForRetention 365 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 30Days -Type Personal -RetentionEnabled $true -AgeLimitForRetention 30 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag 5Years -Type Personal -RetentionEnabled $true -AgeLimitForRetention 1825 -RetentionAction MoveToDeletedItems
New-RetentionPolicyTag NeverExpire -Type Personal -RetentionEnabled $false
```

For detailed syntax and parameter information, see [New-RetentionPolicyTag](/powershell/module/exchange/New-RetentionPolicyTag).

## Step 2: Create a retention policy

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Messaging records management" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

> [!NOTE]
> You can also use the EAC to create a retention policy and add retention tags to the policy. For details, see [Create a Retention Policy](create-a-retention-policy-exchange-2013-help.md).

This example creates the retention policy RP-Corp and links the newly created retention tags to the policy.

```powershell
New-RetentionPolicy RP-Corp -RetentionPolicyTagLinks Corp-DeletedItems,Corp-SentItems,Corp-JunkMail,Corp-EntireMailbox,30Days,NeverExpire
```

For detailed syntax and parameter information, see [New-RetentionPolicy](/powershell/module/exchange/New-RetentionPolicy).

## Step 3: Remove the managed folder mailbox policy from user mailboxes

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Applying retention policies" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

This example removes the managed folder mailbox policy and any managed folders from Ken Kwok's mailbox. Managed folders that have any messages are not removed.

```powershell
Set-Mailbox -Identity Kwok -RemoveManagedFolderAndPolicy RP-Corp
```

## Step 4: Apply the retention policy to user mailboxes

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Applying retention policies" entry in the [Messaging policy and compliance permissions](messaging-policy-and-compliance-permissions-exchange-2013-help.md) topic.

> [!NOTE]
> You can also use the EAC to apply a retention policy to users. For details, see [Apply a retention policy to mailboxes](apply-retention-policy-exchange-2013-help.md).

This example applies the newly created retention policy RP-Corp to the mailbox user Ken Kwok.

```powershell
Set-Mailbox -Identity Kwok -RetentionPolicy RP-Corp
```

For detailed syntax and parameter information, see [Set-Mailbox](/powershell/module/exchange/Set-Mailbox).

## How do you know this task worked?

To verify that you have migrated from managed folders to retention policies, do the following:

- Generate a report of all user mailboxes and the retention policy applied to them.

  This command retrieves the retention policy applied to all mailboxes in an organization, and their retention hold status.

  ```powershell
  Get-Mailbox -ResultSize unlimited -Filter "Name -NotLike 'DiscoverySearch*'" | Format-Table Name,RetentionPolicy,RetentionHoldEnabled -Auto
  ```

- After the Managed Folder Assistant has processed a mailbox with a retention policy, use the [Get-RetentionPolicyTag](/powershell/module/exchange/Get-RetentionPolicyTag) cmdlet to retrieve the retention tags provisioned in the user mailbox.

  This command retrieves the retention tags actually applied to April Stewart's mailbox.

  ```powershell
  Get-RetentionPolicyTag -Mailbox astewart
  ```
