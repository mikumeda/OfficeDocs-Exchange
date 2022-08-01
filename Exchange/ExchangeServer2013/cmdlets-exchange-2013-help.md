---
title: 'Cmdlets: Exchange 2013 Help'
TOCTitle: Cmdlets
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 49352361
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Use of cmdlets in Exchange Management Shell.
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Cmdlets

_**Applies to:** Exchange Server 2013_

A _cmdlet_, pronounced "command-let", is the smallest unit of functionality in the Exchange Management Shell. Cmdlets resemble built-in commands in other shells, for example, the `dir` command found in `cmd.exe`. Like these familiar commands, cmdlets can be called directly from the command line in the Shell and run under the context of the Shell, not as a separate process.

> [!NOTE]
> Since Microsoft Exchange Server 2007, there have been changes to how Exchange 2013 uses cmdlets internally due to the use of Windows PowerShell remoting functionality. These changes have little to no impact on how you need to use cmdlets, but they may offer additional flexibility in how you manage your Exchange servers.

Cmdlets are usually designed around repetitive administrative tasks, and, in the Shell, several hundred cmdlets are provided for Exchange-specific management tasks. These cmdlets are available in addition to the non-Exchange system cmdlets included in the basic Windows PowerShell shell design. For information about how to open the Exchange Management Shell, see [Open the Shell](/powershell/exchange/open-the-exchange-management-shell).

All cmdlets in the Shell are presented in verb-noun pairs. The verb-noun pair is always separated by a hyphen (-) without spaces, and the cmdlet nouns are always singular. Verbs refer to the action that the cmdlet takes. Nouns refer to the object on which the cmdlet takes action. For example, in the **Get-SystemMessage** cmdlet, the verb is **Get**, and the noun is **SystemMessage**. All Shell cmdlets that manage a specific feature share the same noun. The following table provides examples of some verbs available in the Shell.

> [!NOTE]
> By default, if the verb is omitted, the Shell assumes the **Get** verb. For example, when you call **Mailbox**, you retrieve the same results as when you call **Get-Mailbox**.

|Verb|Description|
|---|---|
|**Disable**|**Disable** cmdlets set the `Enabled` status of the specified Exchange object to `$False`. This prevents the object from processing data even though the object exists.|
|**Enable**|**Enable** cmdlets set the Enabled status of the specified Exchange object to `$True`. This enables the object to process data.|
|**Get**|**Get** cmdlets retrieve information about a specific Exchange object. **Note**: Most **Get** cmdlets only return summary information when you run them. To tell the **Get** cmdlet to return verbose information when you run a command, pipe the command to the **Format-List** cmdlet. For more information about the **Format-List** command, see [Working with command output](working-with-command-output-exchange-2013-help.md). For more information about pipelining, see [Pipelining](/powershell/module/microsoft.powershell.core/about/about_pipelines).|
|**Install**|**Install** cmdlets install a new object or feature on an Exchange server.|
|**Move**|**Move** cmdlets relocate the specified Exchange object from one container or server to another.|
|**New**|**New** cmdlets create new Exchange object.|
|**Remove**|**Remove** cmdlets delete the specified Exchange object.|
|**Set**|**Set** cmdlets modify the properties of an existing Exchange object.|
|**Test**|**Test** cmdlets test specific Exchange components and provide log files that you can examine.|
|**Uninstall**|**Uninstall** cmdlets remove an object or feature from an Exchange server.|

The following list of cmdlets is an example of a complete cmdlet set. This cmdlet set is used to manage the delivery status notification (DSN) message and mailbox quota message features of Exchange 2013:

- **Get-SystemMessage**

- **New-SystemMessage**

- **Remove-SystemMessage**

- **Set-SystemMessage**
