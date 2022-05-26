---
title: Alert policies in Exchange Online
f1.keywords:
ms.author: v-smandalika
author: v-smandalika
manager: dansimp
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid:
description: This alert policy allows you to track and manage your activities. 
ms.custom:
---

# Alert policies in Exchange Online

An alert policy is the mechanism that enables you to track events related to mail flow in the new Exchange admin center (EAC). 

Alert policies can be created when your organization has fulfilled certain licensing requirements. For more information, see [Licensing requirements](#licensing-requirements).

Certain privileges/permissions are required for a user to view, create, and manage alert policies. 
For more information on the privileges/permissions regarding alert policies, see:

- [Privileges associated with alert policies](#privileges-associated-with-alert-policies).
- The section *RBAC permissions required to view alerts* in [Alert policies in Microsoft 365](/microsoft-365/compliance/alert-policies)

## Licensing requirements

Alert policies can be created and managed when your organization acquires the following licenses:

- Microsoft 365 Enterprise subscription
- Office 365 Enterprisesubscription
- Office 365 US Government E1/F1/G1 subscription
- E3/F3/G3 subscription
- E5/G5 subscription
- Office 365 GCC environment
- GCC High environment
- DoD US government environment

These licenses determine the features/functionalities which users and administrators in the organization can have access to. These are the functionalities for which the user/administrator can create alert policies.

You can create alert policies for advanced features/functionalities if your organization has acquired the following licenses:

- E5/G5 subscription
- E1/F1/G1 or E3/F3/G3 subscription and Microsoft Defender for Office 365 P2/Microsoft 365 E5 Compliance/E5 eDiscovery subscription
- Microsoft Defender for Office 365 P2/Microsoft 365 E5 Compliance/E5 eDiscovery and Audit add-on subscription, and Microsoft Defender for Office 365 P2/Microsoft 365 E5 Compliance/E5 eDiscovery subscription

## Types of alert policies

There are two types of alert policies on the **Alert policies** page, namely [System](#system-policy) and [Custom](#custom-policy).

### System policy

System policy is created by the system, by default, hence, it i also referred to as "default alert policy".

#### Characteristics of a system policy

A system alert policy is one that is:

- Marked in bold
- Labeled as **System** under **Policy type**
- Available to view by a normal user, who just needs to be included in the list of recipients and doesn't need a license

#### User tasks on system policies

The user can perform the following tasks on a system policy:
- Turn it off (by default, it is turned on)
- Choose a list of recipients and group them as the recipients entitled to receive email notifications of an alert
- Set the daily notification limit for the list of recipients

### Custom policy

Custom policy is the policy that can be manually created by the user/tenant.

## Privileges associated with alert policies

The following privileges are associated with an alert policies:

- **Security administrator**: This privilege is required for a user to create and manage alert policies.

> [!NOTE]
> Managing alert policies involve a list of tasks. For more information, see [User tasks on alert policies](#user-tasks-on-custom-policies). 

- **Security reader**:  This privilege is required if the tenant wants to just read/view an alert policy.

## User tasks on custom policies

A user with **security administrator** privileges can perform the following tasks on an alert policy:

- **Creation**: A user with **security administrator** privileges can create an alert policy, which is a custom alert policy. For information on how to create an alert policy, see [Create custom policy](#create-custom-policy). 
- **Edit**: A user can edit both the **system** and **custom** policies. For more information, see [Edit custom policy](#edit-custom-policy).
- **Disable**: A user can disable both the **system** and **custom** policies. For more information, see [Disable alert policy](#disable-alert-policy).  
- **Disable email notifications of alert policies**: A user can disable the email notifications pertaining to both **system** and **custom** policies. For more information, see [Disable email notifications](#disable-email-notifications).
- **View**: A user can view alert policies (system or custom) on the **Alerts** screen. For more information, see [View/read alert policy](#viewread-alert-policy).

### Create custom policy

To create an alert policy, perform the following steps:

1. Launch the URL https://admin.exchange.microsoft.com.
2. In the left pane, select **Mail flow > Alert policies**, and click **New alert policy**. 
3. Provide a name for your policy in the **Name** box and click **Next**.

> [!NOTE]
> Entering a description for the policy in the **Description** box is optional.

4. From the **Severity** drop-down list, select the severity level.

> [!NOTE]
> The **Category** drop-down list is disabled because **Mail flow** is the only category supported in the new EAC.

5. From the **Trigger an alert when the following insight is generated** drop-down list, select one from the following four types of insights:

- Mail loop
- Slow transport rule
- New users forwarding
- New domains being forwarded

6. Click **Next**.
7. Provide the name or email address of the alert notification recipients in the **Email recipients** box.
8. From the **Daily notification limit** drop-down list, select daily notification count.

> [!NOTE] 
> Choosing the daily-notification count value is optional.

9. Click **Next**.
10. Review the alert-policy settings and click **Create**.
    The alert policy is created.

### Edit custom policy

A user can edit the following types of alerts:

**Of custom policies**

- Domain loop
- New users forwarding emails
- Slow mailflow rules
- New domains being forwarded emails

The procedure to edit an alert policy is the same for all types of **custom** policies. For information on how to edit a custom policy, see [Edit custom policy](#edit-custom-policy).

**Of system policies**

- Messages for priority accounts are delayed or rejected
- Messages for normal accounts have been delayed

#### Edit custom policy

To edit a policy of the **custom** alert type, perform the following steps:

1. On the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
1. Select the policy that you want to edit, and click on it.
   The policy details screen appears.

   :::image type="content" source="../../media/domain-loop-alert-edit.png" alt-text="The screen displaying details of the alert policy.":::

1. Click the **Settings** tab.

   :::image type="content" source="../../media/settings-tab-domain-loop.png" alt-text="The screen displaying the settings parameters for the insight type of domain loop.":::

1. Edit the value in either or both of the following fields:
    1. Send email notifications to these users or groups.
    1. Daily notification limit
1. Click **Save**.

#### Edit system policy

This section describes the procedure to edit the following types of system policies:

- **Messages for priority accounts are delayed or rejected**: This type of system policy can be edited in two methods. For detailed information, see [First method](#first-method) and [Second method](#second-method).
- **Messages for normal accounts are delayed**: This type of system policy can be edited in the procedure identical to the one implemented for the type **Messages for priority accounts are delayed or rejected**. See [First method](#first-method).

There are two methods by which a user can edit the policy for the **system** alert type.

##### First method

1. On the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
1. Select the policy that you want to edit, and click on it.
   The policy details screen appears.

   :::image type="content" source="../../media/priority-accounts-alert-type.png" alt-text="The screen displaying the details of alert policy that has the insight type of priority accounts.":::

1. Click the **Settings** tab.
1. Edit the value in any or all of the following fields:
    1. Send email notifications to these users or groups.
    1. Daily notification limit
    1. Threshold
1. Click **Save**.

##### Second method

1. On the left navigation pane of the new EAC, select **Reports** > **Mail flow**.
1. Select the radio button for **Email issues for priority accounts**.
1. On the screen that appears, click **Edit policy**.
   The **Edit policy** screen appears.

   :::image type="content" source="../../media/priority-account-alert-type-2.png" alt-text="The screen on which you can edit the settings of an alert policy.":::

1. Edit the value in any or all of the following fields:
    1. Send email notifications to these users or groups.
    1. Daily notification limit
    1. Threshold
1. Click **Save**.

### Disable alert policy

To disable an alert policy, perform the following steps:

1. In the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
   The **Alert policies** screen appears.
1. Select the alert policy you want to disable and click on it.

   :::image type="content" source="../../media/selecting-an-alert-policy-to-disable.png" alt-text="The screen on which you select an alert policy to disable it.":::

   The alert policy details screen appears.
1. Uncheck the **Enable this policy** check box.

   :::image type="content" source="../../media/disabling-alert-policy.png" alt-text="The screen on which you disable an alert policy by unchecking the check box.":::

1. Click **Save**.
   The alert policy is disabled. The user will no longer receive any email notifications pertaining to this alert policy.

### Disable email notifications

A user has the option of disabling just the email notifications pertaining to an alert policy. This disabling results in non-receipt of email notifications of the alert policy. However, the details of the alert policy can continue to be viewed on the **Alerts** screen.

To disable the email notifications of an alert policy, perform the following steps:

1. In the left navigation pane of the new EAC, select **Mail flow** > **Alert policies**.
   The **Alert policies** screen appears.
1. Select the alert policy for which you to disable email notifications.

   :::image type="content" source="../../media/selecting-an-alert-policy-to-disable.png" alt-text="The screen on which you select an alert policy for which email notifications are to be disabled.":::

   The alert policy details screen appears.

1. Click the **Settings** tab.
1. Uncheck the **Send email notifications** check box.

   :::image type="content" source="../../media/disabling-email-notifications.png" alt-text="The screen on which the email notifications for an alert policy are disabled.":::

   The email notifications for the alert policy are disabled, and the user will no longer receive email notifications pertaining to the alert policy.

### View/read alert policy

An alert policy (**System** or **Custom**) is displayed on the **Alerts** screen. The users can view

To view/read an alert policy, perform the following steps:

1. Launch the URL https://admin.exchange.microsoft.com.
2. In the left pane, select **Mail flow > Alerts**.
   The **Alerts** screen appears, displaying reports of the various alert policies created.
3. Under the **Alert name** column, click the alert for which you want to view the details.
   The alert policy details screen appears.
4. Click **View details**.
   The screen containing elaborate details of the alert policy appears.
