---
ms.localizationpriority: null
description: Learn about the changes to Modern Dynamic distribution groups in Exchange Online.
ms.topic: article
author: JoanneHendrickson
f1.keywords:
- CSH
ms.author: jhendr
ms.reviewer:
title: Modern dynamic distribution groups in Exchange Online
audience: ITPro
ms.service: exchange-online
manager: serdars
---
# Modern Dynamic Distribution Groups in Exchange Online

> [!IMPORTANT]
> This feature will be fully released to all users in March, 2022.

Dynamic distribution groups (DDGs) in Exchange Online are being modernized to bring a more reliable, predictable, and better performing experience. This change will reduce mail delivery latency, improve service reliability, and allow you to see the members of a DDG before sending a message.

The membership list is now stored for each DDG and is updated once every 24 hours. You'll know exactly to whom the message is being sent, and it also addresses potential compliance issues. By storing the calculated list of members on the DDG object, messages can be delivered more quickly and our service will have greater reliability.

## DDG behavior changes

The changes in behavior for dynamic distribution groups in Exchange Online are described in the following table:

|Area|Old behavior|New behavior|
|---|---|---|
|Mail delivery latency|Unpredictable. The time it takes to deliver mail to a DDG depends on how complex the filters are on that DDG.|Faster and more predictable overall. You should see delivery times more in line with those for regular distribution groups.|
|Creation|DDGs could be used immediately after being created. |It takes 2 hours for the initial membership list to be calculated and be available for use.|
|Modification|DDGs could be used immediately after any changes were made|Users have to wait up to 2 hours for the membership list to be recalculated and links updated.|
|Membership list "freshness"|The list of members was up to date in real time.|The list of members for each DDG is refreshed every 24 hours.|

> [!IMPORTANT]
> The list of DDG members might become stale. For example, if a user has left a department that was used as a filter for the DDG, they might continue to receive mail that's sent to the DDG for the next 24 hours util the membership list is refreshed.
>
> Mail flow rules (also known as transport rules) are also affected by this behavior, because the membership list that the mail flow rules use is also refreshed once every 24 hours.

## View DDG members

To view the members of a DDG, replace \<DDGIdentity\> with the name, alias, or email address of the DDG and run the following command in [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell). The command returns the calculated list of members that's stored on the dynamic distribution group object.

```PowerShell
Get-DynamicDistributionGroupMember -Identity <DDGIdentity>
```

For detailed parameter and syntax information, see [Get-DynamicDistributionGroupMember](/powershell/module/exchange/get-dynamicdistributiongroupmember).

> [!NOTE]
> Don't use the old procedure for viewing members of a DDG as described in [View members of a dynamic distribution group in Exchange Online](/exchange/recipients-in-exchange-online/manage-dynamic-distribution-groups/view-group-members). The old procedure returns all users that satisfy the DDG filters at the time you run the command. The old procedure does not return the calculated list of members that are stored on the DDG object.

## Refresh the membership of a DDG

If your DDG membership list isn't updated after the next 24-hour refresh interval, you can force a membership refresh by replacing \<DDGIdentity\> with the name, alias, or email address of the DDG and running the following command in [Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell):

```PowerShell
Set-DynamicDistributionGroup -Identity <DDGIdentity> -ForceMembershipRefresh
```

For detailed syntax and parameter information, see [Set-DynamicDistributionGroup](/powershell/module/exchange/set-dynamicdistributiongroup)

> [!NOTE]
> You can run the refresh command only after more than one hour has passed since the last membership refresh.
