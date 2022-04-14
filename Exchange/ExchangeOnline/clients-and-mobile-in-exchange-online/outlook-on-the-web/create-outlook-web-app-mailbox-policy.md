---
ms.localizationpriority: medium
description: You can create an Outlook on the web mailbox policy to apply a common set of policy settings. Outlook on the web mailbox policies are useful for applying and standardizing settings, for example, attachment settings, for specific groups of users.
ms.topic: article
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 347207fa-cfb7-40a6-b19a-831dcdb54ad5
ms.reviewer: 
title: Create an Outlook on the web mailbox policy in Exchange Online
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH
manager: serdars

---

# Create a mailbox policy in Exchange Online for Outlook on the web and the new Outlook for Windows

You can create mailbox policies to apply settings to users in Outlook on the web (formerly known as Outlook Web App) and the new Outlook for Windows. Outlook on the web mailbox policies are useful for applying and standardizing settings, for example, attachment settings, for specific groups of users.

For more information about Outlook on the web mailbox policies, see [Outlook on the web mailbox policies](outlook-web-app-mailbox-policies.md).

## What do you need to know before you begin?

- Estimated time to complete each procedure: 5 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Outlook on the web mailbox policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions.md) topic.

- To open the Exchange admin center (EAC), see [Exchange admin center in Exchange Online](../../exchange-admin-center.md). To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts for the Exchange admin center](../../accessibility/keyboard-shortcuts-in-admin-center.md).

> [!TIP]
> Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Online](/answers/topics/office-exchange-server-itpro.html) or [Exchange Online Protection](https://social.technet.microsoft.com/forums/forefront/home?forum=FOPE).

## Use the EAC to create a mailbox policy for Outlook on the web and the new Outlook for Windows

1. In the EAC, go to **Permissions** \> **Outlook Web App policies**, and click **New** ![New icon.](../../media/ITPro_EAC_AddIcon.png)

2. In the new policy window that opens, configure the following settings:

   - **Policy name**: Enter a unique name for your policy.

   - Use the check boxes to enable or disable features. By default, the most common features are displayed. To see all features that can be enabled or disabled, click **More options**.

   **Note**: You can configure settings for individual users by using the **Set-CASMailbox** cmdlet in Exchange Online PowerShell.

3. Click **Save** to save the policy.

The following list contains the features you can configure when you create a mailbox policy using the EAC for Outlook on the web and the new Outlook for Windows:

   - **Communication management**:
      - _Instant messaging_: if enabled, users have access to instant messaging functionality such as the ability to send and receive instant messages, view presence information for other users, and change their own presence information.
      - _Text messaging_: when enabled, users can send and receive text messages and create text message notification rules using Outlook on the web and the new Outlook for Windows.
      - _Exchange ActiveSync_: if enabled, users can manage their linked mobile devices using Options in Outlook on the web.
      - _Contacts_: if Enabled, users can use Contacts in Outlook on the web and the new Outlook for Windows.
      - _LinkedIn contact sync_: if enabled, users will be able to add their LinkedIn connections to their mailbox as contacts. When a user's connection updates their information in LinkedIn, the contact will be automatically updated.
      - _Mobile device contact sync_: if enabled, users have access to personal contacts on their devices outside of Outlook on the web.
      - _All address lists_: if enabled, users can view all address lists. If it's set to Disabled, the user can only view the default global address list.

   - **Information management**:
      - _Journaling_: if enabled, the Journal folder will be visible in Outlook on the web and the new Outlook for Windows.
      - _Notes_: if enabled, the Notes folder will be visible in Outlook on the web and the new Outlook for Windows.
      - _Inbox Rules_: if enabled, a user can create and edit custom rules in Outlook on the web and the new Outlook for Windows.
      - _Recover deleted items_ if enabled, users can view items that have been deleted from the Deleted Items folder and choose whether to recover them to the Deleted Items folder or to delete them permanently using Outlook on the web and the new Outlook for Windows.

   - **Security**:
      - _Change password_: if enabled, people can change their passwords by going to Options in Outlook on the web and the new Outlook for Windows.

   - **User experience**:
      - _Themes_: if enabled, users can change the color scheme in Outlook on the web and the new Outlook for Windows.
      - _Premium client_: if enabled, users can use the standard version of Outlook on the web. If you clear the check box, users will be switched to the light version of Outlook on the web and get a simplified experience.
      - _Email signature_: if enabled, users can create a custom signature and choose whether to automatically include it in messages they send.
      - _Weather_: if enabled, users can see weather information on their calendar.
      - _Places_: if enabled, users can see location suggestions for meetings.
      - _Local events_: if enabled, users can see the events happening in their area.
      - _Interesting calendars_: if enabled, users can browse and add interesting calendars.

   - **Time management**:
      - _Calendar_: if enabled, users can use the Calendar in Outlook on the web and the new Outlook for Windows.
      - _Tasks_: if enabled, users can use Tasks in Outlook on the web and the new Outlook for Windows.
      - _Reminders and notifications_: if enabled, users will receive new email notifications and task and calendar reminders.

   - **Select how users can view and access attachments from public or private computers**:
      - _Public or shared computer - Direct file access_: if enabled, users will be able to open attachments by selecting them and then selecting Open.
      - _Private computer or OWA for Devices - Direct file access_: if enabled, users will be able to open attachments by selecting them and then selecting Open.

## Use Exchange Online PowerShell to create a mailbox policy for Outlook on the web and the new Outlook for Windows

In Exchange Online PowerShell, creating a mailbox policy for Outlook on the web and the new Outlook for Windowsis a two-step process:

1. Create the policy by using the following syntax:

   ```PowerShell
   New-OwaMailboxPolicy -Name "<Unique Name>"
   ```

   This example creates a mailbox policy for Outlook on the web and the new Outlook for Windows named Executives.

   ```PowerShell
   New-OwaMailboxPolicy -Name Policy1
   ```

    For detailed syntax and parameter information, see [New-OwaMailboxPolicy](/powershell/module/exchange/new-owamailboxpolicy).

2. Modify the default settings of the policy.

   For more information, see [Use Exchange Online PowerShell to modify Outlook on the web mailbox policies](configure-outlook-web-app-mailbox-policy-properties.md#use-exchange-online-powershell-to-modify-outlook-on-the-web-mailbox-policies).

## How do you know this worked?

To verify that you've successfully created a mailbox policy for Outlook on the web and the new Outlook for Windows:

- In the EAC, click **Permissions** \> **Outlook Web App Policies**, and look for your new mailbox policy.

To verify that you've successfully created a mailbox policy for Outlook on the web and the new Outlook for Windows, do either of the following steps:

- In the EAC, click **Permissions** \> **Outlook Web App Policies**, and verify the policy is listed. You can select the policy and click **Edit** ![Edit icon.](../../media/ITPro_EAC_EditIcon.png) to verify the properties of the policy.

- In Exchange Online PowerShell, run the following command to verify the policy is listed:

  ```PowerShell
  Get-OwaMailboxPolicy | Format-Table Name
  ```

- In Exchange Online PowerShell, replace \<Policy Name\> with the name of the policy, and run the following command to verify the settings:

  ```PowerShell
  Get-OwaMailboxPolicy -Identity "<Policy Name>"
  ```

## Next steps

To modify an existing Outlook on the web mailbox policy, see [View or configure Outlook on the web mailbox policy properties in Exchange Online](configure-outlook-web-app-mailbox-policy-properties.md).
