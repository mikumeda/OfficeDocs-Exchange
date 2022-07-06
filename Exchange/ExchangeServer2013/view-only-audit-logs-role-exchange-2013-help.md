---
title: 'View-Only Audit Logs role: Exchange 2013 Help'
TOCTitle: View-Only Audit Logs role
ms:assetid: 9298fe59-0a16-4a09-bdb8-514d1cea6e2f
ms:mtpsurl: https://technet.microsoft.com/library/Ff461933(v=EXCHG.150)
ms:contentKeyID: 49289353
ms.reviewer: 
ms.topic: article
description: The View-Only Audit Logs management role in Microsoft Exchange Server enables administrators and specialist users to search the administrator audit logs in an organization
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# View-Only Audit Logs role

_**Applies to:** Exchange Server 2013_

The `View-Only Audit Logs` management role enables administrators and specialist users to search the administrator audit logs in an organization.

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
|[Compliance Management](compliance-management-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Management](organization-management-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
