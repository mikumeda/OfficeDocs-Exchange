---
title: 'Network ports for clients and mail flow in Exchange 2013: Exchange 2013 Help'
TOCTitle: Network ports for clients and mail flow in Exchange 2013
ms:assetid: fec09455-e99e-42eb-8b32-1ddc08d9a19e
ms:mtpsurl: https://technet.microsoft.com/library/Bb331973(v=EXCHG.150)
ms:contentKeyID: 64916714
ms.reviewer: 
ms.topic: article
description: Network ports for clients and mail flow in Exchange 2013
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Network ports for clients and mail flow in Exchange 2013

_**Applies to:** Exchange Server 2013_

This topic provides information about the network ports that are used by Microsoft Exchange Server 2013 for communication with email clients, Internet mail servers, and other services that are external to your local Exchange organization. Before we get into that, understand the following ground rules:

- We do not support restricting or altering network traffic between internal Exchange servers, between internal Exchange servers and internal Lync or Skype for Business servers, or between internal Exchange servers and internal Active Directory domain controllers in any and all types of topologies. If you have firewalls or network devices that could potentially restrict or alter this kind of network traffic, you need to configure rules that allow free and unrestricted communication between these servers (rules that allow incoming and outgoing network traffic on any port (including random RPC ports) and any protocol that never alter bits on the wire).

- Edge Transport servers are almost always located in a perimeter network, so it's expected that you'll restrict network traffic between the Edge Transport server and the Internet, and between the Edge Transport server and your internal Exchange organization. These network ports are described in this topic.

- It's expected that you'll restrict network traffic between external clients and services and your internal Exchange organization. It's also OK if you decide to restrict network traffic between internal clients and internal Exchange servers. These network ports are described in this topic.

## Network ports required for clients and services

The network ports that are required for email clients to access mailboxes and other services in the Exchange organization are described in the following diagram and table.

**Notes:**

- The destination for these clients and services is a Client Access server. This could be a standalone Client Access server or a Client Access server and Mailbox server installed on the same computer.

- Although the diagram shows clients and services from the Internet, the concepts are the same for internal clients (for example, clients in an accounts forest accessing Exchange servers in a resource forest). Similarly, the table doesn't have a source column because the source could be any location that's external to the Exchange organization (for example, the Internet or an accounts forest).

- Edge Transport servers have no involvement in the network traffic that's associated with these clients and services.

![Network ports required for clients and services.](images/Bb331973.f5ba3439-f001-43c8-848e-0e3fd0fce931(EXCHG.150).png)

|Purpose|Ports|Comments|
|---|---|---|
|Encrypted web connections are used by the following clients and services: <ul><li>Autodiscover service</li><li>Exchange ActiveSync</li><li>Exchange Web Services (EWS)</li><li>Offline address book distribution</li><li>Outlook Anywhere (RPC over HTTP)</li><li>Outlook MAPI over HTTP</li><li>Outlook Web App</li></ul>|443/TCP (HTTPS)|For more information about these clients and services, see the following topics: <ul><li>[Autodiscover service](autodiscover-service-for-exchange-2013.md)</li><li>[Exchange ActiveSync](exchange-activesync-exchange-2013-help.md)</li><li>[EWS reference for Exchange](/exchange/client-developer/web-service-reference/ews-reference-for-exchange)</li><li>[Offline address books](offline-address-books-exchange-2013-help.md)</li><li>[Outlook Anywhere](outlook-anywhere-exchange-2013-help.md)</li><li>[MAPI over HTTP](mapi-over-http-exchange-2013-help.md)</li><li>[What's new for Outlook Web App in Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md)</li></ul>|
|Unencrypted web connections are used by the following clients and services: <ul><li>Internet calendar publishing</li><li>Outlook Web App (redirect to 443/TCP)</li><li>Autodiscover (fallback when 443/TCP isn't available)</li></ul>|80/TCP (HTTP)|Whenever possible, we recommend using encrypted web connections on 443/TCP to help protect data and credentials. However, you may find that some services must be configured to use unencrypted web connections on 80/TCP to the Client Access server. <br/><br/> For more information about these clients and services, see the following topics: <ul><li>[Enable Internet calendar publishing](enable-internet-calendar-publishing-exchange-2013-help.md)</li><li>[What's new for Outlook Web App in Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md)</li><li>[Autodiscover service](autodiscover-service-for-exchange-2013.md)</li></ul>|
|IMAP4 clients|143/TCP (IMAP), 993/TCP (secure IMAP)|IMAP4 is disabled by default. For more information, see [>POP3 and IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md). <br/><br/> The IMAP4 service on the Client Access server proxies connections to the IMAP4 Backend service on a Mailbox server.|
|POP3 clients|110/TCP (POP3), 995/TCP (secure POP3)|POP3 is disabled by default. For more information, see [>POP3 and IMAP4 in Exchange Server 2013](pop3-and-imap4-in-exchange-server-2013-exchange-2013-help.md). <br/><br/> The POP3 service on the Client Access server proxies connections to the POP3 Backend service on a Mailbox server.|
|SMTP clients (authenticated)|587/TCP (authenticated SMTP)|The default Received connector named "Client Frontend _\<Server name\>_" listens for authenticated SMTP client submissions on port 587 on the Client Access server. <br/><br/> **Note**: If you have mail clients that can submit authenticated SMTP mail only on port 25, you can modify the network adapter bindings value of this Receive connector to also listen for authenticated SMTP mail submissions on port 25.|

## Network ports required for mail flow

How mail is delivered to and from your Exchange organization depends on your Exchange topology. The most important factor is whether you have a subscribed Edge Transport server deployed in your perimeter network.

## Network ports required for mail flow (no Edge Transport servers)

The network ports that are required for mail flow in an Exchange organization that has only Client Access servers and Mailbox servers are described in the following diagram and table. Although the diagram shows separate Mailbox and Client Access servers, the concepts are the same whether the Client Access server and the Mailbox server are installed on the same computer or on separate computers.

![Network ports required for mail flow (no Edge Transport servers).](images/Bb331973.af54dfd3-fe6b-4b6e-bb8e-b00df94a0be0(EXCHG.150).png "Network ports required for mail flow (no Edge Transport servers)")

|Purpose|Ports|Source|Destination|Comments|
|---|---|---|---|---|
|Inbound mail|25/TCP (SMTP)|Internet (any)|Client Access server|The default Receive connector named "Default Frontend _\<Client Access server name\>_" on the Client Access server listens for anonymous inbound SMTP mail on port 25. <br/><br/> Mail is relayed from the Client Access server to a Mailbox server using the implicit and invisible intra-organization Send connector that automatically routes mail between Exchange servers in the same organization.|
|Outbound mail|25/TCP (SMTP)|Mailbox server|Internet (any)|By default, Exchange doesn't create any Send connectors that allow you to send mail to the Internet. You have to create Send connectors manually. For more information, see [Send connectors](send-connectors-exchange-2013-help.md).|
|Outbound mail (if routed through the Client Access server)|25/TCP (SMTP)|Client Access server|Internet (any)|Outbound mail is routed through a Client Access server only when a Send connector is configured with **Proxy through Client Access server** in the Exchange admin center or `-FrontEndProxyEnabled $true` in the Exchange Management Shell. <br/><br/> In this case, the default Receive connector named "Outbound Proxy Frontend _\<Client Access server name\>_" on the Client Access server listens for outbound mail from the Mailbox server. For more information, see [Create a Send connector for email sent to the Internet](create-a-send-connector-for-email-sent-to-the-internet-exchange-2013-help.md).|
|DNS for name resolution of the next mail hop (not pictured)|53/UDP,53/TCP (DNS)|Internet-facing Exchange server (Client Access server or Mailbox server)|DNS server|See the Name resolution section.|

## Network ports required for mail flow with Edge Transport servers

A subscribed Edge Transport server that's installed in your perimeter network basically eliminates SMTP mail flow through the Client Access server. Specifically:

- Outbound mail from the Exchange organization never flows through a Client Access server. Mail always flows from a Mailbox server in the subscribed Active Directory site to the Edge Transport server (regardless of the version of Exchange on the Edge Transport server).

- Inbound mail never flows through a standalone Client Access server. Mail flows from the Edge Transport server to a Mailbox server in the subscribed Active Directory site. If the Mailbox server and the Client Access server are installed on the same computer, mail from an Exchange 2013 Edge Transport server first arrives on the computer at the Front End Transport service (the Client Access server role) before it flows to the Transport service (the Mailbox server role). Exchange 2007 or Exchange 2010 Edge Transport servers always deliver mail directly to the Transport service even when the Mailbox server and the Client Access server are installed on the same computer.

For more information, see [Mail flow](mail-flow-exchange-2013-help.md).

The network ports that are required for mail flow in Exchange organizations that have Edge Transport servers are described in the following diagram and table. Unless otherwise noted, the concepts are the same whether the Client Access server and the Mailbox server are installed on the same computer or on separate computers.

![Network ports required for mail flow with Edge Transport servers.](images/Bb331973.110c79b3-dbd9-4cb5-bba1-02048363ee1c(EXCHG.150).png "Network ports required for mail flow with Edge Transport servers")

|Purpose|Ports|Source|Destination|Comments|
|---|---|---|---|---|
|Inbound mail - Internet to Edge Transport server|25/TCP (SMTP)|Internet (any)|Edge Transport server|The default Receive connector named "Default internal Receive connector _\<Edge Transport server name\>_" on the Edge Transport server listens for anonymous SMTP mail on port 25.|
|Inbound mail - Edge Transport server to internal Exchange organization|25/TCP (SMTP)|Edge Transport server|Mailbox servers in the subscribed Active Directory site|The default Send connector named "EdgeSync - Inbound to _\<Active Directory site name\>_" relays inbound mail on port 25 to any Mailbox server in the subscribed Active Directory site. For more information, see the "Send connectors created during the Edge Subscription process" section in the topic, [Edge Subscriptions](edge-subscriptions-exchange-2013-help.md). <br/><br/> The service that actually receives mail depends on whether the Mailbox server and Client Access server are installed on the same computer or on separate computers. <ul><li>**Standalone Mailbox server**   The default Receive connector named "Default _\<Mailbox server name\>_" listens for inbound mail (including mail from Edge Transport servers) on port 25.</li><li>**Mailbox server and Client Access server installed on the same computer**   The default Receive connector named "Default Frontend _\<Server name\>_" in the Front End Transport service (the Client Access server role) listens for inbound mail (including mail from Exchange 2013 Edge Transport servers) on port 25.</li></ul>|
|Outbound mail - Internal Exchange organization to Edge Transport server|25/TCP (SMTP)|Mailbox servers in the subscribed Active Directory site|Edge Transport servers|Outbound mail always bypasses the Client Access server. <br/><br/> Mail is relayed from any Mailbox server in the subscribed Active Directory site to an Edge Transport server using the implicit and invisible intra-organization Send connector that automatically routes mail between Exchange servers in the same organization. <br/><br/> The default Receive connector named "Default internal Receive connector _\<Edge Transport server name\>_" on the Edge Transport server listens for SMTP mail on port 25 from any Mailbox server in the subscribed Active Directory site.|
|Outbound mail - Edge Transport server to Internet|25/TCP (SMTP)|Edge Transport server|Internet (any)|The default Send connector named "EdgeSync - _\<Active Directory site name\>_ to Internet" relays outbound mail on port 25 from the Edge Transport server to the Internet.|
|EdgeSync synchronization|50636/TCP (secure LDAP)|Mailbox servers in the subscribed Active Directory site that participate in EdgeSync synchronization|Edge Transport servers|When the Edge Transport server is subscribed to the Active Directory site, all Mailbox servers that exist in the site at the time participate in EdgeSync synchronization. However, any Mailbox servers that you add later don't automatically participate in EdgeSync synchronization.|
|DNS for name resolution of the next mail hop (not pictured)|53/UDP,53/TCP (DNS)|Edge Transport server|DNS server|See the Name resolution section.|
|Proxy server definition for sender reputation (not pictured)|user defined|Edge Transport servers|Internet|Sender reputation (the Protocol Analysis agent) analyzes inbound message paths in an effort to reduce spam. If your organization uses a proxy server to control access to the Internet, you need to define details about the proxy server so that sender reputation can work properly (in particular, open proxy detection and sender blocking). You use the _ProxyServerName_, _ProxyServerPort_ and _ProxyServerType_ parameters on the **Set-SenderReputationConfig** cmdlet to define your organization's proxy server so sender reputation can successfully connect to the Internet. For more information, see [Manage sender reputation](manage-sender-reputation-exchange-2013-help.md).|

## Name resolution

DNS resolution of the next mail hop is a fundamental part of mail flow in any Exchange organization. Exchange servers that are responsible for receiving inbound mail or delivering outbound mail must be able to resolve both internal and external host names for proper mail routing. And all internal Exchange servers must be able to resolve internal host names for proper mail routing. There are many different ways to design a DNS infrastructure, but the important result is to ensure name resolution for the next hop is working properly for all of your Exchange servers.

## Network ports required for hybrid deployments

The network ports that are required for an organization that uses both Exchange 2013 and Microsoft 365 or Office 365 are covered in the "Hybrid deployment protocols, port and endpoints" section in [Hybrid deployment prerequisites](../ExchangeHybrid/hybrid-deployment-prerequisites.md).

## Network ports required for Unified Messaging

The network ports that are required for Unified Messaging are covered in the following topics:

- [UM protocols, ports, and services](um-protocols-ports-and-services-exchange-2013-help.md)
- [Exchange Server 2013 SP1 Architecture Poster](https://www.microsoft.com/download/details.aspx?id=42542)
