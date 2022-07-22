---
title: 'Exchange admin center in Exchange 2013: Exchange 2013 Help'
TOCTitle: Exchange admin center in Exchange 2013
ms:assetid: a9aea11a-6ba3-4f4a-a76e-79072e7cfc7d
ms:mtpsurl: https://technet.microsoft.com/library/JJ150562(v=EXCHG.150)
ms:contentKeyID: 47560086
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: About the Exchange admin center in Exchange Server
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Exchange admin center in Exchange 2013

_**Applies to:** Exchange Server 2013_

The Exchange admin center (EAC) is the web-based management console in Microsoft Exchange Server 2013 that's optimized for on-premises, online, and hybrid Exchange deployments. The EAC replaces the Exchange Management Console (EMC) and the Exchange Control Panel (ECP), which were the two interfaces used to manage Exchange Server 2010.

One advantage a web-based EAC provides is that you can partition Internet and intranet access from within the ECP IIS virtual directory. With this functionality, you can control whether users are allowed to have Internet access to the EAC from outside of your organization, while still allowing an end user to access Outlook Web App Options. For more information, see [Turn off access to the Exchange admin center](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

Looking for the Exchange Online version of this topic? See [Exchange admin center in Exchange Online](/exchange/exchange-admin-center).

Looking for the standalone Exchange Online Protection (EOP) version of this topic? See [Exchange admin center in EOP](/microsoft-365/security/office-365-security/exchange-admin-center-eop).

## Accessing the EAC

Because the EAC is now a web-based management console, you'll need to use the ECP virtual directory URL to access the console from your web browser. In most cases the EAC's URL will look similar to the following:

- **Internal URL: `https://<CASServerName>/ecp`**: The internal URL is used to access the EAC from within your organization's firewall.

- **External URL: `https://mail.contoso.com/ecp`**: The external URL is used to access the EAC from outside of your organization's firewall. Some organizations may want to turn off external access to the EAC. For details, see [Turn off access to the Exchange admin center](turn-off-access-to-the-exchange-admin-center-exchange-2013-help.md).

To locate the internal or external URL for the EAC, you can use the [Get-EcpVirtualDirectory](/powershell/module/exchange/Get-EcpVirtualDirectory) cmdlet. For details, see [Find the internal and external URLs for the Exchange admin center](find-the-internal-and-external-urls-for-the-exchange-admin-center-exchange-2013-help.md).

If you're in a coexistence scenario, where you're running Exchange 2010 and Exchange 2013 in the same organization, and your mailbox is still housed on the Exchange 2010 Mailbox server, the browser will default to the Exchange 2010 ECP. You can access the EAC by adding the Exchange version to the URL. For example, to access the EAC whose virtual directory is hosted on the Client Access server CAS15-NA, use the following URL: `https://CAS15-NA/ecp/?ExchClientVer=15`. Conversely, if you want to access the Exchange 2010 ECP and your mailbox resides on an Exchange 2013 Mailbox server, use the following URL: `https://CAS14-NA/ecp/?ExchClientVer=14`.

## Common user interface elements in the EAC

The section describes the user interface elements that are common across the EAC.

![Exchange admin center.](images/JJ150562.cd617bc0-19ef-47d2-bba1-4e9546b12e0c(EXCHG.150).gif "Exchange admin center")

## Cross-premises navigation

The cross-premises navigation allows you to easily switch between your Exchange Online and on-premises Exchange deployments. If you don't have an Exchange Online organization, the link will direct you to the Microsoft 365 or Office 365 sign-up page. To learn more, see [Exchange Server Hybrid Deployments](../ExchangeHybrid/exchange-hybrid.md).

## Feature pane

This is the first level of navigation for most of the tasks that you'll perform in the EAC. The feature pane is similar to the console tree from the EMC in Exchange 2010. However, in Exchange 2013 the feature pane is organized by feature areas as opposed to server roles, and there are fewer clicks to find what you need.

- **Recipients**: This is where you'll manage mailboxes, groups, resource mailboxes, contacts, shared mailboxes, and mailbox migrations and moves.

- **Permissions**: This is where you'll manage administrator roles, user roles, and Outlook Web App policies.

- **Compliance management**: This is where you'll manage In-Place eDiscovery, In-Place Hold, auditing, data loss prevention (DLP), retention policies, retention tags, and journal rules.

- **Organization**: This is where you'll manage the tasks that pertain to your Exchange Organization, including federated sharing, Outlook Apps, and address lists.

- **Protection**: This is where you'll manage anti-malware protection for your organization.

- **Mail flow**: This is where you'll manage rules, delivery reports, accepted domains, email address policies, and send and receive connectors.

- **Mobile**: This is where you'll manage the mobile devices that you allow to connect to your organization. You can manage mobile device access and mobile device mailbox policies.

- **Public folders**: In Exchange 2010, you had to manage public folders by using the Public Folder Management Console, which was located outside of the EMC in the Toolbox. In Exchange 2013, public folders can be managed from within the **public folders** feature area.

- **Unified Messaging**: This is where you'll manage UM dial plans and UM IP gateways.

- **Servers**: This is where you'll manage your Mailbox and Client Access servers, databases, database availability groups (DAGs), virtual directories, and certificates.

- **Hybrid**: This is where you'll set up and configure a Hybrid organization.

## Tabs

The tabs are your second level of navigation. Each of the feature areas contains various tabs, each representing a complete feature. The only exception to this rule is the Hybrid feature area. You must first enable your organization for a hybrid deployment by using the Hybrid Configuration wizard.

## Toolbar

When you click most tabs, you'll see a toolbar. The toolbar has icons that perform a specific action. The following table describes the most common icons and their actions. To display the action associated with an icon, simply hover over the icon.

|Icon|Name|Action|
|---|---|
|![Add icon.](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif)|Add, New|Use this icon to create a new object. Some of these icons have an associated down arrow you can click to show additional objects you can create. For example, in **Recipients** \> **Mailboxes**, clicking the down arrow displays **User mailbox** and **Linked mailbox** as additional options.|
|![Edit icon.](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif)|Edit|Use this icon to edit an object.|
|![Delete icon.](images/Dd298078.14f639f6-61e8-4418-bbfb-0db14de9d2f5(EXCHG.150).gif)|Delete|Use this icon to delete an object. Some delete icons have a down arrow you can click to show additional options.|
|![Search icon.](images/Dn624163.773574d0-9b92-4cab-9f6b-81532c7418b9(EXCHG.150).gif)|Search|Use this icon to open a search box in which you can type the search phrase for an object you want to find.|
|![Refresh icon.](images/Dn624163.85f271ca-32a4-426c-842a-d2172567099d(EXCHG.150).gif)|Refresh|Use this icon to refresh the list view.|
|![More Options Icon(images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif)]|More options|Use this icon to view more actions you can perform for that tab's objects. For example, in **Recipients** \> **Mailboxes** clicking this icon shows the following options: **Disable**, **Add/Remove columns**, **Export data to a CSV file**, **Connect a mailbox**, and **Advanced search**.|
|![Up Arrow icon.](images/JJ150576.1732c727-328b-4a1a-b84d-6d7252c7dcab(EXCHG.150).gif)|Up arrow and down arrow|Use these icons to move an object's priority up or down. For example, in **Mail flow** \> **Email address policies** click the up arrow to raise the priority of an email address policy. You can also use these arrows to navigate the public folder hierarchy and to move rules up or down in the list view.|
|![Copy icon.](images/JJ657480.ed7f7abf-39d8-4f43-a918-ccb3bff87ef5(EXCHG.150).gif)|Copy|Use this icon to copy an object so you can make changes to it without changing the original object. For example, in **Permissions** \> **Admin roles**, select a role from the list view, and then click this icon to create a new role group based on an existing one.|
|![Remove icon.](images/Dd362328.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif)|Remove|Use this icon to remove an item from a list. For example, in the **Public Folder Permissions** dialog box, you can remove users from the list of users allowed to access the public folder by selecting the user and clicking this icon.|

## List view

When you select a tab, in most cases you'll see a list view. The list view in EAC is designed to remove limitations that existed in ECP. ECP can only display up to 500 objects, and if you want to view objects that aren't listed in the details pane, you need to use search and filter options to find those specific objects. In Exchange 2013, the viewable limit from within the EAC list view is approximately 20,000 objects for on-premises deployments and 10,000 objects in Exchange Online. In addition, paging is included so you can page to the results. In the **Recipients** list view, you can also configure page size and export the data to a CSV file.

## Details pane

When you select an object from the list view, information about that object is displayed in the details pane. In some cases (for example, with recipient objects) the details pane includes quick management tasks. For example, if you navigate to **Recipients** \> **Mailboxes** and select a mailbox from the list view, the details pane displays an option to enable or disable the archive for that mailbox. The details pane can also be used to bulk edit several objects. Simply press the CTRL key, select the objects you want to bulk edit, and use the options in the details pane. For example, selecting multiple mailboxes allows you to bulk update users' contact and organization information, custom attributes, mailbox quota, Outlook Web App settings, and more.

## Notifications

The EAC includes a notification viewer that displays the status of long-running processes and provides notifications when the process completes. In addition, for particularly long-running processes (such as a move requests), you can opt-in to receive email notifications.

## Me tile and Help

The _Me tile_ allows you to sign out of the EAC and sign in as a different user. From the Help ![Help Icon.](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Help Icon") drop-down menu, you can perform the following actions:

- **Help**: Click ![Help Icon.](images/JJ150562.a32eac4e-345d-4236-a284-204390aff4ee(EXCHG.150).gif "Help Icon") to view the online help content.
- **Disable Help bubble**: The Help bubble displays contextual help for fields when you create or edit and object. You can turn off the Help bubble help or turn it on if it has been disabled.
- **Copyright and Privacy**: Click the privacy or copyright link to read the copyright and privacy information for Exchange 2013.

## Supported browsers

For the best experience with the EAC, use one of the operating system and browser combinations labeled "Premium".

> [!NOTE]
> Other operating system and browser combinations not listed in the table are unsupported, including touch.

- **Premium:**: All functional features are supported and fully tested.
- **Supported:**: Has same functional feature support as premium. However, supported browsers will be missing features that the browser and operating system combination doesn't support.
- **Unsupported:**: The browser and operating system isn't supported or tested.

|Web Browser|Windows XP and<br>Windows Server 2003|Windows Vista|Windows 7 and<br>Windows Server 2008|Windows 8 and<br> Windows Server 2012|Mac OSX|Linux|
|---|:---:|:---:|:---:|:---:|:---:|:---:|
|Internet Explorer 8|Supported|Supported|Premium|Unsupported|Unsupported|Unsupported|
|Internet Explorer 9|Unsupported|Supported|Premium|Unsupported|Unsupported|Unsupported|
|Internet Explorer 10 or later|Unsupported|Supported|Premium|Premium|Unsupported|Unsupported|
|Firefox 11 or later|Supported|Supported|Premium|Premium|Premium|Supported|
|Safari 5.1 or later|Unsupported|Unsupported|Unsupported|Unsupported|Premium|Unsupported|
|Chrome 18 or later|Supported|Supported|Premium|Premium|Premium|Unsupported|
