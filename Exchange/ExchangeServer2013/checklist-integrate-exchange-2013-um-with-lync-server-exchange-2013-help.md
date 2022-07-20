---
title: 'Checklist: Integrate Exchange 2013 UM with Lync Server: Exchange 2013 Help'
TOCTitle: 'Checklist: Integrate Exchange 2013 UM with Lync Server'
ms:assetid: 3b82e86f-9f30-4445-96ad-744082abeaeb
ms:mtpsurl: https://technet.microsoft.com/library/Dd638120(v=EXCHG.150)
ms:contentKeyID: 49315388
ms.topic: article
description: Use this checklist to install and deploy Unified Messaging (UM) and Microsoft Lync Server 2013.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Checklist: Integrate Exchange 2013 UM with Lync Server

_**Applies to:** Exchange Server 2013, Exchange Server 2016_

Use this checklist to install and deploy Unified Messaging (UM) and Microsoft Lync Server 2013. In this topic, "Lync Server" also refers to Lync Server 2010. However, Microsoft Office Communications Server 2007 R2 can also be deployed together with Unified Messaging.

Before you start working with this checklist, make sure you're familiar with the concepts in:

- [Deploying Exchange 2013 UM and Lync Server overview](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

- [Coexistence with Office Communications Server 2007 R2 and Lync Server](coexistence-with-office-communications-server-2007-r2-and-lync-server-exchange-2013-help.md)

For more information about how to perform the tasks that must be completed for Lync Server, see [Microsoft Lync Server 2013](/lyncserver/microsoft-lync-server-2013).

## Checklist for deploying Microsoft Lync Server and Unified Messaging

|Done?|Tasks|Topic|
|:---:|---|---|
|☐|Review the system requirements before installing Exchange Server 2013.|[Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md)|
|☐|Verify that you meet the prerequisites for installation.|[Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md)|
|☐|Review the prerequisites for integrating Microsoft Lync Server 2013 and Microsoft Exchange Server 2013.|[Prerequisites for Integrating Microsoft Lync Server 2013 and Microsoft Exchange Server 2013] (/skypeforbusiness/plan-your-deployment/integrate-with-exchange/integrate-with-exchange) <br/><br/> **Tip**: The Unified Communications Managed API (UCMA) 4.0 Runtime is required for Exchange 2013 and Lync Server 2010 and 2013 and is installed during installation. To download and review information about UCMA 4.0, see [Unified Communications Managed API 4.0 Runtime](https://www.microsoft.com/download/details.aspx?id=34992).|
|☐|Install the required Client Access and Mailbox servers.|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)|
|☐|Verify the installation and review the server setup logs.|[Verify an Exchange 2013 installation](verify-an-exchange-2013-installation-exchange-2013-help.md)|
|☐|If required, install the required UM language packs.|[Install a UM language pack](install-a-um-language-pack-exchange-2013-help.md)|
|☐|Create the number of SIP URI dial plans required for your organization.|[Create a UM dial plan](create-um-dial-plan-exchange-2013-help.md)|
|☐|Configure the dial plan security setting.|[Configure the VoIP security setting](configure-voip-security-setting-exchange-2013-help.md)|
|☐|Configure the number of concurrent calls on your Mailbox servers.|[Configure the number of incoming calls on a Mailbox server](configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md)|
|☐|Configure Outlook Voice Access numbers and other settings.|[Manage a UM dial plan](manage-um-dial-plan-exchange-2013-help.md)|
|☐|Add all Client Access and Mailbox servers to each SIP URI dial plan.|[Add Mailbox and Client Access servers to a SIP URI dial plan](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)|
|☐|Configure outbound dialing for Unified Messaging. Allow all calls on the SIP URI dial plans and UM mailbox policies that are linked to those dial plans.|[Authorize calls for users in a dial plan](authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md) <br/><br/> [Authorize calls for a group of users](authorize-calls-for-a-group-of-users-exchange-2013-help.md)|
|☐|Create the required number of auto attendants.|[Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md)|
|☐|Set up and configure each of the UM auto attendants.|[Set up a UM auto attendant](set-up-um-auto-attendant-exchange-2013-help.md)|
|☐|Create, import, and enable a new Exchange certificate for UM or enable a mutually-trusted third-party certificate.|[Add Mailbox and Client Access servers to a SIP URI dial plan](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)|
|☐|Configure the UM startup mode to Dual or TLS for each Client Access and Mailbox server.|[Configure the startup mode on a Mailbox server](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)  <br/><br/> [Configure the startup mode on a Client Access server](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)|
|☐|Restart the Microsoft Exchange Unified Messaging service and the Unified Messaging Call Router service on all Exchange servers to load the required certificates.|[Stop the Microsoft Exchange Unified Messaging service](stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md)  <br/><br/>  [Start the Microsoft Exchange Unified Messaging service](start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md) <br/><br/> [Stop the Microsoft Exchange Unified Messaging Call Router service](stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md) <br/><br/> [Start the Microsoft Exchange Unified Messaging Call Router service](start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md)|
|☐|Create a UM mailbox policy or configure the default UM mailbox policy.|[Create a UM mailbox policy](create-um-mailbox-policy-exchange-2013-help.md) <br/><br/> [Manage a UM mailbox policy](manage-um-mailbox-policy-exchange-2013-help.md)|
|☐|Enable users for Unified Messaging with a SIP address and link them to a SIP URI dial plan.|[Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md)|
|☐|Review the Lync Server 2013 Planning documentation.|[Planning](/lyncserver/lync-server-2013-planning)|
|☐|Install and deploy Lync Server 2013.|[Deploying Lync Server 2013](/lyncserver/lync-server-2013-deploying-lync-server)|
|☐|Import the mutually-trusted internal PKI or third-party certificate that is imported on the Exchange UM servers.|[Configure Certificates for Servers](/lyncserver/lync-server-2013-configure-certificates-for-servers) <br/><br/> [Configure Certificates on the Server Running Microsoft Exchange Server Unified Messaging](/lyncserver/lync-server-2013-configure-certificates-on-the-server-running-microsoft-exchange-server-unified-messaging)|
|☐|If required, start Lync services on servers to load the certificates.|[Start Services on Servers](/lyncserver/lync-server-2013-start-services-on-servers)|
|☐|Open the Exchange Management Shell and run the exchucutil.ps1 script located in the %Program Files%\Microsoft\Exchange Server\V15\Scripts folder.|[Configure UM to work with Lync Server](configure-um-to-work-with-lync-server-exchange-2013-help.md)|
|☐|Review the requirements for Enterprise Voice.|[Software Prerequisites for Enterprise Voice](/lyncserver/lync-server-2013-software-prerequisites-for-enterprise-voice) <br/><br/> [Security and Configuration Prerequisites for Enterprise Voice](/skypeforbusiness/deploy/deploy-enterprise-voice/enterprise-voice-security)|
|☐|Deploy and configure media gateways or Mediation Servers and define peers.|[Deploying Mediation Servers and Defining Peers](/lyncserver/lync-server-2013-deploying-mediation-servers-and-defining-peers)|
|☐|Configure a trunk between a Mediation Server and one or more of the peers to provide public switched telephone network (PSTN) connectivity.|[Configuring Trunks](/lyncserver/lync-server-2013-configuring-trunks)|
|☐|Create and configure a Lync dial plan and create, define, and associate normalization rules.|[Configuring Dial Plans](/lyncserver/lync-server-2013-configuring-dial-plans)|
|☐|Configure voice policies and define telephone usage and outbound call routes.|[Configuring Voice Policies, PSTN Usage Records, and Voice Routes](/skypeforbusiness/deploy/deploy-enterprise-voice/voice-and-pstn)|
|☐|Run the Exchange Integration utility (ocsumutil.exe), which creates the contact objects for Outlook Voice Access and for the auto attendants.|[Configure Lync Server 2013 to Work with Unified Messaging on Microsoft Exchange Server](/lyncserver/lync-server-2013-configure-lync-server-2013-to-work-with-unified-messaging-on-microsoft-exchange-server)|
|☐|Define, deploy, and configure any required advanced Enterprise Voice features.|[Deploying Advanced Enterprise Voice Features](/skypeforbusiness/deploy/deploy-enterprise-voice/deploy-advanced-enterprise-voice-features)|
|☐|Enable the users for Enterprise Voice. Enter a line URI and assign a voice policy and a Lync dial plan.|[Enable Users for Enterprise Voice](/skypeforbusiness/deploy/deploy-enterprise-voice/enable-users-for-enterprise-voice)|
