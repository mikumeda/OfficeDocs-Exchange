---
title: 'View-Only Recipients role: Exchange 2013 Help'
TOCTitle: View-Only Recipients role
ms:assetid: 37e66b92-81d3-412f-b7a9-e1bb8cbeb468
ms:mtpsurl: https://technet.microsoft.com/library/Dd876872(v=EXCHG.150)
ms:contentKeyID: 49289230
ms.reviewer: 
ms.topic: article
description: About the View-Only Recipients management role in Microsoft Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# View-Only Recipients role

_**Applies to:** Exchange Server 2013_

The `View-Only Recipients` management role enables administrators to view the configuration of recipients, such as mailboxes, mail users, mail contacts, distribution groups, and dynamic distribution groups.

This role can be combined with roles associated with the `View-Only Configuration` role to create a role group that can view every object in the organization. For more information, see [View-Only Configuration role](view-only-configuration-role-exchange-2013-help.md).

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
|[Help Desk](help-desk-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Hygiene Management](hygiene-management-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Management](organization-management-exchange-2013-help.md)|X|X|`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
|[View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|X||`Organization`|`Organization`|`OrganizationConfig`|`OrganizationConfig`|
