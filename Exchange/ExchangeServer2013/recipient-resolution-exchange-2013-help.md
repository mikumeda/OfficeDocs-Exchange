---
title: 'Recipient resolution: Exchange 2013 Help'
TOCTitle: Recipient resolution
ms:assetid: 09deda5a-d405-45b1-a3ff-fefd3d76cdea
ms:mtpsurl: https://technet.microsoft.com/library/Bb430743(v=EXCHG.150)
ms:contentKeyID: 50934209
ms.reviewer: 
ms.topic: article
description: About recipient resolution in Microsoft Exchange
manager: serdars
ms.author: serdars
author: serdars
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Recipient resolution

_**Applies to:** Exchange Server 2013_

_Recipient resolution_ is the process of expanding and resolving all the recipients in a message. The act of resolving the recipients matches a recipient to the corresponding Active Directory object in the Microsoft Exchange organization. The act of expanding the recipients expands all distribution groups into a list of individual recipients. Recipient resolution allows message limits and alternative recipients to be applied correctly to each recipient.

In a Microsoft Exchange Server 2013 organization, recipient resolution is performed by the categorizer in the Transport service on Mailbox servers. Categorization on each message happens after a newly arrived message is put in the Submission queue. Recipient resolution, in addition to content conversion and routing, is performed on the message before the message is put in a delivery queue. The categorizer performs recipient resolution before routing. The component of the categorizer that's responsible for recipient resolution is frequently called the _resolver_.

## Top-level resolution

_Top-level resolution_ is the first stage of recipient resolution. Top-level resolution associates each recipient in an incoming message to a matching recipient object in Active Directory. During top-level resolution, the categorizer creates a list that contains the sender and the initial, unexpanded recipient email addresses that exist within the message. The categorizer then uses that list of email addresses to query Active Directory to find any mail-enabled objects that have matching email address attributes. When a match is found, the properties of matching Active Directory objects are cached for later use. Any sender message restrictions are also enforced.

## Recipient email addresses

Top-level resolution begins with a message and the initial, unexpanded list of recipients from the _message envelope_. The message envelope contains the commands that are used to transmit messages among SMTP messaging servers. The sender's email address is contained in the **MAIL FROM:** command. Each recipient's email address is contained in a separate **RCPT TO:** command. The envelope sender and envelope recipients are typically created from the sender and recipients in the `To:`, `From:`, `Cc:`, and `Bcc:` header fields in the message header. However, this isn't always true. The `To:`, `From:`, `Cc:`, and `Bcc:` header fields in a message are easily forged and may not match the actual sender or recipient email addresses that were used to transmit the message.

## Encapsulated email addresses

Standard SMTP email addresses follow the specifications of RFC 2821 and RFC 2822, such as chris@contoso.com, for example. However, an email address can also be a non-SMTP email address that's encapsulated inside a valid SMTP address. Exchange supports encapsulated addresses that use the Internet Mail Connector Encapsulated Address (IMCEA) encapsulation method.

This encapsulation method requires the encoding of any characters that are invalid in SMTP email addresses. Alphanumeric characters, the equal sign (=) and the hyphen (-) don't require encoding. Other characters use the following encoding syntax:

- A forward slash (/) is replaced by an underscore (\_).

- Other US-ASCII characters are replaced by a plus sign (+) and the two digits of its ASCII value are written in hexadecimal. For example, the space character has the encoded value `+20`.

The IMCEA encapsulation method uses the following syntax: `IMCEA<Type>-<address>@<domain>`

The placeholder \<_Type_\> identifies the type of non-SMTP address, for example `EX`, `X400`, or `FAX`.

> [!NOTE]
> Although `SMTP` and `X500` are theoretically valid values for \<_Type_\>, Exchange recipient resolution rejects any IMCEA-encoded addresses that use either of these types.

The placeholder \<_address_\> is the encoded original address. The placeholder \<_domain_\> represents the SMTP domain that's used to encapsulate the non-SMTP address, for example, contoso.com

With the IMCEA encapsulation method, addresses are unencapsulated only when the domain matches the default authoritative domain in the Exchange organization. For more information about accepted domains, see [Accepted domains](accepted-domains-exchange-2013-help.md).

The maximum length for an SMTP email address in Exchange is 571 characters. This limit includes the following:

- 315 characters for the name part of the address
- 255 characters for the domain name
- The at sign (@) character that separates the name part of the address from the domain name

Note that Exchange doesn't support messages that are encoded with the IMCEA encapsulation method when the name part of the address exceeds 315 characters, even if the complete email address is less than 571 characters.

## Address resolution

For each message, the sender email address and all recipient email addresses are added to a list that's used to query Active Directory. Any encapsulated addresses are unencapsulated before they're added to the list of email addresses. The Active Directory query is performed on up to 20 email addresses at a time. If the Active Directory query encounters any transient errors, the message is returned to the Submission queue and deferred for the time that's specified by the _ResolverRetryInterval_ key in the `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` XML application configuration file that's associated with the Microsoft Exchange Transport service. The default value is 30 minutes.

The following table describes the recipient objects that are found in Active Directory. For more information about Exchange recipient types, see [Recipients](recipients-exchange-2013-help.md).

### Recipient objects in Active Directory

|Active Directory recipient type|Description|
|---|---|
|DistributionGroup|Any mail-enabled group object. The distribution group object types are as follows: <ul><li>**MailUniversalDistributionGroup**   A universal distribution group object</li><li>**MailUniversalSecurityGroup**   A universal security group (USG) object that has an email address</li><li>**MailNonUniversalGroup**   A local security group object or global security group object that has an email address</li></ul>|
|DynamicDistributionGroup|An object that has the Active Directory class **msExchDynamicDistributionList**. For more information, see [Manage dynamic distribution groups](manage-dynamic-distribution-groups-exchange-2013-help.md).|
|Mailbox|A user object that has an email address and a defined _Database_ parameter|
|MailUser|A user object that has an email address without a defined _Database_ parameter. For more information, see [Manage mail users](manage-mail-users-exchange-2013-help.md).|
|MailContact|A contact object that has an email address. Typically, a mail contact is used for recipients outside the Exchange organization. A mail contact is also used in cross-forest Exchange environments. For more information, see [Manage mail contacts](manage-mail-contacts-exchange-2013-help.md).|
|MailPublicFolder|A public folder object that has an email address.|
|MicrosoftExchangeRecipient|An object that has the Active Directory class **msExchExchangeServerRecipient**. For more information about the Microsoft Exchange recipient object, see [Recipients](recipients-exchange-2013-help.md).|
|SystemAttendantMailbox|An object that has the Active Directory class **exchangeAdminService**. There should be only one system attendant mailbox in the Exchange organization.|
|SystemMailbox|A user object that has an email address and that's located in the Microsoft Exchange System Objects container. There should be one system mailbox for each mailbox database in the Exchange organization.|

An object that contains missing or malformed critical properties is classified by the Active Directory query as an invalid object. For example, a dynamic distribution group object without an email address is considered invalid. Messages that are sent to recipients that are classified as invalid objects generate a non-delivery report (NDR).

For each email address, a single initial query is performed for all possible recipient properties, such as the recipient identifiers, recipient type, message limits, email addresses, and alternative recipients. The applicable properties for the recipient are cached for later use. Recipient resolution classifies the recipients based on similarities in how the recipients are resolved, and the similarity of the applicable recipient properties.

The LDAP filter that's used for address resolution is described as follows:

- For the **EX** email address type, the LDAP filter is based on the recipient **legacyExchangeDN** Active Directory attribute or the recipient **proxyAddresses** Active Directory attribute. The **legacyExchangeDN** Active Directory attribute takes precedence.
- For all other email addresses types, the recipient **proxyAddresses** Active Directory attribute is used as the LDAP filter.

If the email address that's used in the message doesn't match the primary SMTP address of the corresponding Active Directory object, the categorizer rewrites the email address in the message to match the primary SMTP address. The original email address is saved in the `ORCPT=` entry in the **RCPT TO:** command in the message envelope.

## Sender message restrictions

The size that's used for the sender message size restriction is the value of the **X-MS-Exchange-Organization-OriginalSize:** header field in the message header. Exchange uses this header field to record the original message size of the message when it entered the Exchange organization. Whenever the message is checked against the specified message size limits, the lower value of the current message size or the original message size header is used. The size of the message can change because of content conversion, encoding, and agent processing. If this header field doesn't exist, it's created by using the current message size value. If the message is too large, an NDR is generated and additional message processing is stopped.

The sender recipient limit is only enforced in the Transport service on the first Mailbox server that processes the message. The original, unexpanded message envelope recipient count is compared to the sender recipient limit. The original, unexpanded message envelope recipient count is used to avoid the partial message delivery problems that occured in Microsoft Exchange Server 2003 when nested distribution lists used remote expansion servers.

The message sender and all recipients are marked as resolved by stamping an extended property in the message. This extended property allows the message to bypass top-level resolution if the message must go through recipient resolution again. A message may have to go through recipient resolution again because the Microsoft Exchange Transport service restarted.

## Expansion

Expansion occurs after top-level resolution. Expansion completely expands nested levels of recipients into individual recipients. Expansion may require multiple trips through the expansion process to expand all recipients. Not all recipients have to be expanded. However, all recipients must go through the expansion process. The expansion process also enforces recipient message restrictions for all kinds of recipients.

The following list describes the kinds of recipients that require expansion:

- **Distribution groups and dynamic distribution groups**: Distribution groups are expanded based on the **memberOf** Active Directory property. Dynamic distribution groups are expanded by using the Active Directory query definition. If the _ExpansionServer_ parameter is set on the group, the group isn't expanded by the current server. The distribution group is routed to the specified server for expansion.

    > [!NOTE]
    > If you select a specific transport server in your organization as the expansion server, the distribution group usage becomes dependent on the availability of the expansion server. If the expansion server is unavailable, any messages that are sent to the distribution group can't be delivered. If you plan to use specific expansion servers for your distribution groups, to reduce the risk of service interruption, you should consider implementing high availability solutions for these servers.

- **Alternative recipients**: The _ForwardingAddress_ parameter may be set on mailboxes and mail-enabled public folders. The _ForwardingAddress_ parameter redirects all messages to the specified alternative recipient. This is known as a _forwarded recipient_. When an alternative delivery address is specified in the _ForwardingAddress_ parameter and the _DeliverToMailboxAndForward_ parameter is set to `$true`, the message is delivered to the original recipient and the alternative recipient. This is known as _delivered and forwarded recipient_.

- **Contact chains**: A _contact chain_ is a mail user or mail contact that has the _ExternalEmailAddress_ parameter set to the email address of another recipient in the Exchange organization.

## Detection of recipient loops

As the distribution groups, alternative recipients, and contacts chains are expanded, the categorizer checks for _recipient loops_. A recipient loop is a recipient configuration problem that causes message delivery to the same recipients in an endless circle. The following list describes the different types of recipient loops:

- **Harmless recipient loop**: A harmless recipient loop results in successful message delivery. The following list describes two scenarios when harmless recipient loops occur:

  - When two distribution groups contain one another as members.
  - When mailboxes or mail-enabled public folders are set to deliver and forward to one another. This happens when the _DeliverToMailboxAndForward_ parameter of both recipients is set to `$true` and the _ForwardingAddress_ parameter is set to one another.

  When a harmless recipient loop is detected, the message is delivered to the recipient, but no additional attempts are made to deliver the message to the same recipient.

- **Broken recipient loop**: A broken recipient loop can't result in successful message delivery. An example of a broken recipient loop is when mailboxes or mail-enabled public folders have the _ForwardingAddress_ parameter set to one another. When the categorizer detects a broken recipient loop, expansion activity for the current recipient stops, and an NDR is generated for the recipient.

Detection of recipient loops doesn't prevent duplicate message delivery. For example, Distribution Group C will experience duplicate message delivery if the following conditions are true:

- Distribution Group B and Distribution Group C are members of Distribution Group A.
- Distribution Group C is also a member of Distribution Group B.

## Delivery report redirection for distribution groups

When a distribution group is expanded, the message type is checked to determine whether it's a delivery report message. If the message is a delivery report, the redirection settings of the distribution group are checked to determine whether redirection of the delivery report is required. You may want to suppress the delivery reports because the delivery reports may disclose unwanted information about the distribution group and its membership.

The following list describes the delivery report redirection settings that are available for distribution groups and dynamic distribution groups:

- **ReportToManagerEnabled**: This parameter enables delivery reports to be sent to the distribution group manager. Valid values are `$true` or `$false`. The default value is `$false`. For a distribution group, the manager is controlled by the _ManagedBy_ parameter in the **Set-Group** cmdlet. For a dynamic distribution group, the manager is controlled by the _ManagedBy_ parameter in the **Set-DynamicDistributionGroup** cmdlet.

- **ReportToOriginatorEnabled**: This parameter enables delivery reports to be sent to the sender of email messages that are sent to this distribution group. Valid values are `$true` or `$false`. The default value is `$true`.

    > [!NOTE]
    > The values of the _ReportToManagerEnabled_ parameter and _ReportToOriginatorEnabled_ parameter can't both be `$true`. If one parameter is set to `$true`, the other must be set to `$false`. The values of both parameters can be `$false`. This suppresses all redirection of all delivery report messages.

The following list describes the available delivery report messages:

- **Delivery receipt (DR)**: This report confirms that a message was delivered to its intended recipient.

- **Delivery status notification (DSN)**: This report describes the result of an attempt to deliver a message. For more information about DSN messages, see [DSNs and NDRs in Exchange 2013](dsns-and-ndrs-in-exchange-2013-exchange-2013-help.md).

- **Message disposition notification (MDN)**: This report describes the status of a message after it has been successfully delivered to a recipient. A read notification (RN) and a non-read notification (NRN) are both examples of an MDN message. MDN messages are defined in RFC 2298 and are controlled by the **Disposition-Notification-To:** header field in the message header. MDN settings that use the `Disposition-Notification-To:` header field are compatible with many different message servers. MDN settings can also be defined by using MAPI properties in Microsoft Outlook and Exchange.

- **Non-delivery report (NDR)**: This report indicates to the message sender that the message couldn't be delivered to the specified recipients.

- **Non-read notification (NRN)**: This report indicates that a message was deleted before it was read.

- **Out of office (OOF)**: This report indicates that the recipient won't respond to email messages. The acronym OOF dates back to the original Microsoft messaging system where the corresponding notification was named "out of facility."

- **Read notification (RN)**: This report indicates that a message was read.

- **Recall Report**: This report indicates the status of a recall request for a specific recipient. A recall request is when a sender tries to recall a sent message by using Outlook.

When a delivery report message is sent to a distribution group, the following settings cause the report message to be deleted:

- Report redirection isn't set. Alternatively, report redirection is set to the message sender.
- Report redirection is set to the distribution group manager, and the delivery report message isn't an NDR.

When a delivery report message is sent to a distribution group, the delivery report message may be delivered to the distribution group manager. This happens when report redirection is set to the distribution group manager, and the report message is an NDR.

When a message that isn't a delivery report message is sent to a distribution group, the message is delivered to the distribution group members. The report request settings are summarized in the following list:

- If report redirection is set to the message sender, the report request settings aren't modified.
- If report redirection isn't set, all report request settings are suppressed. The `NOTIFY=NEVER` entry is added to **RCPT TO:** for each recipient in the message envelope.
- If report redirection is set to the distribution group manager, all report request settings are suppressed except NDR messages that are sent to the distribution group manager.

## Message restrictions on recipients

The expansion process also enforces any message restrictions that are configured for recipients. These restrictions may be configured individually for each recipient or organizationally for all Hub Transport servers in the Exchange organization. The following table describes the message restrictions that are configured for recipients.

|Source|Parameter|Description|
|---|---|---|
|**Set-DistributionGroup** <br/><br/> **Set-DynamicDistributionGroup** <br/><br/> **Set-Mailbox** <br/><br/> **Set-MailContact** <br/><br/> **Set-MailPublicFolder** <br/><br/> **Set-MailUser** <br/><br/> **Set-TransportConfig**|_MaxReceiveSize_|The _MaxReceiveSize_ parameter specifies the size that's used for message restrictions that are configured for recipients is the value of the **X-MS-Exchange-Organization-OriginalSize:** header field in the message header. Exchange uses this header field to record the original message size of the message when it entered the Exchange organization. Whenever the message is checked against the specified message size limits, the lower value of the current message size or the original message size header is used. The size of the message can change because of content conversion, encoding, and agent processing. If this header field doesn't exist, it's created by using the current message size value. If the message is too large, an NDR is generated and additional message processing is stopped.|
|**Set-DistributionGroup** <br/><br/> **Set-DynamicDistributionGroup** <br/><br/> **Set-Mailbox** <br/><br/> **Set-MailContact** <br/><br/> **Set-MailPublicFolder** <br/><br/> **Set-MailUser**|_RequireSenderAuthenticationEnabled_|The _RequireSenderAuthenticationEnabled_ parameter requires that all messages that are sent to the recipient come from authenticated senders. When the value of this parameter is set to `$true`, messages from unauthenticated senders are rejected. All senders who send messages to the System and System Attendant mailboxes must be authenticated.|
|**Set-DistributionGroup** <br/><br/> **Set-DynamicDistributionGroup** <br/><br/> **Set-Mailbox** <br/><br/> **Set-MailContact** <br/><br/> **Set-MailPublicFolder** <br/><br/> **Set-MailUser**|_AcceptMessagesOnlyFromSendersOrMembers_ <br/><br/> _RejectMessagesFromSendersOrMembers_|The _AcceptMessagesOnlyFromSendersOrMembers_ parameter specifies the senders or distribution groups whose members are allowed to send messages to the recipient. Note that this parameter combines the functionality of the older _AcceptMessagesOnlyFrom_ and _AcceptMessagesOnlyFromDLMembers_ parameters. <br/><br/> The _RejectMessagesFromSendersOrMembers_ parameter specifies the senders or distribution groups whose members aren't allowed to send messages to the recipient. Note that this parameter combines the functionality of the older _RejectMessagesFrom_ and _RejectMessagesFromDLMembers_ parameters. <br/><br/> The categorizer checks the recipient permission in two passes. The first pass determines whether the sender is present in the _AcceptOnlyMessagesFromSendersOrMembers_ or _RejectMessagesFromSendersOrMembers_ parameter. If the sender isn't found in either parameter, the distribution groups in those parameters are fully expanded. This complete expansion of distribution groups may take some time. We recommend that you minimize the depth of nested distribution groups in those parameters.|

Certain types of messages that are sent by authenticated senders are exempt from restrictions. The following list describes the messages that are exempt from recipient restrictions:

- **All messages that are sent by the Microsoft Exchange recipient**: These messages include DSN messages, journal reports, quota messages, and other system-generated messages that are sent to internal message senders. For more information about the Microsoft recipient, see [Recipients](recipients-exchange-2013-help.md).

- **All messages that are sent by the external postmaster address**: These messages include DSN messages and other system-generated messages that are sent to external message senders. For more information about the external postmaster address, see [Configure the external postmaster address](configure-the-external-postmaster-address-exchange-2013-help.md).

Certain types of messages are blocked when they are sent from the Exchange organization to external domains. The settings are controlled by the following parameters in the **Set-RemoteDomain** cmdlet:

- _AllowedOOFType_
- _AutoForwardEnabled_
- _AutoReplyEnabled_
- _DeliveryReportEnabled_
- _NDREnabled_

For more information, see [Remote domains](remote-domains-exchange-2013-help.md).

## Bifurcation and controlling recipient expansion

Because the complete list of message recipients is expanded and resolved by recipient resolution, there are occasions when different copies of the same message must be created. These occasions are described by the following scenarios:

- **When message recipients require different message settings**: Message properties such as read receipts may have to be enabled for some recipients and blocked for other recipients. Creating a new version of the message that has slightly different properties than the original message is called _bifurcation_.

- **To limit the number of envelope recipients in a single message**: The recipient expansion process can generate thousands of individual recipients when large distribution groups are expanded. In Exchange, instead of creating a single copy of the message that has thousands of envelope recipients, multiple copies of the same message that have a limited number of envelope recipients are created.

## Bifurcation

Recipient resolution bifurcates a message if the following conditions are true:

- When the message sender in **MAIL FROM:**, in the message envelope, is updated. An example is when the _ReportToManagerEnabled_ parameter on a distribution group has a value of `$true`.

- When auto-response messages, such as DSNs, OOF messages, and recall reports must be suppressed.

- When alternative recipients are expanded.

- When a **Resent-From:** header field must be added to the message header. Resent header fields are informational header fields that can be used to determine whether a message has been forwarded by a user. Resent header fields are used so that the message appears to the recipient as if it was sent directly by the original sender. The recipient can view the message header to discover who forwarded the message. Resent header fields are defined in section 3.6.6 of RFC 2822.

- When the history of the expansion of the distribution group must be transmitted.

## Controlling recipient expansion

When the number of expanded recipients is too large, the categorizer splits the message into multiple copies. This is done to reduce system resource use during message expansion. The maximum number of envelope recipients in a message is controlled by the _ExpansionSizeLimit_ key in the `%ExchangeInstallPath%Bin\EdgeTransport.exe.config` application configuration file. The default value is 1000.

> [!WARNING]
> We recommend that you don't modify the value of the _ExpansionSizeLimit_ key on an Exchange transport server in a production environment.

## Recipient resolution diagnostics

Reporting and diagnostic information for recipient resolution is provided by performance counters, and message tracking log entries. These sources can help you identify and diagnose problems with recipient resolution.

## Recipient resolution performance counters

The following table describes the performance counters that are available for recipient resolution.

|Counter name|Display name|Description|
|---|---|---|
|AmbiguousRecipientsTotal|Ambiguous Recipients|This is the total number of ambiguous recipients that were detected during recipient resolution. Ambiguous recipients are different recipients that have matching **legacyExchangeDN** Active Directory attributes or matching **proxyAddresses** Active Directory attributes.|
|AmbiguousSendersTotal|Ambiguous Senders|This is the number of ambiguous senders that were detected during recipient resolution. Ambiguous senders are different senders that have matching **legacyExchangeDN** Active Directory attributes or matching **proxyAddresses** Active Directory attributes.|
|FailedRecipientsTotal|Failed Recipients|This is the number of failed recipients that were detected during recipient resolution.|
|LoopRecipientsTotal|Loop Recipients|This is the number of recipients that failed recipient resolution because of recipient loops.|
|MessagesChippedTotal|Messages Chipped|This is the total number of copies of the same message that were created during recipient resolution to control the number of envelope recipients in a single message. In Exchange, this process is referred to as _chipping_.|
|MessagesCreatedTotal|Messages Created|This is the number of messages that were created during recipient resolution.|
|MessagesRetriedTotal|Messages Retried|This is the number of messages that were scheduled for retry during recipient resolution.|
|UnresolvedOrgRecipientsTotal|Unresolved Org Recipients|This is the number of unresolved recipients from an authoritative domain that were detected during recipient resolution.|
|UnresolvedOrgSendersTotal|Unresolved Org Senders|This is the number of unresolved senders from an authoritative domain that were detected during recipient resolution.|

## Recipient resolution events in the message tracking log

The following table describes the recipient resolution events that are written in the message tracking log.

|Message tracking event|Description|
|---|---|
|EXPAND|This event indicates that a distribution group was expanded.|
|REDIRECT|This event indicates that a message sent to a mailbox recipient or a mail-enabled public folder recipient was redirected to an alternative recipient as specified by the _ForwardingAddress_ parameter.|
|RESOLVE|This event indicates that a recipient email address was changed to the primary SMTP email address of the corresponding Active Directory recipient object.|
|TRANSFER|This event indicates that message bifurcation or chipping occurred.|

For more information about message tracking, see [Message tracking](message-tracking-exchange-2013-help.md).
