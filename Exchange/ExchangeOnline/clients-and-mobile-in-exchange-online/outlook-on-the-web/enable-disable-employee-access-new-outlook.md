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

The new Outlook for Windows is enabled by default for all users with an Azure Active Directory account. You can use Exchange Online PowerShell to prevent or allow access to mailboxes by the new Outlook for Windows.

## What do you need to know before you begin?

- Estimated time to complete this procedure: 5 minutes.

- You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Outlook on the web mailbox policies" entry in the [Feature permissions in Exchange Online](../../permissions-exo/feature-permissions.md) article.

- To connect to Exchange Online PowerShell, see [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

> [!TIP]
> Having problems? Ask for help in the [Exchange Online](/answers/topics/office-exchange-server-itpro.html) forum.

## Enable or disable the new Outlook for Windows for an individual mailbox

In Exchange Online PowerShell, use the following syntax:

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

To enable the new Outlook for Windows for the mailbox, use the value $true for the OneWinNativeOutlookEnabled parameter.

## Enable or disable the new Outlook for Windows for multiple mailboxes

You can use the **Get-Mailbox**, **Get-User** or **Get-Content** cmdlets to identify the mailboxes that you want to modify. For example:

- **Filter mailboxes by attributes**: This method requires that the mailboxes all share a unique filterable attribute. For example:

  - Title, Department, or address information for user accounts as seen by the **Get-User** cmdlet.
  - CustomAttribute1 through CustomAttribute15 for mailboxes as seen by the **Get-Mailbox** cmdlet.

  For more information, see [Filterable Properties for the -Filter Parameter](/powershell/exchange/filter-properties).

  The syntax uses the following two commands: one command to identify the mailboxes, and the other to enable or disable the new Outlook for Windows for the mailbox:

    ```PowerShell
    $<VariableName> = <Get-User | Get-Mailbox> -ResultSize unlimited -Filter <Filter>
    $<VariableName> | foreach {Set-CasMailbox -Identity $_.MicrosoftOnlineServicesID -OneWinNativeOutlookEnabled <$true | $false>}
    ```

    This example disables the new Outlook for Windows for all mailboxes whose **Title** attribute contains "Vendor" or "Contractor".

    ```PowerShell
    $Mgmt = Get-User -ResultSize unlimited -Filter "(RecipientType -eq 'UserMailbox') -and (Title -like '*Vendor*' -or Title -like '*Contractor*')"
    $Mgmt | foreach {Set-CasMailbox -Identity $_.MicrosoftOnlineServicesID -OneWinNativeOutlookEnabled $false}
    ```

- **Use a list of specific mailboxes**: This method requires a text file to identify the mailboxes. Values that don't contain spaces work best (for example, the user ID or email address). The text file must contain one mailbox on each line like this:

  > akol@contoso.com <br/> ljohnston@contoso.com <br/> kakers@contoso.com

  The syntax uses the following two commands: one command to identify the mailboxes, and the other to enable or disable the new Outlook for Windows for the mailbox:

  ```PowerShell
  $<VariableName> = Get-Content "<text file>"
  $<VariableName> | foreach {Set-CasMailbox -Identity $_ -OneWinNativeOutlookEnabled <$true | $false>}
  ```

  This example disables the new Outlook for Windows for the mailboxes specified in the file C:\My Documents\Management.txt.

  ```PowerShell
  $Mgrs = Get-Content "C:\My Documents\Management.txt"
  $Mgrs | foreach {Set-CasMailbox -Identity $_ -OneWinNativeOutlookEnabled $false}
  ```

## Verify access to mailboxes by the new Outlook for Windows

To verify the new Outlook for Windows is enabled or disabled for a specific mailbox, replace \<MailboxIdentity\> with the name, alias, email address or user ID of the mailbox, and run the following command:

```PowerShell
Get-CASMailbox -Identity <MailboxIdentity> | Format-List OneWinNativeOutlookEnabled
```

The value False for the OneWinNativeOutlookEnabled property means the new Outlook for Windows is disabled for the mailbox. True or absence of value means it is enabled.

To verify if the new Outlook for Windows is enabled or disabled for all mailboxes, run the following command to verify the value of the UniversalOutlookEnabled property:

```PowerShell
Get-CASMailbox -ResultSize unlimited -Filter "RecipientTypeDetailsValue -eq 'UserMailbox'" | Format-Table Name,PrimarySMTPAddress,OneWinNativeOutlookEnabled
```
