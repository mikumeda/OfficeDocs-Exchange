---
title: Perform manual Google Workspace migration in the new Exchange admin center in Exchange Online
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
description: Instructions for manually migrating from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches in new EAC.
ms.custom: seo-marvel-jun2021
---

# Perform a manual Google Workspace Migration to Microsoft 365 or Office 365 in the new EAC

The migration process takes several steps and can take from several hours to a couple of days depending on the amount of data you are migrating.

## Prerequisites

Before you begin Google Workspace migration:

1. Ensure you are signed into Google Workspace as a project creator.
2. You have completed the following procedures:
    1. Create a subdomain for mail routing to Microsoft 365 or Office 365
    2. Create a subdomain for mail routing to your Google Workspace domain
    3. Provision users in Microsoft 365 or Office 365

For more information, see [Prerequisites](googleworkspace-migration-prerequisites.md).

## Start a Google Workspace migration batch with the new Exchange admin center (New EAC)

> [!IMPORTANT]
> Microsoft's data migration tool is currently unaware of tools enforcing messaging records management (MRM) or archival policies. Because of this, any messages that are deleted or moved to archive by these policies will result in the migration process flagging these items as "missing". The result is perceived data loss rather than actual data loss, which makes it much harder to identify actual data loss during any content verification checks.
>
> Therefore, Microsoft strongly recommends disabling all MRM and archival policies before attempting any data migration to mailboxes.

1. In the new Exchange Admin center at <https://admin.exchange.microsoft.com/#/>, go to **Migration** and then click **Add migration batch**.

2. The migration batch wizard opens. On the first page, configure the following settings:
   - **Give migration batch a unique name**: Enter a unique name.
   - **Select the mailbox migration path**: Verify that **Migration to Exchange Online** is selected.

   When you're finished, click **Next**.

3. On the **Select the migration type** page, select **Google Workspace (Gmail) migration**, and then click **Next**

   :::image type="content" source="../media/migration-onboarding-selection_new.png" alt-text="Select Migration Type.":::

4. On the **Prerequisites for Google Workspace migration** page, expand the **Manually configure your Google Workspace for migration**. As described in the section, configure the following steps:
   1. [Create a Google Service Account](manually-configuring-gsuite-for-migration.md#create-a-google-service-account)
   2. [Enable API Usage in your project](manually-configuring-gsuite-for-migration.md#enable-api-usage-in-your-project)
   3. [Grant access to the service account for your Google tenant](manually-configuring-gsuite-for-migration.md#grant-access-to-the-service-account-for-your-google-tenant)

   When you're finished, click **Next**.

5. On the **Set a migration endpoint** page of the wizard, select one of the following options:
   - **Select the migration endpoint**: Select the existing migration endpoint from the drop down list.
   - **Create a new migration endpoint**: Select this option if you're a first-time user.

   > [!NOTE]
   > To migrate Gmail mailboxes successfully, Microsoft 365 or Office 365 needs to connect and communicate with Gmail. To do this, Microsoft 365 or Office 365 uses a migration endpoint. Migration endpoint is a technical term that describes the settings that are used to create the connection so you can migrate the mailboxes.

   If you selected **Create a new migration endpoint**, do the following steps:

   1. On the **General Information** page, configure the following settings:
      - **Migration Endpoint Name**: Enter a value.
      - **Maximum concurrent migrations**: Leave the default value 20 or change the value as required.
      - **Maximum concurrent incremental syncs**: Leave the default value 10 or change the value as required.

      When you're finished, click **Next**.

   2. On the **Gmail migration configuration** page, configure the following settings:
      - **Email address**: Enter the email address that you use to sign in to the Google Workspace.
      - JSON key: Click **Import JSON**. In the dialog that appears, find and select the downloaded JSON file, and then click **Open**.

      Once the endpoint is successfully created, it will be listed under **Select migration endpoint** drop-down.

      Select the endpoint from the drop-down list, and click **Next**.

6. On the **Add user mailboxes** page, click **Import CSV file** and navigate to the folder where you have saved the CSV file.

   If you haven't already, create a CSV file containing the set of all of the users you want to migrate. You will need its filename below. The allowed headers are:

   - **EmailAddress** (required): Contains the primary email address for an existing Microsoft 365 or Office 365 mailbox.
   - **Username** (optional). Contains the Gmail primary email address, if it differs from EmailAddress.

   ```CSV
   EmailAddress
   will@fabrikaminc.net
   user123@fabrikaminc.net
   ```

   When you're finished, click **Next**.

7. On the **Move configuration** page, enter the details and then click **Next**.

8. On the **Schedule batch migration** page, verify all the details, click **Save**, and then click **Done**.

    ![Schedule batch migration.](../media/schedule-batch1-migration.png)

    Once the batch status changes from **Syncing** to **Synced**, you need to complete the batch.

To learn more, see the following topics:

- Completion of migration batch: See [Completion of migration batch in new EAC](completion-gspace-migration-batch-neweac.md).
- How the migration happens on the backend: See [Overview of the process](how-it-all-works-in-the-backend.md).
