---
title: 'Database Copies role: Exchange 2013 Help'
TOCTitle: Database Copies role
ms:assetid: 71a95f5b-1f75-4ae9-9ee9-515c3a19d394
ms:mtpsurl: https://technet.microsoft.com/library/Dd876905(v=EXCHG.150)
ms:contentKeyID: 49289302
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: About the Database Copies role in Exchange Server
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Database Copies role

_**Applies to:** Exchange Server 2013_

The `Database Copies` management role enables administrators to add, remove, suspend, resume, view, and update database copies on individual servers.

## Additional scope considerations

The **Set-MailboxDatabaseCopy** and **Remove-MailboxDatabaseCopy** cmdlets, which are included with this role, require that the database you want to configure or remove must be within the database scope and the database must reside on a server that's within the server scope. For more information about scopes, see [Understanding management role scopes](understanding-management-role-scopes-exchange-2013-help.md).

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
|[Organization Management](organization-management-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Server Management](server-management-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
