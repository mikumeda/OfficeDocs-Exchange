---
title: Enable or Disable employee access to the new Outlook for Windows 
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

# Enable or Disable employee access to the new Outlook for Windows 

The new Outlook for Windows is enabled by default for all users with an AAD account. 

To disable the new Outlook for Windows, do the following:

 1. Go to PowerShell app, right click and select **Run as administrator**. 

 2. Enter the following command:
 
    ```PowerShell
    Connect-ExchangeOnline -UserPrincipalName <administrator email> 
    Input set-CASMailbox <Email being changed> -OneWinNativeOutlookEnabled <$true>  if  or <$false>
    ```

You can also use the following command to confirm that the new Outlook for Windows is disabled for your account:  

```PowerShell
Get-CASMailbox <email being checked> | Select * 
```

Go through the list of mail clients and confirm that `OneWinNativeOutlookEnabled` has the required value next to it. 
