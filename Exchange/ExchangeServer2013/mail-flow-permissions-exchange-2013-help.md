---
title: 'Mail flow permissions: Exchange 2013 Help'
TOCTitle: Mail flow permissions
ms:assetid: f49f4fb5-af75-43cb-900f-c5f7b8cfa143
ms:mtpsurl: https://technet.microsoft.com/library/Dd638213(v=EXCHG.150)
ms:contentKeyID: 48385715
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: About Mail flow permissions in Exchange 2013 
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Mail flow permissions

_**Applies to:** Exchange Server 2013_

The permissions required to perform tasks related to mail flow vary depending on the procedure being performed or the cmdlet you want to run. For more information about transport features, see [Mail flow](mail-flow-exchange-2013-help.md).

This topic lists the permissions required to manage the mail flow features in Microsoft Exchange Server 2013. For information about how Office 365 permissions relate to Exchange permissions, see [About admin roles](/microsoft-365/admin/add-users/about-admin-roles).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

> [!NOTE]
> Some features that you want to manage might exist on Edge Transport servers. To manage features on Edge Transport servers, you need to become a member of the Local Administrators group on the Edge Transport server you want to manage. Edge Transport servers don't use Role Based Access Control (RBAC). Features that can be managed on Edge Transport servers have Edge Transport Local Administrator in the "Permissions required" column in the table below.
>
> Some features may require that you have local administrator permissions on the server you want to manage. To manage these features, you must be a member of the Local Administrators group on that server.

You can use the features in the following tables to configure mail flow settings in the Front End Transport service on Client Access servers, in the Transport service on Mailbox servers, in the Mailbox Transport service on Mailbox servers, and on Edge Transport servers. The permissions that are required to configure each feature are listed.

Users who are assigned the View Only Management role group can view the configuration of the features shown in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

**Mailbox servers and Client Access servers**:

|Feature|Permissions required|
|---|---|
|Accepted domains|[Organization Management](organization-management-exchange-2013-help.md)|
|Active Directory site and site link management|[Organization Management](organization-management-exchange-2013-help.md)|
|Anti-spam features|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|Anti-spam updates|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|Certificate management|[Organization Management](organization-management-exchange-2013-help.md)|
|Delivery Agent connectors|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|DSNs|[Organization Management](organization-management-exchange-2013-help.md)|
|EdgeSync|[Organization Management](organization-management-exchange-2013-help.md)|
|Foreign connectors|[Organization Management](organization-management-exchange-2013-help.md)|
|Front End Transport service|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|Journaling|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Mailbox access|[Organization Management](organization-management-exchange-2013-help.md)|
|Mailbox junk email configuration|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Mailbox Transport service|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|MailTips|[Organization Management](organization-management-exchange-2013-help.md)|
|Message classifications|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Message tracking|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Moderated transport|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Queues|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Receive connectors|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|Remote domains|[Organization Management](organization-management-exchange-2013-help.md)|
|SafeList aggregation|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Send connectors|[Organization Management](organization-management-exchange-2013-help.md)|
|Shadow redundancy|[Organization Management](organization-management-exchange-2013-help.md)|
|Testing mail flow|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Testing Transport rule processing|[Organization Management](organization-management-exchange-2013-help.md)|
|Transport agents|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Transport configuration|[Organization Management](organization-management-exchange-2013-help.md)|
|Transport logs|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Transport rules|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Transport service|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|X.400 domains|[Organization Management](organization-management-exchange-2013-help.md)|

**Edge Transport servers**:

|Feature|Permissions required|
|---|---|
|Accepted domains - Edge Transport|Edge Transport Local Administrator|
|Address Rewriting - Edge Transport|Edge Transport Local Administrator|
|Edge Transport server|Edge Transport Local Administrator|
|EdgeSync - Edge Transport|Edge Transport Local Administrator|
|Queues - Edge Transport|Edge Transport Local Administrator|
|Receive connectors - Edge Transport|Edge Transport Local Administrator|
|Send connectors - Edge Transport|Edge Transport Local Administrator|
|Transport configuration - Edge Transport|Edge Transport Local Administrator|
|Transport logs - Edge Transport|Edge Transport Local Administrator|
|Transport rules - Edge Transport|Edge Transport Local Administrator|
