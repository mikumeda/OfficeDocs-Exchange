---
title: 'Transport rule conditions and exceptions (predicates) in Exchange 2013'
TOCTitle: Transport rule conditions and exceptions (predicates)
ms:assetid: c918ea00-1e68-4b8b-8d51-6966b4432e2d
ms:mtpsurl: https://technet.microsoft.com/library/Dd638183(v=EXCHG.150)
ms:contentKeyID: 49361079
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: About Transport rule conditions and exceptions in Exchange 2013
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Transport rule conditions and exceptions (predicates) in Exchange 2013

_**Applies to:** Exchange Server 2013_

Conditions and exceptions in transport rules identify the messages that the rule is applied to or not applied to. For example, if the rule adds a disclaimer to messages, you can configure the rule to only apply to messages that contain specific words, messages sent by specific users, or to all messages except those sent by the members of a specific group. Collectively, the conditions and exceptions in transport rules are also known as *predicates*, because for every condition, there's a corresponding exception that uses the exact same settings and syntax. The only difference is conditions specify messages to include, while exceptions specify messages to exclude.

Most conditions and exceptions have one property that requires one or more values. For example, the **The sender is** condition requires the sender of the message. Some conditions have two properties. For example, the **A message header includes any of these words** condition requires one property to specify the message header field, and a second property to specify the text to look for in the header field. Some conditions or exceptions don't have any properties. For example, the **Any attachment has executable content** condition simply looks for attachments in messages that have executable content.

For more information about transport rules in Exchange Server 2013, see [Transport rules in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md).

For more information about conditions and exceptions in transport rules in Exchange Online Protection or Exchange Online, see [Mail flow rule conditions and exceptions (predicates) in Exchange Online](../ExchangeOnline/security-and-compliance/mail-flow-rules/conditions-and-exceptions.md).

## Conditions and exceptions for transport rules on Mailbox servers

The tables in the following sections describe the conditions and exceptions that are available in transport rules on Mailbox servers. The properties types are described in the Property types section.

[Senders](#senders)

[Recipients](#recipients)

[Message subject or body](#message-subject-or-body)

[Attachments](#attachments)

[Any recipients](#any-recipients)

[Message sensitive information types, To and Cc values, size, and character sets](#message-sensitive-information-types-to-and-cc-values-size-and-character-sets)

[Sender and recipient](#sender-and-recipient)

[Message properties](#message-properties)

[Message headers](#message-headers)

**Notes**:

- After you select a condition or exception in the Exchange admin center (EAC), the value that's ultimately shown in the **Apply this rule if** or **Except if** field is often different (shorter) than the click path value you selected. Also, when you create new rules based on a template (a filtered list of scenarios), you can often select a short condition name instead of following the complete click path. The short names and full click path values are shown in the EAC column in the tables.

- If you select **\[Apply to all messages\]** in the EAC, you can't specify any other conditions. The equivalent in the Exchange Management Shell is to create a rule without specifying any condition parameters.

- The settings and properties are the same in conditions and exceptions, so the output of the **Get-TransportRulePredicate** cmdlet doesn't list exceptions separately. Also, the names of some of the predicates that are returned by this cmdlet are different than the corresponding parameter names, and a predicate might require multiple parameters.

## Senders

For conditions and exceptions that examine the sender's address, you can specify where rule looks for the sender's address.

In the EAC, in the **Properties of this rule** section, click **Match sender address in message**. Note that you might need to click **More options** to see this setting. In the Exchange Management Shell, the parameter is *SenderAddressLocation*. The available values are:

- **Header**: Only examine senders in the message headers (for example, the **From**, **Sender**, or **Reply-To** fields). This is the default value, and is the way transport rules worked before Exchange 2013 Cumulative Update 1 (CU1).

- **Envelope**: Only examine senders from the message envelope (the **MAIL FROM** value that was used in the SMTP transmission, which is typically stored in the **Return-Path** field). Note that message envelope searching is only available for the following conditions (and the corresponding exceptions):

- **The sender is** (_From_)
  - **The sender is a member of** (_FromMemberOf_)
  - **The sender address includes** (_FromAddressContainsWords_)
  - **The sender address matches** (_FromAddressMatchesPatterns_)
  - **The sender's domain is** (_SenderDomainIs_)

- **Header or envelope** (`HeaderOrEnvelope`) Examine senders in the message header and the message envelope.

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**The sender is** <br/><br/> **The sender** \> **is this person**|_From_ <br/><br/> _ExceptIfFrom_|`Addresses`|Messages that are sent by the specified mailboxes, mail users, or mail contacts in the Exchange organization.|Exchange 2007 or later|
|**The sender is located** <br/><br/> **The sender** \> **is external/internal**|_FromScope_ <br/><br/> _ExceptIfFromScope_|`UserScopeFrom`|Messages that are sent by either internal senders or external senders.|Exchange 2007 or later|
|**The sender is a member of** <br/><br/> **The sender** \> **is a member of this group**|_FromMemberOf_ <br/><br/> _ExceptIfFromMemberOf_|`Addresses`|Messages that are sent by a member of the specified group.|Exchange 2007 or later|
|**The sender address includes** <br/><br/> **The sender** \> **address includes any of these words**|_FromAddressContainsWords_ <br/><br/> _ExceptIfFromAddressContainsWords_|`Words`|Messages that contain the specified words in the sender's email address.|Exchange 2007 or later|
|**The sender address matches** <br/><br/> **The sender** \> **address matches any of these text patterns**|_FromAddressMatchesPatterns_ <br/><br/> _ExceptIfFromAddressMatchesPatterns_|`Patterns`|Messages where the sender's email address contains text patterns that match the specified regular expressions.|Exchange 2007 or later|
|**The sender's specified properties include any of these words** <br/><br/> **The sender** \> **has specific properties including any of these words**|_SenderADAttributeContainsWords_ <br/><br/> _ExceptIfSenderADAttributeContainsWords_|First property: `ADAttribute` <br/><br/> Second property: `Words`|Messages where the specified Active Directory attribute of the sender contains any of the specified words. <br/><br/> Note that the **Country** attribute requires the two-letter country code value (for example, DE for Germany).|Exchange 2010 or later|
|**The sender's specified properties match these text patterns** <br/><br/> **The sender** \> **has specific properties matching these text patterns**|_SenderADAttributeMatchesPatterns_ <br/><br/> _ExceptIfSenderADAttributeMatchesPatterns_|First property: `ADAttribute` <br/><br/> Second property: `Patterns`|Messages where the specified Active Directory attribute of the sender contains text patterns that match the specified regular expressions.|Exchange 2010 or later|
|**The sender has overridden the Policy Tip** <br/><br/> **The sender** \> **has overridden the Policy Tip**|_HasSenderOverride_ <br/><br/> _ExceptIfHasSenderOverride_|n/a|Messages where the sender has chosen to override a data loss prevention (DLP) policy. For more information about DLP policies, see [Data loss prevention](data-loss-prevention-exchange-2013-help.md).|Exchange 2013 or later|
|**Sender's IP address is in the range** <br/><br/> **The sender** \> **IP address is in any of these ranges or exactly matches**|_SenderIPRanges_ <br/><br/> _ExceptIfSenderIPRanges_|`IPAddressRanges`|Messages where the sender's IP address matches the specified IP address, or falls within the specified IP address range.|Exchange 2013 or later|
|**The sender's domain is** <br/><br/> **The sender** \> **domain is**|_SenderDomainIs_ <br/><br/> _ExceptIfSenderDomainIs_|`DomainName`|Messages where the domain of the sender's email address matches the specified value. <br/><br/> If you need to find sender domains that _contain_ the specified domain (for example, any subdomain of a domain), use **The sender address matches** (_FromAddressMatchesPatterns_) condition and specify the domain by using the syntax: `'\.domain\.com$'`.|Exchange 2013 or later|

## Recipients

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**The recipient is** <br/><br/> **The recipient** \> **is this person**|_SentTo_ <br/><br/> _ExceptIfSentTo_|`Addresses`|Messages where one of the recipients is the specified mailbox, mail user, or mail contact in the Exchange organization. The recipients can be in the **To**, **Cc**, or **Bcc** fields of the message. <p> **Note:** You can't specify distribution groups or mail-enabled security groups. If you need to take action on messages that are sent to a group, use the **To box contains** (_AnyOfToHeader_) condition instead.|Exchange 2007 or later|
|**The recipient is located** <br/><br/> **The recipient** \> **is external/external**|_SentToScope_ <br/><br/> _ExceptIfSentToScope_|`UserScopeTo`|Messages that are sent to internal recipients, external recipients, external recipients in partner organizations, or external recipients in non-partner organizations.|Exchange 2007 or later|
|**The recipient is a member of** <br/><br/> **The recipient** \> **is a member of this group**|_SentToMemberOf_ <br/><br/> _ExceptIfSentToMemberOf_|`Addresses`|Messages that contain recipients who are members of the specified group. The group can be in the **To**, **Cc**, or **Bcc** fields of the message.|Exchange 2007 or later|
|**The recipient address includes** <br/><br/> **The recipient** \> **address includes any of these words**|_RecipientAddressContainsWords_ <br/><br/> _ExceptIfRecipientAddressContainsWords_|`Words`|Messages that contain the specified words in the recipient's email address. <p> **Note:** This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address.|Exchange 2010 or later|
|**The recipient address matches** <br/><br/> **The recipient** \> **address matches any of these text patterns**|_RecipientAddressMatchesPatterns_ <br/><br/> _ExceptIfRecipientAddressMatchesPatterns_|`Patterns`|Messages where a recipient's email address contains text patterns that match the specified regular expressions. <p> **Note:** This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address.|Exchange 2010 or later|
|**The recipient's specified properties include any of these words** <br/><br/> **The recipient** \> **has specific properties including any of these words**|_RecipientADAttributeContainsWords_ <br/><br/> _ExceptIfRecipientADAttributeContainsWords_|First property: `ADAttribute` <br/><br/> Second property: `Words`|Messages where the specified Active Directory attribute of a recipient contains any of the specified words. <br/><br/> Note that the **Country** attribute requires the two-letter country code value (for example, DE for Germany).|Exchange 2010 or later|
|**The recipient's specified properties match these text patterns** <br/><br/> **The recipient** \> **has specific properties matching these text patterns**|_RecipientADAttributeMatchesPatterns_ <br/><br/> _ExceptIfRecipientADAttributeMatchesPatterns_|First property: `ADAttribute` <br/><br/> Second property: `Patterns`|Messages where the specified Active Directory attribute of a recipient contains text patterns that match the specified regular expressions.|Exchange 2010 or later|
|**A recipient's domain is** <br/><br/> **The recipient** \> **domain is**|_RecipientDomainIs_ <br/><br/> _ExceptIfRecipientDomainIs_|`DomainName`|Messages where the domain of a recipient's email address matches the specified value. <br/><br/> If you need to find recipient domains that _contain_ the specified domain (for example, any subdomain of a domain), use **The recipient address matches** (_RecipientAddressMatchesPatterns_) condition, and specify the domain by using the syntax `'\.domain\.com$'`.|Exchange 2013 or later|

## Message subject or body

> [!NOTE]
> The search for words or text patterns in the subject or other header fields in the message occurs _after_ the message has been decoded from the MIME content transfer encoding method that was used to transmit the binary message between SMTP servers in ASCII text. You can't use conditions or exceptions to search for the raw (typically, Base64) encoded values of the subject or other header fields in messages.

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**The subject or body includes** <br/><br/> **The subject or body** \> **subject or body includes any of these words**|_SubjectOrBodyContainsWords_ <br/><br/> _ExceptIfSubjectOrBodyContainsWords_|`Words`|Messages that have the specified words in the **Subject** field or message body.|Exchange 2007 or later|
|**The subject or body matches** <br/><br/> **The subject or body** \> **subject or body matches these text patterns**|_SubjectOrBodyMatchesPatterns_ <br/><br/> _ExceptIfSubjectOrBodyMatchesPatterns_|`Patterns`|Messages where the **Subject** field or message body contain text patterns that match the specified regular expressions.|Exchange 2007 or later|
|**The subject includes** <br/><br/> **The subject or body** \> **subject includes any of these words**|_SubjectContainsWords_ <br/><br/> _ExceptIfSubjectContainsWords_|`Words`|Messages that have the specified words in the **Subject** field.|Exchange 2007 or later|
|**The subject matches** <br/><br/> **The subject or body** \> **subject matches these text patterns**|_SubjectMatchesPatterns_ <br/><br/> _ExceptIfSubjectMatchesPatterns_|`Patterns`|Messages where the **Subject** field contains text patterns that match the specified regular expressions.|Exchange 2007 or later|

## Attachments

For more information about how transport rules inspect message attachments, see [Use transport rules to inspect message attachments in Exchange 2013](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md).

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**Any attachment's content includes** <br/><br/> **Any attachment** \> **content includes any of these words**|_AttachmentContainsWords_ <br/><br/> _ExceptIfAttachmentContainsWords_|`Words`|Messages where an attachment contains the specified words.|Exchange 2010 or later|
|**Any attachments content matches** <br/><br/> **Any attachment** \> **content matches these text patterns**|_AttachmentMatchesPatterns_ <br/><br/> _ExceptIfAttachmentMatchesPatterns_|`Patterns`|Messages where an attachment contains text patterns that match the specified regular expressions. <p> **Note:** Only the first 150 kilobytes (KB) of the attachments are scanned.|Exchange 2010 or later|
|**Any attachment's content can't be inspected** <br/><br/> **Any attachment** \> **content can't be inspected**|_AttachmentIsUnsupported_ <br/><br/> _ExceptIfAttachmentIsUnsupported_|n/a|Messages where an attachment isn't natively recognized by Exchange, and the required IFilter isn't installed on the Mailbox server. For more information, see [Register Filter Pack IFilters with Exchange 2013](register-filter-pack-ifilters-with-exchange-2013-exchange-2013-help.md).|Exchange 2010 or later|
|**Any attachment's file name matches** <br/><br/> **Any attachment** \> **file name matches these text patterns**|_AttachmentNameMatchesPatterns_ <br/><br/> _ExceptIfAttachmentNameMatchesPatterns_|`Patterns`|Messages where an attachment's file name contains text patterns that match the specified regular expressions.|Exchange 2010 or later|
|**Any attachment's file extension matches** <br/><br/> **Any attachment** \> **file extension includes these words**|_AttachmentExtensionMatchesWords_ <br/><br/> _ExceptIfAttachmentExtensionMatchesWords_|`Words`|Messages where an attachment's file extension matches any of the specified words.|Exchange 2013 or later|
|**Any attachment is greater than or equal to** <br/><br/> **Any attachment \> size is greater than or equal to**|_AttachmentSizeOver_ <br/><br/> _ExceptIfAttachmentSizeOver_|`Size`|Messages where any attachment is greater than or equal to the specified value. <br/><br/> In the EAC, you can only specify the size in kilobytes (KB).|Exchange 2007 or later|
|**The message didn't complete scanning** <br/><br/> **Any attachment** \> **didn't complete scanning**|_AttachmentProcessingLimitExceeded_ <br/><br/> _ExceptIfAttachmentProcessingLimitExceeded_|n/a|Messages where the rules engine couldn't complete the scanning of the attachments. You can use this condition to create rules that work together to identify and process messages where the content couldn't be fully scanned.|Exchange 2013 or later|
|**Any attachment has executable content** <br/><br/> **Any attachment** \> **has executable content**|_AttachmentHasExecutableContent_ <br/><br/> _ExceptIfAttachmentHasExecutableContent_|n/a|Messages where an attachment is an executable file. The system inspects the file's properties rather than relying on the file's extension.|Exchange 2013 or later|
|**Any attachment is password protected** <br/><br/> **Any attachment** \> **is password protected**|_AttachmentIsPasswordProtected_ <br/><br/> _ExceptIfAttachmentIsPasswordProtected_|n/a|Messages where an attachment is password protected (and therefore can't be scanned). Password detection only works for Office documents, .zip files, and .7z files.|Exchange 2013 or later|

## Any recipients

The conditions and exceptions in this section provide a unique capability that affects _all_ recipients when the message contains at least one of the specified recipients. For example, let's say you have a rule that rejects messages. If you use a recipient condition from the Recipients section, the message is only rejected for those specified recipients. For example, if the rule finds the specified recipient in a message, but the message contains five other recipients. The message is rejected for that one recipient, and is delivered to the five other recipients.

If you add a recipient condition from this section, that same message is rejected for the detected recipient and the five other recipients.

Conversely, a recipient exception from this section _prevents_ the rule action from being applied to _all_ recipients of the message, not just for the detected recipients.

> [!NOTE]
> This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address.

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**Any recipient address includes** <br/><br/> **Any recipient** \> **address includes any of these words**|_AnyOfRecipientAddressContainsWords_ <br/><br/> _ExceptIfAnyOfRecipientAddressContainsWords_|`Words`|Messages that contain the specified words in the **To**, **Cc**, or **Bcc** fields of the message.|Exchange 2013 or later|
|**Any recipient address matches** <br/><br/> **Any recipient** \> **address matches any of these text patterns**|_AnyOfRecipientAddressMatchesPatterns_ <br/><br/> _ExceptIfAnyOfRecipientAddressMatchesPatterns_|`Patterns`|Messages where the **To**, **Cc**, or **Bcc** fields contain text patterns that match the specified regular expressions.|Exchange 2013 or later|

## Message sensitive information types, To and Cc values, size, and character sets

The conditions in this section that look for values in the **To** and **Cc** fields behave like the conditions in the Any recipients section (_all_ recipients of the message are affected by the rule, not just the detected recipients).

> [!NOTE]
> This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address.

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**The message contains sensitive information** <br/><br/> **The message** \> **contains any of these types of sensitive information**|_MessageContainsDataClassifications_ <br/><br/> _ExceptIfMessageContainsDataClassifications_|`SensitiveInformationTypes`|Messages that contain sensitive information as defined by data loss prevention (DLP) policies. <br/><br/> This condition is required for rules that use the **Notify the sender with a Policy Tip** (_NotifySender_) action.|Exchange 2013 or later|
|**The To box contains** <br/><br/> **The message** \> **To box contains this person**|_AnyOfToHeader_ <br/><br/> _ExceptIfAnyOfToHeader_|`Addresses`|Messages where the **To** field includes any of the specified recipients.|Exchange 2007 or later|
|**The To box contains a member of** <br/><br/> **The message** \> **To box contains a member of this group**|_AnyOfToHeaderMemberOf_ <br/><br/> _ExceptIfAnyOfToHeaderMemberOf_|`Addresses`|Messages where the **To** field contains a recipient who is a member of the specified group.|Exchange 2007 or later|
|**The Cc box contains** <br/><br/> **The message** \> **Cc box contains this person**|_AnyOfCcHeader_ <br/><br/> _ExceptIfAnyOfCcHeader_|`Addresses`|Messages where the **Cc** field includes any of the specified recipients.|Exchange 2007 or later|
|**The Cc box contains a member of** <br/><br/> **The message** \> **contains a member of this group**|_AnyOfCcHeaderMemberOf_ <br/><br/> _ExceptIfAnyOfCcHeaderMemberOf_|`Addresses`|Messages where the **Cc** field contains a recipient who is a member of the specified group.|Exchange 2007 or later|
|**The To or Cc box contains** <br/><br/> **The message** \> **To or Cc box contains this person**|_AnyOfToCcHeader_ <br/><br/> _ExceptIfAnyOfToCcHeader_|`Addresses`|Messages where the **To** or **Cc** fields contain any of the specified recipients.|Exchange 2007 or later|
|**The To or Cc box contains a member of** <br/><br/> **The message** \> **To or Cc box contains a member of this group**|_AnyOfToCcHeaderMemberOf_ <br/><br/> _ExceptIfAnyOfToCcHeaderMemberOf_|`Addresses`|Messages where the **To** or **Cc** fields contain a recipient who is a member of the specified group.|Exchange 2007 or later|
|**The message size is greater than or equal to** <br/><br/> **The message** \> **size is greater than or equal to**|_MessageSizeOver_ <br/><br/> _ExceptIfMessageSizeOver_|`Size`|Messages where the total size (message plus attachments) is greater than or equal to the specified value. <br/><br/> In the EAC, you can only specify the size in kilobytes (KB). <p> **Note:** Message size limits on mailboxes are evaluated before transport rules. A message that's too large for a mailbox will be rejected before a rule with this condition is able to act on the message.|Exchange 2013 or later|
|**The message character set name includes any of these words** <br/><br/> **The message** \> **character set name includes any of these words**|_ContentCharacterSetContainsWords_ <br/><br/> _ExceptIfContentCharacterSetContainsWords_|`CharacterSets`|Messages that have any of the specified character set names.|Exchange 2013 or later|

## Sender and recipient

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**The sender is one of the recipient's** <br/><br/> **The sender and the recipient** \> **the sender's relationship to a recipient is**|_SenderManagementRelationship_ <br/><br/> _ExceptIfSenderManagementRelationship_|`ManagementRelationship`|Messages where the either sender is the manager of a recipient, or the sender is managed by a recipient.|Exchange 2010 or later|
|**The message is between members of these groups** <br/><br/> **The sender and the recipient** \> **the message is between members of these groups**|_BetweenMemberOf1_ and _BetweenMemberOf2_ <br/><br/> _ExceptIfBetweenMemberOf1_ and _ExceptIfBetweenMemberOf2_|`Addresses`|Messages that are sent between members of the specified groups.|Exchange 2007 or later|
|**The manager of the sender or recipient is** <br/><br/> **The sender and the recipient** \> **the manager of the sender or recipient is this person**|_ManagerForEvaluatedUser_ and _ManagerAddress_ <br/><br/> _ExceptIfManagerForEvaluatedUser_ and _ExceptIfManagerAddress_|First property: `EvaluatedUser` <br/><br/> Second property: `Addresses`|Messages where either a specified user is the manager of the sender, or a specified user is the manager of a recipient.|Exchange 2010 or later|
|**The sender's and any recipient's property compares as** <br/><br/> **The sender and the recipient** \> **the sender and recipient property compares as**|_ADAttributeComparisonAttribute_ and _ADComparisonOperator_ <br/><br/> _ExceptIfADAttributeComparisonAttribute_ and _ExceptIfADComparisonOperator_|First property: `ADAttribute` <br/><br/> Second property: `Evaluation`|Messages where the specified Active Directory attribute for the sender and recipient either match or don't match.|Exchange 2010 or later|

## Message properties

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**The message type is** <br/><br/> **The message properties** \> **include the message type**|_MessageTypeMatches_ <br/><br/> _ExceptIfMessageTypeMatches_|`MessageType`|Messages of the specified type. <p> **Note**: When Outlook or Outlook Web App is configured to forward a message, the **ForwardingSmtpAddress** property is added to the message. The message type isn't changed to `AutoForward`.|Exchange 2010 or later|
|**The message is classified as** <br/><br/> **The message properties** \> **include this classification**|_HasClassification_ <br/><br/> _ExceptIfHasClassification_|`MessageClassification`|Messages that have the specified message classification. This is a custom message classification that you can create in your organization by using the **New-MessageClassification** cmdlet.|Exchange 2007 or later|
|**The message isn't marked with any classifications** <br/><br/> **The message properties** \> **don't include any classification**|_HasNoClassification_ <br/><br/> _ExceptIfHasNoClassification_|n/a|Messages that don't have a message classification.|Exchange 2010 or later|
|**The message has an SCL greater than or equal to** <br/><br/> **The message properties** \> **include an SCL greater than or equal to**|_SCLOver_ <br/><br/> _ExceptIfSCLOver_|`SCLValue`|Messages that are assigned a spam confidence level (SCL) that's greater than or equal to the specified value.|Exchange 2007 or later|
|**The message importance is set to** <br/><br/> **The message properties** \> **include the importance level**|_WithImportance_ <br/><br/> _ExceptIfWithImportance_|`Importance`|Messages that are marked with the specified Importance level.|Exchange 2007 or later|

## Message headers

> [!NOTE]
> The search for words or text patterns in the subject or other header fields in the message occurs _after_ the message has been decoded from the MIME content transfer encoding method that was used to transmit the binary message between SMTP servers in ASCII text. You can't use conditions or exceptions to search for the raw (typically, Base64) encoded values of the subject or other header fields in messages.

|Condition or exception in the EAC|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|**A message header includes** <br/><br/> **A message header** \> **includes any of these words**|_HeaderContainsMessageHeader_ and _HeaderContainsWords_ <br/><br/> _ExceptIfHeaderContainsMessageHeader_ and _ExceptIfHeaderContainsWords_|First property: `MessageHeaderField` <br/><br/> Second property: `Words`|Messages that contain the specified header field, and the value of that header field contains the specified words. <br/><br/> The name of the header field and the value of the header field are always used together.|Exchange 2007 or later|
|**A message header matches** <br/><br/> **A message header** \> **matches these text patterns**|_HeaderMatchesMessageHeader_ and _HeaderMatchesPatterns_ <br/><br/> _ExceptIfHeaderMatchesMessageHeader_ and _ExceptIfHeaderMatchesPatterns_|First property: `MessageHeaderField` <br/><br/> Second property: `Patterns`|Messages that contain the specified header field, and the value of that header field contains the specified regular expressions. <br/><br/> The name of the header field and the value of the header field are always used together.|Exchange 2007 or later|

## Conditions and exceptions for transport rules on Edge Transport servers

The conditions and exceptions that are available in transport rules on Edge Transport servers are a small subset of what's available on Mailbox servers. There's no EAC on Edge Transport servers, so you can only manage transport rules in the Exchange Management Shell on the local Edge Transport server. The conditions and exceptions are described in the following table. The properties types are described in the Property types section.

|Condition and exception parameters in the Exchange Management Shell|Property type|Description|Available in|
|---|---|---|---|---|
|_AnyOfRecipientAddressContainsWords_ <br/><br/> _ExceptIfAnyOfRecipientAddressContainsWords_|`Words`|Messages that contain the specified words in the **To**, **Cc**, or **Bcc** fields. <br/><br/> When a message contains the specified recipient, the rule action is applied (or not applied) to _all_ recipients of the message. For example, the message is rejected for all recipients of the message, not just for the specified recipient.|Exchange 2013 or later|
|_AnyOfRecipientAddressMatchesPatterns_ <br/><br/> _ExceptIfAnyOfRecipientAddressMatchesPatterns_|`Patterns`|Messages where the **To**, **Cc**, or **Bcc** fields contain text patterns that match the specified regular expressions. <br/><br/> When a message contains the specified recipient, the rule action is applied (or not applied) to _all_ recipients of the message. For example, the message is rejected for all recipients of the message, not just for the specified recipient.|Exchange 2013 or later|
|_AttachmentSizeOver_ <br/><br/> _ExceptIfAttachmentSizeOver_|`Size`|Messages with attachments where any attachment is greater than or equal to the specified value.|Exchange 2007 or later|
|_FromAddressContainsWords_ <br/><br/> _ExceptIfFromAddressContainsWords_|`Words`|Messages that contain the specified words in the sender's email address.|Exchange 2007 or later|
|_FromAddressMatchesPatterns_ <br/><br/> _ExceptIfFromAddressMatchesPatterns_|`Patterns`|Messages where the sender's email address contains text patterns that match the specified regular expressions.|Exchange 2007 or later|
|_FromScope_ <br/><br/> _ExceptIfFromScope_|`UserScopeFrom`|Messages that are sent by either internal senders or external senders.|Exchange 2007 or later|
|_HeaderContainsMessageHeader_ and _HeaderContainsWords_ <br/><br/> _ExceptIfHeaderContainsMessageHeader_ and _ExceptIfHeaderContainsWords_|First property: `MessageHeaderField` <br/><br/> Second property: `Words`|Messages that contain the specified header field, and the value of that header field contains the specified words. <br/><br/> The name of the header field and the value of the header field are always used together.|Exchange 2007 or later|
|_HeaderMatchesMessageHeader_ and _HeaderMatchesPatterns_ <br/><br/> _ExceptIfHeaderMatchesMessageHeader_ and _ExceptIfHeaderMatchesPatterns_|First property: `MessageHeaderField` <br/><br/> Second property: `Patterns`|Messages that contain the specified header field, and the value of that header field contains the specified regular expressions. <br/><br/> The name of the header field and the value of the header field are always used together.|Exchange 2007 or later|
|_MessageSizeOver_ <br/><br/> _ExceptIfMessageSizeOver_|`Size`|Messages where the total size (message plus attachments) is greater than or equal to the specified value.|Exchange 2013 or later|
|_SCLOver_ <br/><br/> _ExceptIfSCLOver_|`SCLValue`|Messages that are assigned an SCL that's greater than or equal to the specified value.|Exchange 2007 or later|
|_SubjectContainsWords_ <br/><br/> _ExceptIfSubjectContainsWords_|`Words`|Messages that contain the specified words in the **Subject** field.|Exchange 2007 or later|
|_SubjectMatchesPatterns_ <br/><br/> _ExceptIfSubjectMatchesPatterns_|`Patterns`|Messages where the **Subject** field contains text patterns that match the specified regular expressions.|Exchange 2007 or later|
|_SubjectOrBodyContainsWords_ <br/><br/> _ExceptIfSubjectOrBodyContainsWords_|`Words`|Messages that contain the specified words in the **Subject** field or message body.|Exchange 2007 or later|
|_SubjectOrBodyMatchesPatterns_ <br/><br/> _ExceptIfSubjectOrBodyMatchesPatterns_|`Patterns`|Messages where the **Subject** field or message body contain text patterns that match the specified regular expressions.|Exchange 2007 or later|

## Property types

The property types that are used in conditions and exceptions are described in the following table.

> [!NOTE]
> If the property is a string, trailing spaces are not allowed.

|Property type|Valid values|Description|
|---|---|---|---|---|
|`ADAttribute`|Select from a predefined list of Active Directory attributes|You can check against any of the following Active Directory attributes: <ul><li>**City**</li><li>**Company**</li><li>**Country**</li><li>**CustomAttribute1 - CustomAttribute15**</li><li>**Department**</li><li>**DisplayName**</li><li>**Email**</li><li>**FaxNumber**</li><li>**FirstName**</li><li>**HomePhoneNumber**</li><li>**Initials**</li><li>**LastName**</li><li>**Manager**</li><li>**MobileNumber**</li><li>**Notes**</li><li>**Office**</li><li>**OtherFaxNumber**</li><li>**OtherHomePhoneNumber**</li><li>**OtherPhoneNumber**</li><li>**PagerNumber**</li><li>**PhoneNumber**</li><li>**POBox**</li><li>**State**</li><li>**Street**</li><li>**Title**</li><li>**UserLogonName**</li><li>**ZipCode**</li></ul> <p> In the EAC, to specify multiple words or text patterns for the same attribute, separate the values with commas. For example, the value **San Francisco,Palo Alto** for the **City** attribute looks for "City equals San Francisco" or City equals Palo Alto". <br/><br/> In the Exchange Management Shell, use the syntax `"AttributeName1:Value1,Value 2 with spaces,Value3...","AttributeName2:Word4,Value 5 with spaces,Value6..."`, where `Value` is the word or text pattern that you want to match. <br/><br/> For example, `"City:San Francisco,Palo Alto"` or `"City:San Francisco,Palo Alto"`,`"Department:Sales,Finance"`. <br/><br/> When you specify multiple attributes, or multiple values for the same attribute, the **or** operator is used. Don't use values with leading or trailing spaces. <br/><br/> Note that the **Country** attribute requires the ISO 3166-1 two-letter country code value (for example, DE for Germany). For more information, see [Country Codes - ISO 316](https://www.iso.org/iso-3166-country-codes.html).|
|`Addresses`|Exchange recipients|Depending on the nature of the condition or exception, you might be able to specify any mail-enabled object in the organization (for example, recipient-related conditions), or you might be limited to a specific object type (for example, groups for group membership conditions). And, the condition or exception might require one value, or allow multiple values. <br/><br/> In the Exchange Management Shell, separate multiple values by commas. <br/><br/> **Note:** This condition doesn't consider messages that are sent to recipient proxy addresses. It only matches messages that are sent to the recipient's primary email address.|
|`CharacterSets`|Array of character set names|One or more content character sets that exist in a message. For example: <ul><li>`Arabic/iso-8859-6`</li><li>`Chinese/big5`</li><li>`Chinese/euc-cn`</li><li>`Chinese/euc-tw`</li><li>`Chinese/gb2312`</li><li>`Chinese/iso-2022-cn`</li><li>`Cyrillic/iso-8859-5`</li><li>`Cyrillic/koi8-r`</li><li>`Cyrillic/windows-1251`</li><li>`Greek/iso-8859-7`</li><li>`Hebrew/iso-8859-8`</li><li>`Japanese/euc-jp`</li><li>`Japanese/iso-022-jp`</li><li>`Japanese/shift-jis`</li><li>`Korean/euc-kr`</li><li>`Korean/johab`</li><li>`Korean/ks_c_5601-1987`</li><li>`Turkish/windows-1254`</li><li>`Turkish/iso-8859-9`</li><li>`Vietnamese/tcvn`</li></ul>|
|`DomainName`|Array of SMTP domains|For example, `contoso.com` or `eu.contoso.com`. <br/><br/> In the Exchange Management Shell, you can specify multiple domains separated by commas.|
|`EvaluatedUser`|Single value of **Sender** or **Recipient**|Specifies whether the rule is looking for the manager of the sender or the manager of the recipient.|
|`Evaluation`|Single value of **Equal** or **Not equal** (`NotEqual`)|When comparing the Active Directory attribute of the sender and recipients, this specifies whether the values should match, or not match.|
|`Importance`|Single value of **Low**, **Normal**, or **High**|The Importance level that was assigned to the message by the sender in Outlook or Outlook Web App.|
|`IPAddressRanges`|Array of IP addresses or address ranges|You enter the IPv4 addresses using the following syntax: <ul><li>**Single IP address**: For example, `192.168.1.1`.</li><li>**IP address range**: For example, `192.168.0.1-192.168.0.254`.</li><li>**Classless InterDomain Routing (CIDR) IP address range**: For example, `192.168.0.1/25`.</li></ul> <br/><br/>In the Exchange Management Shell, you can specify multiple IP addresses or ranges separated by commas.|
|`ManagementRelationship`|Single value of **Manager** or **Direct report**(`DirectReport`)|Specifies the relationship between the sender and any of the recipients. The rule checks the **Manager** attribute in Active Directory to see if the sender is the manager of a recipient, or if the sender is managed by a recipient.|
|`MessageClassification`|Single message classification|In the EAC, you select from the list of message classifications that you've created. <br/><br/> In the Exchange Management Shell, you use the **Get-MessageClassification** cmdlet to identify the message classification. For example, use the following command to search for messages with the `Company Internal` classification and prepend the message subject with the value `CompanyInternal`. <br/><br/> `New-TransportRule "Rule Name" -HasClassification @(Get-MessageClassification "Company Internal").Identity -PrependSubject "CompanyInternal"`|
|`MessageHeaderField`|Single string|Specifies the name of the header field. The name of the header field is always paired with the value in the header field (word or text pattern match). <br/><br/> The _message header_ is a collection of required and optional header fields in the message. Examples of header fields are **To**, **From**, **Received**, and **Content-Type**. Official header fields are defined in RFC 5322. Unofficial header fields start with **X-** and are known as _X-headers_.|
|`MessageType`|Single message type value|Specifies one of the following message types: <ul><li>**Automatic reply** (`OOF`)</li><li>**Auto-forward** (`AutoForward`)</li><li>**Encrypted**</li><li>**Calendaring**</li><li>**Permission controlled** (`PermissionControlled`)</li><li>**Voicemail**</li><li>**Signed**</li><li>**Approval request** (`ApprovalRequest`)</li><li>**Read receipt** (`ReadReceipt`)</li></ul> <p> **Note**: When Outlook or Outlook Web App is configured to forward a message, the **ForwardingSmtpAddress** property is added to the message. The message type isn't changed to `AutoForward`.|
|`Patterns`|Array of regular expressions|Specifies one or more regular expressions that are used to identify text patterns in values. For more information, see [Regular Expression Syntax](/visualstudio/ide/using-regular-expressions-in-visual-studio). <br/><br/> In the Exchange Management Shell, you specify multiple regular expressions separated by commas, and you enclose each regular expression in quotation marks (").|
|`SCLValue`|One of the following values: <ul><li>**Bypass spam filtering** (`-1`)</li><li>Integers 0 through 9</li></ul>|Specifies the spam confidence level (SCL) that's assigned to a message. A higher SCL value indicates that a message is more likely to be spam.|
|`SensitiveInformationTypes`|Array of sensitive information types|Specifies one or more sensitive information types that are defined in your organization. For a list of built-in sensitive information types, see [What the sensitive information types in Exchange 2013 look for](what-the-sensitive-information-types-in-exchange-look-for-exchange-2013-help.md). <br/><br/> In the Exchange Management Shell, use the syntax `@{<SensitiveInformationType1>},@{<SensitiveInformationType2\>},...`. For example, to look for content that contains at least two credit card numbers, and at least one ABA routing number, use the value `@{Name="Credit Card Number"; minCount="2"},@{Name="ABA Routing Number"; minCount="1"}`.|
|`Size`|Single size value|Specifies the size of an attachment or the whole message. <br/><br/> In the EAC, you can only specify the size in kilobytes (KB). <br/><br/> In the Exchange Management Shell, when you enter a value, qualify the value with one of the following units: <ul><li>`B` (bytes)</li><li>`KB` (kilobytes)</li><li>`MB` (megabytes)</li><li>`GB` (gigabytes)</li></ul> <br/><br/> For example, `20MB` <br/><br/> Unqualified values are typically treated as bytes, but small values may be rounded up to the nearest kilobyte.|
|`UserScopeFrom`|Single value of **Inside the organization** (`InOrganization`) or **Outside the organization** (`NotInOrganization`)|A sender is considered to be inside the organization if either of the following conditions is true: <ul><li>The sender is a mailbox, mail user, group, or mail-enabled public folder that exists in the organization's Active Directory.</li><li>The sender's email address is in an accepted domain that's configured as an authoritative domain or an internal relay domain, **and** the message was sent or received over an authenticated connection. For more information about accepted domains, see [Accepted domains](accepted-domains-exchange-2013-help.md).</li></ul> <br/><br/> A sender is considered to be outside the organization if either of the following conditions is true: <ul><li>The sender's email address isn't in an accepted domain.</li><li>The sender's email address is in an accepted domain that's configured as an external relay domain.</li></ul> <p> **Note**: To determine whether mail contacts are considered to be inside or outside the organization, the sender's address is compared with the organization's accepted domains.|
|`UserScopeTo`|One of the following values: <ul><li>**Inside the organization** (`InOrganization`)</li><li>**Outside the organization** (`NotInOrganization`)</li><li>**In an external partner organization** (`ExternalPartner`)</li><li>**In an external non-partner organization** (`ExternalNonPartner`)</li></ul>|A recipient is considered to be inside the organization if either of the following conditions is true: <ul><li>The recipient is a mailbox, mail user, group, or mail-enabled public folder that exists in the organization's Active Directory.</li><li>The recipient's email address is in an accepted domain that's configured as an authoritative domain or an internal relay domain, **and** the message was sent or received over an authenticated connection.</li></ul> <br/><br/> A recipient is considered to be outside the organization if either of the following conditions is true: <ul><li>The recipient's email address isn't in an accepted domain.</li><li>The recipient's email address is in an accepted domain that's configured as an external relay domain.</li></ul> <br/><br/> External partner organizations are external domains where you've configured Domain Security (mutual TLS authentication) to send mail. <br/><br/> External non-partner organizations are all other external domains that aren't considered partner domains.|
|`Words`|Array of strings|Specifies one or more words to look for. The words aren't case-sensitive, and can be surrounded by spaces and punctuation marks. Wildcards and partial matches aren't supported. <br/><br/> For example, "contoso" matches " Contoso.". However, if the text is surrounded by other characters, it isn't considered a match. For example, "contoso" doesn't match the following values: <ul><li>Acontoso</li><li>Contosoa</li><li>Acontosob</li></ul> <br/><br/> The asterisk (\*) is treated as a literal character, and isn't used as a wildcard character.|

## For more information

[Transport rules in Exchange 2013](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)

[Transport rule actions in Exchange 2013](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Transport rule procedures in Exchange 2013](mail-flow-or-transport-rule-procedures-exchange-2013-help.md)

[Mail flow rule conditions and exceptions (predicates) in Exchange Online](../ExchangeOnline/security-and-compliance/mail-flow-rules/conditions-and-exceptions.md)
