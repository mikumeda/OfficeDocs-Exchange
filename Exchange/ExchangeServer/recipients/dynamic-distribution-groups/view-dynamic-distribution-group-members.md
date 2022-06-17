---
ms.localizationpriority: medium
description: 'Summary: Learn how to use the Exchange Management Shell to view dynamic distribution group membership.'
ms.topic: article
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 40b100c6-864e-4c82-9f98-08dd5c83e378
ms.reviewer:
title: View members of a dynamic distribution group
ms.collection: exchange-server
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# View members of a dynamic distribution group

Dynamic distribution groups are distribution groups whose membership is based on specific recipient filters rather than a defined set of recipients. For more information, see [Manage dynamic distribution groups](dynamic-distribution-groups.md).

You can't use the Exchange admin center (EAC) to view the members of a dynamic distribution group. You can only use the Exchange Management Shell.

## What do you need to know before you begin?

- Estimated time to complete: 2 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Dynamic distribution groups" entry in the [Recipients Permissions](../../permissions/feature-permissions/recipient-permissions.md) topic.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](../../about-documentation/exchange-admin-center-keyboard-shortcuts.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forum at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

## Use the Exchange Management Shell to view the members of a dynamic distribution group
<a name="Shell"> </a>

To view the members of a dynamic distribution group, use the following syntax:

```PowerShell
$<VariableName> = Get-DynamicDistributionGroup -Identity <DynamicDistributionGroupIdentity>

Get-Recipient -RecipientPreviewFilter ($<VariableName>.RecipientFilter) [-OrganizationalUnit ($<VariableName>.RecipientContainer)]
```

- `<DynamicDistributionGroupIdentity>` is the name, alias, or email address of the dynamic distribution group.
- The _OrganizationalUnit_ parameter is required only if you used the _RecipientContainer_ parameter in the filter for the dynamic distribution group to specify an OU or container that's different than where the dynamic distribution group object resides (typically, the Users container). It's OK to include the _OrganizationalUnit_ parameter even if it isn't required.

This example returns the list of members for the dynamic distribution group named Full Time Employees. The first command stores the dynamic distribution group object in the variable `$FTE`. The second command uses the **Get-Recipient** cmdlet to list the recipients that match the criteria defined for the dynamic distribution group.

```PowerShell
$FTE = Get-DynamicDistributionGroup -Identity "Full Time Employees"

Get-Recipient -RecipientPreviewFilter ($FTE.RecipientFilter)
```

This example returns the members of the dynamic distribution group named Project X that exists in the Users container, but uses the OU named ContosoProjects in the filter for the group.

```powershell
$ProjectX = Get-DynamicDistributionGroup -Identity "Project X"

Get-Recipient -RecipientPreviewFilter ($ProjectX.RecipientFilter) -OrganizationalUnit ($ProjectX.RecipientContainer)
```

For detailed syntax and parameter information, see [Get-DynamicDistributionGroup](/powershell/module/exchange/get-dynamicdistributiongroup) and [Get-Recipient](/powershell/module/exchange/get-recipient).
