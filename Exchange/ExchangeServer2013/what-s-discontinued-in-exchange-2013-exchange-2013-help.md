---
title: "What's discontinued in Exchange 2013: Exchange 2013 Help"
TOCTitle: What's discontinued in Exchange 2013
ms:assetid: 0ac0001c-b314-4108-b895-d9c0e271b489
ms:mtpsurl: https://technet.microsoft.com/library/JJ619283(v=EXCHG.150)
ms:contentKeyID: 49289156
ms.reviewer: 
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about what's discontinued in Exchange 2013 as compared to Exchange 2010 and Exchange 2007.
---

# What's discontinued in Exchange 2013

_**Applies to:** Exchange Server 2013_

This topic discusses the components, features, or functionality that have been removed, discontinued, or replaced in Microsoft Exchange Server 2013.

> [!NOTE]
> The following topics may also interest you:
>
> - [What's new in Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md): Information about new features and functionality in Exchange Server 2013.
> - [Exchange Online and Exchange development](/exchange/client-developer/exchange-server-development)

## Discontinued features from Exchange 2010 to Exchange 2013

This section lists the Exchange Server 2010 features that are no longer available in Exchange 2013.

## Exchange 2010 Architecture

|Feature|Comments and mitigation|
|---|---|
|Hub Transport server role|The Hub Transport server role has been replaced by Transport services which run on the Mailbox and Client Access server roles. The Mailbox server role includes the Microsoft Exchange Transport, Microsoft Exchange Mailbox Transport Delivery, and the Microsoft Exchange Mailbox Transport Submission service. The Client Access server role includes the Microsoft Exchange Frontend Transport service. For more information, see [Mail flow](mail-flow-exchange-2013-help.md).|
|Unified Messaging server role|The Unified Messaging server role has been replaced by Unified Messaging services which run on the Mailbox and Client Access server roles. The Mailbox server role includes the Microsoft Exchange Unified Messaging service and the Client Access server role includes the Microsoft Exchange Unified Messaging Call Router service. For more information, see [Voice architecture changes](voice-architecture-changes-exchange-2013-help.md).|

## Exchange 2010 Management interfaces

|Feature|Comments and mitigation|
|---|---|
|Exchange Management Console and Exchange Control Panel|The Exchange Management Console and the Exchange Control Panel have been replaced by the Exchange admin center (EAC). EAC uses the same virtual directory (/ecp) as the Exchange Control Panel. For more information, see [Exchange admin center in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).|

## Exchange 2010 Client access

|Feature|Comments and mitigation|
|---|---|
|Outlook 2003 is not supported|To connect Microsoft Outlook to Exchange 2013, the use of the Autodiscover service is required. However, Microsoft Outlook 2003 doesn't support the use of the Autodiscover service.|
|RPC/TCP access for Outlook clients|In Exchange 2013, Microsoft Outlook clients can connect using Outlook Anywhere (RPC/HTTP) or MAPI over HTTP in Exchange 2013 Service Pack 1 and Outlook 2013 Service Pack 1 and later. If you have Outlook clients in your organization, using Outlook Anywhere and/or MAPI over HTTP is required. For more information, see [Outlook Anywhere](outlook-anywhere-exchange-2013-help.md) and [MAPI over HTTP](mapi-over-http-exchange-2013-help.md).|

## Exchange 2010 Outlook Web App and Outlook

|Feature|Comments and mitigation|
|---|---|
|Spell check|Outlook Web App no longer has built-in spell check services. Instead, it uses the spell check features in your Web browsers.|
|Customizable filters|Outlook Web App no longer has customizable filtered views and no longer supports saving filtered views to Favorites. Customizable filters have been replaced by fixed filters that can be used to view all messages, unread messages, messages sent to the user, or flagged messages.|
|Message flags|The ability to set a custom date on a message flag isn't available in Outlook Web App. You can use Outlook to set custom dates.|
|Chat contact list|The chat contact list that appeared in the folder list in Outlook Web App for Exchange 2010 is no longer available.|
|Search folders|The ability for users to use Search folders isn't currently available in Outlook Web App.|

## Exchange 2010 Mail flow

|Feature|Comments and mitigation|
|---|---|
|Linked connectors|The ability to link a Send connector to a Receive connector has been removed. Specifically, the _LinkedReceiveConnector_ parameter has been removed from [New-SendConnector](/powershell/module/exchange/New-SendConnector) and [Set-SendConnector](/powershell/module/exchange/Set-SendConnector).|

## Exchange 2010 Anti-spam and anti-malware

|Feature|Comments and mitigation|
|---|---|
|Anti-spam agent management in the EMC|In Exchange 2010, when you enabled the anti-spam agents on a Hub Transport server, you could manage the anti-spam agents in the Exchange Management Console (EMC). In Exchange 2013, when you enable the anti-spam agents on a Mailbox server, you can't manage the agents using the EAC. You can only use the Shell. For information about how to enable the anti-spam agents on a Mailbox server, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md).|
|Connection Filtering agent on Hub Transport servers|In Exchange 2010, when you enabled the anti-spam agents on a Hub Transport server, the Attachment Filter agent was the only anti-spam agent that wasn't available. In Exchange 2013, when you enable the anti-spam agents on a Mailbox server, the Attachment Filter agent and the Connection Filtering agent aren't available. The Connection Filtering agent provides IP Allow List and IP Block List capabilities. For information about how to enable the anti-spam agents on a Mailbox server, see [Enable anti-spam functionality on Mailbox servers](enable-anti-spam-functionality-on-mailbox-servers-exchange-2013-help.md). <br><br> **Note**: You can't enable the anti-spam agents on an Exchange 2013 Client Access server. Therefore, the only way to get the Connection Filtering agent is to install an Edge Transport server in the perimeter network. For more information, see [Edge Transport servers](edge-transport-servers-exchange-2013-help.md).|

## Exchange 2010 Messaging policy and compliance

|Feature|Comments and mitigation|
|---|---|
|Managed Folders|In Exchange 2010, you use managed folders for messaging retention management (MRM). In Exchange 2013, managed folders aren't supported. You must use retention policies for MRM. <br><br> **Note**: Cmdlets related to managed folders are still available. You can create managed folders, managed content settings and managed folder mailbox policies, and apply a managed folder mailbox policy to a user, but the MRM assistant skips processing of mailboxes that have a managed folder mailbox policy applied.|
|Port Managed Folder wizard|In Exchange 2010, you use the Port Managed Folder wizard to create retention tags based on managed folder and managed content settings. In Exchange 2013, the Exchange admin center doesn't include this functionality. You can use the **New-RetentionPolicyTag** cmdlet with the _ManagedFolderToUpgrade_ parameter to create a retention tag based on a managed folder.|

## Exchange 2010 Unified Messaging and voice mail

|Feature|Comments and mitigation|
|---|---|
|Directory lookups using Automatic Speech Recognition (ASR)|In Exchange 2010, Outlook Voice Access users can use speech inputs using Automatic Speech Recognition (ASR) to search for users listed in the directory. Speech inputs could be also used in Outlook Voice Access to navigate menus, messages, and other options. However, even if an Outlook Voice Access user is able to use speech inputs, they have to use the telephone key pad to enter their PIN, and navigate personal options. <br><br> In Exchange 2013, authenticated and non-authenticated Outlook Voice Access users can't search for users in the directory using speech inputs or ASR in any language. However, callers that call into an auto attendant can use speech inputs in multiple languages to navigate auto attendant menus and search for users in the directory.|

## Exchange 2010 Tools

|Feature|Comments and mitigation|
|---|---|
|Exchange Best Practice Analyzer|In Exchange 2010, the Exchange Best Practice Analyzer examined your Exchange deployment and determined whether the configuration was in line with Microsoft best practices. In Exchange 2013, the Exchange Best Practice Analyzer has been replaced by the [Office 365 Best Practices Analyzer for Exchange Server 2013](https://techcommunity.microsoft.com/t5/exchange-team-blog/beta-of-microsoft-office-365-best-practices-analyzer-for/ba-p/591294).|
|Mail flow troubleshooter|In Exchange 2010, the mail flow troubleshooter assisted you in troubleshooting common mail flow problems. In Exchange 2013, the mail flow troubleshooter has been retired. You can now use the messaging tracking feature in EAC in Exchange 2013. For more information, see [Track messages with delivery reports](track-messages-with-delivery-reports-exchange-2013-help.md).|
|Performance monitor|In Exchange 2010, the Performance Monitor was included in the Exchange toolbox to allow you to collect information about the performance of your messaging system. Performance Monitor is commonly used to view key parameters while troubleshooting performance problems. In Exchange 2013, the Performance Monitor has been retired from the toolbox. You can still find the Performance Monitor under **Administrative Tools** in Windows Server 2008.|
|Performance troubleshooter|In Exchange 2013, the Performance Troubleshooter has been retired.|
|Routing Log Viewer|In Exchange 2013, the routing log viewer has been retired.|

## Exchange 2010 Mailbox database copies

|Feature|Comments and mitigation|
|---|---|
|**Update-MailboxDatabaseCopy** <br><br> Update Mailbox Database Copy wizard|Content index catalog seeding is no longer possible over the replication network; it can only be done over a MAPI network. This is true even when you use the _Network_ parameter in the **Update-MailboxDatabaseCopy** cmdlet.|

## Discontinued features from Exchange 2007 to Exchange 2013

This section lists the Exchange Server 2007 features that are no longer available in Exchange 2013.

## Exchange 2007 APIs and development

|Feature|Comments and mitigation|
|---|---|
|Exchange WebDAV|Use [Exchange Web Services (EWS) or the EWS Managed API](/exchange/client-developer/exchange-web-services/explore-the-ews-managed-api-ews-and-web-services-in-exchange). Alternatively, you can maintain an Exchange 2007 server for mailboxes that are managed by applications that use WebDAV.|

## Exchange 2007 Architecture

|Feature|Comments and mitigation|
|---|---|
|Storage groups|Exchange 2013 no longer uses the storage group construct, and instead you simply manage mailbox databases. For more information, see [Manage mailbox databases in Exchange 2013](manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md).|
|Extensible Storage Engine (ESE) streaming backup APIs|Exchange 2013 supports only Exchange-aware Volume Shadow Copy Service (VSS)-based backups. Exchange 2013 does include a plug-in for Windows Server Backup that enables you to backup and restore data. For information, see [Backup, restore, and disaster recovery](backup-restore-and-disaster-recovery-exchange-2013-help.md).|
|User Datagram Protocol (UDP) notifications|Support for User Datagram Protocol (UDP) notifications is removed from Exchange 2013. This affects the user experience when Outlook 2003 clients connect to their mailboxes on an Exchange 2013 server. For more information, see Microsoft Knowledge Base article 2009942, [Folders take a long time to update when an Exchange Server 2010 user uses Outlook 2003 in online mode](https://support.microsoft.com/help/2009942).|

## Exchange 2007 High availability

|Feature|Comments and mitigation|
|---|---|
|Cluster continuous replication (CCR)|Exchange 2013 uses database availability groups (DAGs) and mailbox database copies. For information, see [High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md).|
|Local continuous replication (LCR)|Exchange 2013 uses DAGs and mailbox database copies. For information, see [High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md).|
|Standby continuous replication (SCR)|Exchange 2013 uses DAGs and mailbox database copies. For information, see [High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md).|
|Single copy cluster (SCC)|Exchange 2013 uses DAGs and mailbox database copies. For information, see [High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md).|
|Setup /recoverCMS|Exchange 2013 uses Setup /m:recoverServer. For information, see [Recover an Exchange Server](recover-an-exchange-server-exchange-2013-help.md).|
|Clustered mailbox servers|Exchange 2013 uses DAGs and mailbox database copies. For information, see [High availability and site resilience](high-availability-and-site-resilience-exchange-2013-help.md).|

## Exchange 2007 Client access

|Feature|Comments and mitigation|
|---|---|
|Client authentication using Integrated Windows authentication (NTLM) for POP3 and IMAP4 users|NTLM isn't supported for POP3 or IMAP4 client connectivity in Exchange 2013. Connections from POP3 or IMAP4 client programs using NTLM will fail. If you're running the RTM version of Exchange 2013, the recommended alternative to NTLM is to use Plain Text Authentication with SSL. <br><br> If you're using Exchange 2013, to use NTLM, you must retain an Exchange 2007 server in your Exchange 2013 organization.|

## Exchange 2007 Outlook Web App and Outlook

|Feature|Comments and mitigation|
|---|---|
|Document access|Outlook Web App can't be used to access Microsoft SharePoint document libraries and Windows file shares.|
|Message flags|The ability to set a custom date on a message flag isn't available in Outlook Web App 2013. You can use Outlook to set custom dates.|
|Spell check|Outlook Web App uses the spell check features in your Web browser.|
|Search Folders|The ability for users to use Search folders isn't currently available in Outlook Web App.|
|Maximum Cached Views|Exchange 2007 supported modifying the maximum number of cached views per database (msExchMaxCachedViews) parameter for Outlook clients. Exchange 2013 no longer uses this parameter.|

## Exchange 2007 Recipient-related features

|Feature|Comments and mitigation|
|---|---|
|**Export-Mailbox** and **Import-Mailbox** cmdlets|In Exchange 2013, use export requests or import requests. For more information, see [Mailbox import and export requests](mailbox-import-and-export-requests-exchange-2013-help.md).|
|**Move-Mailbox** cmdlet set|In Exchange 2013, use move requests to move mailboxes. For information, see [Mailbox moves in Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md).|
|ISInteg|In Exchange 2013, use [New-MailboxRepairRequest](/powershell/module/exchange/New-MailboxRepairRequest).|

## Exchange 2007 Messaging policy and compliance

|Feature|Comments and mitigation|
|---|---|
|Managed Folders|In Exchange 2007, you use managed folders for messaging retention management (MRM). In Exchange 2013, managed folders aren't supported. You must use retention policies for MRM. <br><br> **Note**: Cmdlets related to managed folders are still available. You can create managed folders, managed content settings and managed folder mailbox policies, and apply a managed folder mailbox policy to a user, but the MRM assistant skips processing of mailboxes that have a managed folder mailbox policy applied.|

## Exchange 2007 Unified Messaging and voice mail

|Feature|Comments and mitigation|
|---|---|
|Directory lookups using Automatic Speech Recognition (ASR) for Outlook Voice Access|In Exchange 2007, Outlook Voice Access users can use speech inputs using Automatic Speech Recognition (ASR) in English (US) - (en-US) to search for users listed in the directory. Speech inputs could be also used in Outlook Voice Access to navigate menus, messages, and other options. However, even if an Outlook Voice Access user is able to use speech inputs, they have to use the telephone key pad to enter their PIN, and navigate personal options. <br><br> In Exchange 2013, authenticated and non-authenticated Outlook Voice Access users can't search for users in the directory using speech inputs or ASR in any language. However, callers that call into an auto attendant can use speech inputs in multiple languages to navigate auto attendant menus and search for users in the directory.|
