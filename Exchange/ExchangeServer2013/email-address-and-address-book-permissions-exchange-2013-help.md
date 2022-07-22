---
title: 'Email address and address book permissions: Exchange 2013 Help'
TOCTitle: Email address and address book permissions
ms:assetid: 1c1de09d-16ef-4424-9bfb-eb7edffbc8c2
ms:mtpsurl: https://technet.microsoft.com/library/JJ150492(v=EXCHG.150)
ms:contentKeyID: 47559955
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Email address and address book permissions in Exchange Server 
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Email address and address book permissions

_**Applies to:** Exchange Server 2013_

The permissions required to configure email address and address book features vary depending on the procedure being performed or the cmdlet you want to run. For more information about email addresses and address books, see [Email addresses and address books](email-addresses-and-address-books-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Address book policies|[Organization Management](organization-management-exchange-2013-help.md)|
|Address lists|[Organization Management](organization-management-exchange-2013-help.md)|
|Email address policies|[Organization Management](organization-management-exchange-2013-help.md)|
|Details templates|[Organization Management](organization-management-exchange-2013-help.md)|
|Global address lists|[Organization Management](organization-management-exchange-2013-help.md)|
|Offline address books|[Organization Management](organization-management-exchange-2013-help.md)|
|Offline address book connectivity|[Organization Management](organization-management-exchange-2013-help.md)|
