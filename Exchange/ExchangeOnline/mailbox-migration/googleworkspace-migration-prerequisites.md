---
title: Google Workspace migration prerequisites in Exchange Online
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
description: Procedures that must be performed prior to initiating manual or automated migration
ms.custom: seo-marvel-jun2021
---

# Google Workspace migration prerequisites in Exchange Online

The following procedures must be performed before you start the process of Google Workspace migration in the order mentioned:

1. [Create a subdomain for mail routing to Microsoft 365 or Office 365](#create-a-subdomain-for-mail-routing-to-microsoft-365-or-office-365)
2. [Create a subdomain for mail routing to your Google Workspace domain](#create-a-subdomain-for-mail-routing-to-your-google-workspace-domain)
3. [Provision users in Microsoft 365 or Office 365](#provision-users-in-microsoft-365-or-office-365)

## Create a subdomain for mail routing to Microsoft 365 or Office 365

1. Go to the [Google Workspace Admin page](https://admin.google.com/AdminHome) and sign in as a Google Workspace admin for your tenant.

2. Select **Add a domain**.

   > [!NOTE]
   > The option _Add a domain_ will not be available if using the legacy free edition of G Suite.

3. Enter the domain that you will use for routing mails to Microsoft 365 or Office 365, select **User alias domain**, and then select **ADD DOMAIN & START VERIFICATION**. A subdomain of your primary domain is recommended (such as "o365.fabrikaminc.net" when "fabrikaminc.net" is your primary domain) so that it will be automatically verified. Keep track of the name of the domain you enter because you will need it for the following steps, and later in the instructions as the Target Delivery Domain when you [Create a migration batch in Microsoft 365 or Office 365](perform-gspace-migration-powershell.md#create-a-migration-batch-in-microsoft-365-or-office-365).

   > [!NOTE]
   > A sub-domain of your primary domain is recommended. If another domain (such as "fabrikaminc.onmicrosoft.com") is set, Google will send emails to each individual address with a link to verify the permission to route mail. Migration won't complete until the verification is completed.

   ![Add domain.](../media/add-a-new-domain-im8.png)

4. Follow any subsequent steps that are then required to verify your domain, making sure that the status is shown as **Active**. If you chose a subdomain of your primary domain in step 3 above, your new domain may have been verified automatically.

   ![Verify domain.](../media/verify-ownership-im9.png)

5. Log into your DNS provider and update your DNS records so that you have an MX record at the domain you created above in step 3, pointing to Microsoft 365 or Office 365. Ensure that this domain that you created above is an accepted domain in Microsoft 365 or Office 365. Follow the instructions in [Add a domain to Microsoft 365](/microsoft-365/admin/setup/add-domain) to add the Microsoft 365 or Office 365 routing domain ("o365.fabrikaminc.net") to your organization and to configure DNS to route mail to Microsoft 365 or Office 365.

> [!NOTE]
> The migration process won't be able to complete if a routing domain is used that is not verified as described above. Choosing the built-in "tenantname.onmicrosoft.com" domain for routing mail to Office 365 instead of a sub-domain of the primary Google Workspace domain occasionally causes issues that Microsoft is not able to assist with besides to recommend that the user manually verify the forwarding address or contact Google support.

## Create a subdomain for mail routing to your Google Workspace domain

1. Go to the [Google Workspace Admin page](https://admin.google.com/AdminHome) and sign in as a Google Workspace admin for your tenant.

2. Select **Add a domain**.

3. Enter the domain that you will use for routing mails to Google Workspace, select **User alias domain**, and then select **ADD DOMAIN & START VERIFICATION**. A subdomain of your primary domain is recommended (such as "gsuite.fabrikaminc.net" when "fabrikaminc.net" is your primary domain) so that it will be automatically verified.

   ![Add domain alias.](../media/add-a-new-domain-alias-im10.png)

4. Follow any subsequent steps that are then required to verify your domain, making sure that the status is shown as **Active**. If you chose a subdomain of your primary domain in step 3 above, your new domain may have been verified automatically.

   ![Verify domain.](../media/verify-ownership-im9.png)

5. Follow Google's instructions to [Set up MX records for Google Workspace Gmail](https://support.google.com/a/answer/140034) for this domain.

   > [!NOTE]
   > It may take up to 24 hours for Google to propagate this setting to all of the users in your organization.

   > [!IMPORTANT]
   > If you are using non-default Transport settings in your Microsoft 365 or Office 365 organization, you should check that mail flow will work from Office 365 to Google Workspace. Be sure that either your default Remote Domain ("\*") has Automatic Forwarding enabled, or that there is a new Remote Domain for your Google Workspace routing domain (e.g. "gsuite.fabrikaminc.net") that has Automatic Forwarding enabled.

## Check Google Cloud platform permissions

An [automated scenario](/exchange/mailbox-migration/automated-migration-neweac) requires the Google Migration admin to be able to perform the following steps:
 1. Create a Google Workspace project
 2. Create a Google Workspace service account in the project
 3. Create a service key
 4. Enable all APIs - Gmail, Calendar, Contacts

The Google Migration admin needs the following permissions to complete these steps:
- resourcemanager.projects.create
- iam.ServiceAccounts.create

The most secure way to achieve this is to assign the following roles to the Google Migration admin:
- Projector Creator
- Service Accounts Creator

Here is how you do it:
1. Navigate to https://console.developers.google.com.
2. Expand the hamburger menu in the upper right-hand corner.
   
   ![image](https://user-images.githubusercontent.com/5260172/152607089-76d8f272-3bd5-4f19-9e23-4fca882a789d.png)
   
3. Select **IAM & Admin**.
4. Select **Manage Resources**.
5. Select the appropriate resource and in the right-hand pane under the **Permissions** tab click on **Add Principal**
6. Enter your Google Migration admin login, type in "Project Creator" into the Filter and select **Project Creator**.
7. Click **Add Another Role**, type in "Create Service Accounts" into the Filter and select **Create Service Accounts**.
8. Select **Save**.

 > [!NOTE]
 > It might take up to 15 minutes to propagate role assignment changes across the globe.


## Provision users in Microsoft 365 or Office 365

Once your Google Workspace environment has been properly configured, you can complete your migration in the Exchange admin center or through the Exchange Online PowerShell.

Before proceeding with either method, make sure that Mail Users have been provisioned for every user in the organization who will be migrated (either now or eventually). If any users aren't provisioned, provision them using the instructions in [Manage mail users](../recipients-in-exchange-online/manage-mail-users.md).

For more advanced scenarios, you may be able to deploy Azure Active Directory (Azure AD) Connect to provision your Mail Users. See [Deploy Microsoft 365 Directory Synchronization in Microsoft Azure](/office365/enterprise/deploy-office-365-directory-synchronization-dirsync-in-microsoft-azure) for an overview, and [Set up directory synchronization for Microsoft 365](/office365/enterprise/set-up-directory-synchronization) for setup instructions. Then, you need to deploy an Exchange server in your on-premises environment for user management, and mail-enable your users using this server. For more information, see [How and when to decommission your on-premises Exchange servers in a hybrid deployment](../../ExchangeHybrid/decommission-on-premises-exchange.md) and [Manage mail users](/Exchange/recipients/mail-users). Once the Mail Users have been created in Microsoft 365, the Azure AD Connect may need to be disabled in order to allow the migration process to convert these users into mailboxes - see [Turn off directory synchronization for Microsoft 365](/office365/enterprise/turn-off-directory-synchronization).

We recommend that the primary address (sometimes referred to as the "User ID") for each user be at the primary domain (such as "will@fabrikaminc.net"). Typically, this means that the primary email address should match between Microsoft 365 or Office 365 and Google Workspace. If any user is provisioned with a different domain for their primary address, then that user should at least have a proxy address at the primary domain. Each user should have their `ExternalEmailAddress` point to the user in their Google Workspace routing domain ("will@gsuite.fabrikaminc.net"). The users should also have a proxy address that will be used for routing to their Microsoft 365 or Office 365 routing domain (such as "will@o365.fabrikaminc.net").

> [!NOTE]
> We recommend that the Default MRM Policy and Archive policies be disabled for these users until after their migration has been completed. When such features remain enabled during migration, there is a chance that some messages will end up being considered "missing" during the content verification process.
