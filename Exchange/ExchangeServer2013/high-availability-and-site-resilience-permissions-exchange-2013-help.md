---
title: 'High availability and site resilience permissions: Exchange 2013 Help'
TOCTitle: High availability and site resilience permissions
ms:assetid: 66085107-4d4d-41c3-a425-82314acd9eee
ms:mtpsurl: https://technet.microsoft.com/library/Dd638136(v=EXCHG.150)
ms:contentKeyID: 48385175
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: High availability and site resilience permissions in Exchange Server 
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# High availability and site resilience permissions

_**Applies to:** Exchange Server 2013_

The permissions required to configure high availability vary depending on the procedure being performed or the cmdlet you want to run. For more information about high availability, see [High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

## Database availability group permissions

You can use the features in the following table to add, remove, and configure settings for database availability groups (DAGs).

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Database availability group membership|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Database Availability Groups role](database-availability-groups-role-exchange-2013-help.md)|
|Database availability group properties|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Database Availability Groups role](database-availability-groups-role-exchange-2013-help.md)|
|Database availability groups|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Database Availability Groups role](database-availability-groups-role-exchange-2013-help.md)|
|Database availability networks|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Database Availability Groups role](database-availability-groups-role-exchange-2013-help.md)|

## Mailbox database copy permissions

You can use the features in the following table to add, remove, update, and activate mailbox database copies.

|Feature|Permissions required|
|---|---|
|Database switchover|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Databases role](databases-role-exchange-2013-help.md)|
|Mailbox database copies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Database Copies role](database-copies-role-exchange-2013-help.md)|
|Server switchover|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Databases role](databases-role-exchange-2013-help.md)|
|Update a mailbox database copy|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Database Copies role](database-copies-role-exchange-2013-help.md)|
