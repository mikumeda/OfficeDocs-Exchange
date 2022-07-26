---
title: 'Checklist: Deploy Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 'Checklist: Deploy Exchange 2013 UM'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 49315398
ms.topic: article
description: Checklist to help you install and deploy Unified Messaging (UM) in your Exchange Server organization.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Checklist: Deploy Exchange 2013 UM

_**Applies to:** Exchange Server 2013, Exchange Server 2016_

Use this checklist to help you install and deploy Unified Messaging (UM) in your organization.

Before you start working with this checklist, make sure you're familiar with the concepts in:

- [Unified Messaging](unified-messaging-exchange-2013-help.md)

- [New voice mail features](new-voice-mail-features-exchange-2013-help.md)

- [Planning for Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md)

For step-by-step guidance about how to deploy UM and Microsoft Lync Server, see [Checklist: Integrate Exchange 2013 UM with Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).

## Checklist for deploying Unified Messaging

|Done?|Tasks|Topic|
|:---:|---|---|
|☐|Deploy and configure telephony components.|[Connect UM to your telephone system](connect-um-to-your-telephone-system-exchange-2013-help.md)|
|☐|Review the system requirements before installing Exchange 2013.|[Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md)|
|☐|Verify that you meet the prerequisites for installation.|[Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md)|
|☐|Install the required Client Access and Mailbox servers. <br/><br/> **Warning**: You must deploy at least one Exchange 2013 Mailbox server in your organization before you configure the VoIP gateways or IP PBXs to send UM SIP and RTP traffic to the Exchange 2013 Client Access servers.|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)|
|☐|Verify the installation and review the server setup logs.|[Verify an Exchange 2013 installation](verify-an-exchange-2013-installation-exchange-2013-help.md)|
|☐|If required, install the required UM language packs.|[Install a UM language pack](install-a-um-language-pack-exchange-2013-help.md)|
|☐|Create the number of dial plans required for your organization.|[Create a UM dial plan](create-um-dial-plan-exchange-2013-help.md)|
|☐|Configure the dial plan security setting.|[Configure the VoIP security setting](configure-voip-security-setting-exchange-2013-help.md)|
|☐|Configure the UM startup mode for each Client Access and Mailbox server.|[Configure the startup mode on a Mailbox server](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md) <br/><br/> [Configure the startup mode on a Client Access server](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)|
|☐|Configure the number of concurrent calls on your Mailbox servers.|[Configure the number of incoming calls on a Mailbox server](configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md)|
|☐|Configure Outlook Voice Access numbers and other settings.|[Manage a UM dial plan](manage-um-dial-plan-exchange-2013-help.md)|
|☐|Configure outbound dialing for Unified Messaging.|[Authorize calls using dialing rules](authorize-calls-using-dialing-rules-exchange-2013-help.md) <br/><br/> [Authorize calls for users in a dial plan](authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md) <br/><br/> [Authorize calls for a group of users](authorize-calls-for-a-group-of-users-exchange-2013-help.md)|
|☐|Create the required number of auto attendants.|[Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md)|
|☐|Set up and configure each of the UM auto attendants.|[Set up a UM auto attendant](set-up-um-auto-attendant-exchange-2013-help.md)|
|☐|Create, import, and enable a new Exchange certificate for UM or enable a mutually-trusted third-party certificate. Also, import the certificate on all VoIP gateways, IP PBXs, and SBCs.|[Add Mailbox and Client Access servers to a SIP URI dial plan](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md)|
|☐|Restart the Microsoft Exchange Unified Messaging service and the Unified Messaging Call Router service on all Exchange servers to load the required certificates.|[Stop the Microsoft Exchange Unified Messaging service](stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md) <br/><br/> [Start the Microsoft Exchange Unified Messaging service](start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md) <br/><br/> [Stop the Microsoft Exchange Unified Messaging Call Router service](stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md) <br/><br/> [Start the Microsoft Exchange Unified Messaging Call Router service](start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md)|
|☐|Create a UM mailbox policy or configure the default UM mailbox policy.|[Create a UM mailbox policy](create-um-mailbox-policy-exchange-2013-help.md) <br/><br/> [Manage a UM mailbox policy](manage-um-mailbox-policy-exchange-2013-help.md)|
|☐|Enable users for Unified Messaging with an extension number and an E.164 number, if required.|[Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md)|
|☐|Enable incoming faxing (Optional).|[Enable voice mail users to receive faxes](enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md)|
|☐|Set up Protected Voice Mail (Optional).|[Protect voice mail](protect-voice-mail-exchange-2013-help.md)|
