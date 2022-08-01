---
title: 'Sharing: Exchange 2013 Help'
TOCTitle: Sharing
ms:assetid: 09e6732a-4e99-44d0-801d-9463fdc57a9b
ms:mtpsurl: https://technet.microsoft.com/library/Dd638083(v=EXCHG.150)
ms:contentKeyID: 48384809
ms.reviewer: 
ms.topic: article
description: In Microsoft Exchange, administrators can set up different levels of calendar access to allow businesses to collaborate with other businesses and enable users share their schedules
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Sharing

_**Applies to:** Exchange Server 2013_

You may need to coordinate schedules with people in different organizations or with friends and family members so that you can work together on projects or plan social events. With Exchange 2013, administrators can set up different levels of calendar access to allow businesses to collaborate with other businesses and to let users share their schedules with others. Business-to-business calendar sharing is set up by creating _organization relationships_. User-to-user calendar sharing is set up by applying _sharing policies_.

> [!IMPORTANT]
> This feature of Exchange Server 2013 isn't fully compatible with Office 365 operated by 21Vianet in China and some feature limitations may apply. For more information, see [Learn about Office 365 operated by 21Vianet](/microsoft-365/admin/services-in-china/services-in-china).

## Sharing Scenarios in Exchange 2013

The following sharing scenarios are supported in Exchange 2013:

|Sharing goal|Setting to use|Requirements|
|---|---|---|
|Share calendars with a Microsoft 365 or Office 365 organization|Organization relationships|The Microsoft 365 or Office 365 organization is ready to configure. The on-premises Exchange administrator has to set up an authentication relationship with the cloud (also known as "federation") and must meet minimum software requirements. To learn more about setting up federation, see [Federation](federation-exchange-2013-help.md).|
|Share calendars with another on-premises Exchange organization|Organization relationships|Both on-premises Exchange organizations have to set up federation and must meet minimum software requirements|
|Share an Exchange user's calendar with an Internet user|Sharing policies|None, ready to configure|
|Share an Exchange user's calendar with another Exchange on-premises user|Sharing policies|Both on-premises Exchange organizations have to set up federation and must meet minimum software requirements.|

The following table lists the differences between organization relationships and sharing policies.

### Organization relationships vs. sharing policies

|Functionality|Organization relationship|Sharing policy|
|---|---|---|
|Requires a federation trust for your organization|Yes|Yes when sharing with other federated domain organizations. Not required for Internet sharing policies.|
|Recommends that the external domain be federated|Yes|Yes when sharing with other federated domain organizations. Not required for Internet sharing policies.|
|Allows sharing of free/busy information (including subject and location) with external organizations for a set of many users.|Yes|No|
|Allows sharing of Calendar folders with free/busy information|No|Yes|
|Allows sharing of Calendar folders with free/busy information, including subject and body|No|Yes|
|Requires users to send a sharing invitation to external recipients|No|Yes|
|Provides an access method|Your Client Access server accesses the Client Access server of the external organization and retrieves free/busy information for the external user when requested.|Your Client Access server accesses the Client Access server of the external organization and subscribes to the external user's Calendar folder. For Internet sharing policies, external users access either a restricted or public URL on the Client Access server.|
|Can be applied to all external domains|No (a one-to-one relationship between two Exchange 2013 organizations)|Yes|
|Provides users with different sharing experiences with external recipients|No|Yes, based on the sharing policy that's applied|
|Disables sharing for some users|Yes, by specifying a security distribution group for the organization relationship|Yes, by disabling the sharing policy that's applied|
|Requires that the mailbox reside on an Exchange 2013 Mailbox server|No|Yes|

## Limitations of free/busy sharing

The following limitations apply when sharing free/busy information between Exchange organizations:

1. **Outlook Web Access 2003**: When a user in an Exchange 2003 organization uses Outlook Web Access to access free/busy for users in a remote Exchange 2013 organization, the request will fail. Outlook Web Access connections from Exchange 2003 can't make WebDAV (Web-based Distributed Authoring and Versioning) connections to a free/busy system folder to retrieve the free/busy information for remote users. Because Exchange 2013 doesn't support WebDAV connections, the Exchange 2003 server can't connect to External (FYDIBOHF25SPDLT) on the Exchange 2013 CAS server for Outlook Web Access requests. Outlook clients don't experience this limitation because they use MAPI instead of WebDAV when connecting to External (FYDIBOHF25SPDLT).

2. **Wide Area Network (WAN) latency**: In Exchange 2003 organizations, the replicas for all free/busy folders must reside on Exchange 2010 SP2 or higher Mailbox servers. In environments where Exchange 2003 public folder databases are located in multiple physical sites, there may be excessive latency and performance issues if internal free/busy queries have to traverse WAN links to access Exchange 2010 public folder databases not located in the same physical site.

3. **Free/busy information period**: Free/busy information requests to an Exchange 2007 organization from an Exchange 2013 organization may fail due to a mismatch in the requested free/busy information period. By default, Exchange 2007 accepts availability requests for 42 days of free/busy information and Exchange 2013 may request 62 days of free/busy information. If the request exceeds the default 42 limit imposed by Exchange 2007, the request will fail.

    Follow the steps below to configure your Exchange 2007 CAS servers to accept longer period free/busy information requests:

    1. On all your Exchange 2007 CAS servers, open the following file with a text editor such as Notepad: \<Exchange Installation Path\>\\V14\\ClientAccess\\ExchWeb\\EWS\\web.config

        > [!CAUTION]
        > Before you make any changes to the web.config file, make a copy of the file and store it in a safe location.

    2. Locate the **appSettings** section in the web.config file.

    3. Add a new key "\<add key="maximumQueryIntervalDays" value="62" /\>" and save the web.config file.

        > [!NOTE]
        > The maximumQueryIntervalDays value isn't present by default. When this value isn't present, Exchange 2007 uses the default interval of 42 days.

    4. Stop and restart the Microsoft Internet Information Services (IIS) on all the Exchange 2007 CAS servers.

4. **Exchange organizations that have both on-premises and cloud users**: If you set up calendar sharing with another Exchange organization that is configured in a hybrid deployment with Microsoft 365 or Office 365, free/busy availability lookups for Microsoft 365-based or Office 365-based or remote users that have been moved to the cloud will fail. Because the organization relationship for your Exchange organization is with the remote on-premises Exchange organization, not the Microsoft 365-based or Office 365-based Exchange Online organization, the free/busy request can't query the Microsoft 365-based or Office 365-based users. Exchange 2013 doesn't support functionality to proxy these availability requests through the on-premises organization to the Microsoft 365 or Office 365 service.

For details about how to configure free/busy sharing between common Exchange deployments, see [Configuring federated sharing between Exchange organizations](configuring-federated-sharing-between-exchange-organizations-exchange-2013-help.md).

## Firewall considerations for federated sharing

Federated sharing features require that the Client Access servers in your organization have outbound access to the Internet by using HTTPS. You must allow outbound HTTPS access (port 443 for TCP) to all Exchange 2013 Mailbox servers in the organization.

For an external organization to access your organization's free/busy information, you must publish at least one Client Access server to the Internet. This requires inbound HTTPS access from the Internet to the Client Access server. Client Access servers in Active Directory sites that don't have a Client Access server published to the Internet can use Client Access servers in other Active Directory sites that are accessible from the Internet. The Client Access servers that aren't published to the Internet must have the external URL of the Web services virtual directory set with the URL that's visible to external organizations.

## Coexistence with Exchange 2010

In organizations that contain both Exchange 2010 and Exchange 2013 servers, users who have a mailbox on an Exchange 2010 Mailbox server can use organization relationships to share free/busy information with recipients in external Exchange 2013 federated domain organizations. The Exchange 2010 Client Access and Mailbox servers must be running SP2 or higher, and you must have at least one Exchange 2013 Client Access server in the Exchange 2010 organization.

## Coexistence with Exchange 2007

In organizations that contain both Exchange 2013 and Exchange 2007 servers, users who have a mailbox on an Exchange 2007 Mailbox server can use organization relationships to share free/busy information with recipients in external federated domain organizations. The Mailbox server must be running Exchange 2007 SP2 or higher, and you must have at least one Exchange 2013 Client Access server in the Exchange organization. You can use organization relationships by introducing a single Exchange 2013 Client Access server in the organization, providing a more robust solution than solutions that synchronize free/busy information and require GAL synchronization.

When using Outlook 2010 or Outlook Web App to scheduling a meeting on an Exchange 2007 server, a user who has a mailbox on an Exchange 2007 server can see free/busy information for a user in the external organization. Free/busy information for Exchange 2007 mailboxes is visible to recipients in the external organization.

Sharing policies are assigned to Exchange 2013 mailbox users. To use sharing policies, a mailbox must be located on an Exchange 2013 Mailbox server. Only Outlook 2010 and Outlook Web App clients can be used to generate or respond to sharing invitations.

## Sharing documentation

The following table contains links to topics that will help you learn about and manage sharing in Exchange 2013.

|Topic|Description|
|---|---|
|[Federation](federation-exchange-2013-help.md)|Learn more about the underlying trust infrastructure that supports sharing, an easy method for users to share calendar information with external recipients.|
|[Organization relationships](organization-relationships-exchange-2013-help.md)|Learn more about the one-to-one relationships between Exchange organizations that enable calendar free/busy sharing.|
|[Sharing policies](sharing-policies-exchange-2013-help.md)|Learn more about the person-to-person policies that enable sharing.|
