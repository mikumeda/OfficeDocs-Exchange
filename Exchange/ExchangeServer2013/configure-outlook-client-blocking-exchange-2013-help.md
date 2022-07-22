---
title: 'Configure Outlook client blocking: Exchange 2013 Help'
TOCTitle: Configure Outlook client blocking
ms:assetid: 3a579c83-8bc7-4adc-a25c-8eb6eed7220c
ms:mtpsurl: https://technet.microsoft.com/library/Dd335207(v=EXCHG.150)
ms:contentKeyID: 50873794
ms.reviewer: 
ms.topic: article
description: How to configure Outlook client blocking in Exchange Server
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Configure Outlook client blocking

_**Applies to:** Exchange Server 2013_

In Exchange Server 2013, you can use retention policies or managed folders for messaging records management (MRM). Only users running Microsoft Outlook 2010 and later have access to all client features for retention policies. However, retention policies are applied on the Mailbox server by the Managed Folder Assistant, regardless of the Outlook client version used by the user. Older Outlook clients do not expose the MRM functionality of these features. For example, because Outlook 2007 does not support retention policies, users can't apply personal tags to items or folders.

You can block users who are running older versions of Outlook from accessing their Exchange mailboxes. You can also block access on a per-mailbox or on a per-Client Access server basis.

For other management tasks related to MRM, see [Messaging Records Management Procedures](/office365/securitycompliance/inactive-mailboxes-in-office-365).

## MRM Feature Availability by Client Application and Version

The following table lists the MRM features available in various client applications and versions.

### MRM features

|Client application|Available MRM client features|
|---|---|
|Outlook 2013 and Outlook 2010|All|
|Outlook 2007|Managed folders|
|Outlook 2003 and older|Not supported|
|Other e-mail client software|None|

The following table shows version numbers for Outlook.

### Outlook versions

|Outlook version|Version number|
|---|---|
|Outlook 2013|15|
|Outlook 2010|14|
|Outlook 2007|12|
|Outlook 2003|11|
|Outlook 2002|10|
|Outlook 2000|9|
|Outlook 98|8.5|
|Outlook 97|8|

> [!NOTE]
> Before making any changes, note that hotfixes and service pack releases may affect the client version string. Be careful when you restrict client access because server-side Exchange components must also use MAPI to log on. Some components report their client version as the component name (such as SMTP or OLE DB), while others report the Exchange build number (such as 6.0.4712.0). For this reason, avoid restricting clients that have version numbers that start with 6.&lt;_x_._x_.&gt;. For example, to prevent MAPI access completely, instead of specifying **0.0.0-6.5535.65535.65535**, specify the two ranges so that the server components can log on. For example, specify the following: **0.0.0-5.9.9; 7.0.0-**.

After you perform these procedures, be aware that when users are blocked from accessing their mailboxes, they will receive the following warning message.

|Your Exchange Server administrator has blocked the version of Outlook that you are using. Contact your administrator for assistance.|

To bypass the warning that MRM features aren't supported for e-mail clients running versions of Outlook earlier than Outlook 2010, you can use the _ManagedFolderMailboxPolicyAllowed_ parameter of the **New-Mailbox**, **Enable-Mailbox**, and **Set-Mailbox** cmdlets in the Shell. When a managed folder mailbox policy is assigned to a mailbox by using the _ManagedFolderMailboxPolicy_ parameter, the warning appears by default unless you use the _ManagedFolderMailboxPolicyAllowed_ parameter.

## What do you need to know before you begin?

- Estimated time to complete: 1 minute.

- You can't use the Exchange admin center (EAC) to perform these procedures. You must use the Shell.

- Procedures in this topic require specific permissions. See each procedure for its permissions information.

- For information about keyboard shortcuts that may apply to the procedures in this topic, see [Keyboard shortcuts in the Exchange admin center](keyboard-shortcuts-in-the-exchange-admin-center-2013-help.md).

Having problems? Ask for help in the Exchange forums. Visit the forums at [Exchange Server](https://social.technet.microsoft.com/forums/office/home?category=exchangeserver).

## Block versions of Outlook on a per-mailbox basis

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "User mailboxes" entry in the [Recipients Permissions](recipients-permissions-exchange-2013-help.md) topic.

This example blocks all Outlook versions earlier than 11.8010.8036.

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions "-11.8010.8036"
```

This example restores access to a mailbox that's blocked by a version of Outlook.

```powershell
Set-CASMailbox -Identity adam@contoso.com -MAPIBlockOutlookVersions $null
```

For detailed syntax and parameter information, see [Set-CASMailbox](/powershell/module/exchange/Set-CASMailbox).

## Block Outlook versions on a Client Access server

You need to be assigned permissions before you can perform this procedure or procedures. To see what permissions you need, see the "RPC Client Access settings" entry in the [Clients and mobile devices permissions](clients-and-mobile-devices-permissions-exchange-2013-help.md) topic.

This example blocks Outlook clients prior to version 12.0.0 from accessing the mailbox on an Exchange 2010 or later Client Access server.

> [!IMPORTANT]
> The values used with the _BlockedClientVersions_ parameter are examples. You can determine the correct client software versions by parsing the RPC Client Access log files located at `%ExchangeInstallPath%Logging\RPC Client Access`.

```powershell
Set-RpcClientAccess -Server CAS01 -BlockedClientVersions "0.0.0-5.65535.65535;7.0.0;8.02.4-11.65535.65535"
```

For detailed syntax and parameter definition, see [Set-RpcClientAccess](/powershell/module/exchange/Set-RpcClientAccess).
