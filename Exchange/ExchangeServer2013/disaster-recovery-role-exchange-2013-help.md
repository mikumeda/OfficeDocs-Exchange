---
title: 'Disaster Recovery role: Exchange 2013 Help'
TOCTitle: Disaster Recovery role
ms:assetid: 6dd321a8-7621-44be-b3c5-76535e006653
ms:mtpsurl: https://technet.microsoft.com/library/Dd876902(v=EXCHG.150)
ms:contentKeyID: 49289296
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: Disaster Recovery role lets you restore mailboxes and mailbox databases, create mailbox databases, and do datacenter switchovers and switchbacks.
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Disaster Recovery role

_**Applies to:** Exchange Server 2013_

The `Disaster Recovery` management role enables administrators to restore mailboxes and mailbox databases, create mailbox databases, and perform datacenter switchovers and switchbacks for database availability groups in an organization.

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
