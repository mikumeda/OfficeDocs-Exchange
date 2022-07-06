---
title: 'User Options role: Exchange 2013 Help'
TOCTitle: User Options role
ms:assetid: fb4d58f5-cc62-4ce8-b2e4-c3cc91795a12
ms:mtpsurl: https://technet.microsoft.com/library/Dd876960(v=EXCHG.150)
ms:contentKeyID: 49289475
ms.reviewer: 
ms.topic: article
description: About the User Options management role in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# User Options role

_**Applies to:** Exchange Server 2013_

The `User Options` management role enables administrators to view the Outlook Web App options of a user in an organization. This role can be used to help diagnose configuration problems.

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
|[Help Desk](help-desk-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Management](organization-management-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
