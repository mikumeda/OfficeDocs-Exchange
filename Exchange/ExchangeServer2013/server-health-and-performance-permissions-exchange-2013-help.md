---
title: 'Server health and performance permissions: Exchange 2013 Help'
TOCTitle: Server health and performance permissions
ms:assetid: 00b23fd3-6679-4b06-a3d4-51df3112b9cd
ms:mtpsurl: https://technet.microsoft.com/library/JJ150479(v=EXCHG.150)
ms:contentKeyID: 47559932
ms.reviewer: 
ms.topic: article
description: Server health and performance permissions in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Server health and performance permissions

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

## Exchange workload management permissions

The following table lists the permissions required to perform tasks that manage the health and performance of your Exchange 2013 organization. For more information, see [Exchange workload management](exchange-workload-management-exchange-2013-help.md).

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|User throttling|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|Exchange workload throttling|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|

## Exchange event log permissions

The following table lists the permissions required to perform tasks that manage Exchange event log settings.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Exchange event log management|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
