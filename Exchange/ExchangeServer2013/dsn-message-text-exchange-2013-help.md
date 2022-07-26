---
title: 'DSN message text: Exchange 2013 Help'
TOCTitle: DSN message text
ms:assetid: eae4a050-5ecb-4c87-b377-74edb93a5995
ms:mtpsurl: https://technet.microsoft.com/library/Bb125135(v=EXCHG.150)
ms:contentKeyID: 49286855
ms.topic: article
description: You can include text in a customized delivery status notification (DSN) message in Microsoft Exchange Server 2013.
ms.reviewer: 
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# DSN message text

_**Applies to:** Exchange Server 2013_

You can include text in a customized delivery status notification (DSN) message in Microsoft Exchange Server 2013, and you can format that text in HTML.

You can include any information that you want to display to the recipient of the DSN message. For example, you can include a detailed description of the DSN, contact information for your help desk, and a link to your support department's Web site. Each DSN message can contain a maximum of 512 characters.

Because DSN messages can be displayed in HTML, you can embed HTML formatting tags in the DSN text. For example, if you want to make some text in your DSN message bold, enclose the text in `<B>` and `</B>` HTML tags. The following table provides some examples of valid HTML tags that can be used in DSN message text.

|HTML tag|Description|
|---|---|
|`<B>`|Bold begin|
|`</B>`|Bold end|
|`<A HREF="url">`|Hyperlink begin|
|`</A>`|Hyperlink end|
|`<BR>`|Link break|
|`<EM>`|Italic begin|
|`</EM>`|Italic end|
|`<P>`|Paragraph begin|
|`</P>`|Paragraph end|

> [!NOTE]
> By default, Exchange sends HTML DSN messages, but you can configure whether Exchange sends HTML DSN messages to internal senders, external senders, or both. To configure this behavior, modify the _InternalDsnSendHtml_ parameter and the _ExternalDsnSendHtml_ parameter with the **Set-TransportService** command.
>
> If the _InternalDsnSendHtml_ parameter is set to `$false`, Exchange suppresses HTML tags in DSN messages sent to internal senders. If the _ExternalDsnSendHtml_ parameter is set to `$false`, Exchange suppresses HTML tags in DSN messages sent to external senders.

The following characters that Exchange uses in DSN message text have special meanings:

- Greater than sign (\>)
- Less than sign (\<)
- Ampersand (&)
- Quotation marks (")

These characters are used to determine where HTML tags begin and end, and where text that should be displayed to senders starts and stops. If you want to display these characters in your DSN messages, you must use the escape codes in the following table.

For example, if you want to display the message `"Please contact the Help Desk at <1234>."`, you must add `Please contact the Help Desk at &lt;1234&gt;.` to the DSN message text.

|Escape code|Character|
|---|---|
|`&lt;`|\<|
|`&gt;`|\>|
|`&quot;`|"|
|`&amp;`|&|

> [!IMPORTANT]
> If you include an HTML tag in your DSN message text that contains quotation marks ("), such as `<A HREF="url">`, you must use single quotation marks (') around the whole DSN message text. You will receive an error message if you use double quotation marks around the whole DSN message text and around an HTML tag.
