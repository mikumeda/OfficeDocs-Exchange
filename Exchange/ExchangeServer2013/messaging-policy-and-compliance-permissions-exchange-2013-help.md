---
title: 'Messaging policy and compliance permissions: Exchange 2013 Help'
TOCTitle: Messaging policy and compliance permissions
ms:assetid: ec4d3b9f-b85a-4cb9-95f5-6fc149c3899b
ms:mtpsurl: https://technet.microsoft.com/library/Dd638205(v=EXCHG.150)
ms:contentKeyID: 48385692
ms.reviewer: 
ms.topic: article
description: Messaging policy and compliance permissions in Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Messaging policy and compliance permissions

_**Applies to:** Exchange Server 2013_

The permissions required to configure messaging policy and compliance vary depending on the procedure being performed or the cmdlet you want to run. For more information about messaging policy and compliance, see [Messaging policy and compliance](messaging-policy-and-compliance-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

> [!NOTE]
> Some features that you want to manage might exist on Edge Transport servers. To manage features on Edge Transport servers, you need to become a member of the Local Administrators group on the Edge Transport server you want to manage. Edge Transport servers don't use Role Based Access Control (RBAC). Features that can be managed on Edge Transport servers have Edge Transport Local Administrator in the "Permissions required" column in the table below.

You can use the features in the following table to configure messaging policy and compliance features. The role groups that are required to configure each feature are listed.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Data loss prevention (DLP)|[Compliance Management](compliance-management-exchange-2013-help.md)|
|Delete mailbox content (using the [Search-Mailbox](/powershell/module/exchange/Search-Mailbox) cmdlet with the _DeleteContent_ switch)|[Discovery Management](discovery-management-exchange-2013-help.md) **and** <br/><br/> [Mailbox Import Export role](mailbox-import-export-role-exchange-2013-help.md) <br/><br/> **Note**: By default, the Mailbox Import Export role isn't assigned to any role group. You can assign a management role to a built-in or custom role group, a user or a universal security group. Assigning a role to a role group is recommended. For more information, see [Add a role to a user or USG](add-a-role-to-a-user-or-usg-exchange-2013-help.md).|
|Discovery mailboxes - Create|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Journaling|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Mailbox audit logging|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Message classifications|[Organization Management](organization-management-exchange-2013-help.md)|
|Messaging records management|[Compliance Management](compliance-management-exchange-2013-help.md) <br/><br/> [Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|In-Place eDiscovery|[Discovery Management](discovery-management-exchange-2013-help.md) <br/><br/> **Note**: By default, the Discovery Management role group doesn't have any members. No users, including administrators, have the required permissions to search mailboxes. For more information, see [Assign eDiscovery permissions in Exchange](/exchange/security-and-compliance/in-place-ediscovery/assign-ediscovery-permissions).|
|In-Place Hold|[Discovery Management](discovery-management-exchange-2013-help.md) <br/><br/> [Organization Management](organization-management-exchange-2013-help.md) <br/><br/> **Important**: To create a query-based In-Place Hold, a user requires the Mailbox Search and Litigation Hold roles to be assigned directly or via membership in a role group that has both roles assigned. To create an In-Place Hold without using a query, which places all mailbox items on hold, you must have the Litigation Hold role assigned. The Discovery Management role group is assigned both roles.<BR>The Organization Management role group is assigned the Litigation Hold role. Members of the Organization Management role group can place an In-Place Hold on all items in a mailbox, but can't create a query-based In-Place Hold.|
|In-Place Archive|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|In-Place Archive - Test connectivity|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Information Rights Management (IRM) configuration|[Compliance Management](compliance-management-exchange-2013-help.md) <br/><br/> [Organization Management](organization-management-exchange-2013-help.md)|
|Retention policies - Apply|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Retention policies - Create|See the entry for Messaging Records Management|
|Transport rules|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
