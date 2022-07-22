---
title: 'Header firewall: Exchange 2013 Help'
TOCTitle: Header firewall
ms:assetid: 9b148f7b-47a9-4379-a55b-8d5310c1772f
ms:mtpsurl: https://technet.microsoft.com/library/Bb232136(v=EXCHG.150)
ms:contentKeyID: 50934222
ms.reviewer: 
ms.topic: article
description: In Exchange Server, header firewall removes specific header fields from messages
manager: serdars
ms.author: serdars
author: msdmaguire

f1.keywords:
- CSH
mtps_version: v=EXCHG.150
ms.custom:
- header firewall, organization X-headers
- header firewall, forest X-headers
- header firewall, header firewall permissions
- header firewall, routing headers
- header firewall, X-headers
- header firewall, transport architecture
---

# Header firewall

_**Applies to:** Exchange Server 2013_

In Microsoft Exchange Server 2013, _header firewall_ is a mechanism that removes specific header fields from inbound and outbound messages. There are two different types of header fields that are affected by header firewall:

- **X-headers**: An _X-header_ is a user-defined, unofficial header field. X-headers aren't specifically mentioned in RFC 2822, but the use of an undefined header field starting with **X-** has become an accepted way to add unofficial header fields to a message. Messaging applications, such as anti-spam, antivirus, and messaging servers may add their own X-headers to a message. In Exchange, the X-header fields contain details about the actions that are performed on the message by the Transport service, such as the spam confidence level (SCL), content filtering results, and rules processing status. Revealing this information to unauthorized sources could pose a potential security risk.

- **Routing headers**: Routing headers are standard SMTP header fields that are defined in RFC 2821 and RFC 2822. Routing headers stamp a message by using information about the different messaging servers that were used to deliver the message to the recipient. Routing headers that are inserted into messages by malicious users can misrepresent the routing path that a message traveled to reach a recipient.

Header firewall prevents the spoofing of these Exchange-related X-headers by removing them from inbound messages that enter the Exchange organization from untrusted sources. Header firewall prevents the disclosure of these Exchange-related X-headers by removing them from outbound messages sent to untrusted destinations outside the Exchange organization. Header firewall also prevents the spoofing of standard routing headers that are used to track the routing history of a message.

## Message header fields affected by header firewall in Exchange

The following types of X-headers and routing headers are affected by header firewall:

- **Organization X-headers**: These X-header fields start with **X-MS-Exchange-Organization-**.

- **Forest X-headers**: These X-header fields start with **X-MS-Exchange-Forest-**.

    For examples of organization X-headers and forest X-headers, see the Organization X-headers and forest X-headers in Exchange section at the end of this topic.

- **Received: routing headers**: A different instance of this header field is added to the message header by every messaging server that accepted and forwarded the message to the recipient. The **Received:** header typically includes the name of the messaging server and a date-timestamp.

- **Resent-\*: routing headers**: Resent header fields are informational header fields that can be used to determine whether a message has been forwarded by a user. The following resent header fields are available: **Resent-Date:**, **Resent-From:**, **Resent-Sender:**, **Resent-To:**, **Resent-Cc:**, **Resent-Bcc:**, and **Resent-Message-ID:**. The **Resent-** fields are used so that the message appears to the recipient as if it was sent directly by the original sender. The recipient can view the message header to discover who forwarded the message.

Exchange uses two different ways to apply header firewall to organization X-headers, forest X-headers, and routing headers that exist in messages:

- Permissions are assigned to Send connectors or Receive connectors that can be used to preserve or remove specific types of headers in messages when the message travels through the connector.

- Header firewall is automatically implemented for specific types of headers in messages during other types of message submission.

## How header firewall is applied to Receive connectors and Send connectors

Header firewall is applied to messages that travel through Send connectors and Receive connectors based on specific permissions that are assigned to the connectors.

If the permission is assigned to the Receive connector or Send connector, header firewall isn't applied to the messages that travel through the connector. The affected header fields are preserved in the messages.

If the permission isn't assigned to the Receive connector or Send connector, header firewall is applied to the messages that travel through the connector. The affected header fields are removed from the messages.

The following table describes the permissions on Send connectors and Receive connectors that are used to apply header firewall, and the affected header fields.

|Connector type|Permission|Description|
|---|---|---|
|Receive connector|**Ms-Exch-Accept-Headers-Organization**|This permission affects organization X-header fields that start with **X-MS-Exchange-Organization-** in inbound messages.|
|Receive connector|**Ms-Exch-Accept-Headers-Forest**|This permission affects forest X-header fields that start with **X-MS-Exchange-Forest-** in inbound messages.|
|Receive connector|**Ms-Exch-Accept-Headers-Routing**|This permission affects **Received:** and **Resent-*:** routing header fields in inbound messages.|
|Send connector|**Ms-Exch-Send-Headers-Organization**|This permission affects organization X-header fields that start with **X-MS-Exchange-Organization-** in outbound messages.|
|Send connector|**Ms-Exch-Send-Headers-Forest**|This permission affects forest X-header fields that start with **X-MS-Exchange-Forest-** in outbound messages.|
|Send connector|**Ms-Exch-Send-Headers-Routing**|This permission affects **Received:** and **Resent-*:** routing header fields in outbound messages.|

## Header firewall for inbound messages on Receive connectors

The following table describes the default application of the header firewall permissions on Receive connectors.

|Permission|Default Exchange security principals that have the permission assigned|Permission group that has the security principals as members|Default usage type that assigns the permission groups to the Receive connector|
|---|---|---|---|
|**Ms-Exch-Accept-Headers-Organization** and **Ms-Exch-Accept-Headers-Forest**|<ul><li>Hub Transport servers</li><li>Edge Transport servers</li><li>Exchange Servers <br/><br/> **Note**: On Hub Transport servers only</li></ul>|**ExchangeServers**|`Internal`|
|**Ms-Exch-Accept-Headers-Routing**|Anonymous user account|**Anonymous**|`Internet`|
|**Ms-Exch-Accept-Headers-Routing**|Authenticated user accounts|**ExchangeUsers**|`Client` (unavailable on Edge Transport servers)|
|**Ms-Exch-Accept-Headers-Routing**|<ul><li>Hub Transport servers</li><li>Edge Transport servers</li><li>Exchange Servers <br/><br/> **Note**: Hub Transport servers only</li><li>Externally Secured servers</li></ul>|**ExchangeServers**|`Internal`|
|**Ms-Exch-Accept-Headers-Routing**|Partner Server account|**Partner**|`Internet` and `Partner`|

## Header firewall on custom Receive connectors

If you want to apply header firewall to messages in a custom Receive connector scenario, use any of the following methods:

- Create the Receive connector with a usage type that automatically applies header firewall to messages. Note that you can set the usage type only when you create the Receive connector.

  - To remove the organization X-headers or forest X-headers from messages, create a Receive connector and select a usage type other than `Internal`.

  - To remove the routing headers from messages, do one of the following actions:

    - Create a Receive connector and select the usage type `Custom`. Don't assign any permission groups to the Receive connector.

    - Modify an existing Receive connector, and set the _PermissionGroups_ parameter to the value `None`.

      Note that if you have a Receive connector that has no permission groups assigned to it, you need to add security principals to the Receive connector as described in the last step.

- Use the **Remove-ADPermission** cmdlet to remove the **Ms-Exch-Accept-Headers-Organization** permission, the **Ms-Exch-Accept-Headers-Forest** permission, and the **Ms-Exch-Accept-Headers-Routing** permission from a security principal that's configured on the Receive connector. This method doesn't work if the permission has been assigned to the security principal using a permission group on the Receive connector, because you can't modify the permissions assignments or the group membership of a permission group.

- Use the **Add-ADPermission** cmdlet to add the appropriate security principals that are required for mail flow on the Receive connector. Make sure that no security principals have the **Ms-Exch-Accept-Headers-Organization** permission, the **Ms-Exch-Accept-Headers-Forest** permission, and the **Ms-Exch-Accept-Headers-Routing** permission assigned to them. If necessary, use the **Add-ADPermission** cmdlet to deny the **Ms-Exch-Accept-Headers-Organization** permission, the **Ms-Exch-Accept-Headers-Forest** permission, and the **Ms-Exch-Accept-Headers-Routing** permission to the security principals that are configured on the Receive connector.

For more information, see the following topics:

- [Receive connectors](receive-connectors-exchange-2013-help.md)
- [Add-ADPermission](/powershell/module/exchange/Add-ADPermission)
- [Remove-ADPermission](/powershell/module/exchange/Remove-ADPermission)

## Header firewall for outbound messages on Send connectors

The following table describes the default application of the header firewall permissions on Send connectors.

|Permission|Default Exchange security principals that have the permission assigned|Default usage type that assigns the security principals to the Send connector|
|---|---|---|
|**Ms-Exch-Send-Headers-Organization** and **Ms-Exch-Send-Headers-Forest**|<ul><li>Hub Transport servers</li><li>Edge Transport servers</li><li>Exchange Servers  **Note**: On Hub Transport servers only</li><li>Externally Secured servers</li><li>**ExchangeLegacyInterop** universal security group</li></ul>|`Internal`|
|**Ms-Exch-Send-Headers-Routing**|<ul><li>Hub Transport servers</li><li>Edge Transport servers</li><li>Exchange Servers <br/><br/> **Note**: On Hub Transport servers only</li><li>Externally Secured servers</li><li>**ExchangeLegacyInterop** universal security group</li></ul>|`Internal`|
|**Ms-Exch-Send-Headers-Routing**|Anonymous User Account|`Internet`|
|**Ms-Exch-Send-Headers-Routing**|Partner Servers|`Partner`|

## Header firewall on custom Send connectors

If you want to apply header firewall to messages in a custom Send connector scenario, use the any of the following methods:

- Create the Send connector with a usage type that automatically applies header firewall to messages. Note that you can set the usage type only when you create the Send connector.

  - To remove the organization X-headers or forest X-headers from messages, create a Send connector and select a usage type other than `Internal` or `Partner`.

  - To remove the routing headers from messages, create a Send connector and select the usage type `Custom`. The **Ms-Exch-Send-Headers-Routing** permission is assigned to all Send connector usage types except `Custom`.

- Remove a security principal that assigns the **Ms-Exch-Send-Headers-Organization** permission, the **Ms-Exch-Send-Headers-Forest**, and the **Ms-Exch-Send-Headers-Routing** permission from the connector.

- Use the **Remove-ADPermission** cmdlet to remove the **Ms-Exch-Send-Headers-Organization** permission, the **Ms-Exch-Send-Headers-Forest** permission, and the **Ms-Exch-Send-Headers-Routing** permission from one of the security principals that's configured on the Send connector.

- Use the **Add-ADPermission** cmdlet to deny the **Ms-Exch-Send-Headers-Organization** permission, the **Ms-Exch-Send-Headers-Forest** permission, and the **Ms-Exch-Send-Headers-Routing** permission to one of the security principals that are configured on the Send connector.

For more information, see the following topics:

- [Send connectors](send-connectors-exchange-2013-help.md)
- [Add-ADPermission](/powershell/module/exchange/Add-ADPermission)
- [Remove-ADPermission](/powershell/module/exchange/Remove-ADPermission)

## Header firewall for other message sources

Messages can enter the transport pipeline on a Mailbox server or an Edge Transport server without using Send connectors or Receive connectors. Header firewall is applied to these other message sources as described in the following list:

- **Pickup directory and Replay directory**: The Pickup directory is used by administrators or applications to submit message files. The Replay directory is used to resubmit messages that have been exported from Exchange message queues. For more information about the Pickup and Replay directories, see [Pickup directory and Replay directory](pickup-directory-and-replay-directory-exchange-2013-help.md).

  Organization X-headers, forest X-headers, and routing headers are removed from the message files in the Pickup directory.

  Routing headers are preserved in messages submitted by the Replay directory.

  Whether or not organization X-headers and forest X-headers are preserved or removed from messages in the Replay directory is controlled by the **X-CreatedBy:** header field in the message file:

  - If the value of **X-CreatedBy:** is `MSExchange15`, organization X-headers and forest X-headers are preserved in messages.
  - If the value of **X-CreatedBy:** isn't `MSExchange15`, organization X-headers and forest X-headers are removed from messages.
  - If the **X-CreatedBy:** header field doesn't exist in the message file, organization X-headers and forest X-headers are removed from messages.

- **Drop directory**: The Drop directory is used by Foreign connectors on Mailbox servers to send messages to messaging servers that don't use SMTP to transfer messages. For more information about Foreign connectors, see [Foreign connectors](foreign-connectors-exchange-2013-help.md).

  Organization X-headers and forest X-headers are removed from message files before they're put in the Drop directory.

  Routing headers are preserved in messages submitted by the Drop directory.

- **Mailbox Transport**: The Mailbox Transport service exists on Mailbox servers to transmit messages to and from mailboxes on Mailbox servers. For more information about the Mailbox Transport service, see [Mail flow](mail-flow-exchange-2013-help.md).

  Organization X-headers, forest X-headers, and routing headers are removed from outgoing messages that are sent from mailboxes by the Mailbox Transport Submission service.

  Routing headers are preserved for inbound messages to mailbox recipients by the Mailbox Transport Delivery service. The following organization X-headers are preserved for inbound messages to mailbox recipients by the Mailbox Transport Delivery service:

  - **X-MS-Exchange-Organization-SCL**
  - **X-MS-Exchange-Organization-AuthDomain**
  - **X-MS-Exchange-Organization-AuthMechanism**
  - **X-MS-Exchange-Organization-AuthSource**
  - **X-MS-Exchange-Organization-AuthAs**
  - **X-MS-Exchange-Organization-OriginalArrivalTime**
  - **X-MS-Exchange-Organization-OriginalSize**

- **DSN messages**: Organization X-headers, forest X-headers, and routing headers are removed from the original message or the original message header that's attached to the DSN message. For more information about DSN messages, see [DSNs and NDRs in Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

- **Transport agent submission**: Organization X-headers, forest X-headers, and routing headers are preserved in messages that are submitted by transport agents.

## Organization X-headers and forest X-headers in Exchange

The Transport service on Mailbox servers or Edge Transport servers insert custom X-header fields into the message header.

Organization X-headers start with **X-MS-Exchange-Organization-**. Forest X-headers start with **X-MS-Exchange-Forest-**. The following table describes some of the organization X-headers and forest X-headers that are used in messages in an Exchange organization.

|X-header|Description|
|---|---|
|**X-MS-Exchange-Forest-RulesExecuted**|Transport rules that acted on the message.|
|**X-MS-Exchange-Organization-Antispam-Report**|A summary of the anti-spam filter results that have been applied to the message by the Content Filter agent.|
|**X-MS-Exchange-Organization-AuthAs**|Specifies the authentication source. This X-header is always present when the security of a message has been evaluated. The possible values are `Anonymous`, `Internal`, `External`, or `Partner`.|
|**X-MS-Exchange-Organization-AuthDomain**|Populated during Domain Secure authentication. The value is the FQDN of the remote authenticated domain.|
|**X-MS-Exchange-Organization-AuthMechanism**|Specifies the authentication mechanism for the submission of the message. The value is a 2-digit hexadecimal number.|
|**X-MS-Exchange-Organization-AuthSource**|Specifies the FQDN of the server computer that evaluated the authentication of the message on behalf of the organization.|
|**X-MS-Exchange-Organization-Journal-Report**|Identifies journal reports in transport. As soon as the message leaves the transport service, the header becomes **X-MS-Journal-Report**.|
|**X-MS-Exchange-Organization-OriginalArrivalTime**|Identifies the time when the message first entered the Exchange organization.|
|**X-MS-Exchange-Organization-Original-Sender**|Identifies the original sender of a quarantined message when it first entered the Exchange organization.|
|**X-MS-Exchange-Organization-OriginalSize**|Identifies the original size of a quarantined message when it first entered the Exchange organization.|
|**X-MS-Exchange-Organization-Original-Scl**|Identifies the original SCL of a quarantined message when it first entered the Exchange organization.|
|**X-MS-Exchange-Organization-PCL**|Identifies the phishing confidence level. The possible phishing confidence level values are from 1 through 8. A larger value indicates a suspicious message. For more information, see [Anti-spam stamps](anti-spam-stamps-exchange-2013-help.md).|
|**X-MS-Exchange-Organization-Quarantine**|Indicates the message has been quarantined in the spam quarantine mailbox and a delivery status notification (DSN) has been sent. Alternatively, it indicates that the message was quarantined and released by the administrator. This X-header field prevents the released message from being submitted to the spam quarantine mailbox again. For more information, see [Release quarantined messages from the spam quarantine mailbox](release-quarantined-messages-from-the-spam-quarantine-mailbox-exchange-2013-help.md.|
|**X-MS-Exchange-Organization-SCL**|Identifies the SCL of the message. The possible SCL values are from 0 through 9. A larger value indicates a suspicious message. The special value -1 exempts the message from processing by the Content Filter agent. For more information, see [Content filtering](content-filtering-exchange-2013-help.md).|
|**X-MS-Exchange-Organization-SenderIdResult**|Contains the results of the Sender ID agent. The Sender ID agent uses the sender policy framework (SPF) to compare the message's source IP address to the domain that's used in the sender's email address. The Sender ID results are used to calculate the SCL of a message. For more information, see [Sender ID](sender-id-exchange-2013-help.md).|
