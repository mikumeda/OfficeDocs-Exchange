---
title: 'Organization-wide disclaimers, signatures, footers, or headers'
TOCTitle: Organization-wide disclaimers, signatures, footers, or headers
ms:assetid: e45e33c9-e53b-427c-ada5-70901bc399b8
ms:mtpsurl: https://technet.microsoft.com/library/Dn600437(v=EXCHG.150)
ms:contentKeyID: 61071241
ms.reviewer: 
manager: serdars
ms.topic: article
description: About organization-wide disclaimers, signatures, footers, or headers in email in Microsoft Exchange
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Organization-wide disclaimers, signatures, footers, or headers in Exchange 2013

_**Applies to:** Exchange Server 2013_

You can add an email disclaimer, legal disclaimer, disclosure statement, signature, or other information to the top or bottom of email messages that enter or leave your organization. This might be needed for legal, business, or regulatory requirements, to identify potentially unsafe e-mail messages, or for other reasons unique to your organization.

To set up a disclaimer, you create a transport rule that includes the conditions, such when the sender is in a specific group or when the message includes specific text patterns, and the text to add. To apply multiple disclaimers to a single email message, you use multiple transport rules.

> [!IMPORTANT]
> If you want the information to be added only to outgoing messages, you must add a condition such as recipients located outside the organization. By default, transport rules are applied to both incoming and outgoing messages.

## Examples

Here are a few ideas for how to use disclaimers.

|Type|Sample text added|
|---|---|
|Legal - outgoing messages|This email and any files transmitted with it are confidential and intended solely for the use of the individual or entity to whom they are addressed. If you have received this email in error, please notify the system manager.|
|Legal - incoming messages|Employees are expressly required not to make defamatory statements and not to infringe or authorize any infringement of copyright or any other legal right by email communications. Employees who receive such an email must notify their supervisor immediately.|
|Notice that message was sent to an alias|This message was sent to the Sales discussion group.|
|Signature - pulls in data for each employee|Kathleen Mayer <br/> Sales Department <br/> Contoso <br/> www.contoso.com <br/> kathleen@contoso.com <br/> cell: 111-222-1234|
|Advertisement|Click here for March specials|

The examples in this article are not intended for use as-is. Modify them for your needs.

## Scoping your disclaimer

As you work on your disclaimers, consider which messages they should apply to. For example, you might want different disclaimers for internal and external messages or for messages sent by users in specific departments. To make sure only the first message in a conversation gets a disclaimer, add an exception that looks for unique text in your disclaimer.

Here are some examples of the conditions and exceptions you can use.

|Description|Conditions and exceptions in EAC|Conditions and exceptions in the Shell|
|---|---|---|
|Outside your organization, if the original message doesn't include text from your disclaimer, such as "CONTOSO LEGAL NOTICE"|Condition: **The recipient is located** \> **Outside the organization** <br/><br/> Exception: **The subject or body** \> **Subject or body matches these text patterns** \> **CONTOSO LEGAL NOTICE**|`-FromScope NotInOrganization -ExceptIf -SubjectOrBodyMatches "CONTOSO LEGAL NOTICE"`|
|Incoming messages with executable attachments|Condition 1: **The sender is located** \> **Outside the organization** <br/><br/> Condition 2: **Any attachment** \> **has executable content**|`-FromScope NotInOrganization -AttachmentHasExecutableContent`|
|Sender is in the marketing department|Condition: **The sender** \> **is a member of this group** \> **group name**|`-FromMemberOf "Marketing Team"`|
|Every message that comes from an external sender to the sales discussion group|Condition 1: **The sender is located** \> **Outside the organization** <br/><br/> Condition 2: **The message** \> **To or Cc box contains this person** \> **group name**|`-FromScope NotInOrganization -SentTo "Sales Discussion Group" -PrependSubject "Sent to Sales Discussion Group: "`|
|Prepend an advertisement to outgoing messages for one month|Condition 1: **The recipient is located** \> **Outside the organization** <br/><br/> Specify the dates at the bottom of the **New rule** dialog.|`-ApplyHtmlDisclaimerLocation 'Prepend' -SentToScope 'NotInOrganization' -ActivationDate '03/1/2014' -ExpiryDate '03/31/2014'`|

For a complete list of transport rule conditions you can use to target the disclaimer, see [Transport rule conditions (predicates)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

## Formatting your disclaimer

You can format your disclaimer as needed. Here's what can be included in your disclaimer text.

|Type of information|Description|
|---|---|
|Text|The maximum length is 5,000 characters, including any HTML tags and inline Cascading Style Sheets (CSS).|
|HTML and inline CSS|You can use HTML and inline CSS styles to format the text. For example, use the `<HR>` tag to add a line before the disclaimer. <br/><br/> HTML in a disclaimer is ignored if the disclaimer is added to a plain text message.|
|Add Images|Use the `<IMG>` tag to point to an image available on the internet. For example, `<IMG src="http://contoso.com/images/companylogo.gif" alt="Contoso logo">` <br/><br/> Keep in mind that Outlook Web App and Outlook block external web content, including images, by default. Users may need to perform a specific action if they want to view the blocked external content. This means that images added by using the `IMG` tag may not be visible by default. We recommend that you test a disclaimer with `IMG` tags in the email clients your recipients are likely to use to make sure it displays well.|
|Add information for personalized signatures|If you want everyone to have signatures formatted the same way with the same information, you can add unique information for each employee, such as `DisplayName`, `FirstName`, `LastName`, `PhoneNumber`, `Email`, `FaxNumber`, and `Department`. This information must be enclosed in two percent signs (%%) on each side of the information. For example, to use `DisplayName`, you must use **%%DisplayName%%** in your disclaimer. <br/><br/> When a disclaimer rule is triggered, the corresponding values for that user are inserted. The data comes from the sender's Active Directory user account (for on-premises Exchange Server), or from the sender's Microsoft 365 or Office 365 account for Exchange Online. <br/><br/> For a complete list of attributes that can be used in disclaimers and personalized signatures, see the description for the `ADAttribute` property in [Transport rule conditions (predicates)](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)|

For example, here's an example of an HTML disclaimer that includes a signature, an `IMG` tag, and embedded CSS.

```HTML
<div style="font-size:9pt;  font-family: 'Calibri',sans-serif;">
%%displayname%%<br/>
%%title%%<br/>
%%company%%<br/>
%%street%%<br/>
%%city%%, %%state%% %%zipcode%%</div>
 <br/>
<div style="background-color:#D5EAFF; border:1px dotted #003333; padding:.8em; ">
<div><img alt="Fabrikam"  src="http://fabrikam.com/images/fabrikamlogo.png"></div>
<span style="font-size:12pt;  font-family: 'Cambria','times new roman','garamond',serif; color:#ff0000;">HTML Disclaimer Title</span><br/>
<p style="font-size:8pt; line-height:10pt; font-family: 'Cambria','times roman',serif;">This message contains confidential information and is intended only for the individual(s) addressed in the message. If you are not the named addressee, you should not disseminate, distribute, or copy this e-mail. If you are not the intended recipient, you are notified that disclosing, distributing, or copying this e-mail is strictly prohibited.   
<span style="padding-top:10px; font-weight:bold; color:#CC0000; font-size:10pt; font-family: 'Calibri',Arial,sans-serif; "><a href="http://www.fabrikam.com">Fabrikam, Inc.</a></span><br/><br/>
</div>
```

## Fallback options if the disclaimer can't be added

Some messages, such as encrypted messages, prevent Exchange from modifying the content of the original message. You can control how your organization handles these messages. You specify whether to wrap a message that can't be modified in a message envelope that contains the disclaimer, reject the message if a disclaimer can't be added, or ignore the disclaimer action and deliver the message without a disclaimer.

The following list describes each fallback action:

- **Wrap**: If the disclaimer can't be inserted into the original message, Exchange encloses, or "wraps," the original message in a new message envelope. Then the disclaimer is inserted into the new message. If the original message can't be wrapped in a new message envelope, the original message is not delivered. The sender of the message receives a non-delivery report (NDR) that explains why the message was not delivered.

  > [!IMPORTANT]
  > If an original message is wrapped in a new message envelope, subsequent transport rules are applied to the new message envelope, not to the original message. Therefore, you must configure transport rules with disclaimer actions that wrap original messages in a new message body after you configure other transport rules.

- **Reject**: If the disclaimer can't be inserted into the original message, Exchange doesn't deliver the message. The sender of the message receives an NDR that explains why the message wasn't delivered.

- **Ignore**: If the disclaimer can't be inserted into the original message, Exchange delivers the original message unmodified. No disclaimer is added.

## For more information

[Transport rules](mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md)
