---
title: 'IPv6 support in Exchange 2013: Exchange 2013 Help'
TOCTitle: IPv6 support in Exchange 2013
ms:assetid: 33543023-eb9a-4102-b990-84a818a52814
ms:mtpsurl: https://technet.microsoft.com/library/Gg144561(v=EXCHG.150)
ms:contentKeyID: 48384951
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
ms.topic: article
description: Internet Protocol version 6 support in Exchange 2013
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# IPv6 support in Exchange 2013

_**Applies to:** Exchange Server 2013_

Internet Protocol version 6 (IPv6) is the most recent version of the Internet Protocol (IP). IPv6 is intended to correct many of the shortcomings of IPv4, which was the previous version of the IP.

In Microsoft Exchange Server 2013, IPv6 is supported only when IPv4 is also installed and enabled. If Exchange 2013 is deployed in this configuration, and the network supports IPv4 and IPv6, all Exchange servers can send data to and receive data from devices, servers, and clients that use IPv6 addresses.

This topic discusses IPv6 addressing in Exchange 2013. For additional background information about IPv6, see [Internet Protocol Version 6 (IPv6) Overview](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd379473(v=ws.10)).

## IPv6 support in Exchange 2013 components

The following table describes the components in Exchange 2013 that are affected by IPv6.

|Feature|IPv6 supported|Comments|
|---|---|---|
|IP Allow list and IP Block list in the Connection Filtering agent|Yes||
|IP Allow List providers and IP Block List providers in the Connection Filtering agent.|No|Currently, there is no widely accepted industry standard protocol for looking up IPv6 addresses. Most IP Block List providers don't support IPv6 addresses. If you allow anonymous connections from unknown IPv6 addresses on a Receive connector, you increase the risk that spammers will bypass IP Block List providers and successfully deliver spam into your organization.|
|Sender reputation in the Protocol Analysis agent|No|The Protocol Analysis agent doesn't compute the sender reputation level (SRL) for messages that originate from IPv6 senders. For more information about sender reputation, see [Sender reputation and the Protocol Analysis agent](sender-reputation-and-the-protocol-analysis-agent-exchange-2013-help.md).|
|Sender ID|Yes|For more information, see [Sender ID](sender-id-exchange-2013-help.md).|
|Receive connectors|Yes|IPv6 addresses are accepted for the following components: <ul><li>Local IP address bindings</li><li>Remote IP addresses</li><li>IP address ranges</li></ul> <p> We strongly recommend against configuring Receive connectors to accept anonymous connections from unknown IPv6 addresses. If your organization must receive mail from senders who use IPv6 addresses, create a dedicated Receive connector that restricts the remote IP addresses to the specific IPv6 addresses that those senders use. <br/><br/> For more information, see [Receive connectors](receive-connectors-exchange-2013-help.md).|
|Send connectors|Yes|IPv6 addresses are accepted for the following components: <ul><li>Smart host IP addresses</li><li>The _SourceIPAddress_ parameter for Send connectors configured on Edge Transport servers</li></ul> <p> **Note**: If you want to specify an IPv6 address for the _SourceIPAddress_ parameter, make sure that the appropriate DNS AAAA and mail exchange (MX) records are configured correctly. This helps ensure message delivery if a remote messaging server tries any kind of reverse lookup test on the specified IPv6 address. <br/><br/> For more information, see [Send connectors](send-connectors-exchange-2013-help.md).|
|Incoming message rate limits|Partial|Incoming message rate limits that you can set on a Receive connector, such as the _MaxInboundConnectionPercentagePerSource_ parameter, the _MaxInboundConnectionPerSource_ parameter, and the _TarpitInterval_ parameter, only apply to a global IPv6 address. Link local IPv6 addresses and site local IPv6 addresses aren't affected by any specified incoming message rate limits.|
|Unified Messaging|Yes|For more information, see [IPv6 support in Unified Messaging](ipv6-support-in-unified-messaging-exchange-2013-help.md).|
|Database availability group (DAG) member|Yes|Static IPv6 addresses are supported by Windows Server and the Cluster service. However, using static IPv6 addresses goes against best practices. Exchange 2013 doesn't support the configuration of static IPv6 addresses during setup. <br/><br/> Failover clusters support Intra-site Automatic Tunnel Addressing Protocol (ISATAP). They support only IPv6 addresses that allow for dynamic registration in DNS. Link local addresses can't be used in a cluster. <br/><br/> For more information about DAG network requirements, see the "Network requirements" section in [Planning for high availability and site resilience](planning-for-high-availability-and-site-resilience-exchange-2013-help.md).|

## Enable or disable protocols in the operating system

Exchange 2013 servers fully support IPv6 networks. Therefore, even if you aren't using IPv6, you don't need to disable IPv6 on your Exchange servers.

IPv6 support in Exchange 2013 requires IPv4 to be installed and enabled on all Exchange 2013 servers. Uninstalling IPv4 from your Exchange 2013 servers isn't supported.

To learn more about IPv6 support in Microsoft Windows, see [Internet Protocol Version 6 (IPv6) Overview](/previous-versions/windows/it-pro/windows-8.1-and-8/hh831730(v=ws.11)).

## IPv6 address basics

An IPv6 address is 128-bits long. The address is described by using colon-hexadecimal notation. Colon-hexadecimal notation describes the 128-bit address by using eight 16-bit, 4-digit hexadecimal numbers separated by the colon character (:). An example of an IPv6 address in colon-hexadecimal notation is 2001:0DB8:0000:0000:02AA:00FF:C0A8:640A.

You can express an IPv6 address by using the following methods:

- **Suppress leading zeros**: You can omit the leading zeros in any of the eight 4-digit hexadecimal numbers in an IPv6 address.

- **Double-colon compression**: You can use two colons (::) to represent contiguous 16-bit hexadecimal digits that contain all zeros. These all-zero digits may exist at the beginning, middle, or end of the IPv6 address. You can only use double-colon compression one time in an IPv6 address.

- **Trailing dotted-decimal notation**: You may express the last 32 bits at the end of an IPv6 address in dotted-decimal notation by separating the 8-bit digits with a period (.). Trailing dotted-decimal notation is frequently used with IPv4-compatible addresses.

The following table provides examples of the IPv6 address notation and the equivalent IPv6 address syntax.

### IPv6 address notation and syntax

|IPv6 address notation|IPv6 address syntax|
|---|---|
|Full IPv6 address|2001:0DB8:0000:0000:02AA:00FF:C0A8:640A|
|IPv6 address that uses suppressed leading zeros|2001:DB8:0:0:2AA:FF:C0A8:640A|
|IPv6 address that uses double-colon compression|2001:DB8::2AA:FF:C0A8:640A|
|IPv6 address that uses trailing dotted-decimal notation|2001:DB8::2AA:FF:192.168.100.10|

IPv6 addresses are categorized into the following types:

- **Unicast address**: A packet is delivered to one interface.
- **Multicast address**: A packet is delivered to multiple interfaces.
- **Anycast address**: A packet is delivered to the nearest of multiple interfaces. The distance between interfaces is defined by the routing cost.

IPv6 unicast addresses have the following possible scopes:

- **Link local**: The scope of the IPv6 address is the local subnet. IPv6 link local addresses are comparable to IPv4 link local addresses used in Automatic Private IP Addressing (APIPA).
- **Site local**: The scope of the IPv6 address is the local organization. Site local addresses were deprecated by RFC 3879 and replaced by unique local addresses as defined in RFC 4193. IPv6 site local addresses and IPv6 unique local addresses are comparable to IPv4 private IP addresses.
- **Global**: The scope of the IPv6 address is the whole world. IPv6 global addresses are comparable to IPv4 public IP addresses.

The following table provides a comparison of IPv4 elements and IPv6 elements.

### IPv4 vs. IPv6 elements

|Item|IPv4|IPv6|
|---|---|---|
|Private IP address|10.0.0.0/8 <br/><br/> 172.16.0.0/12 <br/><br/> 192.168.0.0/16|FD00::/8|
|Link local address|169.254.0.0/16|FE80::/64|
|Loopback address|127.0.0.1|::1|
|Unspecified address|0.0.0.0|::|
|Address resolution|Address Resolution Protocol (ARP)|Neighbor Discovery (ND)|
|Domain Name System (DNS) host name resolution|Address record (A record)|AAAA record or A6 record|

For more information about IPv6 addressing, see [IPv6 Address Types](/previous-versions/windows/it-pro/windows-server-2003/cc757359(v=ws.10)).

## Supported IPv6 Address Input Formats

The following types of IPv6 address input formats are supported in Exchange 2013:

- A single IPv6 address
- An IPv6 address range
- An IPv6 address together with a subnet mask
- An IPv6 address together with a subnet mask that uses Classless Interdomain Routing (CIDR) notation

The following table provides examples of the acceptable IPv6 address input formats in Exchange 2013.

### IPv6 address examples

|Type|Example of an IPv6 address|
|---|---|
|Single address|2001:DB8::2AA:FF:C0A8:640A|
|Address range|2001:DB8::2AA:FF:C0A8:640A-2001:DB8::2AA:FF:C0A8:6414|
|Address together with subnet mask|2001:DB8::2AA:FF:C0A8:640A(FFFF:FFFF:FFFF:FFFF::)|
|Address together with subnet mask that uses CIDR notation|2001:DB8::2AA:FF:C0A8:640A/64|

In Exchange 2013, the following input formats are supported:

- Suppression of leading zeros
- Double-colon compression
- Trailing dotted-decimal notation
