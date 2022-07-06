---
title: 'MyVoiceMail role: Exchange 2013 Help'
TOCTitle: MyVoiceMail role
ms:assetid: 5c7310e9-742c-4bdf-90b6-0a0d17c3bda1
ms:mtpsurl: https://technet.microsoft.com/library/Dd876890(v=EXCHG.150)
ms:contentKeyID: 49289264
ms.reviewer:
ms.topic: article
description: About the MyVoiceMail role in Exchange 2013 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# MyVoiceMail role

_**Applies to:** Exchange Server 2013_

The `MyVoiceMail` management role enables individual users to view and modify their voice mail settings.

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
|Default role assignment policy. <br><br> For more information, see [Understanding management role assignment policies](understanding-management-role-assignment-policies-exchange-2013-help.md).|X||`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
|[Organization Management](organization-management-exchange-2013-help.md)||X|`Self`|`Self`|`OrganizationConfig`|`OrganizationConfig`|
