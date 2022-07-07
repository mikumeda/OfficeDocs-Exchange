---
title: 'OfficeExtensionApplication role: Exchange 2013 Help'
TOCTitle: OfficeExtensionApplication role
ms:assetid: a78f69b8-2403-40a0-8c86-7e0fb7b10d29
ms:mtpsurl: https://technet.microsoft.com/library/JJ657479(v=EXCHG.150)
ms:contentKeyID: 49289367
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: About the OfficeExtensionApplication role in Exchange 2013
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# OfficeExtensionApplication role

_**Applies to:** Exchange Server 2013_

The `OfficeExtensionApplication` management role enables Microsoft Office extension applications to access user mailboxes.

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
|[Organization Management](organization-management-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
