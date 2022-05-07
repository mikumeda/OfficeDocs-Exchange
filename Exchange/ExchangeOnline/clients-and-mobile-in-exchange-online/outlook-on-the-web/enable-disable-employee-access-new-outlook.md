---
title: Enable or disable access to the new Outlook for Windows 
author: Benny-54
ms.author: v-bshilpa
manager: serdars
ms.localizationpriority: medium
description: Learn how to enable or disable the new Outlook for Windows.
ms.topic: conceptual
ms.assetid: 
ms.reviewer: 
ms.collection: 
- exchange-online
- M365-email-calendar
audience: ITPro
ms.service: exchange-online
f1.keywords:
- NOCSH

---

# Enable or disable employee access to the new Outlook for Windows

The new Outlook for Windows is enabled by default for all users with an Azure Active Directory account.

To disable the new Outlook for Windows for users, [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell) and run the following command:

```PowerShell
Set-CASMailbox -Identity <MailboxIdentity> -OneWinNativeOutlookEnabled <$true | $false>
```

\<MailboxIdentity\> is any value that uniquely identifies the mailbox. For example:

- Name
- Alias
- Email address
- User ID

This example disables the new Outlook for Windows for the specified user.

```PowerShell
Set-CASMailbox -Identity colin@contoso.onmicrosoft.com -OneWinNativeOutlookEnabled $false
```

To enable the new Outlook for Windows, use the value $true for the OneWinNativeOutlookEnabled parameter.

To verify the new Outlook for Windows is disabled for a specific user, replace \<MailboxIdentity\> with the name, alias, email address or user ID of the user, and then run the following command:

```PowerShell
Get-CASMailbox -Identity <MailboxIdentity> | Format-List UniversalOutlookEnabled
```

The value False for the UniversalOutlookEnabled property means the new Outlook for Windows is disabled for the user.

To verify if the new Outlook for Windows is enabled or disabled for all users, run the following command:

```PowerShell
Get-CASMailbox -ResultSize unlimited | Format-Table -Auto Name,UniversalOutlookEnabled
```
