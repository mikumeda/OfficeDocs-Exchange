---
title: 'Anti-virus software in the operating system on Exchange servers'
TOCTitle: Anti-Virus Software in the Operating System on Exchange Servers
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 48385271
ms.topic: article
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about the exclusions you need to make when you run Windows anti-virus software on Exchange 2013 servers.
---

# Anti-Virus Software in the Operating System on Exchange Servers

_**Applies to:** Exchange Server 2013_

This topic describes the effects of file-level antivirus programs on computers that are running Microsoft Exchange Server 2013. If you implement the recommendations described in this topic, you can help enhance the security and health of your Exchange organization.

File-level scanners are frequently used. However, if they are configured incorrectly, they can cause problems in Exchange 2013. There are two types of file-level scanners:

- _Memory-resident file-level scanning_ refers to a part of file-level antivirus software that is loaded in memory at all times. It checks all the files that are used on the hard disk and in computer memory.

- _On-demand file-level scanning_ refers to a part of file-level antivirus software that you can configure to scan files on the hard disk manually or on a schedule. Some versions of antivirus software start the on-demand scan automatically after virus signatures are updated to make sure that all files are scanned with the latest signatures.

The following problems may occur when you use file-level scanners with Exchange 2013:

- File-level scanners may scan a file when the file is being used or at a scheduled interval. This can cause the scanners to lock or quarantine an Exchange log or a database file while Exchange 2013 tries to use the file. This behavior may cause a severe failure in Exchange 2013 and may also cause -1018 event log errors.

- File-level scanners don't provide protection against email viruses, such as Storm Worm. Storm Worm was a backdoor Trojan horse program that propagated itself through email messages. The worm joined the infected computer to a botnet, where the computer was used to send spam in periodic bursts.

## Recommendations for using file-level scanning with Exchange 2013

If you're deploying file-level scanners on Exchange 2013 servers, make sure that the appropriate exclusions, such as directory exclusions, process exclusions, and file name extension exclusions, are in place for both memory-resident and file-level scanning. This section describes recommended directory exclusions, process exclusions, and file name extension exclusions.

## Directory exclusions

You must exclude specific directories for each Exchange server on which you run a file-level antivirus scanner. This section describes the directories that you should exclude from file-level scanning.

- **Mailbox servers**

  - **Mailbox databases**

    - Exchange databases, checkpoint files, and log files. By default, these are located in sub-folders under the %ExchangeInstallPath%Mailbox folder. To determine the location of a mailbox database, transaction log, and checkpoint file, run the following command: `Get-MailboxDatabase -Server <servername>| Format-List _path*`

    - Database content indexes. By default, these are located in the same folder as the database file.

    - Group Metrics files. By default, these files are located in the %ExchangeInstallPath%GroupMetrics folder.

    - General log files, such as message tracking and calendar repair log files. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs folder and %ExchangeInstallPath%Logging folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-MailboxServer <servername> | Format-List _path*`

    - The Offline Address Book files. By default, these are located in subfolders under the %ExchangeInstallPath%ClientAccess\\OAB folder.

    - IIS system files in the %SystemRoot%\\System32\\Inetsrv folder.

    - The Mailbox database temporary folder: %ExchangeInstallPath%Mailbox\\MDBTEMP

  - **Members of Database Availability Groups**

    - All the items listed in the **Mailbox databases** list, and the cluster quorum database that exists at %Windir%\\Cluster.

    - The witness directory files. These files are located on another server in the environment, typically a Client Access server that isn't installed on the same computer as a Mailbox server. By default, the witness directory files are located in %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>.

  - **Transport service**

    - Log files, for example, message tracking and connectivity logs. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-TransportService <servername> | Format-List _logpath*,*tracingpath*`

    - Pickup and Replay message directory folders. By default, these folders are located under the %ExchangeInstallPath%TransportRoles folder. To determine the paths being used, run the following command in the Exchange Management Shell: `Get-TransportService <servername>| Format-List _dir*path*`

    - The queue databases, checkpoints, and log files. By default, these are located in the %ExchangeInstallPath%TransportRoles\\Data\\Queue folder.

    - The Sender Reputation database, checkpoint, and log files. By default, these are located in the %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation folder.

    - The temporary folders that are used to perform conversions:

      - By default, content conversions are performed in the Exchange server's %TMP% folder.

      - By default, rich text format (RTF) to MIME/HTML conversions are performed in %ExchangeInstallPath%\\Working\\OleConverter folder.

    - The content scanning component is used by the Malware agent and data loss prevention (DLP). By default, these files are located in the %ExchangeInstallPath%FIP-FS folder.

  - **Mailbox Transport service**

    - Log files, for example, connectivity logs. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-MailboxTransportService <servername> | Format-List _logpath*`

  - **Unified Messaging**

    - The grammar files for different locales, for example en-EN or es-ES. By default, these are stored in the subfolders in the %ExchangeInstallPath%UnifiedMessaging\\grammars folder.

    - The voice prompts, greetings and informational message files. By default, these are stored in the subfolders in the %ExchangeInstallPath%UnifiedMessaging\\Prompts folder

    - The voicemail files that are temporarily stored in the %ExchangeInstallPath%UnifiedMessaging\\voicemail folder.

    - The temporary files generated by Unified Messaging. By default, these are stored in the %ExchangeInstallPath%UnifiedMessaging\\temp folder.

  - **Setup**

    - Exchange Server setup temporary files. These files are typically located in %SystemRoot%\\Temp\\ExchangeSetup.

  - **Exchange Search service**

    - Temporary files used by the Exchange Search service and Microsoft Filter Pack to perform file conversion in a sandboxed environment. These files are located in %SystemRoot%\\Temp\\OICE\___\<GUID\>_\\.

- **Client Access servers**

  - **Web components**

    - For servers using Internet Information Services (IIS) 7.0, the compression folder that is used with Microsoft Outlook Web App. By default, the compression folder for IIS 7.0 is located at %SystemDrive%\\inetpub\\temp\\IIS Temporary Compressed Files.

    - IIS system files in the %SystemRoot%\\System32\\Inetsrv folder

    - Inetpub\\logs\\logfiles\\w3svc

    - Sub-folders in %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary ASP.NET Files

  - **POP3 and IMAP4 protocol logging**

    - POP3 folder: %ExchangeInstallPath%Logging\\POP3

    - IMAP4 folder: %ExchangeInstallPath%Logging\\IMAP4

  - **Front End Transport service**

    - Log files, for example, connectivity logs and protocol logs. By default, these files are located in subfolders under the %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd folder. To determine the log paths being used, run the following command in the Exchange Management Shell: `Get-FrontEndTransportService <servername> | Format-List _logpath*`

  - **Setup**

    - Exchange Server setup temporary files. These files are typically located in %SystemRoot%\\Temp\\ExchangeSetup.

## Process exclusions

Many file-level scanners now support the scanning of processes, which can adversely affect Microsoft Exchange if the incorrect processes are scanned. Therefore, you should exclude the following processes from file-level scanners.

|Process|Path|Comments|Servers|
|---|---|---|---|
|Dsamain.exe|%SystemRoot%\System32|Active Directory Lightweight Directory Services (AD LDS) on subscribed Edge Transport servers.|Edge Transport servers|
|EdgeTransport.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Transport service worker process|Mailbox servers <br/><br/> Edge Transport servers|
|fms.exe|%ExchangeInstallPath%FIP-FS\Bin|Content scanning component that's used by the Malware agent and DLP.|Mailbox servers|
|hostcontrollerservice.exe|%ExchangeInstallPath%Bin\Search\Ceres\HostController|Microsoft Exchange Search Host Controller service (HostControllerService)|Mailbox servers <br/><br/> Client Access servers|
|inetinfo.exe|%SystemRoot%\System32\inetsrv|Internet Information Services (IIS)|Mailbox servers <br/><br/> Client Access servers|
|Microsoft.Exchange.AntispamUpdateSvc.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Anti-spam Update service (MSExchangeAntispamUpdate)|Mailbox servers <br/><br/> Edge Transport servers|
|Microsoft.Exchange.ContentFilter.Wrapper.exe|%ExchangeInstallPath%TransportRoles\agents\Hygiene|Content Filter agent|Mailbox servers <br/><br/> Edge Transport servers|
|Microsoft.Exchange.Diagnostics.Service.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Diagnostics service (MSExchangeDiagnostics)|Mailbox servers <br/><br/> Client Access servers <br/><br/> Edge Transport servers|
|Microsoft.Exchange.Directory.TopologyService.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Active Directory Topology service (MSExchangeADTopology)|Mailbox servers <br/><br/> Client Access servers|
|Microsoft.Exchange.EdgeCredentialSvc.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Credential service (MSExchangeEdgeCredential)|Edge Transport servers|
|Microsoft.Exchange.EdgeSyncSvc.exe|%ExchangeInstallPath%Bin|Microsoft Exchange EdgeSync service (MSExchangeEdgeSync)|Mailbox servers|
|Microsoft.Exchange.Imap4.exe|ExchangeInstallPath%FrontEnd\PopImap|Microsoft Exchange IMAP4 service (MSExchangeImap4)|Client Access servers|
|Microsoft.Exchange.Imap4service.exe|%ExchangeInstallPath%ClientAccess\PopImap|Microsoft Exchange IMAP4 Backend service (MSExchangeIMAP4BE)|Mailbox servers|
|Microsoft.Exchange.Pop3.exe|%ExchangeInstallPath%FrontEnd\PopImap|Microsoft Exchange POP3 service (MSExchangePop3)|Client Access servers|
|Microsoft.Exchange.Pop3service.exe|%ExchangeInstallPath%ClientAccess\PopImap|Microsoft Exchange POP3 Backend service (MSExchangePOP3BE)|Mailbox servers|
|Microsoft.Exchange.ProtectedServiceHost.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Service Host service (MSExchangeServiceHost)|Mailbox servers <br/><br/> Client Access servers <br/><br/> Edge Transport servers|
|Microsoft.Exchange.RPCClientAccess.Service.exe|%ExchangeInstallPath%Bin|Microsoft Exchange RPC Client Access service (MSExchangeRPC)|Mailbox servers|
|Microsoft.Exchange.Search.Service.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Search service (MSExchangeFastSearch)|Mailbox servers|
|Microsoft.Exchange.Servicehost.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Service Host service (MSExchangeServiceHost)|Mailbox servers <br/><br/> Client Access servers <br/><br/> Edge Transport servers|
|Microsoft.Exchange.Store.Service.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Information Store service (MSExchangeIS)|Mailbox servers|
|Microsoft.Exchange.Store.Worker.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Information Store service worker process|Mailbox servers|
|Microsoft.Exchange.UM.CallRouter.exe|%ExchangeInstallPath%FrontEnd\CallRouter|Microsoft Exchange Unified Messaging Call Router service (MSExchangeUMCR)|Client Access servers|
|MSExchangeDagMgmt.exe|%ExchangeInstallPath%Bin|Microsoft Exchange DAG Management service (MSExchangeDagMgmt)|Mailbox servers|
|MSExchangeDelivery.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Mailbox Transport Delivery service (MSExchangeDelivery)|Mailbox servers|
|MSExchangeFrontendTransport.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Frontend Transport service (MSExchangeFrontEndTransport)|Client Access servers|
|MSExchangeHMHost.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Health Manager service (MSExchangeHM)|Mailbox servers <br/><br/> Client Access servers <br/><br/> Edge Transport servers|
|MSExchangeHMWorker.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Health Manager service worker process|Mailbox servers <br/><br/> Client Access servers <br/><br/> Edge Transport servers|
|MSExchangeMailboxAssistants.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Mailbox Assistants service (MSExchangeMailboxAssistants)|Mailbox servers|
|MSExchangeMailboxReplication.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Mailbox Replication service (MSExchangeMailboxReplication)|Mailbox servers|
|MSExchangeMigrationWorkflow.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Migration Workflow service (MSExchangeMigrationWorkflow)|Mailbox servers|
|MSExchangeRepl.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Replication service (MSExchangeRepl)|Mailbox servers|
|MSExchangeSubmission.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Mailbox Transport Submission service (MSExchangeSubmission)|Mailbox servers|
|MSExchangeTransport.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Transport service (MSExchangeTransport)|Mailbox servers <br/><br/> Edge Transport servers|
|MSExchangeTransportLogSearch.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Transport Log Search service (MSExchangeTransportLogSearch)|Mailbox servers <br/><br/> Edge Transport servers|
|MSExchangeThrottling.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Throttling service (MSExchangeThrottling)|Mailbox servers|
|Noderunner.exe|%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0|Microsoft Exchange Search service (MSExchangeFastSearch)|Mailbox servers|
|OleConverter.exe|%ExchangeInstallPath%Bin|Converts rich text format (RTF) messages to MIME/HTML for external recipients.|Mailbox servers|
|ParserServer.exe|%ExchangeInstallPath%Bin\Search\Ceres\ParserServer|Microsoft Exchange Search service (MSExchangeFastSearch)|Mailbox servers|
|Powershell.exe|C:\Windows\System32\WindowsPowerShell\v1.0|Exchange Management Shell|Mailbox servers <br/><br/> Client Access servers <br/><br/> Edge Transport servers|
|ScanEngineTest.exe|%ExchangeInstallPath%FIP-FS\Bin|Content scanning component that's used by the Malware agent and DLP.|Mailbox servers|
|ScanningProcess.exe|%ExchangeInstallPath%FIP-FS\Bin|Content scanning component that's used by the Malware agent and DLP.|Mailbox servers|
|TranscodingService.exe|%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing|WebReady Document Viewing in Outlook Web App.|Mailbox servers|
|UmService.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Unified Messaging service (MSExchangeUM)|Mailbox servers|
|UmWorkerProcess.exe|%ExchangeInstallPath%Bin|Microsoft Exchange Unified Messaging service worker process|Mailbox servers|
|UpdateService.exe|%ExchangeInstallPath%FIP-FS\Bin|Content scanning component that's used by the Malware agent and DLP.|Mailbox servers|
|W3wp.exe|%SystemRoot%\System32\inetsrv|Internet Information Services (IIS)|Mailbox servers <br/><br/> Client Access servers|

## File name extension exclusions

In addition to excluding specific directories and processes, you should exclude the following Exchange-specific file name extensions in case directory exclusions fail or files are moved from their default locations.

- Application-related extensions:

  - .config

  - .dia

  - .wsb

- Database-related extensions:

  - .chk

  - .edb

  - .jrs

  - .jsl

  - .log

  - .que

- Offline address book-related extensions:

  - .lzx

- Content Index-related extensions:

  - .ci

  - .dir

  - .wid

  - .000

  - .001

  - .002

- Unified Messaging-related extensions:

  - .cfg

  - .grxml

- Group Metrics-related extensions:

  - .dsc

  - .txt
