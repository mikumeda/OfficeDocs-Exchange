---
title: 'File formats indexed by Exchange Search: Exchange 2013 Help'
TOCTitle: File formats indexed by Exchange Search
ms:assetid: e5110ac1-28e1-4554-acc3-85d08c997bc5
ms:mtpsurl: https://technet.microsoft.com/library/Ee633485(v=EXCHG.150)
ms:contentKeyID: 51407274
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: File formats that Exchange Search indexes 
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# File formats indexed by Exchange Search

_**Applies to:** Exchange Server 2013_

In Microsoft Exchange Server 2013 and Exchange Online, Exchange Search includes filters for indexing most common types of file formats included as message attachments. You can also install filters to index additional file types.

> [!NOTE]
> In Exchange 2013, it isn't required to install and register Microsoft Office Filter Pack.
>
> By default, the maximum size file that can be indexed by Exchange Server 2013 on-premises is 32 MB. To increase this size limit, you must add the following registry key on all CAS and multi-role servers in your organization:
>
> `@"SOFTWARE\Microsoft\ExchangeServer\V15\Search\SystemParameters" DWORD: "MaxAttachmentSize"`

When managing or using Exchange Search and the dependent features (such as [In-Place eDiscovery](../ExchangeOnline/security-and-compliance/in-place-ediscovery/in-place-ediscovery.md)), consider the difference between unsearchable items and file formats that are disabled for indexing or contain content that can't be indexed:

- **Unsearchable items**: When Exchange Search can't index a particular file type for any reason (for example, if a filter isn't installed), the search for the file type fails. Messages containing such attachments are marked as _partially indexed_. Unsearchable items can be retrieved using the [Get-FailedContentIndexDocuments](/powershell/module/exchange/Get-FailedContentIndexDocuments) cmdlet. When copying In-Place eDiscovery search results to a discovery mailbox or exporting search results to a PST file, you can include unsearchable items. For more information, see [Unsearchable items in Exchange eDiscovery](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md).

- **File formats with content that can't be indexed**: Certain file types such as Windows Media Video (WMV) don't contain content that can be indexed and therefore aren't indexed. Messages containing attachments of such file types are also returned as unsearchable items in In-Place eDiscovery searches.

- **Disabled file formats**: In on-premises organizations, an administrator can disable indexing of a specified file format. Messages that contain an attachment that is of a disabled format are returned as unsearchable items.

> [!IMPORTANT]
> Although a message attachment may be unsearchable or is of a file format that can't be indexed, the message subject, message body and other metadata may be indexed so that the message can be returned in searches.

For additional management tasks related to Exchange Search in on-premises organizations, see [Exchange Search procedures](exchange-search-procedures-exchange-2013-help.md).

## Default filters

The following table lists the default search filters installed on an Exchange 2013 Mailbox server and in Exchange Online. You can retrieve the list of default filters by using the [Get-SearchDocumentFormat](/powershell/module/exchange/Get-SearchDocumentFormat) cmdlet.

|Filter|File extension|
|---|---|
|Email message|.eml|
|Graphics Interchange Format|.gif|
|JPEG|.jpeg|
|Microsoft Excel|.xls, .xlt, .xlsx, .xlsm, .xlb, .xlc, .xlsb|
|Excel File|odbcexcel|
|Microsoft InfoPath|.infopathml|
|Microsoft Office Binder|.obt, obd|
|Microsoft PowerPoint|.pptx, .pptm, .ppt, .ppsx, .ppsm, .pps, .ppam, .potm, .pot, .potx|
|Microsoft Publisher|.pub|
|Microsoft Word|.doc, .docm, .dotx, .dotm, .dot, .docx|
|Microsoft XML Paper Specification|.xps|
|OneNote|.one|
|OpenDocument Presentation|.odp|
|OpenDocument Spreadsheet|.ods|
|OpenDocument Text|.odt|
|Outlook Item|.msg|
|Portable Document Format|.pdf|
|Rich Text|.rtf|
|Text|.txt|
|vCalendar|.vcs|
|vCard|.vcf|
|Visio|.vdw, .vsd, .vss, .vst, .vsx, .vtx, .vssx, .vssm, .vsdm, .vstx, .vstm, .vdx|
|Web archive|.mhtml|
|Web page|.html|
|XML document|.xml|
|ZIP archive|.zip|

## Disabled file formats

The following table lists the search filters that are disabled for indexing by default on an Exchange 2013 Mailbox server and in Exchange Online. In Exchange 2013, administrators can disable or re-enable a supported file format for indexing by using the [Set-SearchDocumentFormat](/powershell/module/exchange/Set-SearchDocumentFormat) cmdlet. This cmdlet isn't available in Exchange Online.

|Filter|File extension|
|---|---|
|AVI|.avi|
|Bitmap|.bmp|
|MP3|.mp3|
|MPEG|.mpeg|
|PNG|.png|
|Microsoft Windows Wave Audio|.wav|
