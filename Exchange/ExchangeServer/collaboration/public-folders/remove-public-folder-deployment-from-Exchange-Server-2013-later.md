---
title: Remove public folder deployment from Exchange Server 2013 or later versions 
ms.localizationpriority: medium
ms.author: jhendr
ms.topic: article
author: JoanneHendrickson
manager: serdars
ms.prod: exchange-server-it-pro
ms.collection:
- exchange-server
description: "Learn how to remove public folder deployment from Exchange Server 2013 or later versions."
f1.keywords:
- NOCSH
audience: ITPro

---
# Remove public folder deployment from Exchange Server 2013 or later versions 

You've migrated all the on-premises users and public folders to Exchange Online and are getting ready to remove the public folders deployment at on-premises. Performing clean removal of the on-premises public folders deployment is an essential step as improper removal can lead to issues like orphaned **Mail Enabled Public Folders (MEPFs)** and blocked SMTP addresses in Microsoft Azure Active Directory (Azure AD) or Exchange Online. 

This article lists the steps to safely remove public folders and related data from an on-premises deployment of Exchange Server 2013 or later versions. 

## Prerequisites

Before you begin, make sure that:

- You've migrated the on-premises public folders to Exchange Online. 

- There are no users on-premises or in Exchange Online that are connecting to or using public folders deployed on-premises. 

- On-premises public folder mailboxes are backed up before removal. 

- All the following steps must be performed from Exchange Management Shell with the admin account that has necessary roles assigned. 


## Clean-up mail enabled public folders

Use the Exchange Management Shell to run the PowerShell commands listed in these steps.
1. **Backup the MEPF details.** Mail Enabled Public folders don't hold any data themselves but are objects in Active Directory that are linked to public folder that hosts the actual data. Run the following:

```powershell

Set-ADServerSettings -ViewEntireForest:$true 
Get-MailPublicFolder -ResultSize Unlimited| Export-Clixml MEPF.XML
 
```

2. Disable MEPFs.

Run the following command:
 
```powershell
Set-ADServerSettings -ViewEntireForest:$true 
Get-MailPublicFolder -ResultSize Unlimited | Disable-MailPublicFolder 

```

3. Verify that no MEPFs are listed. You also might verify that there's no more object of type “PublicFolder” in any of the Microsoft Exchange System Objects OUs in your on-premises AD.

Run:

```powershell
Get-MailPublicFolder

```

4. Clear the box MEPF sync from Azure AD connect tool, if you were using the Azure AD connect tool to synchronize on-premises directory to Azure AD (this should have been unchecked already when you started the migration, but it's good to verify) 



5. Perform the Azure AD connect sync 


## Remove the public folder mailboxes

The following command locks the public folders for user connections and indicates public folder migration has been completed in the environment: 

```powershell
Set-OrganizationConfig -PublicFolderMailboxesLockedForNewConnections $true -PublicFolderMailboxesMigrationComplete $true 

```

2. Remove secondary hierarchy PF mailboxes.

```powershell
Set-ADServerSettings -ViewEntireForest:$true 

Get-Mailbox -PublicFolder -ResultSize Unlimited |?{$_.IsRootPublicFolderMailbox -ne "True"} | Remove-Mailbox -PublicFolder 

```

2. Remove the primary hierarchy PF mailbox: 

```powershell

Get-Mailbox -PublicFolder |?{$_.IsRootPublicFolderMailbox -eq "True"} | Remove-Mailbox -PublicFolder 

```
