---
title: "Feature availability for Exchange Server"
ms.author: jhendr
author: JoanneHendrickson
manager: gailw
audience: ITPro
ms.topic: reference
f1_keywords:
- 'feature-availability-for-exchange-server'
ms.prod: exchange-server-it-pro
ms.localizationpriority: medium
ms.custom: Adm_ServiceDesc
ms.assetid: cdfe686d-a059-4f4d-bb8d-9c2c0ebfa423
description: Learn about the major Exchange Server features available across different supported versions.
---

# Feature availability for Exchange Server

The following table lists the major Exchange Server features available across different supported versions (certain caveats apply -- see the footnotes for further information -- this table may change without notice).

| Feature | Description | Exchange Server 2013 | Exchange Server 2016 | Exchange Server 2019 |
|:-----|:-----|:-----|:-----|:-----|
|[Anti-spam and anti-malware protection](/exchange/antispam-and-antimalware/antispam-and-antimalware)|Built-in anti-spam and anti-malware protection|Yes|Yes|Yes|
||Customize anti-spam and anti-malware policies|Yes<sup>via PowerShell</sup>|Yes<sup>via PowerShell</sup>|Yes<sup>via PowerShell</sup>|
||Quarantine - administrator management|Yes|Yes|Yes|
||Quarantine - end-user self-management|Yes|Yes|Yes|
|[Clients and mobile devices](/exchange/clients-and-mobile-in-exchange-online/clients-and-mobile-in-exchange-online)|Outlook for Windows and Mac<sup>1</sup>|Yes|Yes|Yes|
||Outlook on the web<sup>1</sup>|Yes|Yes|Yes|
||Outlook for iOS and Android<sup>1</sup>|Yes|Yes|Yes|
||Outlook add-ins and Outlook MAPI<sup>3</sup>|Yes|Yes|Yes|
||[Web Parts](/exchange/using-outlook-web-app-web-parts-exchange-2013-help)|Yes|Yes|Yes|
||Exchange ActiveSync|Yes|Yes|Yes|
||SMTP, POP and IMAP|Yes|Yes|Yes|
||EWS application support|Yes|Yes|Yes|
|[Exchange Online setup and administration](/exchange/architecture/client-access/exchange-admin-center)|Exchange admin center access|Yes|Yes|Yes|
||Remote Windows PowerShell access|Yes|Yes|Yes|
||ActiveSync policies for mobile devices|Yes|Yes|Yes|
||[Usage reporting](/exchange/monitoring/monitoring)|Yes|Yes|Yes|
|[High availability](/exchange/high-availability/high-availability) and business continuity|Database availability groups|Yes|Yes|Yes|
||[Deleted mailbox and deleted item recovery](/exchange/recipients/disconnected-mailboxes/restore-deleted-mailboxes)|Yes|Yes|Yes|
||[Single item recovery](/exchange/recipients-in-exchange-online/manage-user-mailboxes/enable-or-disable-single-item-recovery)|Yes|Yes|Yes|
|[Interoperability, connectivity, and compatibility](/exchange/security-and-compliance/interoperability-connectivity-and-compatiblity)|Skype for Business presence in OWA and Outlook|Yes|Yes|Yes|
||SharePoint interoperability|Yes|Yes|Yes|
||EWS connectivity and SMTP relay support|Yes|Yes|Yes|
|[Mail flow](/exchange/mail-flow/mail-flow)|Hybrid email and custom routing of outbound mail|Yes|Yes|Yes|
||Secure messaging with a trusted partner|Yes|Yes|Yes|
||Conditional mail routing and adding to an inbound safe list|Yes|Yes|Yes|
|[Message policy and compliance](/exchange/policy-and-compliance/policy-and-compliance)|Cloud-based archiving of on-premises mailboxes<sup>4</sup>|Yes|Yes|Yes|
||Messaging Records Management (MRM) and Journaling|Yes|Yes|Yes|
||[Manual retention policies, labels, and tags](/exchange/policy-and-compliance/mrm/retention-tags-and-retention-policies)|Yes|Yes|Yes|
||Encryption of data at rest (BitLocker)<sup>5</sup>|Yes|Yes|Yes|
||[IRM using Azure Information Protection](/exchange/policy-and-compliance/information-rights-management)|Yes|Yes|Yes|
||IRM using Windows Server AD RMS<sup>6</sup>|Yes|Yes|Yes|
||S/MIME|Yes|Yes|Yes|
||In-Place Hold and Litigation Hold|Yes|Yes|Yes|
||In-Place eDiscovery|Yes|Yes|Yes|
||Transport rules<sup>8</sup>|Yes|Yes|Yes|
||Data loss prevention<sup>9,10</sup>|Yes|Yes|Yes|
|[Permissions](/exchange/permissions-exo/permissions-exo)|Role-based permissions, role groups and assignment policies|Yes|Yes|Yes|
|[Planning and deployment](/exchange/plan-and-deploy/plan-and-deploy)|[Hybrid deployment](/exchange/hybrid-deployment/hybrid-deployment) support [IMAP](/exchange/mailbox-migration/migrating-imap-mailboxes/migrating-imap-mailboxes), cutover, and [staged migration](/exchange/mailbox-migration/what-to-know-about-a-staged-migration) support|Yes|Yes|Yes|
|[Recipients](/exchange/recipients-in-exchange-online/recipients-in-exchange-online)|Capacity alerts, Inbox rules and Mail Tips|Yes|Yes|Yes|
||Clutter|No|No|No|
||Delegate access|Yes|Yes|Yes|
||Connected accounts|Yes|Yes|Yes|
||Inactive mailboxes|No|No|No|
||Offline address book and policies|Yes|Yes|Yes|
||Hierarchical address book|Yes|Yes|Yes|
||Address lists and global address list|Yes|Yes|Yes|
||Universal contact card, contact linking with social networks and external contacts|Yes|Yes|Yes|
||Out-of-office replies, conference room management and resource mailboxes|Yes|Yes|Yes|
||Calendar sharing|Yes|Yes|Yes|
|[Reporting features](/exchange/mail-flow/transport-logs/delivery-reports) and [troubleshooting tools](/exchange/plan-and-deploy/post-installation-tasks/install-management-tools)|Message trace|Yes|No|Yes|
||[Auditing reports](/exchange/exchange-auditing-reports-exchange-2013-help)|Yes|Yes|Yes|
||Unified Messaging reports|Yes|Yes|Yes|
|[Sharing](/exchange/sharing/sharing) and [collaboration](/exchange/collaboration-exo/collaboration-exo)|Federated sharing (including calendar publishing)|Yes|Yes|Yes|
||Site mailboxes<sup>11</sup>|Yes|Yes|Yes|
||Public folders|Yes|Yes|Yes|
|[Voice message services](/exchange/recipients/recipients)|Voice mail|Yes<sup>12</sup>|No|No|
||Integration between voice mail and third-party FAX|Yes<sup>12</sup>|No|No|
||Third-party voice mail interoperability and Skype for Business integration|Yes<sup>12</sup>|No|No|

<sup>1</sup> The table indicates if the client works with the server. It does not mean the clients are included in the purchase of these servers. <br/>
<sup>3</sup> Some third-party web parts and add-ins may not be available.<br/>
<sup>4</sup> Requires an Exchange Online Archiving subscription for each on-premises mailbox user that has a cloud-based archive. <br/>
<sup>5</sup> BitLocker drive encryption is supported for Exchange Server, but an administrator needs to enable the feature. <br/>
<sup>6</sup> Windows Server AD RMS is an on-premises server that must be purchased and managed separately in order to enable the supported IRM features. <br/>
<sup>7</sup> Supported for customers running Exchange Server 2013 or later on-premises customers who purchase Azure Information Protection. Office 365 Message Encryption requires on-premises customers to route email through Exchange Online, either by using Exchange Online Protection for email filtering, or by establishing hybrid mail flow.<br/>
<sup>8</sup> Transport rules are made up of flexible criteria, which allow you to define conditions and exceptions, and actions to take based on the criteria. <br/>
<sup>9</sup> For Exchange 2013, DLP requires an Exchange Enterprise Client Access License (CAL). <br/>
<sup>10</sup> Customers running Exchange Server 2013 or later need to download and install the latest cumulative update (CU) or the immediately previous CU, to access Document Fingerprinting and Policy Tips in OWA and OWA for Devices. <br/>
<sup>11</sup> SharePoint Server must be deployed in the on-premises Exchange organization. <br/>
<sup>12</sup> Cloud Voicemail works with Exchange Online and Exchange 2019. See [Plan Cloud Voicemail service for on-premises users - Skype for Business Hybrid | Microsoft Docs](/skypeforbusiness/hybrid/plan-cloud-voicemail). <br/>

For information regarding Exchange Online, go to [Exchange Online Service Description](/office365/servicedescriptions/exchange-online-service-description/exchange-online-service-description).
