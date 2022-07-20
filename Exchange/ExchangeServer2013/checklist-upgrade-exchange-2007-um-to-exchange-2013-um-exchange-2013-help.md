---
title: 'Checklist: Upgrade Exchange 2007 UM to Exchange 2013 UM: Exchange 2013 Help'
TOCTitle: 'Checklist: Upgrade Exchange 2007 UM to Exchange 2013 UM'
ms:assetid: 99b1a081-4052-4516-b63c-77622cbdf962
ms:mtpsurl: https://technet.microsoft.com/library/Dn169229(v=EXCHG.150)
ms:contentKeyID: 53382780
ms.topic: article
description: Use this checklist to help you upgrade Exchange 2007 Unified Messaging (UM) to Exchange 2013 UM.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Checklist: Upgrade Exchange 2007 UM to Exchange 2013 UM

_**Applies to:** Exchange Server 2013_

Use this checklist to help you upgrade Exchange 2007 Unified Messaging (UM) to Exchange 2013 UM. Be sure to refer to this information when you're upgrading your Exchange 2007 organization and your UM deployment to Exchange 2013. For step-by-step instructions for upgrading to Exchange 2013 UM, see [Upgrade Exchange 2007 UM to Exchange 2013 UM](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md).

Before you start working with this checklist, make sure you're familiar with the concepts in:

- [Planning for Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md)

- [Telephone system integration with UM](../ExchangeOnline/voice-mail-unified-messaging/telephone-system-integration-with-um/telephone-system-integration-with-um.md)

- [Connect your voice mail system to your telephone network](../ExchangeOnline/voice-mail-unified-messaging/connect-voice-mail-system/connect-voice-mail-system.md)

For step-by-step guidance about how to upgrade from Exchange 2010 UM to Exchange 2013 UM, see [Checklist: Upgrade Exchange 2010 UM to Exchange 2013 UM](checklist-upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md).

## Checklist for upgrading Exchange 2007 UM to Exchange 2013 UM

|Done?|Tasks|Topic|
|:---:|---|---|
|☐|Deploy and configure telephony components|[Connect UM to your telephone system](connect-um-to-your-telephone-system-exchange-2013-help.md)|
|☐|Review the system requirements before installing Exchange 2013|[Exchange 2013 system requirements](exchange-2013-system-requirements-exchange-2013-help.md)|
|☐|Verify that you meet the prerequisites for installation|[Exchange 2013 prerequisites](exchange-2013-prerequisites-exchange-2013-help.md)|
|☐|Install the required Client Access and Mailbox servers|[Install Exchange 2013 using the Setup wizard](install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md)|
|☐|Verify the installation and review the server setup logs|[Verify an Exchange 2013 installation](verify-an-exchange-2013-installation-exchange-2013-help.md)|
|☐|If required, install the required UM language packs|[Install a UM language pack](install-a-um-language-pack-exchange-2013-help.md)|
|☐|Import dial plan and auto attendant custom prompts|[Import custom prompts from Exchange 2007 to Exchange 2013](import-custom-prompts-from-exchange-2007-to-exchange-2013-exchange-2013-help.md)|
|☐|Export and import certificates|[Deploying certificates for UM](deploying-certificates-for-um-exchange-2013-help.md)|
|☐|Configure the UM startup mode on all Exchange 2013 Client Access servers|[Configure the startup mode on a Client Access server](configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md)|
|☐|Configure the UM startup mode on all Exchange 2013 Mailbox servers|[Configure the startup mode on a Mailbox server](configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md)|
|☐|Create or configure existing UM dial plans|[Create a UM dial plan](create-um-dial-plan-exchange-2013-help.md) <br/><br/> [Manage a UM dial plan](manage-um-dial-plan-exchange-2013-help.md)|
|☐|Create or configure existing UM IP gateways|[Create a UM IP gateway](create-um-ip-gateway-exchange-2013-help.md) <br/><br/> [>Manage a UM IP gateway](manage-um-ip-gateway-exchange-2013-help.md)|
|☐|Create a UM hunt group|[Create a UM hunt group](create-um-hunt-group-exchange-2013-help.md)|
|☐|Create or configure UM auto attendants|[Create a UM auto attendant](create-a-um-auto-attendant-exchange-2013-help.md) <br/><br/> [Manage a UM auto attendant](manage-um-auto-attendant-exchange-2013-help.md)|
|☐|Create or configure UM mailbox policies|[Create a UM mailbox policy](create-um-mailbox-policy-exchange-2013-help.md) <br/><br/> [Manage a UM mailbox policy](manage-um-mailbox-policy-exchange-2013-help.md)|
|☐|Move existing UM-enabled mailboxes to Exchange 2013|[Mailbox moves in Exchange 2013](mailbox-moves-in-exchange-2013-exchange-2013-help.md)|
|☐|Enable new users for UM or configure settings for an existing UM-enabled user|[Enable a user for voice mail](enable-a-user-for-voice-mail-exchange-2013-help.md) <br/><br/> Manage voice mail settings for a user](manage-voice-mail-settings-exchange-2013-help.md)|
|☐|Configure your VoIP gateways, IP PBXs, and SIP-enabled PBXs to send all incoming calls to the Exchange 2013 Client Access servers|[Configuration notes for supported VoIP gateways, IP PBXs, and PBXs](configuration-notes-for-voip-gateways-exchange-2013-help.md) <br/><br/> [Connect a VoIP gateway, IP PBX, or session border controller to UM](connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md)|
|☐|Disable call answering on the Exchange 2007 UM servers|[How to Disable Unified Messaging on Exchange 2007](/previous-versions/office/exchange-server-2007/bb123529(v=exchg.80))|
|☐|Remove an Exchange 2007 UM server from a dial plan|[How to Remove a Unified Messaging Server from a Dial Plan](/previous-versions/office/exchange-server-2007/aa997238(v=exchg.80))|
