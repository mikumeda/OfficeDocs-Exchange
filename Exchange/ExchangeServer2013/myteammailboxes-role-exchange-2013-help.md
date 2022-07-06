---
title: 'MyTeamMailboxes role: Exchange 2013 Help'
TOCTitle: MyTeamMailboxes role
ms:assetid: 269bf64a-5028-40e4-96ec-17c362a73e69
ms:mtpsurl: https://technet.microsoft.com/library/JJ673048(v=EXCHG.150)
ms:contentKeyID: 49289203
ms.reviewer: 
ms.topic: article
description: About the MyTeamMailboxes role in Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# MyTeamMailboxes role

_**Applies to:** Exchange Server 2013_

The `MyTeamMailboxes` management role enables individual users to create site mailboxes and connect them to Microsoft SharePoint sites.

## Default management role assignments

This role has role assignments to one or more role assignees. The following table indicates whether the role assignment is regular or delegating, and also indicates the management scopes applied to each assignment. The following list describes each column:

- **Regular assignment**: Regular role assignments enable the role assignee to access the permissions provided by the management role entries on this role.
- **Delegating assignment**: Delegating role assignments give the role assignee the ability to assign this role to role groups, users, or USGs.
- **Recipient read scope**: The recipient read scope determines what recipient objects the role assignee is allowed to read from Active Directory.
- **Recipient write scope**: The recipient write scope determines what recipient objects the role assignee is allowed to modify in Active Directory.
- **Configuration read scope**: The configuration read scope determines what configuration and server objects the role assignee is allowed to read from Active Directory.
- **Configuration write scope**: The configuration write scope determines what organizational and server objects the role assignee is allowed to modify in Active Directory.

### Default management role assignments for this role

|Role group|Regular assignment|Delegating assignment|Recipient read scope|Recipient write scope|Configuration read scope|Configuration write scope|
|---|:---:|:---:|---|---|---|---|
|Default role assignment policy. <br><br> For more information, see [Understanding management role assignment policies](understanding-management-role-assignment-policies-exchange-2013-help.md).|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Management](organization-management-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
