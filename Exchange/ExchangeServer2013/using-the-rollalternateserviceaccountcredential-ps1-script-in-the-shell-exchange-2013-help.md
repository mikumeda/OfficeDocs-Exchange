---
title: 'Use the RollAlternateserviceAccountCredential.ps1 script in the shell'
TOCTitle: Using the RollAlternateserviceAccountCredential.ps1 Script in the Shell
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63937186
ms.reviewer: 
ms.topic: article
description: Use the RollAlternateServiceAccountPassword.ps1 script in Microsoft Exchange Server to update an alternate service account credential and distribute the update to specified Client Access servers
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Using the RollAlternateserviceAccountCredential.ps1 Script in the Shell

_**Applies to:** Exchange Server 2013_

You can use the RollAlternateServiceAccountPassword.ps1 script in Exchange Server 2013 to update an alternate service account credential (ASA credential) and distribute the update to specified Client Access servers.

> [!NOTE]
> The Exchange Management Shell doesn't load scripts automatically. You need to precede all scripts with **.\\** For example, to run the RollAlternateServiceAccountPassword.ps1 script, type `.\RollAlternateServiceAccountPassword.ps1`.
>
> This script is provided in English only.

For more information about how to use and write scripts, see [Scripting with the Exchange Management Shell](/powershell/module/microsoft.powershell.core/about/about_scripts).

## Syntax

```powershell
RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -
```

## Detailed Description

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "Client Access Security" entry in the Client Access Permissions topic.

## Technical Details of the Alternate Service Account Credential Script

This script facilitates setup and maintenance of the ASA credential. After you've created the ASA credential and set the appropriate Service Principle Names, you can use the script to distribute the credential to all targeted Client Access servers.

To use the script, you need to identify which servers you want to target and which credential you want to use as your ASA credential.

## Server Scope

You can choose to have the script target all the Client Access servers in the forest, all members of a particular Client Access server array, or specific servers. The available parameters are _ToEntireForest_, _ToArraryMembers_, and _ToSpecificServers_. If you target the script to specific servers or to members of a specific server array, the _Identity_ parameter need to be specified with the servers or server array names you want to target.

## Credential Source

The script can copy the alternate service account password from an existing server. Or, you can specify the account you want to use and let the script generate a new password for the account. The available parameters are _GenerateNewPasswordFor_ and _CopyFrom_. The _GenerateNewPasswordFor_ parameter requires that you specify an account string in the following format: DOMAIN\\Account Name. If you're using a computer account, you need to append "$" at the end of the account name, for example CONTOSO\\ClientServerAcct$. The _CopyFrom_ parameter takes the name of an existing Client Access server as the credential source.

## Generating a New Password for a Credential

The password is created by the script. No user input is required. The script will try to distribute the password to all target computers, and will then try to update the Active Directory account credential with the newly-generated password.

The newly-generated password is 73 characters long and will satisfy standard strong password requirements. If your password requirements differ, you may need to set the password manually and then copy it to the target servers.

To prevent service interruption, the script examines each Client Access server and maintains the current password in addition to adding the new password. After the script has run, the shared ASA credential will be able to use either of 2 passwords: the current password as stored in Active Directory or the new password that hasn't yet been set in Active Directory.

All passwords that are no longer valid, such as an expired password, will be removed from the destination servers. If the password in Active Directory can't be changed, perhaps because the password has expired, the script will attempt a password reset. This will require the account running the script to have permissions to reset either Active Directory computer account passwords or user account passwords, depending on whether your alternate service account is a computer account or a user account.

If the passwords aren't changed successfully for all target Client Access servers, updating the Active Directory password can cause an authentication failure. If the script is run in unattended mode, it won't update the Active Directory password with the new password unless all target Client Access servers have been updated successfully. If the script is run in attended mode, you will be asked whether you want to update the password in Active Directory.

## Creating a Scheduled Task to Automate Password Maintenance

If you want the script to create a scheduled task to maintain the password on an ongoing basis, use the _CreateScheduledTask_ parameter. This parameter requires a string for the name of the task you want to create.

> [!NOTE]
> Run the script and verify that it works correctly in attended mode before you create the unattended scheduled task.

The script creates a .cmd file in the folder where the script is located. It then creates a task to run that .cmd file every three weeks. You can use Windows Task Scheduler to modify the scheduled task, for example, to set it to run more or less often. By default, the task will run as the currently logged-on user. In addition, the script will only run when the user is logged on to the computer. We recommend that you modify the scheduled task to run whether the user is logged on or not. You can also choose to run it under a different account, if that account has Active Directory permissions to reset passwords as well as the Exchange Enterprise Administrator role. When creating a scheduled task, the script will automatically run in unattended mode.

## Tasks Out of Scope of the Script

The script won't manage the SPNs of the ASA credential or allow you to remove an alternate service account from a server. To remove an alternate service account from a server, see the [Turn Kerberos authentication off](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md) section in [Configuring Kerberos authentication for load-balanced Client Access servers](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md).

## Troubleshooting the Script

We recommend that you run the script and verify that it works correctly in attended mode before you create the unattended scheduled task. For troubleshooting information, see [Troubleshooting the RollAlternateServiceAccountCredential.ps1 Script](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md).

## Validating the Script

The output of the script when you run it interactively with the -verbose flag should indicate what script operations were successful. To confirm that the Client Access servers were updated, you can verify the last modified time stamp on the ASA credential. The following example generates a list of Client Access servers and the last time the alternate service account was updated.

```powershell
Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration
```

You can also examine the event log on the computer on which the script is run. The event log entries for the script are in the Application Event log and are from the source _MSExchange Management Application_. The following table lists the events that are logged and what the events mean.

### Script Event IDs and their explanations

|Event|Explanation|
|---|---|
|14001|Start|
|14002|Success (information)|
|14003|Successful but with Warnings. <br/><br/> The script encountered some issues but was able to overcome them, or user input confirmed they weren't necessary. If the script is running in interactive mode, read the script output for further warning details.|
|14004|Failed|

If the script runs as a scheduled task, its results are logged to the Exchange server **Logging** folder in a subfolder called **RollAlternateServiceAccountPassword**.

You can use the log to confirm that the task has been running successfully.

## Parameters

|Parameter|Required|Description|
|---|---|---|
|_ToEntireForest_|Optional|The _ToEntireForest_ parameter targets the script to all Client Access servers in the forest.|
|_ToArrayMembers_|Optional|The _ToArrayMembers_ parameter targets the script to all members of a specific Client Access server array. <br/><br/> **Note**: If you're using the _ToArrayMembers_ parameter or the _ToSpecificServers_ parameter, you need to specify the server names or the server array names using the _Identity_ parameter.|
|_ToSpecificServers_|Optional|The _ToSpecificServers_ parameter targets the script to specific servers. <br/><br/> **Note**: If you're using the _ToArrayMembers_ parameter or the _ToSpecificServers_ parameter, you need to specify the server names or the server array names using the _Identity_ parameter.|
|_Identity_|Required|The _Identity_ parameter specifies name of the Client Access server array or the names of the specific servers that you're targeting.|
|_GenerateNewPasswordFor&lt;String\>_|Optional|The _GenerateNewPasswordFor_ parameter specifies that the script should generate a new password for the ASA. The string value need to be the ASA account in the following format: DOMAIN\Account Name. If you're using a computer account, you need to append the $ character at the end of the account name.|
|_CopyFrom&lt;String\>_|Optional|The _CopyFrom_ parameter specifies that the credential is copied from another Client Access server. The string value specified is the name of the Client Access server.|
|_Mode_|Optional|The _Mode_ switch specifies whether the script runs in attended or unattended mode. Unattended mode doesn't prompt for user input and automatically chooses more conservative options, when necessary.|
|_CreateScheduledTask&lt;String\>_|Optional|The _CreateScheduledTask_ parameter tells the script to create a scheduled task to perform the ASA credential update. The string value is the name of the scheduled task that will be created. <br/><br/> **Note**: This script creates a .cmd file in the folder where the script is located. The scheduled task will run the .cmd file once every three weeks. You can edit the task directly in Windows Task Scheduler to change the frequency of the task.|
|_WhatIf_|Optional|The _WhatIf_ switch instructs the command to simulate the actions that it would take on the object. By using the _WhatIf_ switch, you can view what changes would occur without having to apply any of those changes. You don't have to specify a value with the _WhatIf_ switch.|
|_Confirm_|Optional|The _Confirm_ switch causes the command to pause processing and requires you to acknowledge what the command will do before processing continues. You don't have to specify a value with the _Confirm_ switch.|
|_Verbose_|Optional|The _Verbose_ parameter tells the script to perform verbose logging, so that additional information about the script's actions is written to the log file.|
|_Debug_|Optional|The _Debug_ parameter tells the script to run in debugging mode. This parameter should be used to determine why the script fails.|

## Examples

## Example 1

This example uses the script to push the credential to all Client Access servers in the forest for first-time setup.

```powershell
.\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose
```

## Example 2

This example generates a new password for a user account ASA credential and distributes the password to all members of Client Access server arrays where the name matches \*mailbox\*.

```powershell
.\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers _mailbox_ -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose
```

## Example 3

This example schedules a once-a-month automated password roll scheduled task called "Exchange-RollAsa". It will update the ASA credential for all Client Access servers in the entire forest with a new, script-generated password. The scheduled task is created, but the script is not run. When the scheduled task is run, the script runs in unattended mode.

```powershell
.\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'
```

## Example 4

This example updates the ASA credential for all Client Access servers in the Client Access server array named CAS01. It obtains the credential from the Active Directory computer account ServiceAc1 in the domain Contoso.

```powershell
.\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$"
```

## Example 5

This example shows how you can use the script to distribute the ASA to a new computer or to a computer that's being put back into service either because you're increasing the size of your server array or because you're re-introducing array members after maintenance.

You need to update the ASA credential before the Client Access server receives traffic. Copy the shared ASA credential from any Client Access server that's already configured correctly. For example, if Server A currently has a working ASA credential and you've just added Server B to the array, you can use the script to copy the credential (including the password) from Server A to Server B. This is useful if Server B was down or not yet a member of the array when the password was rolled the last time.

```powershell
.\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose
```
