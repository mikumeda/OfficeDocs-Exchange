---
title: 'Recipients Permissions: Exchange 2013 Help'
TOCTitle: Recipients Permissions
ms:assetid: 5b690bcb-c6df-4511-90e1-08ca91f43b37
ms:mtpsurl: https://technet.microsoft.com/library/Dd638132(v=EXCHG.150)
ms:contentKeyID: 48385139
ms.reviewer: 
ms.topic: article
description: About recipients permissions in Microsoft Exchange
manager: serdars
ms.author: serdars
author: serdars
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Recipients Permissions

_**Applies to:** Exchange Server 2013_

The permissions required to perform tasks to manage recipients vary depending on the procedure being performed or the cmdlet you want to run.

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

## Mailbox server permissions

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Calendar repair, server configuration|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Delegating Mailbox servers|[Organization Management](organization-management-exchange-2013-help.md)|
|Email address policies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Exchange Search|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Exchange Search - diagnostics|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> Support Diagnostics role <br/><br/> **Note**: The Support Diagnostics role isn't assigned to a role group. For more information, see [Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md).|
|Group metrics|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Import Export|Mailbox Import Export role <br/><br/> **Note**: The Mailbox Import Export role isn't assigned to a role group. For more information, see [Mailbox Import Export role](mailbox-import-export-role-exchange-2013-help.md).|
|Mailbox Assistants|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Mailbox moves|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Mailbox recovery|[Organization Management](organization-management-exchange-2013-help.md)|
|Mailbox repair request|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Mailbox restore request|[Organization Management](organization-management-exchange-2013-help.md)|
|Mailbox server configuration|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Manage Exchange Search Indexer service on a Mailbox server|Local Administrator on the Mailbox server|
|MAPI connectivity|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|OAB virtual directories|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Remove store mailbox|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|

## Calendar and sharing permissions

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Calendar configuration|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Calendar diagnostics|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md) <br/><br/> [Compliance Management](compliance-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Calendar processing|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Notifications|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Organization relationships|[Organization Management](organization-management-exchange-2013-help.md)|
|Sharing policies|[Organization Management](organization-management-exchange-2013-help.md)|

## Resource mailbox configuration permissions

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Booking policies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Delegation|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Resource mailbox schema configuration|[Organization Management](organization-management-exchange-2013-help.md)|

## Mailbox database permissions

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Mailbox databases|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|

## Recipient provisioning permissions

This table contains the various permissions that are required to manage recipients.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Address list, GAL|[Organization Management](organization-management-exchange-2013-help.md)|
|Anti-spam|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Apps for Outlook|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Applying sharing policies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Arbitration|[Organization Management](organization-management-exchange-2013-help.md)|
|Archive connectivity|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Assigning offline address books|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Automatic replies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Calendar configuration|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Calendar repair|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Contact aggregation settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|Disconnected mailboxes|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Distribution groups|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Dynamic distribution groups|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Email addresses|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|Inbox rules|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Mail contacts|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Mail tips|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Mail user|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Mailbox folder permissions|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Mailbox folders|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|MAPI connectivity|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> |
|Message configuration|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Message quotas|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Moderation|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Permissions and delegation|[Organization Management](organization-management-exchange-2013-help.md)|
|Archive mailboxes|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Recipient data properties|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Remote mailboxes|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Retention and legal holds|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Send As|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Spelling configuration|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Unified Messaging|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|User mailboxes|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|User photos|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|

## Mailbox move and migration permissions

The table contains the permissions that are required to move on-premises mailboxes to different domains or forests and to migrate on-premises mailboxes to and from your cloud-based organization.

|Feature|Permissions required|
|---|---|
|Mailbox moves (local or cross-forest)|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Mailbox moves (hybrid deployment)|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Migration (on-boarding and off-boarding from the cloud)|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
