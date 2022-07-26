---
title: 'WhatIf, Confirm, and ValidateOnly switches: Exchange 2013 Help'
TOCTitle: WhatIf, Confirm, and ValidateOnly switches
ms:assetid: a850eea7-431e-49c5-b877-1ebde2a2b48f
ms:mtpsurl: https://technet.microsoft.com/library/Bb124088(v=EXCHG.150)
ms:contentKeyID: 49289365
ms.reviewer:
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about the WhatIf, Confirm, and ValidateOnly switches in Exchange 2013 PowerShell.
---

# WhatIf, Confirm, and ValidateOnly switches

_**Applies to:** Exchange Server 2013_

Both experienced administrators and script writers, and administrators who are new to Exchange and scripting, can benefit from using the _WhatIf_, _Confirm_, and _ValidateOnly_ switches. These switches let you control how your commands run and indicate exactly what a command will do before it affects data. This functionality is quite valuable as you transition from your test environment into your production environment and as you roll out new scripts or commands.

The _WhatIf_, _Confirm_, and _ValidateOnly_ switches are especially useful when you use them with commands that modify objects that are returned by using a filter or by using a **Get** command in a pipeline. This topic describes each switch and also provides an example command for each switch.

> [!IMPORTANT]
> If you want to use the _WhatIf_, _Confirm_, and _ValidateOnly_ switches with commands in a script, you must add the appropriate switch to each command in the script, and not on the command line that calls the script.

> [!NOTE]
> _WhatIf_, _Confirm_, and _ValidateOnly_ are called switch parameters. For more information about switch parameters, see [Parameters](/powershell/module/microsoft.powershell.core/about/about_parameters).

## WhatIf switch

The _WhatIf_ switch instructs the command to which it is applied to run but only to display the objects that would be affected by running the command and what changes would be made to those objects. The switch does not actually change any of those objects. When you use the _WhatIf_ switch, you can see whether the changes that would be made to those objects match your expectations, without the worry of modifying those objects.

When you run a command together with the _WhatIf_ switch, you put the _WhatIf_ switch at the end of the command, as in the following example:

```powershell
New-AcceptedDomain -Name "Contoso Domain" -DomainName "contoso.com" -WhatIf
```

When you run this example command, the following text is returned by the Shell:

```console
What if: Creating Accepted Domain "Contoso Domain" with domain name "contoso.com".
```

## Confirm switch

The _Confirm_ switch instructs the command to which it is applied to stop processing before any changes are made. The command then prompts you to acknowledge each action before it continues. When you use the _Confirm_ switch, you can step through changes to objects to make sure that changes are made only to the specific objects that you want to change. This functionality is useful when you apply changes to many objects and want precise control over the operation of the Shell. A confirmation prompt is displayed for each object before the Shell modifies the object.

By default, the Shell automatically applies the _Confirm_ switch to cmdlets that have the following verbs:

- **Clear**
- **Disable**
- **Dismount**
- **Move**
- **Remove**
- **Stop**
- **Suspend**
- **Uninstall**

When a cmdlet runs that has any of these verbs, the Shell automatically stops the command and waits for your acknowledgement before it continues to process.

If you want to manually apply the _Confirm_ switch to a command, include the _Confirm_ switch at the end of the command, as in the following example:

```powershell
Get-JournalRule | Enable-JournalRule -Confirm
```

When you run this example command, the following confirmation prompt is returned by the Shell:

```console
Confirm
Are you sure you want to perform this action?
Enabling journal rule "Litigation Journal Rule".
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

The confirmation prompt gives you the following choices:

- **\[Y\] Yes**: Type **Y** to instruct the command to continue the operation. The next operation will present another confirmation prompt. `[Y] Yes` is the default choice.

- **\[A\] Yes to All**: Type **A** to instruct the command to continue the operation and all subsequent operations. You will not receive additional confirmation prompts for the duration of this command.

- **\[N\] No**: Type **N** to instruct the command to skip this operation and continue with the next operation. The next operation will present another confirmation prompt.

- **\[L\] No to All**: Type **L** to instruct the command to skip this operation and all subsequent operations.

- **\[S\] Suspend**: Type **S** to pause the current pipeline and return to the command line. Type **Exit** to resume the pipeline.

- **\[?\] Help**: Type **?** to display confirmation prompt Help on the command line.

If you want to override the default behavior of the Shell and suppress the confirmation prompt for cmdlets on which it is automatically applied, you can include the _Confirm_ switch with a value of `$False`, as in the following example:

```powershell
Get-JournalRule | Disable-JournalRule -Confirm:$False
```

In this case, no confirmation prompt is displayed.

> [!WARNING]
> The default value of the _Confirm_ switch is <CODE>$True</CODE>. The default behavior of the Shell is to automatically display a confirmation prompt. If you suppress this default behavior, you instruct the command to suppress all confirmation prompts for the duration of that command. The command will process all objects that meet the criteria for the command without confirmation.

## ValidateOnly switch

The _ValidateOnly_ switch instructs the command to which it is applied to evaluate all the conditions and requirements that are needed to perform the operation before you apply any changes. The _ValidateOnly_ switch is available on cmdlets that may take a long time to run, have several dependencies on multiple systems, or affect critical data, such as mailboxes.

When you apply the _ValidateOnly_ switch to a command, the command runs through the whole process. The command performs each action as it would without the _ValidateOnly_ switch. But the command doesn't change any objects. When the command completes its process, it displays a summary with the results of the validation. If the validation indicates that the command was successful, you can run the command again without the _ValidateOnly_ switch.

When you run a command together with the _ValidateOnly_ switch, you put the _ValidateOnly_ switch at the end of the command.
