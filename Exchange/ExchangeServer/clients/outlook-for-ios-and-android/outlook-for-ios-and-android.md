---
ms.localizationpriority: medium
description: 'Summary: These articles contain architectural and security information for administrators about Outlook for iOS and Android in an Exchange Server 2016 or Exchange Server 2019 on-premises environment.'
ms.topic: article
author: JoanneHendrickson
ms.author: jhendr
ms.assetid: 8b46e0bf-334d-44ed-bf20-eab605fdcae6
title: Outlook for iOS and Android
ms.collection: exchange-server
ms.reviewer: smithre4
f1.keywords:
- NOCSH
audience: ITPro
ms.prod: exchange-server-it-pro
manager: serdars

---

# Outlook for iOS and Android

Outlook for iOS and Android supports two authentication types in Exchange on-premises environments: _Basic authentication_ and _hybrid Modern Authentication_.

Outlook for iOS and Android uses Basic authentication with Exchange ActiveSync in the following environments:

- In Exchange Server 2010 environments

- When a hybrid relationship with Microsoft 365 or Office 365 has not been configured

- When hybrid Modern Authentication has not been enabled

For more information see [Using Basic authentication with Outlook for iOS and Android](use-basic-auth.md).

For customers running Exchange Server 2013, Exchange Server 2016, or Exchange Server 2019 in a hybrid relationship with Microsoft 365 or Office 365, Outlook for iOS and Android can be configured to leverage hybrid Modern Authentication. For more information, see [Using hybrid Modern Authentication with Outlook for iOS and Android](use-hybrid-modern-auth.md).

> [!NOTE]
> The [Outlook for iOS and Android Help Center](https://support.microsoft.com/office/cd84214e-a5ac-4e95-9ea3-e07f78d0cde6) is available for users, including help for using the app on specific devices and troubleshooting information.

## Differences when managing devices on "Hybrid Modern Auth (HMA)" enabled on-premises Exchange servers

Historically for other EAS implementations, a unique device ID is provisioned for each smartphone trying to connect to the same OnPrem mailbox and ABQ (Allow, Block, Quarantine) or any MDM can manage these device IDs like for native EAS applications.

However, when connecting to HMA enabled on-premises tenant using Outlook Mobile there are some differences in design as the user's data is stored in a central cache inside of Exchange Online tenant . To understand the design philosophy and its benefits see section [Using hybrid Modern Authentication with Outlook for iOS and Android](/exchange/clients/outlook-for-ios-and-android/use-hybrid-modern-auth?view=exchserver-2019&preserveview=true). This capability also allows tenant admins to safely issue remote wipe of data for scenarios where a user leaves the company, or a device is compromised. Some of the differences are described below.

- **Users connect to a cache created inside the Exchange Online tenant**: When a user connects to a Hybrid Modern Authentication enabled On Premise tenant using Outlook Mobile application, on the backend Exchange creates a synchronized cache of users 4 weeks of data in a user-protected mailbox. What this means is if multiple devices connect, they will be accessing a single endpoint inside Exchange. And a unique device ID is seen On Premise side. The synchronized cache is also called a Cloud Cache account.

- **Cloud Cache might generate multiple devices**: The on-premises admin might see multiple devices because of how the Cloud Cache is bootstrapped and because expired devices may not be expired. When Exchange first validates the Cloud Cache account, it will use a generic device ID.  Once the account has been verified, a new personalized device ID called the subscription is used.

- **Blocking or issuing remote wipe**: If the on-premises admin wants to remove access to content, they should run a remote wipe on-premises. The Cloud Cache will proxy the remote wipe to all connected devices. If the on-premises admin wants to block access to content, they should do it through on-premises. Then Cloud Cache will be unable to sync any new content. To get more detail about remote wipe, see section [Perform a remote wipe on a mobile phone](/Exchange/clients/exchange-activesync/remote-wipe?view=exchserver-2019&preserveview=true)

## Best practice with MDM

- We recommend using an MDM like Intune associated with Conditional Access feature to manage Outlook Mobile application.
Refer to section [Managing Outlook for iOS and Android in Exchange Online](/exchange/clients-and-mobile-in-exchange-online/outlook-for-ios-and-android/manage-outlook-for-ios-and-android)

- Intune management works for accounts connected using Hybrid Modern Auth to on-premises servers. Indeed, that is one of its value propositions. All devices connected to a single Cloud Cache present the same ID to the on-premises server because they share the same physical storage in that Microsoft 365 "middle tier". Intune management does not work for accounts connecting via Basic auth to on-premises because the on-premises admin has little visibility into the Microsoft 365 identities involved.

- A single on-premises user may have a single Microsoft 365 identity. He may have more than 1. That's because the Microsoft 365 identity is _computed_ from the logon name presented by the client user. This may be tim@contoso.com. It may be contoso.com/tim. Each can be used to control logon to the on-premises server but there's no way inside Microsoft 365 to discover that these 2 different names represent the same on-premises user. As such, each will have a different Microsoft 365 identity, a different Microsoft 365 Cloud Cache and present a different device ID to the on-premises EAS server.
