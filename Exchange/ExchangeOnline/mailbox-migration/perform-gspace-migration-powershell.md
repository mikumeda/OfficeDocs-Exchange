---
title: Perform Google Workspace migration to Microsoft 365 or Office 365 using Exchange Online PowerShell
ms.author: v-aiyengar
author: AshaIyengar21
manager: serdars
audience: Admin
ms.topic: conceptual
ms.service: exchange-online
localization_priority: Normal
search.appverid: MET150
f1.keywords:
- NOCSH
description: Instructions for migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches using PowerShell
ms.custom: seo-marvel-jun2021
---

# Perform Google Workspace migration to Microsoft 365 or Office 365 using Exchange Online PowerShell

## Create a migration endpoint in Microsoft 365 or Office 365

1. [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

2. Find the email address for the super admin within the Google Workspace environment. This email address will be used to test connectivity between Google Workspace and Microsoft 365 or Office 365. The following steps use 'admin123' as an example.

3. Run the following command:

   ```PowerShell
   Test-MigrationServerAvailability -Gmail -ServiceAccountKeyFileData $([System.IO.File]::ReadAllBytes("C:\\somepath\\yourkeyfile.json")) -EmailAddress admin123@fabrikaminc.net
   ```

4. Verify the test is successful.

5. If successful, run the following command:

   ```PowerShell
   New-MigrationEndpoint -Gmail -ServiceAccountKeyFileData $([System.IO.File]::ReadAllBytes("C:\\somepath\\yourkeyfile.json")) -EmailAddress admin123@fabrikaminc.net -Name gmailEndpoint
   ```

## Create a migration batch in Microsoft 365 or Office 365

1. [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

2. Create a CSV file containing the set of all of the users you want to migrate. You will need its filename below. The allowed headers are:

   - EmailAddress (required). Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.

   - Username (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

   ```CSV
   EmailAddress
   will@fabrikaminc.net
   user123@fabrikaminc.net
   ```

3. Run the following command:

   ```PowerShell
   New-MigrationBatch -SourceEndpoint gmailEndpoint -Name gmailBatch -CSVData $([System.IO.File]::ReadAllBytes("C:\\somepath\\gmail.csv")) -TargetDeliveryDomain "o365.fabrikaminc.net"
   ```

   > [!TIP]
   > See [New-MigrationBatch](/powershell/module/exchange/new-migrationbatch) for an explanation of all of the individual parameters you can use with this cmdlet.

4. Run the following command to start the migration batch:

   ```PowerShell
   Start-MigrationBatch -Identity gmailBatch
   ```

   > [!NOTE]
   > When the batch starts, all the users to be migrated will be converted from MailUsers to Mailboxes. The Microsoft 365 or Office 365 Exchange license must be assigned only after this moment. You have 30 days to assign the license.

To learn more about:

- Completion of migration batch, see [Completion of migration batch in PowerShell](completion-gspae-migration-batch-powershell.md)
- How the migration happens in the backend, see [Overview of the process](how-it-all-works-in-the-backend.md)
