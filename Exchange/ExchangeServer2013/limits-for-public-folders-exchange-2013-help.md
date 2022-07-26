---
title: 'Limits for public folders: Exchange 2013 Help'
TOCTitle: Limits for public folders
ms:assetid: 709b075e-9584-484b-bcaa-e781c26497b4
ms:mtpsurl: https://technet.microsoft.com/library/Dn594582(v=EXCHG.150)
ms:contentKeyID: 61218734
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: Limits for public folders in Exchange 
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Limits for public folders

_**Applies to:** Exchange Server 2013_

In Exchange Server 2013, we moved public folders from a traditional database architecture to a mailbox architecture. This shift allows public folders to benefit from things such as the resiliency of a Database Availability Group (DAG) and other mailbox enhancements made over the years. However, there are new limits and performance concerns that should be taken into account. In this document we provide some high level guidance for configuration options you have that could affect public folder performance and connectivity.

## Limits

The following table lists the limits for public folders in on-premises Exchange Server 2013. Unless the limits are specifically stated as recommended, the values listed in this table are the supported limits for public folders.

> [!IMPORTANT]
> Looking for Exchange Online limits for Microsoft 365 or Office 365? See [Exchange Online Limits](/office365/servicedescriptions/exchange-online-service-description/exchange-online-limits).

|Item|Limits|Notes|
|---|---|---|
|Total number of public folder mailboxes|100|Although you can create more than 100 public folder mailboxes, it isn't supported. [Create a public folder mailbox](create-public-folder-mailbox-exchange-2013-help.md)|
|Total public folders in hierarchy|1,000,000|Although you can create more than 1,000,000 public folders, it isn't supported. For any deployment of 100,000 or more public folders, we recommend reading [Considerations when deploying public folders](considerations-when-deploying-public-folders-exchange-2013-help.md).|
|Sub-folders under the parent folder|10,000|While you can create more than 1,000 sub-folders under a parent folder, we don't recommend that you do so. <br/><br/> _FolderHierarchyChildrenCountReceiveQuota_ parameter on the [Set-Mailbox](/powershell/module/exchange/Set-Mailbox) cmdlet.|
|Folder depth|300|The folder depth is the number levels of nested folders that can exist in one branch of a public folder tree. _FolderHierarchyDepthRecieveQuota_ parameter on the [Set-Mailbox](/powershell/module/exchange/Set-Mailbox) cmdlet.|
|Maximum messages per public folder|1 million|_MailboxMessagesPerFolderCountReceiveQuota_ parameter on the [Set-Mailbox](/powershell/module/exchange/Set-Mailbox) cmdlet.|
|Maximum individual public folder size|10 GB|This limit doesn't include subfolders beneath a single folder. <br/><br/> [Configure storage quotas for a mailbox](configure-storage-quotas-for-a-mailbox-exchange-2013-help.md)|
|Public folder mailbox size|100 GB|[Configure storage quotas for a mailbox](configure-storage-quotas-for-a-mailbox-exchange-2013-help.md)|
|Number of user logons per public folder mailbox|2,000 concurrent user logons|We recommend that you configure your hierarchy so that you have no more than 2,000 users per public folder mailbox. For example, if you have 20,000 users, you should have 10 public folder mailboxes.|
|Moved item retention|14 days recommended|Use the _DefaultPublicFolderMovedItemRetention_ parameter on the **Set-OrganizationConfig** cmdlet.|
|Age limit|We recommend that you set this as the same default that you use for regular mailboxes.|These settings can be set at the following levels: <ul><li>**Organizational level**: _DefaultPublicFolderAgeLimit_ parameter on the **Set-OrganizationConfig** cmdlet.</li><li>**Mailbox level**: _AgeLimit_ parameter on the **Set-Mailbox** cmdlet.</li><li>**Folder level**: _AgeLimit_ parameter on the **Set-PublicFolder** cmdlet.</li></ul>|
|Deleted item retention|We recommend that you set this as the same default that you use for regular mailboxes.|These settings can be set at the following levels: <ul><li>**Organizational level**: _DefaultPublicFolderMovedItemRetention_ parameter on the **Set-OrganizationConfig** cmdlet.</li><li>**Mailbox level**: _RetainDeletedItemsFor_ on the **Set-Mailbox** cmdlet.</li><li>**Folder level**: _RetainDeleteItemsFor_ parameter on the **Set-PublicFolder** cmdlet.</li></ul>|
|Maximum number of public folders that can be migrated to Exchange 2013|500,000|This is the maximum number of public folders you can move to Exchange 2013 from a legacy version of Exchange in a single migration. For details on migrating public folders, see [Use batch migration to migrate public folders to Exchange 2013 from previous versions](use-batch-migration-to-migrate-public-folders-to-exchange-2013-from-previous-versions-exchange-2013-help.md)|
