---
title: 'Using Outlook Web App Web parts: Exchange 2013 Help'
TOCTitle: Using Outlook Web App Web parts
ms:assetid: 7272e3ab-430c-4d6c-8621-9535236ce463
ms:mtpsurl: https://technet.microsoft.com/library/Mt574711(v=EXCHG.150)
ms:contentKeyID: 70319891
ms.reviewer:
ms.topic: article
description: Use Microsoft Office Outlook Web App Web Parts in Microsoft Exchange to specify the mailbox to open, the folder within that mailbox to open, and the content view to use
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Using Outlook Web App Web parts

_**Applies to:** Exchange Server 2013_

You can use Microsoft Office Outlook Web App Web Parts to specify the mailbox to open, the folder within that mailbox to open, and the content view to use.

Outlook Web App Web Parts let you access Outlook Web App content directly from a URL. The URL can be entered into a Web browser or embedded in an application. Generally, Web Parts aren't created manually. Instead, they're created programmatically based on selections made in a user interface (UI), or they're embedded directly in an application, such as a SharePoint Server page. The code behind the UI then creates the URL. One use for Outlook Web App Web Parts is to display a user's Inbox or Calendar on a SharePoint page.

> [!NOTE]
> To use Outlook Web App Web Parts, both the user's mailbox and the mailbox being opened through a Web Part must be located in the same Active Directory forest.

## Permissions for Using Outlook Web App Web Parts

To use Outlook Web App Web Parts, you must, at a minimum, be delegated "Reviewer" access to the content that you're opening. If you've embedded an Outlook Web App Web Part that requires authentication into an application, you must pass authentication information through together with the request for the Web Part. One way to do this is by configuring the Outlook Web App virtual directory to use Integrated Windows authentication. Integrated Windows authentication lets users who've already logged on by using their Active Directory account use Outlook Web App without having to enter their credentials again.

## Outlook Web App Web Parts Syntax

Outlook Web App in Exchange 2013 has a URL format to use for requests to the /owa virtual directory. These requests can be made by typing a URL directly into a Web browser or by embedding the URL in a Web application, such as a SharePoint Server page.

Outlook Web App Web Parts can be used to create URLs of varying complexity. A simple Web Part URL can be used to open the Inbox of any mailbox. A more complex Web Part URL could be used to specify the mailbox to open, the folder within that mailbox to open, and the content view to use.

Depending on the security measures that have been applied to your network, you may have to configure encoding for the Web Parts URL. After you configure the encoding, the code behind the UI will create the URL by using the URL-encoded parameters. URL-encoded parameters use %20 in place of spaces and %2f in place of the path delimiter "/". All examples in this topic use encoded parameters.

The following table lists the parameters of a Web Part and examples of how they're used.

> [!NOTE]
> Exchange 2016, Exchange 2019, and Exchange Online no longer include support for Web Parts.

### Web Part parameters and how they're used

|URL parameter|Description|Values and examples|
|---|---|---|
|Server name and directory (required)|The URL of the Outlook Web App virtual directory.|This may be the same URL that users use to sign in to Outlook Web App, for example: <br/><br/> `https://<server name>/owa`|
|Exchange 2013 explicit logon mailbox identification (optional)|Any SMTP address that's associated with the mailbox to be opened. <br/><br/> If this section of the URL is missing, the default mailbox of the authenticated user is opened. <br/><br/> If no additional parameters are specified, the default behavior is to open the Inbox.|To open the mailbox with the SMTP address tsmith@fourthcoffee.com, use the following URL: <br/><br/> `https://<server name>/owa/tsmith@fourthcoffee.com`|
|cmd (required if you're specifying any parameter other than the explicit logon mailbox identification)|`?cmd=contents` displays the Outlook Web App Web Part that's specified by the parameters instead of the full Outlook Web App user interface.|If no mailbox is specified, the cmd parameter comes after the sign-in address, as follows: <br/><br/> `https://<server name>/owa/?cmd=contents` <br/><br/> If a mailbox is specified, the cmd parameter comes after the explicit mailbox identification, as follows: <br/><br/> `https://<server name>/owa/<SMTP address>/?cmd=contents` <br/><br/> If no additional parameters are specified, the default behavior is to open the Inbox.|
|exsvurl|This parameter must be included when using LiveID authentication <br/><br/> All parameters will be discarded during LiveID authentication if `"exsvurl=1"` is not present. This parameter is for Microsoft 365 and Office 365 mailboxes only.|`https://<server name>/owa/?cmd=contents&exsvurl=1`|
|fpath (optional)|THis part of the URL may have to be written by using URL encoding so that it can pass through firewalls. <br/><br/> When you use URL encoding, a space becomes %20, and a path delimiter (/) becomes %2f. <br/><br/> The folder hierarchy should start from the mailbox root. <br/><br/> This folder path can point to ordinary folders or search folders.|To open the subfolder Projects in the Inbox, use the following URL: <br/><br/> `https://<server name>/owa/?cmd=contents&fpath=inbox%2fprojects`|
|module (optional)|This parameter can be used to specify any of the default folders without knowing the localized name.|Values for the module parameter aren't case sensitive, and include the following values: <ul><li>Inbox</li><li>Calendar</li><li>Teammailbox</li></ul> <p> To open the calendar of a mailbox regardless of localization, use the following URL: <br/><br/> `https://<server name>/owa/?cmd=contents&module=calendar`|
|view (optional)|This parameter specifies the view to be displayed for the folder. <br/><br/> The default views when this parameter is not present are as follows: <ul><li>Calendar: Daily</li><li>Messages: Messages</li></ul> <p> **Note**: The strings for the default views are automatically URL encoded. <br/><br/> The default sort for a view is the way the folder would be sorted if it was opened in the Outlook Web App client. <br/><br/> The strings identifying the views aren't localized and are not case sensitive.|The views available vary according to the folder type. <br/><br/> Calendar views: <ul><li>Daily: The daily calendar view</li><li>Weekly: The weekly calendar view</li><li>Monthly: The monthly calendar view</li></ul> <p> Message views: <ul><li>Messages: Message view, with default sort</li><li>By%20Sender: Message view sorted by From with sender names that begin with "a" on top</li><li>By%20Subject: Message view sorted by Subject with subjects that begin with "a" on top</li><li>By%20Conversation%20Topic: Conversation View, not available in the light version of Outlook Web App</li></ul>|
|d, m, y (optional)|Specifies the date for which the calendar should be displayed. These parameters can be entered in any order and can be used singly or together. <br/><br/> If any of these parameters aren't specified, the default values are the current day, month, and year values. For example, if the current day is May 3, 2016 and you specify a month value of "9" for September, the date displayed will be September 3, 2016.|The valid values for the data parameters are as follows: <br/><br/> d=[1-31] <br/><br/> m=[1-12] <br/><br/> y=[four digit year] <br/><br/> To open a calendar to the date May 3, 2016, you would use the following URL: `https://<server name>/owa/?cmd=content&fpath=calendar&view=daily&d=3&m=5&y=2016`|
|part (optional)|Specifies that Outlook Web App should display a smaller Web Part.|When you use Web Parts to access Outlook Web App content, the UI that is displayed will be smaller than the full Outlook Web App UI. The part parameter reduces the UI further. The following example URL shows the Tasks list in the smallest Web Part format: <br/><br/> `https://<server name>/owa/?cmd=contents&part=1` <br/><br/> The part parameter doesn't apply to the calendar module.|
|FolderList|This part parameter includes the folder list control for users to switch between subfolders. This only applies to email folders.|`https://<server name>/owa/?cmd=contents&folderlist=1`|

## Enter Outlook Web App Web Parts manually

Outlook Web App Web Parts can be also be entered manually in a Web browser. For example, a user can use an Outlook Web App Web Part URL to open another user's calendar.

The following examples show how to directly access common Outlook Web App views:

- **Inbox**: `https://<server name>_/owa/?cmd=contents\&module=inbox`
- **Calendar (today)**: `https://<server name>/owa/?cmd=contents\&module=calendar\&exsvurl=1`
- **Calendar (weekly)**: `https://<server name>/owa/?cmd=contents\&module=calendar\&view=weekly\&exsvurl=1`
- **Calendar (monthly)**: `https://<server name>/owa/?cmd=contents\&module=calendar\&view=monthly\&exsvurl=1`

## For More Information

- [Customize the Outlook Web App sign-In, language selection, and error pages](customize-the-outlook-web-app-sign-in-language-selection-and-error-pages-exchange-2013-help.md)
- [Create a theme for Outlook Web App](create-a-theme-for-outlook-web-app-exchange-2013-help.md)
