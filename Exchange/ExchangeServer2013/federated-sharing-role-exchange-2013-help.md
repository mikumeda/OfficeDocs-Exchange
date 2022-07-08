---
title: 'Federated Sharing role: Exchange 2013 Help'
TOCTitle: Federated Sharing role
ms:assetid: 3d81048c-24bf-447d-a1ee-7fb2974a51fd
ms:mtpsurl: https://technet.microsoft.com/library/Dd876876(v=EXCHG.150)
ms:contentKeyID: 49289238
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: About the Federated Sharing role in Exchange Server
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Federated Sharing role

_**Applies to:** Exchange Server 2013_

The `Federated Sharing` management role enables administrators to manage cross-forest and cross-organization sharing in an organization.

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
