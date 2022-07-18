---
title: 'Appendix A: Exchange health sets'
TOCTitle: 'Appendix A: Exchange health sets'
ms:assetid: 29af464e-ae07-40f8-ac6e-28e876a91d90
ms:mtpsurl: https://technet.microsoft.com/library/Dn195906(v=EXCHG.150)
ms:contentKeyID: 53181783
ms.reviewer: 
ms.topic: article
description: The health sets available in Microsoft Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Appendix A: Exchange health sets

_**Applies to:** Exchange Server 2013_

The Exchange Server 2013 Management Pack relies on the Managed Availability feature in Exchange 2013. In Managed Availability, each component in Exchange 2013 monitors itself using _probes_, _monitors_ and _responders_. Each Exchange 2013 component that implements Managed Availability is referred to as a _health set_. The following tables list all the health sets available in Exchange 2013.

> [!NOTE]
> Only the health sets that apply to your Exchange deployment are seen in the SCOM console. Therefore, depending on your configuration, some of these health sets may not be present in your deployment.

## Customer Touch Points Health Sets

|Health set|Server Role|Description|
|---|---|---|
|ActiveSync|CAS, Mailbox|Monitors the overall health of the Exchange ActiveSync service for mobile clients.|
|Autodiscover|CAS|Monitors the overall health of the Autodiscover service for clients.|
|Compliance|CAS|Monitors the health of compliance features.|
|ECP|CAS, Mailbox|Monitors the overall health of the Exchange admin center (EAC), as well as the overall health of the Outlook Web App end user setting service.|
|EWS|CAS|Monitors the overall health of Exchange Web Services.|
|IMAP|CAS|Monitors the overall health and availability of the IMAP4 service and IMAP4 client connectivity.|
|Outlook|CAS|Monitors the health of Outlook client connectivity.|
|OWA|CAS|Monitors the overall health of the Outlook Web App service.|
|POP|CAS|Monitors the overall health and availability of the POP3 service and POP3 client connectivity.|
|PublicFolders|Mailbox|Monitors the overall health of public folder availability and replication in your organization.|
|RPS|CAS, Mailbox|Monitors the overall health of the Remote PowerShell service.|
|SiteMailbox|Mailbox|Monitors the overall health and accessibility of site mailboxes in your organization.|
|UM|CAS|Monitors the overall health of the Unified Messaging service in your organization.|

## Service Components Health Sets

|Health set|Server Role|Description|
|---|---|---|
|ActiveSync.Protocol|Mailbox|Monitors the Exchange ActiveSync communications protocol on the Mailbox server.|
|ActiveSync.Proxy|CAS|Monitors the Exchange ActiveSync infrastructure on the Client Access server.|
|Antimalware|Mailbox|Monitors the health of the basic anti-malware protection feature.|
|Antispam|Mailbox|Monitors the health of the basic anti-spam protection feature.|
|Autodiscover.Protocol|Mailbox|Monitors the Autodiscover communications protocol on the Mailbox server.|
|Autodiscover.Proxy|CAS|Monitors the availability of the Autodiscover proxy infrastructure on the Client Access server.|
|Classification|Mailbox|Monitors the health of the Data loss prevention (DLP) feature.|
|ClientAccess.Proxy|CAS|Monitors the availability of the proxy infrastructure on the Client Access server.|
|DataProtection|CAS, Mailbox|Monitors the redundancy of databases in a database availability group (DAG).|
|ECP.Proxy|CAS|Monitors the availability of the EAC proxy infrastructure on the Client Access server.|
|Ediscovery.Procotol|Mailbox|Monitors the eDiscovery protocol on the Mailbox server.|
|EDS|CAS, Mailbox|Extracts performance counters and generates notifications when a threshold is exceeded.|
|EventAssistants|Mailbox|Monitors the health of event-based mailbox assistants.|
|EWS.Protocol|Mailbox|Monitors the Exchange Web Services communications protocol on the Mailbox server.|
|EWS.Proxy|CAS|Monitors the availability of the Exchange Web Services proxy infrastructure on the Client Access server.|
|FfoQuarantine|Mailbox|Monitors the health of the Forefront message quarantine feature.|
|FfoTransport|Mailbox|Monitors the Transport components in Forefront such as server and agent latency, DSNs generated, transport databases, SMTP, mailbox transport, and shadow redundancy.|
|FfoUMC|CAS|Monitors the overall health of the Forefront administration website.|
|FfoWebService|CAS|Monitors the health of the Forefront web service.|
|FIPS|CAS, Mailbox|Monitors the health of a Transport rules component that analyzes messages.|
|FreeBusy|Mailbox|Monitors the overall health of the free/busy information in your organization.|
|FrontendTransport|CAS, Mailbox|Monitors the overall health of the Frontend Transport service that runs on Client Access servers.|
|HubTransport|CAS, Mailbox|Monitors the overall health of the Hub Transport service that runs on Mailbox servers.|
|IMAP.Protocol|Mailbox|Monitors the IMAP4 protocol on the Mailbox server.|
|IMAP.Proxy|CAS|Monitors the availability of the IMAP4 proxy infrastructure on the Client Access server.|
|MailboxMigration|Mailbox|Monitors the overall health of the Migration Service.|
|MailboxTransport|Mailbox|Monitors the overall health of the Transport component that delivers messages to and picks messages up from user mailboxes.|
|MailFlow|CAS|Monitors the health of the mail flow paths within your organization.|
|MessageTracing|Mailbox|Monitors the overall health and availability of message tracking and delivery reports.|
|Monitoring|CAS, Mailbox|Monitors the health of the monitoring service itself.|
|MRS|Mailbox|Monitors the overall health of the Mailbox Replication service.|
|MSExchangeCertificateDeployment|Mailbox|Monitors the state of certificates in your Exchange organization.|
|OAB|Mailbox|Monitors the overall health of offline address book (OAB) generation and distribution.|
|OAB.Proxy|CAS|Monitors the availability of the OAB proxy infrastructure on the Client Access server.|
|Outlook.Protocol|Mailbox|Monitors the MAPI protocol on the Mailbox server.|
|Outlook.Proxy|CAS|Monitors the availability of the Outlook Anywhere proxy infrastructure on the Client Access server.|
|OWA.Protocol|Mailbox|Monitors the Outlook Web App protocol on the Mailbox server.|
|OWA.Proxy|CAS|Monitors the availability of the Outlook Web App proxy infrastructure on the Client Access server.|
|POP.Protocol|Mailbox|Monitors the POP3 protocol on the Mailbox server.|
|POP.Proxy|CAS|Monitors the availability of the POP3 proxy infrastructure on the Client Access server.|
|PowershellDataProvider|CAS, Mailbox|Monitors the overall health of the Exchange Management Shell.|
|PushNotifications.Protocol|Mailbox|Monitors the push notifications protocol on the Mailbox server.|
|RemoteMonitoring|CAS, Mailbox|Monitors the health of the monitoring service on other servers.|
|RPS.Protocol|Mailbox|Monitors the Remote PowerShell protocol on the Mailbox server.|
|RPS.Proxy|CAS, Mailbox|Monitors the availability of the Remote PowerShell service proxy infrastructure on the Client Access server.|
|Search|CAS, Mailbox|Monitors the overall health of the Exchange Search service.|
|SMTP|CAS, Mailbox|Monitors the overall health of SMTP on Exchange servers.|
|Store|Mailbox|Monitors the overall health of the Exchange store on the Exchange servers.|
|Transport|CAS|Monitors Transport components such as server and agent latency, DSNs generated, transport databases, SMTP, mailbox transport, and shadow redundancy.|
|UM.CallRouter|CAS, Mailbox|Monitors the overall health of the Unified Messaging Call Router service.|
|UM.Protocol|Mailbox|Monitors the Unified Messaging protocol on the Mailbox server.|
|UserThrottling|CAS, Mailbox|Monitors the overall health of throttling policies in your organization.|

## Server Resources Health Sets

|Health set|Server Role|Description|
|---|---|---|
|Clustering|Mailbox|Monitors the health of the Windows cluster service on a Mailbox server that is a DAG member.|
|DiskSpace|CAS, Mailbox|Monitors the disk space utilization on Exchange servers.|
|MailboxSpace|Mailbox|Monitors the overall health of mailbox databases.|
|Memory|CAS, Mailbox|Monitors the memory utilization on Exchange servers.|

## Key Dependencies Health Sets

|Health set|Server Role|Description|
|---|---|---|
|AD|CAS, Mailbox|Monitors the availability of Active Directory.|
|Network|CAS, Mailbox|Checks to verify that the server is registered in DNS.|
|OWA.Protocol.Dep|Mailbox|Monitors the health of the OWA protocol dependency.|
