---
title: Perform a Google Workspace migration to Microsoft 365 or Office 365
ms.author: jhendr
author: JoanneHendrickson
manager: serdars
audience: Admin
ms.topic: conceptual
ms.service: exchange-online
ms.localizationpriority: medium
search.appverid: MET150
f1.keywords:
- NOCSH
description: Migration instructions from Google Workspace to Microsoft 365 or Office 365 in stages by migrating users in batches.
ms.custom: seo-marvel-apr2020
---

# Perform a Google Workspace (formerly G Suite) migration to Microsoft 365 or Office 365

You can migrate the following functionalities from Google Workspace to Microsoft 365 or Office 365:

- Mail & Rules
- Calendar
- Contacts

You can migrate batches of users from Google Workspace to Microsoft 365 or Office 365, allowing a migration project to be done in stages. This migration requires that you provision all of your users who will be migrated as mail-enabled users outside of the migration process. You must specify a list of users to migrate for each batch.

All procedures in this article assume that your Microsoft 365 or Office 365 domain is verified and that your TXT records have been set up. For more information, see [Set up your domain (host-specific instructions)](/microsoft-365/admin/get-help-with-domains/set-up-your-domain-host-specific-instructions).

   > [!NOTE]
   > Google Workspace migration is not currently available for Office 365 US Government GCC High or DoD.

## Select your method of migration

You can migrate from Google Workspace using any of the following methods:

- [Automated - through the New Exchange admin center](automated-migration-neweac.md)
- [Manual - through the New Exchange admin center as well as Classic Exchange admin center](manual-gspace-migration-overview.md)
- [PowerShell](perform-gspace-migration-powershell.md)

## Migration limitations

> [!NOTE]
> The largest single email message that can be migrated is based on the transport configuration for your configuration. The default limit is 35 MB. To increase this limit, see [Office 365 now supports larger email messages](https://www.microsoft.com/en-us/microsoft-365/blog/2015/04/15/office-365-now-supports-larger-email-messages-up-to-150-mb/).

Throughput limitations for contacts and calendars completely depend on the quota restrictions for your tenant's service account on the Google Workspace side.

Other migration limitations are described in the following table:

|Data type|Limitations|
|---|---|
|Mail|Vacation settings, Automatic reply settings|
|Meeting rooms|Room bookings will not be migrated|
|Calendar|Shared calendars, cloud attachments, and event colors will not be migrated|
|Contacts|A maximum of three email addresses per contact are migrated over|
|Contacts|Gmail tags, contact URLs, and custom tags will not be migrated|

> [!TIP]
>Rules will be migrated and remain turned off by default. We advise users to verify the rules on Outlook before enabling them.
>
>If you will be [starting your migration batch with Exchange Online Powershell](perform-gspace-migration-powershell.md), as described later in this article, use the `-ExcludeFolder` parameter to prevent certain folders from being migrated. This reduces the amount of data in your migration, and the size of a user's new Exchange Online mailbox. You can identify folders you don't want to migrate by name, and you can also identify Gmail labels that apply to multiple messages in order to exclude those messages from the migration. For more information on using `-ExcludeFolder`, see [New-MigrationBatch](/powershell/module/exchange/new-migrationbatch).
>
> To skip the migration of Gmail filters, use the `-SkipRules` parameter to prevent the migration of Outlook rules. For more information on using `-SkipRules`, see [New-MigrationBatch](/powershell/module/exchange/new-migrationbatch). 

## Prerequisites

Ensure you complete the following prerequisites before initiating either manual or automated Google Workspace migration:

1. Ensure you have been assigned a project creator role and you are signed into Google Workspace with the project creator credentials.
1. Ensure you complete the following procedures before initiating the migration process:
   1. Create a subdomain for mail routing to Microsoft 365 or Office 365
   1. Create a subdomain for mail routing to your Google Workspace domain
   1. Provision users in Microsoft 365 or Office 365

For detailed information on these steps, see [Google Workspace migration prerequisites](googleworkspace-migration-prerequisites.md).
