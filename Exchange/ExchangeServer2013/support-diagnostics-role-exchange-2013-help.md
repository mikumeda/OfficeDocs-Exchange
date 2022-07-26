---
title: 'Support Diagnostics role: Exchange 2013 Help'
TOCTitle: Support Diagnostics role
ms:assetid: 3ad2c628-019e-4eb7-af43-64ab2a3a2fbf
ms:mtpsurl: https://technet.microsoft.com/library/Dd876875(v=EXCHG.150)
ms:contentKeyID: 49289234
ms.reviewer: 
ms.topic: article
description: About the Support Diagnostics role in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Support Diagnostics role

_**Applies to:** Exchange Server 2013_

The `Support Diagnostics` management role enables administrators to perform advanced diagnostics under the direction of Microsoft Customer Service and Support in an organization.

> [!WARNING]
> This role grants permissions to cmdlets and scripts that should only be used under the direction of Customer Service and Support.

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
|[Organization Management](organization-management-exchange-2013-help.md)||X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
