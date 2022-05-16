---
title: Plus Addressing in Exchange Online
ms.author: v-bshilpa
author: Benny-54
manager: Serdars
audience: ITPro
f1.keywords:
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid:
ms.collection:
ms.custom:
description: You use plus addressing to support dynamic, disposable recipient (not sender) email addresses in your Exchange Online organization.
---

# Plus Addressing in Exchange Online

> [!NOTE]
> Starting in late April 2022, plus addressing will be turned on by default in all organzations, so the AllowPlusAddressInRecipients parameter will no longer work. After that happens, you can disable plus addressing by using the new DisablePlusAddressInRecipients as described later in this article.

As of September 2020, plus addressing (also known as _subaddressing_) is available in Exchange Online. Subaddressing is an industry-defined way to support dynamic, disposable recipient (not sender) email addresses for mailboxes.

An SMTP email address uses the basic syntax: `<local-part>@<domain>`. For example, sean@contoso.com. 

Plus addressing uses the syntax: `<local-part>+<tag>@<domain>`. For example, sean+newsletter@contoso.com. 

The original email address must be valid. The `+tag` value that you add is arbitrary, although regular character restrictions for SMTP email addresses apply (for example, no spaces). For more information about using plus addresses, see the [Using plus addresses](#using-plus-addresses) section.

Plus addressing is available in Outlook on the web (formerly known as Outlook Web App or OWA) in Exchange Online at <https://outlook.office365.com/mail/>.

By default, plus addressing support is turned off in Exchange Online. Why? Exchange Server and Exchange Online have historically supported the plus sign as a regular character in email addresses. If you have those email addresses and you turn on plus addressing in your organization, those email addresses might stop working.

When you turn on plus addressing, Exchange Online tries to resolve the full email address (for example, sean+newsletter@contoso.com) to a known mailbox. If the first resolution attempt fails, Exchange Online does a second attempt to resolve the email address without the plus sign and tag (for example, sean@contoso.com).

If inbound internet email for your on-premises organization is routed through Exchange Online, your on-premises mailboxes can also use plus addresses if those mailbox addresses are known in Exchange Online. If the on-premises mailbox addresses are unknown to Exchange Online, plus addressing won't work and message delivery will be affected.

## Enable plus addressing in Exchange Online

> [!NOTE]
> These settings won't be available after plus addressing is turned on by default in all organizations starting in late April 2022. After that happens, use the procedures described in the [Use Exchange Online PowerShell to disable plus addressing](#use-exchange-online-powershell-to-disable-plus-addressing) section to disable plus addressing in your organization.

### Use the new Exchange admin center to enable plus addressing

1. In the new Exchange admin center at <https://admin.exchange.microsoft.com>, go to **Settings** \> **Mail flow**.

2. Select **Turn on plus addressing for your organization**, and then select **Save**.

### Use Exchange Online PowerShell to enable plus addressing

1. [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

2. The command uses the following syntax:

   ```PowerShell
   Set-OrganizationConfig -AllowPlusAddressInRecipients <$true | $false>
   ```

   To enable plus addressing in your organization, run the following command:

   ```PowerShell
   Set-OrganizationConfig -AllowPlusAddressInRecipients $true
   ```

## Use Exchange Online PowerShell to disable plus addressing

> [!NOTE]
> This setting will be effective only after plus addressing is turned on by default in all organizations starting in late April 2022. Before that happens, you can disable plus addressing in your organization by using the AllowPlusAddressInRecipients parameter with the value $false as previously described. You can also proactively turn off plus addressing using this setting now so the setting will take affect after April 2022.

1. [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

2. The command uses the following syntax:

   ```PowerShell
   Set-OrganizationConfig -DisablePlusAddressInRecipients <$true | $false>
   ```

   To disable plus addressing in your organization, run the following command:

   ```PowerShell
   Set-OrganizationConfig -DisablePlusAddressInRecipients $true
   ```

## Using plus addresses

You can create new plus addresses by adding a new tag. You can use plus addresses as unique addresses for services that you sign up for. 

> [!NOTE]
>
> Some web forms don't support plus signs in email addresses.
>
> If you need to unsubscribe from an email list subscription service, some subscription services require that you use the original email address that you subscribed with. You can't unsubscribe by sending an email from a plus address.

As plus addresses are not aliases that are configured on the mailbox, they don't resolve to a user's name in Outlook clients. This limitation results in plus addresses being easily identifiable in the `To` or `CC` fields of messages. However, there might be scenarios where you can't use a plus address for a Microsoft service that needs to be associated with your mailbox.

To automatically identify and filter messages that are sent to plus addresses, use Inbox rules to act on those messages. Using the condition *Recipient address includes*, you can specify an action for messages sent to a particular plus address. For example, you can move messages sent to a plus address to a folder.
