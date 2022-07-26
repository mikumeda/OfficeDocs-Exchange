---
title: 'Exchange and Shell infrastructure permissions: Exchange 2013 Help'
TOCTitle: Exchange and Shell infrastructure permissions
ms:assetid: 3646a4e8-36b2-41fb-89a4-79b0963fcb11
ms:mtpsurl: https://technet.microsoft.com/library/Dd638114(v=EXCHG.150)
ms:contentKeyID: 48384969
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Exchange and Shell infrastructure permissions in Exchange Server
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Exchange and Shell infrastructure permissions

_**Applies to:** Exchange Server 2013_

The permissions required to perform tasks to configure various components of Microsoft Exchange Server 2013 depend on the procedure being performed or the cmdlet you want to run. See each of the sections in this topic for more information about their respective features.

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

> [!NOTE]
> Some features may require that you have local administrator permissions on the server you want to manage. To manage these features, you must be a member of the Local Administrators group on that server.

## Exchange infrastructure permissions

The following table lists the permissions required to perform tasks that configure general Exchange 2013 settings.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Administrator audit logging|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
|Exchange admin center configuration settings|[View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|Exchange admin center connectivity|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Exchange server configuration settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Exchange Help settings|[Organization Management](organization-management-exchange-2013-help.md)|
|Message categories|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Help Desk](help-desk-exchange-2013-help.md)|
|Product key|[Organization Management](organization-management-exchange-2013-help.md)|
|Test system health|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|View-only administrator audit logging|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md) <br/><br/> **Note**: You can also manually assign the View-Only Audit Logs management role to a management role group. For more information, see [View-Only Audit Logs role](view-only-audit-logs-role-exchange-2013-help.md).|
|Write to audit log|Users that are members of any role group or assigned any management role can write to the administrator audit log.|

## Shell infrastructure permissions

The following table lists the permissions required to perform tasks that configure features that control how the Exchange Management Shell runs.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Active Directory Domain Services server settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|Cmdlet extension agents|[Organization Management](organization-management-exchange-2013-help.md)|
|PowerShell virtual directories|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|PowerShell and WinRM installation|Local Server Administrator|
|Remote Shell|[Organization Management](organization-management-exchange-2013-help.md)|

## Federation and certificates permissions

The following table lists permissions required for performing tasks related to federation trusts, OAuth configuration, certificate management, and hybrid deployment configuration.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Certificate management|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Federation trusts, OAuth|[Organization Management](organization-management-exchange-2013-help.md)|
|Test federation trusts, OAuth|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Hybrid deployment configuration|[Organization Management](organization-management-exchange-2013-help.md)|
|Intra-Organization connectors|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [Records Management](records-management-exchange-2013-help.md)|
