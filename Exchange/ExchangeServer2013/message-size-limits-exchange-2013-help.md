---
title: 'Message size limits: Exchange 2013 Help'
TOCTitle: Message size limits
ms:assetid: b6a3840d-b821-4e53-877b-59c16be77206
ms:mtpsurl: https://technet.microsoft.com/library/Bb124345(v=EXCHG.150)
ms:contentKeyID: 49284660
ms.reviewer: 
ms.topic: article
description: About setting message size limits in Microsoft Exchange
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Message size limits

_**Applies to:** Exchange Server 2013_

You can apply limits to messages that move through the Microsoft Exchange Server 2013 organization. You can restrict the total size of a message or the size of the individual components of a message, such as the message header, the message attachments, and the number of recipients. You can apply limits globally for the whole Exchange organization, or specifically to a connector or user object.

As you plan the message size limits for your Exchange organization, consider the following questions:

- What size limits should I impose on all incoming messages?
- What size limits should I impose on all outgoing messages?
- What is the mailbox quota for my Exchange organization?
- How do the message size limits that I have chosen relate to the mailbox quota size?
- Are there users in my Exchange organization who must send or receive messages that are larger than the specified allowed size?
- Does my Exchange network topology include other messaging systems or distinctly separate business units that have different message size limits?

This topic provides guidance to help you answer these questions.

## Types of message size limits

Following are the basic categories of the size limits available for individual messages:

- **Message header size limits**: These limits apply to the total size of all message header fields that are present in a message. The size of the message body or attachments isn't considered. Because the header fields are plain text, the size of the header is determined by the number of characters in each header field and by the total number of header fields. Each character of text consumes 1 byte.

    > [!NOTE]
    > Some third-party firewalls or proxy servers apply their own message header size limits. These third-party firewalls or proxy servers may have difficulty processing messages that contain attachment file names that are greater than 50 characters or attachment file names that contain non-US-ASCII characters.

- **Message size limits**: These limits apply to the total size of a message, which includes the message header, the message body, and any attachments. Message size limits may be imposed on incoming messages or outgoing messages. For internal message flow, Exchange uses the custom `X-MS-Exchange-Organization-OriginalSize:` message header to record the original message size of the message as it enters the Exchange organization. Whenever the message is checked against the specified message size limits, the lower value of the current message size or the original message size header is used. The size of the message can change because of content conversion, encoding, and agent processing.

- **Attachment size limits**: These limits apply to the maximum allowed size of a single attachment within a message. The message may contain many attachments that greatly increase the overall size of the message. However, an attachment size limit applies to the size of an individual attachment only.

- **Recipient limits**: These limits apply to the total number of message recipients. When a message is first composed, the recipients exist in the `To:`, `Cc:`, and `Bcc:` header fields. When the message is submitted for delivery, the message recipients are converted into `RCPT TO:` entries in the message envelope. A distribution group is counted as a single recipient during message submission.

## Scope of limits

Following are the basic categories for the scope of the limits available for individual messages:

- **Organizational limits**: These limits apply to all Exchange 2013 Mailbox servers and Exchange 2010 and Exchange 2007 Hub Transport servers that exist in the organization. If you have an Edge Transport server installed in the perimeter network, the specified limits apply to the specific server.

- **Connector limits**: These limits apply to any messages that use the specified Send connector, Receive connector, Delivery Agent connector, or Foreign connector for message delivery. Send connectors are defined in the Transport service on Mailbox servers and on Edge Transport servers. Receive connectors are defined in the Transport service on Mailbox servers, in the Front End Transport service on Client Access servers, and on Edge Transport servers.

- **Active Directory site links**: The Transport service on Mailbox servers use Active Directory sites and the costs that are assigned to the Active Directory IP site links as one of the factors to determine the least-cost routing path between Mailbox servers in the organization. You can assign specific message size limits to the Active Directory site links in your organization.

- **Server limits**: These limits apply to a specific Mailbox server or Edge Transport server. You can set the specified message limits independently on each Mailbox server or Edge Transport server.

    In Outlook Web App, the maximum HTTP request size limit setting on the Client Access servers also controls the size of messages that Outlook Web App users can send.

- **User limits**: These limits apply to a specific user object, such as a mailbox, contact, distribution group, or public folder.

The following tables show the message limits, including information about how to configure the limits in the Exchange Management Shell or the Exchange Administrator Center (EAC).

### Organizational limits

|Size limit|Default value|Shell configuration|EAC configuration|
|---|---|---|---|
|Maximum size for messages received|10 MB|Cmdlet: **Set-TransportConfig** <br/><br/> Parameter: _MaxReceiveSize_|**Mail flow** \> **Receive connectors** \> **More options** ![More Options Icon](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif) \> **Organization transport settings** \> **Limits** tab \> **Maximum receive message size**|
|Maximum size for messages sent|10 MB|Cmdlet: **Set-TransportConfig** <br/><br/> Parameter: _MaxSendSize_|**Mail flow** \> **Receive connectors** \> **More options** ![More Options Icon](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif) \> **Organization transport settings** \> **Limits** tab \> **Maximum send message size**|
|Maximum number of recipients per message|5000|Cmdlet: **Set-TransportConfig** <br/><br/> Parameter: _MaxRecipientEnvelopeLimit_|**Mail flow** \> **Receive connectors** \> **More options** ![More Options Icon](images/JJ150550.5381819e-3b21-4873-8714-e9b956290b28(EXCHG.150).gif) \> **Organization transport settings** \> **Limits** tab \> **Maximum number of recipients**|
|Maximum attachment size in Transport rules that apply to all Mailbox servers in the organization|Not configured|Cmdlets: **New-TransportRule**, **Set-TransportRule** <br/><br/> Parameter: _AttachmentSizeOver_|**Mail flow** \> **Rules** \> **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif) or **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif). <br/><br/> Use the predicate **Apply this rule if** \> **Any attachment** \> **is greater than or equal to** <br/><br/> Use the predicate **Apply this rule if** \> **The message** \> **size is greater than or equal to**|
|Maximum message size in Transport rules that apply to all Mailbox servers in the organization||Cmdlets: **New-TransportRule**, **Set-TransportRule** <br/><br/> Parameter: _MessageSizeOver_|**Mail flow** \> **Rules** \> **Add** ![Add Icon](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif) or **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif). <br/><br/> Use the predicate **Apply this rule if** \> **The message** \> **size is greater than or equal to**|

### Connector limits

|Size limit|Default value|Shell configuration|EAC configuration|
|---|---|---|---|
|Maximum header size through a Receive connector|128 KB|Cmdlets: **New-ReceiveConnector**, **Set-ReceiveConnector** <br/><br/> Parameter: _MaxHeaderSize_|N/A|
|Maximum message size through a Receive connector <br/><br/> **Note**: The actual message size may be smaller due to message encoding and content conversion.|**Transport service on Mailbox servers** <br/><br/> 35 MB for the Default and Client Proxy Receive connectors <br/><br/> **Front End Transport service on Client Access servers** <br/><br/> 36 MB for the Default Frontend and Outbound Proxy Frontend Receive connectors. <br/><br/> 35 MB for the Client Frontend Receive connector.|Cmdlets: **New-ReceiveConnector**, **Set-ReceiveConnector** <br/><br/> Parameter: _MaxMessageSize_|**Mail flow** \> **Receive connectors** \> **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif) \> **General** tab \> **Maximum receive message size**|
|Maximum number of recipients per message through a Receive connector|**Transport service on Mailbox servers** <br/><br/> 5,000 for the Default Receive connector <br/><br/> 200 for the Client Proxy Receive connector <br/><br/> **Front End Transport service on Client Access servers** <br/><br/> 200 for the Default Frontend, Client Frontend, and Client Proxy Frontend Receive connectors. <br/><br/> **Note**: If the number of recipients is exceeded for an anonymous sender, the message is accepted for the first 200 recipients. Most SMTP messaging servers detect that a recipient limit is in effect. The SMTP messaging server continues to resend the message in groups of 200 recipients until the message is delivered to all recipients.|Cmdlets: **New-ReceiveConnector**, **Set-ReceiveConnector** <br/><br/> Parameter: _MaxRecipientsPerMessage_|N/A|
|Maximum message size through a Send connector|10 MB|Cmdlets: **New-SendConnector**, **Set-SendConnector** <br/><br/> Parameter: _MaxMessageSize_|**Mail flow** \> **Send connectors** \> **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif) \> **General** tab \> **Maximum send message size**|
|Maximum message size through an Active Directory site link|Unlimited|Cmdlet: **Set-AdSiteLink** <br/><br/> Parameter: _MaxMessageSize_|N/A|
|Maximum message size through a delivery agent connector|Unlimited|Cmdlets: **New-DeliveryAgentConnector**, **Set-DeliveryAgentConnector** <br/><br/> Parameter: _MaxMessageSize_|N/A|
|Maximum message size through a foreign connector|Unlimited|**Cmdlet: Set-ForeignConnector** Parameter: _MaxMessageSize_|N/A|

### Server limits

|Size limit|Default value|Shell configuration|EAC configuration|
|---|---|---|---|
|Maximum header size for messages in the pickup directory|64 KB|Cmdlet: **Set-TransportService** <br/><br/> Parameter: _PickupDirectoryMaxHeaderSize_|N/A|
|Maximum number of recipients per message for messages in the pickup directory|100|Cmdlet: **Set-TransportService** <br/><br/> Parameter: _PickupDirectoryMaxRecipientsPerMessage_|N/A|
|Client-specific maximum messages size limits for Outlook Web App, Exchange ActiveSync, and Exchange Web Services clients|Outlook Web App: 35 MB <br/><br/> Exchange ActiveSync: 10 MB <br/><br/> Exchange Web Services: 64 MB  <br/><br/> **Note**: These values are approximately 33% larger than the actual usable maximum message size because of the overhead that's associated with Base64 encoding.|You configure these values in the appropriate web.config XML application configuration file on Client Access servers. For more information, see [Configure client-specific message size limits](configure-client-specific-message-size-limits-exchange-2013-help.md).|N/A|

### User limits

|Size Limit|Default value|Shell configuration|EAC configuration|
|---|---|---|---|
|Maximum message size that can be sent by this recipient|Unlimited|Cmdlets: <br/><br/> **Set-DistributionGroup** <br/><br/> **Set-DynamicDistributionGroup** <br/><br/> **Set-Mailbox** <br/><br/> **Set-MailContact** <br/><br/> **Set-MailUser** <br/><br/> **Set-MailPublicFolder** <br/><br/> **Set-RemoteMailbox** <br/><br/> Parameter: _MaxSendSize_|For mailboxes: <br/><br/> **Recipients** \> **Mailboxes** \> **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif) \> **Mailbox features** \> **Mail flow** \> **Message size restrictions** \> **View details** \> **Sent messages** <br/><br/> **Note**: This setting isn't configurable using the EAC for other recipient types.|
|Maximum message size that can be sent to this recipient|Unlimited <br/><br/> For site mailbox provisioning policies: 36 MB|Cmdlets: <br/><br/> **Set-DistributionGroup** <br/><br/> **Set-DynamicDistributionGroup** <br/><br/> **Set-Mailbox** <br/><br/> **Set-MailContact** <br/><br/> **Set-MailUser** <br/><br/> **Set-MailPublicFolder** <br/><br/> **New-SiteMailboxProvisioningPolicy** <br/><br/> **Set-SiteMailboxProvisioningPolicy** <br/><br/> Parameter: _MaxReceiveSize_|For mailboxes: <br/><br/> **Recipients** \> **Mailboxes** \> **Edit** ![Edit icon](images/JJ218640.6f53ccb2-1f13-4c02-bea0-30690e6ea71d(EXCHG.150).gif) \> **Mailbox features** \> **Mail flow** \> **Message size restrictions** \> **View details** \> **Received messages** <br/><br/> **Note**: This setting isn't configurable using the EAC for other recipient types.|
|Maximum number of recipients per message sent by this recipient|Unlimited|Cmdlets: <br/><br/> **Set-Mailbox**, **Set-MailUser** <br/><br/> Parameter: _RecipientLimits_|N/A|

## Order of precedence for message size limits

You can set different message size limits at different levels in the Exchange organization. As a message is routed through your Transport infrastructure, it may be subjected to several different message size restrictions. You should plan your message size restrictions in a way that makes sure that messages in the transport pipeline are rejected as early as possible if they violate message size limits. Generally speaking, you should set more restrictive limits at the points where messages enter your infrastructure. For example, any message size restrictions on your Receive connectors that receive messages from the Internet should be less than or equal to the message size restrictions you configure for your internal Exchange organization. It would be a waste of system resources for the Exchange server to accept and process a message from the Internet that would be rejected by the Transport service on your Mailbox servers. Make sure that your organization, server, and connector limits are configured in a way that minimizes any unnecessary processing of messages.

One exception to this approach is the user limits. User level limits take precedence over other message size restrictions. Therefore, you can configure a user to exceed the default message size limits for your organization. For example, you can allow a specific group of user mailboxes to send larger messages than the rest of the organization by configuring custom send and receive limits for those mailboxes.

The exceptions for the user limits only apply to message exchanges between authenticated users. If a message is sent to or received by a recipient on the Internet, the organizational limits will be applied. For example, assume that you have an organizational message size restriction of 10 MB, but you have configured the users in your marketing department to send and receive messages up to 50 MB. These users will be able to exchange large messages with each other, but they still won't be able to receive large messages from Internet users because such messages will be coming from unauthenticated senders.

## Messages exempt from size limits

The following list shows the types of messages generated by a Mailbox server or an Edge Transport server and exempted from all message size limits:

- System messages
- Agent-generated message
- Delivery status notification (DSN) messages
- Journal report messages
- Quarantined messages

However, these messages are still subject to the organizational value for maximum number of recipients in a message.
