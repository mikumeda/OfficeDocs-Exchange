---
ms.topic: article
description: This article describes the roles that enable administrators to manage Unified Messaging (UM) services in an organization.
title: 'Unified Messaging role: Exchange 2013 Help'
TOCTitle: Unified Messaging role
ms:assetid: bf24aa04-5843-4cf3-83e7-3a5fa7bd3522
ms:mtpsurl: https://technet.microsoft.com/library/Dd876935(v=EXCHG.150)
ms:contentKeyID: 49289399
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Unified Messaging role

_**Applies to:** Exchange Server 2013_

The `Unified Messaging` role enables administrators to manage Unified Messaging (UM) services in an organization.

This role doesn't enable you to manage UM-specific mailbox configuration or UM prompts. To manage UM-specific mailbox configuration, use roles associated with the `UM Mailboxes `role. To manage UM prompts, use the roles associated with the `UM Prompts` role. For more information, see:

- [UM Mailboxes role](um-mailboxes-role-exchange-2013-help.md)
- [UM Prompts role](um-prompts-role-exchange-2013-help.md)

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
|[UM Management](um-management-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
