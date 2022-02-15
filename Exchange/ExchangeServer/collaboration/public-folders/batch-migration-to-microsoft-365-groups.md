---
ms.localizationpriority: medium
ms.author: jhendr
manager: serdars
ms.topic: article
author: JoanneHendrickson
ms.prod: exchange-server-it-pro
ms.assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms.reviewer:
ms.collection:
- Strat_EX_EXOBlocker
- exchange-server
description: 'Summary: How to move your Exchange Server public folders to Microsoft 365 Groups.'
f1.keywords:
- NOCSH
audience: ITPro
title: Use batch migration to migrate Exchange Server public folders to Microsoft 365 Groups

---

# Use batch migration to migrate Exchange Server public folders to Microsoft 365 Groups

Through a process known as *batch migration*, you can move some or all of your Exchange Server public folders to Microsoft 365 Groups. Groups is a new collaboration offering from Microsoft that offers certain advantages over public folders. For more information about the features and benefits of Groups, see [Migrate your public folders to Microsoft 365 Groups](migrate-to-microsoft-365-groups.md).

This article contains the step-by-step procedures for performing the actual batch migration of your Exchange Server public folders.

## What do you need to know before you begin?

Verify that you meet all of the following conditions as you prepare your migration:

- We recommend that you read this article in its entirety, as downtime is required for some steps.

- Public folders must be hosted on **Exchange 2016 CU4** or later servers.

- In Exchange Online, you need to be a member of the Organization Management role group. This role group is different from the permissions that are assigned to you when you subscribe to Microsoft 365, Office 365, or Exchange Online. For details about how to enable the Organization Management role group, see [Manage role groups](../../permissions/role-groups.md).

- In Exchange Server, you need to be a member of the Organization Management or Server Management role groups. For details, see [Add Members to a Role Group](/previous-versions/office/exchange-server-2010/dd638143(v=exchg.141)).

- We recommend that you move user mailboxes to Microsoft 365 or Office 365 for those users who need access to Microsoft 365 Groups. For more information, see [Ways to migrate multiple email accounts to Microsoft 365 or Office 365](../../../ExchangeOnline/mailbox-migration/mailbox-migration.md).

- MRS Proxy needs to be enabled on at least one Exchange server, and that server must also host public folder mailboxes. For details, see [Enable the MRS Proxy endpoint for remote moves](../../architecture/mailbox-servers/mrs-proxy-endpoint.md).

- You can't use the Exchange admin center (EAC) to do the procedures in this article. On Exchange server, you need to use the Exchange Management Shell. In Exchange Online, you need to use Exchange Online PowerShell. For more information, see [Connect to Exchange Online PowerShell](/powershell/exchange/connect-to-exchange-online-powershell).

- Currently, you can only migrate Calendar public folders and Mail public folders to Microsoft 365 Groups. Migrating other types of public folders is not supported. Also, the target Groups need to exist in Microsoft 365 or Office 365 before the migration.

- The batch migration process copies only messages and calendar items from public folders to Microsoft 365 Groups. It doesn't copy other properties that are associated with public folder (for example, policies, rules, and permissions).

- Microsoft 365 Groups come with a 50 GB mailbox. Verify that public folder data to be migrated is less than 50 GB. Leave additional storage space for future content. The maximum size that we recommend for public folder migration is 25 GB.

- This migration is not "all or nothing". You can pick and choose specific public folders to migrate. Sub-folders of public folders are not automatically included in the migration. You need to explicitly include any sub-folders that you want to migrate. The migration allows you to map a maximum two sub-folders to a single Microsoft 365 Group mailbox.

- During the migration, existing public folders are not modified or otherwise affected by the migration. After you do the steps in the [Step 6: Lock the public folders (downtime required)](#step-6-lock-the-public-folders-downtime-required) section, users must use the target Microsoft 365 Groups instead of the original public folders that were migrated.

- You must use a single migration batch to migrate all of your public folder data. Exchange allows creating one migration batch at a time. If you attempt to create more than one migration batch simultaneously, you'll receive an error.

## Step 1: Get the scripts

The batch migration to Microsoft 365 groups requires running a number of scripts at different points in the migration. Download the scripts and their supporting files [from this location](https://www.microsoft.com/download/details.aspx?id=55985). After you download all of the scripts and files, save them to the same location, such as `c:\PFtoGroups\Scripts`.

Before you proceed, verify that you downloaded and saved the following scripts and files:

> [!NOTE]
> Be sure to save all scripts and files to the same location.

- **AddMembersToGroups.ps1**: Adds members and owners to Microsoft 365 Groups based on permissions on the source public folders.

- **AddMembersToGroups.strings.psd1**: A support file used by the `AddMembersToGroups.ps1` script.

- **LockAndSavePublicFolderProperties.ps1**. Makes public folders read-only to prevent modifications during the migration. Transfers the mail-related public folder properties, and redirects mail sent to migrated mail-enabled public folders to the target Groups. Backs up the permission entries and the mail properties before modifying them.

- **LockAndSavePublicFolderProperties.strings.psd1**: A support file used by the `LockAndSavePublicFolderProperties.ps1` script.

- **UnlockAndRestorePublicFolderProperties.ps1**: Restores access rights and mail properties of the public folders using backup files that are created by `LockandSavePublicFolderProperties.ps1`.

- **UnlockAndRestorePublicFolderProperties.strings.psd1**: A support file used by the `UnlockAndRestorePublicFolderProperties.ps1` script.

- **WriteLog.ps1**: Enables the preceding three scripts to write logs.

- **RetryScriptBlock.ps1**. Enables the `AddMembersToGroups`, `LockAndSavePublicFolderProperties`, and `UnlockAndRestorePublicFolderProperties` scripts to retry certain actions in the event of transient errors.

For details about `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1`, and `UnlockAndRestorePublicFolderProperties.ps1`, see [Migration scripts](#migration-scripts) later in this article.

## Step 2: Prepare for the migration

The following steps are required to prepare your organization for the migration:

1. Make a list of Mail public folders and Calender public folders that you want to migrate to Microsoft 365 Groups.

2. Make a list of the target Microsoft 365 Groups for each migrated public folder. You can create new Groups or use existing Groups.

   If the permissions of the public folder is set to **Author** or above, the target Microsoft 365 Group should have the **Public** privacy setting. However, users will still need to join the Group to see the public group under the **Groups** node in Outlook.

   For more information, see [Learn about Microsoft 365 Groups](https://support.microsoft.com/office/b565caa1-5c40-40ef-9915-60fdb2d97fa2)

3. Rename any public folders that contain a backslash (**\\**) in the name. Otherwise, those public folders may not get migrated correctly.

4. The migration feature named **PAW** must be enabled for your Microsoft 365 or Office 365 organization. To verify that **PAW** is enabled, run the following command in Exchange Online PowerShell:

   ```PowerShell
   Get-MigrationConfig
   ```

   If the output of the **Features** property contains the value **PAW**, the feature is enabled and you can continue to [Step 3: Create the .csv file](#step-3-create-the-csv-file).

   Existing public folder migration batches or user migration batches in any state will prevent PAW from being enabled. Complete and remove any existing migration batches until no results are returned by the `Get-MigrationBatch` cmdlet. The removal of existing migrations aren't immediately reflected in the output of `Get-MigrationConfig` cmdlet.

   After you remove all existing batches, PAW should automatically enable itself.

   After you complete this step, you can create new user migration batches.

## Step 3: Create the .csv file

Create a .csv file, which will provide input for one of the migration scripts.

The .csv file needs the following columns:

- **FolderPath**: Path of the public folder to be migrated.
- **TargetGroupMailbox**: SMTP address of the target Microsoft 365 Group. You can run the following command to see the primary SMTP address.

  ```PowerShell
  Get-UnifiedGroup -Identity <alias of the group> | Format-Table PrimarySmtpAddress
  ```

An example .csv contains the following information:

```CSV
"FolderPath","TargetGroupMailbox"
"\Sales","sales@contoso.onmicrosoft.com"
"\Sales\APAC","apacsales@contoso.onmicrosoft.com"
"\Sales\EMEA","emeasales@contoso.onmicrosoft.com"
```

You can merge a Mail public folder and a Calendar public folder into the same Microsoft 365 Group. Otherwise, a single migration batch doesn't support any other scenarios for merging multiple public folders into the same Group. Run multiple migration batches one after another to map multiple public folders to the same Microsoft 365 Group. You can have up to 500 entries in each migration batch.

## Step 4: Start the migration request

In this step, you gather information from your Exchange environment, and then you use that information in Exchange Online PowerShell to create a migration batch. After that, you start the migration.

1. On the Exchange 2016 or Exchange 2019 server, find the MRS proxy server endpoint. You'll need this information later when you run the migration request.

2. In Exchange Online PowerShell, use the information from the previous step to run the following commands. The variables in these commands will be the values from step 1.

   1. Store the the credentials of an on-premises Exchange administrator in the variable named `$Source_Credential`.

      ```PowerShell
      $Source_Credential = Get-Credential
      ```

      Enter the username in the format: `<source_domain>\<Account>`.

   2. Use the MRS proxy server information from your Exchange Server environment as described in the previous step, and save that value to the variable named `$Source_RemoteServer`.

      ```PowerShell
      $Source_RemoteServer = "<MRS proxy endpoint>"
      ```

3. In Exchange Online PowerShell, run the following command to create a migration endpoint:

   ```PowerShell
   $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential
   ```

4. Run the following command to create a new public folder to Microsoft 365 Group migration batch:

   ```PowerShell
   New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData ([System.IO.File]::ReadAllBytes('<path to .csv file>')) -PublicFolderToUnifiedGroup -SourceEndpoint  $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
   ```

   - **CSVData**: The .csv file previously created in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to use the full path to this file. If you moved the filed, be sure to use the new location.
   - **NotificationEmails**: An optional parameter that sets the email addresses for notifications about the status and progress of the migration.
   - **AutoStart**: An optional switch that starts the migration batch as soon as you create it.
   - **PublicFolderToUnifiedGroup**: Indicates that this a public folder to Microsoft 365 Groups migration.

5. This step is required only if you didn't use the `AutoStart` switch in the previous command.

   Start the migration by running the following command in Exchange Online PowerShell:

   ```PowerShell
   Start-MigrationBatch PublicFolderToGroupMigration
   ```

Although you create the migration in Exchange Online PowerShell, you can view and manage the migration in the Exchange admin center (EAC) in Exchange Online on the **Migration** page.

In Exchange Online PowerShell, you view the progress of the migration with the [Get-MigrationBatch](/powershell/module/exchange/get-migrationbatch) and [Get-MigrationUser](/powershell/module/exchange/get-migrationuser) cmdlets.

To view the **Migration** page in the EAC, do the following steps:

1. In the EAC at <https://admin.exchange.microsoft.com>, go the **Recipients** \> **Migration**.
2. Select the migration request.
3. In the **Details** pane, select **View Details**.

When the batch status is **Completed**, you can continue to [Step 5: Add members to Microsoft 365 groups from public folders](#step-5-add-members-to-microsoft-365-groups-from-public-folders).

## Step 5: Add members to Microsoft 365 groups from public folders

You can add members to the target Microsoft 365 Group. To add members to the group based on the public folder's permission entries, you need running the `AddMembersToGroups.ps1` script on the Exchange server as described in this section.

You need to synchronize user mailboxes to Exchange Online to add members to the Microsoft 365 group based on permission entries. To see which public folder permissions are eligible, see the [Migration scripts](#migration-scripts) section later in this article.

```PowerShell
.\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir "<path to backup directory>" -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

- **MappingCsv**: The .csv file that you created above in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to provide the full path to this file. If you moved the file, be sure to use the new location.
- **BackupDir**: The folder where the migration log files are stored.
- **ArePublicFoldersOnPremises**: Indicates whether public folders are located in Exchange server or in Exchange Online.
- **Credential**: The Exchange Online username and password.

After you add users to a Microsoft 365 Group, they can use it.

## Step 6: Lock the public folders (downtime required)

After you've migrated the majority of public folder data to Microsoft 365 Groups, you can run the `LockAndSavePublicFolderProperties.ps1` script on the Exchange server. This step ensures that no new data is added to public folders before the migration has completed.

> [!NOTE]
> For mail-enabled pubic folders, the script copies some properties to the target Microsoft 365 Groups (for example, email addresses) and then mail-disables the mail-enabled public folders. After you run the script, mail that sent to those public folders is redirected to the target Microsoft 365 Groups. For details, see the [Migration scripts](#migration-scripts) section later in this article.

```PowerShell
.\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir "<path to backup directory>" -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

- **MappingCsv**: The .csv file that you created in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to provide the full path to this file. If you moved the file, be sure to use the new location.
- **BackupDir**: The folder where the backup files for permission entries, mail-enabled public folder properties, and migration log files are stored. You can use these backup files if you need to roll back to public folders.
- **ArePublicFoldersOnPremises**: Indicate whether public folders are located in Exchange server or in Exchange Online.
- **Credential**: The Exchange Online username and password.

## Step 7: Finalize the public folder to Microsoft 365 Groups migration

After you've made your public folders read-only, you need to perform the migration again. This step is required for a final incremental copy of your data.

1. Before you run the migration again, you need to remove the existing batch migration by running the following command, which you can do by running the following command:

   ```PowerShell
   Remove-MigrationBatch -Identity "<name of migration batch>"
   ```

2. Create a new batch with the same .csv file by running the following command:

   ```PowerShell
   New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData ([System.IO.File]::ReadAllBytes('<path to .csv file>')) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]
   ```

   - **CSVData**: The .csv file that you created in [Step 3: Create the .csv file](#step-3-create-the-csv-file). Be sure to provide the full path to this file. If you moved the file, be sure to use the new location.
   - **NotificationEmails**: An optional parameter that sets the email addresses for notifications about the status and progress of the migration.
   - **AutoStart**: An optional switch that starts the migration batch as soon as you create it.

3. This step is required only if you didn't use the `AutoStart` switch in the previous command.

   Start the migration by running the following command in Exchange Online PowerShell:

   ```PowerShell
   Start-MigrationBatch PublicFolderToGroupMigration
   ```

When the status value of the migration batch is **Completed**, verify that all data has been copied to Microsoft 365 Groups. At that point, if you're satisfied with the Microsoft 365 Groups experience, you can begin deleting the migrated public folders from your Exchange Server environment.

> [!IMPORTANT]
> While there are supported procedures for rolling back your migration and returning to public folders, roll-back isn't possible after you delete the source public folders. For more information, see the [How do I roll back to public folders from Microsoft 365 Groups?](#how-do-i-roll-back-to-public-folders-from-microsoft-365-groups) section in this article.

## Known issues

The following known issues can occur during a typical public folder to Microsoft 365 Groups migration:

- The script that transfers email addresses from mail-enabled public folders to Microsoft 365 Groups adds the primary email address addresses of the public folder as secondary email address on the Microsoft 365 group. Exchange Online Protection (EOP) or Centralized Mail Flow might have issues sending email to the secondary email address of Microsoft 365 Groups after the migration.

- If the public folder path entry in the .csv mapping file file is invalid, no more data is copied after the invalid entry, but the status of the migration batch will  be **Completed**.

## Migration scripts

For your reference, this section provides in-depth descriptions for three of the migration scripts and the tasks they execute in your Exchange environment. You can download all scripts and supporting files [from this location](https://www.microsoft.com/download/details.aspx?id=55985).

### AddMembersToGroups.ps1

The `AddMembersToGroups.ps1` script reads the permissions of public folders and add members and owners to Microsoft 365 groups as described in the following list:

- Users with the following **permission roles** on the public folder are added as members to the Microsoft 365 Group:

  Owner, PublishingEditor, Editor, PublishingAuthor, Author

- Users with the following minimum **access rights** on the public folder are also be added as members of the Microsoft 365 Group:

  ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems

- Users with access right "Owner" on the public folder are added as owners of the Microsoft 365 Group. Users with other eligible access rights are added as members.

- You can't add security groups as members of Microsoft 365 Groups. Instead, the group membership list is expanded, and the individual users are added as members or owners on the Microsoft 365 Groups based their access rights as previously described.

- If a user has access rights on a public folder from both individual permission assignment and security group membership, the individual permissions are given preference.

  For example, the security group named "SG1" has members User1 and User2. The public folder named "PF1" has the following permission entries:

  - SG1: Author on PF1
  - User1: Owner on PF1

  In this example, User1 is added as an owner to the Microsoft 365 Group.

- When the default permission of a public folder is 'Author' or above, the script suggests the value 'Public' for the privacy setting of the target Microsoft 365 Group'.

- If you already ran the `LockAndSavePublicFolderProperties.ps1` script, you can still run the `AddMembersToGroups.ps1` script by using the parameter and value `-ArePublicFoldersLocked $true`. In this scenario, the script reads the permissions from the backup file that was created during lock-down.

### LockAndSavePublicFolderProperties.ps1

The `LockAndSavePublicFolderProperties.ps1` script takes the following actions:

1. Migrated mail-enabled public folders are mail-disabled, and their email addresses are added to the corresponding Microsoft 365 groups.
2. Permission entries on the migrated public folders are modified to make them read-only.
3. Mail properties of mail-enabled public folders and the permission entries of all the public folders are copied before any modifications are made.

If there are multiple migration batches, you should use a separate backup directory with each mapping .csv file.

The following mail properties are stored for mail-enabled public folders and their corresponding Microsoft 365 groups:

- PrimarySMTPAddress
- EmailAddresses
- ExternalEmailAddress
- EmailAddressPolicyEnabled
- GrantSendOnBehalfTo
- SendAs Trustee list

These mail properties are stored in a .csv file, which you can use if you want to roll back the migration as described in the [How do I roll back to public folders from Microsoft 365 Groups?](#how-do-i-roll-back-to-public-folders-from-microsoft-365-groups) section later in this topic.

A snapshot of mail-enabled public folder properties is also stored in a file named `PfMailProperties.csv`. This file is not necessary for rollback, but you can use it for reference.

The following mail properties are migrated from public folders to Microsoft 365 groups by the `LockAndSavePublicFolderProperties.ps1` script:

- PrimarySMTPAddress
- EmailAddresses
- SendAs Trustee list
- GrantSendOnBehalfTo

The script ensures that the **PrimarySMTPAddress** and **EmailAddresses** values of mail-enabled public folders are added as secondary email addresses on the corresponding Microsoft 365 Groups. Also, SendAs and SendOnBehalfTo permissions of users on mail-enabled public folders are given equivalent permissions in the corresponding target Groups.

#### Access rights allowed

Only the following access rights are allowed for users. This change ensures that public folders are read-only for all users:

- ReadItems
- CreateSubfolders
- FolderContact
- FolderVisible

These access rights are stored in the **ListOfAccessRightsAllowed** property. Permission entries are modified as described in the following table:

<br>

****

|Before lock down|After lock down|
|---|---|
|None|None|
|AvailabilityOnly|AvailabilityOnly|
|LimitedDetails|LimitedDetails|
|Contributor|FolderVisible|
|Reviewer|ReadItems, FolderVisible|
|NonEditingAuthor|ReadItems, FolderVisible|
|Author|ReadItems, FolderVisible|
|Editor|ReadItems, FolderVisible|
|PublishingAuthor|ReadItems, CreateSubfolders, FolderVisible|
|PublishingEditor|ReadItems, CreateSubfolders, FolderVisible|
|Owner|ReadItems, CreateSubfolders, FolderContact, FolderVisible|
|

- Access rights for users without read permissions are untouched, and they will continue to be blocked from read rights.

- For users with custom roles, any access rights that are not specified in **ListOfAccessRightsAllowed** will be removed. Users who have only access rights that aren't specified in **ListOfAccessRightsAllowed** after filtering will have their access rights set to the value **None**.

There might be an interruption in sending email to mail-enabled public folders during time when the folders are mail-disabled and the email addresses are added to Microsoft 365 Groups.

### UnlockAndRestorePublicFolderProperties.ps1

The `UnlockAndRestorePublicFolderProperties.ps1` script reassigns permissions back to public folders based on the backup that you took during the public folder lock-down. The script also mail-enables public folders that were mail-disabled. This action happens after the email addresses are removed the corresponding Microsoft 365 Groups. There might be a slight downtime during this process.

## How do I roll back to public folders from Microsoft 365 Groups?
<a name="rollback"> </a>

If you change your mind and want to return to using public folders, you can roll back the migration, as long as the following conditions are met:

- The backup files still exist.
- You didn't delete the public folders after the migration.

On your Exchange server, run the following command to restore your environment to the pre-migration state:

```PowerShell
.\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)
```

- **BackupDir**: The directory where the backup files for permission entries, mail-enabled public folder properties, and migration log files are stored. Confirm that this is the same location from [Step 6: Lock the public folders (downtime required)](#step-6-lock-the-public-folders-downtime-required).
- **ArePublicFoldersOnPremises**: Indicates whether public folders are located on-premises or in Exchange Online.
- **Credential**: The Exchange Online username and password.

Be aware that any added items or edit operations to the Microsoft 365 Groups are not copied back to public folders. In these scenarios, there will be data loss.

You can't restore a subset of public folders. All migrated public folders will be restored.

The corresponding Microsoft 365 Groups aren't deleted as part of the roll back process. You need to manually remove these Groups manually.
