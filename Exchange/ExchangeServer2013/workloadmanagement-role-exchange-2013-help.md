---
title: 'WorkloadManagement role: Exchange 2013 Help'
TOCTitle: WorkloadManagement role
ms:assetid: d5c90eae-95c3-44b0-add5-a97337d17743
ms:mtpsurl: https://technet.microsoft.com/library/JJ657498(v=EXCHG.150)
ms:contentKeyID: 49289423
ms.reviewer: 
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about the WorkloadManagement role in Exchange 2013.
---

# WorkloadManagement role

_**Applies to:** Exchange Server 2013_

The `WorkloadManagement` management role enables administrators to manage workload management policies. Administrators can configure resource health definitions, workload classifications, and enable or disable workload management. Changes should only be made under the direction of Microsoft Customer Service and Support.

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
