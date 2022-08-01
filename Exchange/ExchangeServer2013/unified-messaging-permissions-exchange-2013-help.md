---
title: 'Unified Messaging permissions: Exchange 2013 Help'
TOCTitle: Unified Messaging permissions
ms.topic: article
description: Learn about the permissions required to perform Unified Messaging tasks on Client Access servers and Mailbox servers.
ms:assetid: d326c3bc-8f33-434a-bf02-a83cc26a5498
ms:mtpsurl: https://technet.microsoft.com/library/Dd638193(v=EXCHG.150)
ms:contentKeyID: 48385578
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Unified Messaging permissions

_**Applies to:** Exchange Server 2013_

The permissions required to perform tasks on Client Access servers that are running the Microsoft Exchange Unified Messaging Call Router service and Mailbox servers that are running the Microsoft Exchange Unified Messaging service vary depending on the procedure being performed or the cmdlet you want to run.

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

## UM component permissions

You can configure settings for the UM components and features in the following table.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|UM auto attendants|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM call answering rules|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM call data and summary reports|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|Client Access Server (UM call router service)|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM dial plans|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM hunt groups|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM IP gateways|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM mailbox policies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM mailboxes|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|UM prompts|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [UM Management](um-management-exchange-2013-help.md)|
|Mailbox server (UM service)|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
