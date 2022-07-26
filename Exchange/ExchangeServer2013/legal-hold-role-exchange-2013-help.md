---
title: 'Legal Hold role: Exchange 2013 Help'
TOCTitle: Legal Hold role
ms:assetid: c98ce8ca-3477-479a-ad23-a8e6459bc4d0
ms:mtpsurl: https://technet.microsoft.com/library/Dd876939(v=EXCHG.150)
ms:contentKeyID: 49289408
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: About the Legal Hold role in Exchange 
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Legal Hold role

_**Applies to:** Exchange Server 2013_

The `Legal Hold` management role enables administrators to configure whether data within a mailbox should be retained for litigation purposes in an organization.

## Additional scope considerations

In addition to recipient scopes, the **Enable-Mailbox** cmdlet, which is included with this role, is also scoped using database configuration scopes. Database configuration scopes control which databases the cmdlet can create new mailboxes on. The database where you want to create a mailbox must be within the database scope. This applies both when you specify a database using the *Database* parameter on the **Enable-Mailbox** cmdlet, or if you allow automatic mailbox distribution to select the database for you. For more information, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

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
|[Discovery Management](discovery-management-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Management](organization-management-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
