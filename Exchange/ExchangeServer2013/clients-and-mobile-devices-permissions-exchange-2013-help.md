---
title: 'Clients and mobile devices permissions: Exchange 2013 Help'
TOCTitle: Clients and mobile devices permissions
ms:assetid: 57eca42a-5a7f-4c65-89f0-7a84f2dbea19
ms:mtpsurl: https://technet.microsoft.com/library/Dd638131(v=EXCHG.150)
ms:contentKeyID: 48385114
ms.topic: article
description: Permissions required to perform tasks for clients and mobile devices vary depending on the procedure or cmdlet.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Clients and mobile devices permissions

_**Applies to:** Exchange Server 2013_

The permissions required to perform tasks for clients and mobile devices vary depending on the procedure being performed or the cmdlet you want to run. For more information about client and mobile device features, see [Clients and mobile](clients-and-mobile-exchange-2013-help.md).

To find out what permissions you need to perform the procedure or run the cmdlet, do the following:

1. In the table below, find the feature that is most related to the procedure you want to perform or the cmdlet you want to run.

2. Next, look at the permissions required for the feature. You must be assigned one of those role groups, an equivalent custom role group, or an equivalent management role. You can also click on a role group to see its management roles. If a feature lists more than one role group, you only need to be assigned one of the role groups to use the feature. For more information about role groups and management roles, see [Understanding Role Based Access Control](understanding-role-based-access-control-exchange-2013-help.md).

3. Now, run the **Get-ManagementRoleAssignment** cmdlet to look at the role groups or management roles assigned to you to see if you have the permissions that are necessary to manage the feature.

    > [!NOTE]
    > You must be assigned the Role Management management role to run the **Get-ManagementRoleAssignment** cmdlet. If you don't have permissions to run the **Get-ManagementRoleAssignment** cmdlet, ask your Exchange administrator to retrieve the role groups or management roles assigned to you.

If you want to delegate the ability to manage a feature to another user, see [Delegate role assignments](delegate-role-assignments-exchange-2013-help.md).

> [!NOTE]
> Some features may require that you have local administrator permissions on the server you want to manage. To manage these features, you must be a member of the Local Administrators group on that server.

## Client Access server permissions

You can configure any of the following features for the Client Access server.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Client Access server array settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Client Access server settings|[Server Management](server-management-exchange-2013-help.md)|
|Client Access service email channel settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Client Access user settings|[Server Management](server-management-exchange-2013-help.md)|
|Client Access virtual directory settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|RPC Client Access settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|Push notification proxy settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|OAuth authentication redirection settings|[Organization Management](organization-management-exchange-2013-help.md)|

## Exchange ActiveSync permissions

You can configure any of the following for Exchange ActiveSync.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Exchange ActiveSync Autoblock settings|[Organization Management](organization-management-exchange-2013-help.md)|
|Exchange ActiveSync mailbox policy settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Exchange ActiveSync server settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Exchange ActiveSync settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Exchange ActiveSync user settings|[Recipient Management](recipient-management-exchange-2013-help.md)|
|Exchange ActiveSync virtual directory settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Mobile device mailbox policy settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Mobile device user settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|

## Autodiscover permissions

You can configure the following for the Autodiscover service.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Autodiscover service configuration settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Delegated Setup](delegated-setup-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|Autodiscover virtual directory settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|

## Availability service permissions

You can configure the following for the Availability service.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Availability service address space settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|Availability service configuration settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|

## Client throttling permissions

You can configure the following for client throttling.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Client throttling settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|

## Exchange Web Services permissions

You can configure the following for Web Services virtual directories.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Exchange Web Services virtual directory settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Test Exchange Web Services|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Test Outlook Web Services|[Organization Management](organization-management-exchange-2013-help.md)|

## Outlook Anywhere permissions

You can configure and manage the following settings for Outlook Anywhere.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Outlook Anywhere configuration (enable, disable, change, view)|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Delegated Setup](delegated-setup-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|
|RPC over HTTP Proxy component|Local Server Administrator|
|Test Outlook Anywhere connectivity|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|

## Outlook Web App permissions

You can use the following features to view Outlook Web App settings, control security and user access to Outlook Web App, and test Outlook Web App connectivity.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Graphics editor|Local Server Administrator|
|IIS Manager|Local Server Administrator|
|ISA Server 2006|ISA Server Enterprise Administrator|
|Outlook Web App mailbox policies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md)|
|Outlook Web App virtual directories|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md)|
|Registry Editor|Local Server Administrator|
|S/MIME configuration|[Organization Management](organization-management-exchange-2013-help.md)|
|Text editor|Local Server Administrator|
|View Outlook Web App mailbox policies|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Recipient Management](recipient-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md) <br/><br/> [Delegated Setup](delegated-setup-exchange-2013-help.md) <br/><br/> [Hygiene Management](hygiene-management-exchange-2013-help.md)|

## POP3 and IMAP4 permissions

You can configure the following for POP3 and IMAP4.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|IMAP4 settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|POP3 settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|Test IMAP4 settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|
|Test POP3 settings|[Organization Management](organization-management-exchange-2013-help.md) <br/><br/> [Server Management](server-management-exchange-2013-help.md) <br/><br/> [View-only Organization Management](view-only-organization-management-exchange-2013-help.md)|

## Windows PowerShell virtual directory permissions

You can configure the following for Windows PowerShell.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Test Windows PowerShell|[Organization Management](organization-management-exchange-2013-help.md)|
|Windows PowerShell settings|[Organization Management](organization-management-exchange-2013-help.md)|

## Text Messaging permissions

You can configure the following for text messaging.

Users who are assigned the View-Only Management role group can view the configuration of the features in the following table. For more information, see [View-only Organization Management](view-only-organization-management-exchange-2013-help.md).

|Feature|Permissions required|
|---|---|
|Text messaging notification settings|[Recipient Management](recipient-management-exchange-2013-help.md)|
|Text messaging settings|[Recipient Management](recipient-management-exchange-2013-help.md)|
|Text messaging user settings|[MyTextMessaging role](mytextmessaging-role-exchange-2013-help.md) <br/><br/> Users can configure text messaging settings on their own mailbox. Administrators can't configure the text messaging settings on another user's mailbox.|
