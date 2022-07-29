---
title: 'Message encoding options: Exchange 2013 Help'
TOCTitle: Message encoding options
ms:assetid: c1d9edbb-d87c-41e5-881b-cd612d83d7e4
ms:mtpsurl: https://technet.microsoft.com/library/Bb310794(v=EXCHG.150)
ms:contentKeyID: 49318586
ms.topic: article
description: Specify message encoding options.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Message encoding options

_**Applies to:** Exchange Server 2013_

The message encoding options that are available in Exchange specify message characteristics, such as MIME and non-MIME character sets, binary encoding, and attachment formats. You can specify message encoding options in the following locations:

- Remote domain settings
- Mail user and mail contact settings
- Microsoft Outlook settings
  - Message format
  - Internet message format
  - Internet recipient message format
  - Message character set encoding options

**Content**:

[Message encoding options for messages sent to remote domains](#message-encoding-options-for-messages-sent-to-remote-domains)

[Message encoding options for mail users and mail contacts](#message-encoding-options-for-mail-users-and-mail-contacts)

[Message encoding options available in Outlook](#message-encoding-options-available-in-outlook)

[Message encoding options available in Outlook Web App](#message-encoding-options-available-in-outlook-web-app)

[Order of precedence for message encoding options](#order-of-precedence-for-message-encoding-options)

[For more information](#for-more-information)

## Message encoding options for messages sent to remote domains

When you configure message encoding options for a remote domain, the specific settings are applied for all messages sent to that domain. For remote domains in your organization, you have the following configuration options for message encoding.

|Setting|Available in EAC in<br>Exchange Online Dedicated|Available<br>in the Shell|
|---|:---:|:---:|
|**MIME character set**: The character set that you specify will only be used for MIME messages that don't have their own character set specified. Setting this parameter won't overwrite character sets that are already specified in the outgoing mail. <br/><br/> **Non-MIME character set**: This setting is used if either of the following conditions are true: <ul><li>Incoming messages from a remote domain are missing the value of the _charset=_ setting in the MIME Content-Type: header field.</li><li>Outgoing messages to a remote domain are missing the value of the MIME character set.</li></ul>|Yes|Yes|
|**Content type**: You can specify the content type for MIME messages sent to the recipients in the remote domain. You can use of the following settings: <ul><li>**MimeHtmlText**: All messages are converted to MIME messages that use HTML formatting, unless the original message is a text message. If the original message is a text message, the outgoing message will be a MIME message that uses text formatting. This is the default setting.</li><li>**MimeText**: All messages are converted to MIME messages that use text formatting.</li><li>**MimeHtml**: All messages are converted to MIME messages that use HTML formatting.</li></ul>|No|Yes|
|**Line wrap size**: You can specify the maximum number of characters that can exist on a single line of text in the body of the e-mail message. Older email client applications may prefer 78 characters per line. This option is only available by using the Shell.|No|Yes|

## Message encoding options for mail users and mail contacts

When you configure message encoding options for a mail contact or a mail user, that option is applied to all messages sent to that specific recipient. For mail contacts and mail users in your organization, you have the following configuration options for message encoding:

- **UsePreferMessageFormat**: This parameter specifies whether the message format settings configured for the mail contact override the global settings configured for the remote domain. If you disable this setting, Exchange ignores other message encoding options for this recipient and the message encoding is determined by the configuration of the remote domain or the settings configured by the message sender.

- **MessageFormat**: This parameter specifies the message format. You can either specify Text or Mime as the message format. The value of this setting is dependent on the _MessageBodyFormat_ parameter. If the message body format is Html or TextAndHtml, you must set this parameter to Mime.

- **MessageBodyFormat**: This parameter specifies the message body format. You can specify Text, Html, or TextAndHtml. The value of this setting is dependent on the _MessageFormat_ parameter. If the message format is Text, you must also set this parameter to Text.

- **MacAttachmentFormat**: This parameter specifies the Apple Macintosh operating system attachment format for messages. You can specify BinHex, UuEncode, AppleSingle, or AppleDouble. The value of this setting is dependent on the _MessageFormat_ parameter. If the message format is set to Text, you must set this parameter to either BinHex or UuEncode. If the message format is set to Mime, you must set this parameter to BinHex, AppleSingle or AppleDouble.

You need to use these parameters in the Exchange Management Shell to set the message encoding options for mail users and mail contacts. For more information, see the following topics:

- [Enable-MailContact](/powershell/module/exchange/Enable-MailContact)
- [New-MailContact](/powershell/module/exchange/New-MailContact)
- [Set-MailContact](/powershell/module/exchange/Set-MailContact)
- [Enable-MailUser](/powershell/module/exchange/Enable-MailUser)
- [New-MailUser](/powershell/module/exchange/New-MailUser)
- [Set-MailUser](/powershell/module/exchange/Set-MailUser)

## Message encoding options available in Outlook

As a sender, you can specify message encoding options in Outlook at any of the following stages:

- By configuring the default message format to be either plain text or HTML.
- By setting the message format as you're composing it to either plain text or HTML using the **Format** area in the **Options** tab.
- By configuring the message encoding options for messages that are sent to all recipients outside the Exchange organization. These options are called _Internet message format_ options. The options only apply to remote recipients, and not to recipients in the Exchange organization.
- By configuring the message encoding options for messages that are sent to specific recipients outside the Exchange organization. These options are called _Internet recipient message format_ options. The options only apply to remote recipients in your Contacts folder, and not to recipients in the Exchange organization.

By default, Outlook uses automatic character set message encoding by scanning the whole text of the outgoing message to determine the appropriate encoding to use for the message. This setting applies to messages that you send to Internet recipients and recipients in the Exchange organization. However, you can bypass this and specify a preferred encoding for outgoing messages.

## Message encoding options available in Outlook Web App

As a sender, you can specify message encoding options in Outlook Web App at any of the following stages:

- By configuring the default message format to be either plain text or HTMLin the **Message format** section of the **Settings** \> **Options** \> **Settings** page.
- By setting the message format as you're composing it to either plain text or HTML by using the **More options** (...) menu, and selecting **Switch to plain text** or **Switch to HTML**.

## Order of precedence for message encoding options

Exchange uses the order of precedence as described in the following list to determine the message encoding options for outgoing messages sent to recipients outside the Exchange organization:

1. Remote domain settings
2. Outlook or Outlook Web App settings
3. Mail user or mail contact settings

The list specifies the order of precedence from lowest to highest. A setting made at a higher level may override a setting made at a lower level.

The following table describes the order of precedence from lowest priority to highest priority for message character set encoding options.

### Order of precedence from lowest priority to highest priority for message character set encoding options

|Source|Parameter|Values|
|---|---|---|
|Remote domain entry setting, using the EAC or **Set-RemoteDomain**|_CharacterSet_|Specified|
|Remote domain entry setting, using the EAC or **Set-RemoteDomain**|_NonMimeCharacterSet_|Specified|
|Outlook setting|Message character set encoding|<ul><li>Auto-select</li><li>Specified</li></ul>|

When you set the non-MIME character set for a remote domain, the character set is assigned to the following types of messages:

- Outgoing messages to a configured remote domain that don't contain a specified character set.
- Incoming messages from a configured remote domain that don't contain a specified character set.

The value of the Windows ANSI code page for the transport server is used to assign a character set to the following types of messages:

- Internal messages that don't contain a specified character set.
- Internal messages that contain a specified character set, but don't contain a specified server code page.

If a message contains a specified but invalid character set, the transport server tries to replace the invalid character set with a valid character set.

The following table describes the order of precedence from lowest priority to highest priority for plain text message encoding options.

### Order of precedence from lowest priority to highest priority for plain text message encoding options

|Source|Parameter|Values|
|---|---|---|
|**Set-RemoteDomain**|_LineWrapSize_|<ul><li>From 0 through 132</li><li>unlimited</li></ul>|
|Outlook settings|Message format|Plain text|
|Outlook settings|Internet message format|Plain text options: <ul><li>Encode attachments in UuEncode format when you send a plain text message</li><li>Automatically wrap text at _nn_ characters</li></ul>|
|Outlook settings|Internet recipient message format|Plain text format: <ul><li>Encode attachments in UuEncode attachment format</li><li>Use BinHex Mac attachment format</li></ul>|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_UsePreferMessageFormat_|<ul><li>`$true`</li><li>`$false`</li></ul> <p> If the value is `$false` or if the recipient isn't defined as a mail user or mail contact in the Exchange organization, the mail user or mail contact settings are ignored.|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_MessageFormat_|Text|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_MessageBodyFormat_|Text|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_MacAttachmentFormat_|<ul><li>BinHex</li><li>UuEncode</li></ul>|

The following table describes the order of precedence from lowest priority to highest priority for MIME message encoding options.

### Order of precedence from lowest priority to highest priority for MIME message encoding options

|Source|Parameter|Values|
|---|---|---|
|**Set-RemoteDomain**|_ContentType_|<ul><li>`MimeHtmlText`</li><li>`MimeText`</li><li>`MimeHtml`</li></ul>|
|Outlook or Outlook Web App settings|Message format|<ul><li>Plain text</li><li>HTML</li></ul>|
|Outlook settings|Internet recipient message format|MIME message format <ul><li>Plain text</li><li>Include both plain text and HTML</li><li>HTML</li></ul>|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_UsePreferMessageFormat_|`$true` <br/><br/> `$false` <br/><br/> If the value is `$false` or if the recipient isn't defined as a mail user or mail contact in the Exchange organization, the mail user or mail contact settings are ignored.|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_MessageFormat_|<ul><li>Text</li><li>Mime</li></ul>|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_MessageBodyFormat_|<ul><li>`Text`</li><li>`Html`</li><li>`TextAndHtml`</li></ul>|
|**Set-MailUser** <br/><br/> **Set-MailContact**|_MacAttachmentFormat_|<ul><li>BinHex</li><li>AppleSingle</li><li>AppleDouble</li></ul>|

## For more information

[Message encoding options](message-encoding-options-exchange-2013-help.md)

[TNEF conversion options](tnef-conversion-options-exchange-2013-help.md)

[Remote domains](remote-domains-exchange-2013-help.md)

[Remote domains in Exchange Online](../ExchangeOnline/mail-flow-best-practices/remote-domains/remote-domains.md)

[Manage mail users](../ExchangeOnline/recipients-in-exchange-online/manage-mail-users.md)

[Manage mail contacts](../ExchangeOnline/recipients-in-exchange-online/manage-mail-contacts.md)

[Change the message format in Outlook](https://support.microsoft.com/office/338a389d-11da-47fe-b693-cf41f792fefa)
