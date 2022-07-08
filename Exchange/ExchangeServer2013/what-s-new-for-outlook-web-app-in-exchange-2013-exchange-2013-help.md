---
title: "What's new for Outlook Web App in Exchange 2013: Exchange 2013 Help"
TOCTitle: What's new for Outlook Web App in Exchange 2013
ms:assetid: 7010e116-9daf-4e76-9a37-964ffde27ee6
ms:mtpsurl: https://technet.microsoft.com/library/JJ150522(v=EXCHG.150)
ms:contentKeyID: 47560022
ms.reviewer: 
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
description: Learn about what's new in Outlook Web App in Exchange 2013.
---

# What's new for Outlook Web App in Exchange 2013

_**Applies to:** Exchange Server 2013_

For Microsoft Exchange Server 2013, we've added several new features to Microsoft Outlook Web App and updated its design.

> [!NOTE]
> For more details about using Outlook Web App in your Exchange Server 2013 organization, see [Outlook Web App](outlook-web-app-exchange-2013-help.md).
>
> Outlook Web App users in your organization now have the ability to add public folders to, or remove them from, their Favorites. Previously, this could only be done in Outlook.

## Apps in Outlook Web App

We've added several apps for Outlook: Bing Maps, Suggested Appointments, and Action Items. These apps are integrated with Outlook and Outlook Web App and extend the information and functionality of messages and calendar items.

Apps in Outlook attempt to anticipate your needs and automatically propose actions you might want to take by using the contents of the email message. For example, if an email message contains a street address, the Bing Maps app offers you a Bing tab with a quick link to a map and directions. Or, if a phrase in the email message suggests a possible action item, the Action Items app creates a suggested Task for your review. An offer to meet is suggested as an Appointment to be added to your calendar, thanks to the Suggested Appointments app.

Apps for Outlook aren't dependent on the version of Exchange Server that you're using. You won't have to worry about breaking or losing any apps for Outlook that you have added when you upgrade Exchange servers or move to a new Exchange version.

Administrators can use the Exchange admin center (EAC) to manage the apps available to users in the organization. Users can then manage their apps. Administrators can also allow users to download apps from Office.com. For more information about the EAC, see [Exchange admin center in Exchange 2013](exchange-admin-center-in-exchange-2013-exchange-2013-help.md).

In addition, we encourage third-party developers to create additional apps for Outlook and then offer them at Office.com. To learn more, see [Deploy and publish Office Add-ins](/office/dev/add-ins/publish/publish) for background information and [Outlook add-ins overview](/office/dev/add-ins/outlook/outlook-add-ins-overview) for detailed information about building apps for Outlook.

## People

- Now, users can link multiple entries for the same person and view the information in a single contact card. For example, if a user has two entries for Holly Holt in his Contacts folder, one entry copied from the organization's address list and one entry that he added manually, he can link the two entries in his Contacts folder and view all the information in one place. Contact linking is done automatically, but the user can also manually link and unlink contacts.

- Connected accounts have been extended to include the ability to connect to a user's LinkedIn account. After the link is established, Outlook Web App automatically adds the user's LinkedIn contacts to the Contacts folder.

## Calendar

- Users can now view multiple calendars in a merged view. Entries from each calendar have their own color, making it easy for users to identify which calendar an entry belongs to. In the day view, users can view multiple calendars in a merged view or in separate columns.

- The month view now includes an agenda for the selected day, providing users with helpful information as they review the day's activities.

- In all calendar views, users can click an item to view a pop-up of the item's details. In addition to the details, controls are now available to accept or decline the item if it's a meeting, to edit or delete if it's an appointment, or, if a meeting item, to join the meeting if an online meeting link is included.

## Tablets and smartphones

Outlook Web App emphasizes a streamlined user interface that also supports the use of touch, enhancing the mobile device experience with Exchange.

## Supported browsers

To experience all Outlook Web App features, use one of the operating system and browser combinations labeled "Best", as noted in the tables below. Outlook Web App is supported by many operating system and web browser combinations, but not all Outlook Web App features are available in all combinations. Some browsers support only the light version of Outlook Web App.

## Supported browsers on desktop and laptop computers

In the table below, the following definitions apply:

- Best: All Outlook Web App features are supported.

- Good: Most Outlook Web App features are supported.

- Light: The browser displays the light version of Outlook Web App

### Windows operating system and browser combination

|Web browser|Windows XP and<br>Windows Server 2003|Windows Vista and<br>Windows Server 2008|Windows 7|Windows 8|
|---|---|---|---|---|
|Internet Explorer 7|Light|Not available|Not available|Not available|
|Internet Explorer 8|Light|Good|Good|Not available|
|Internet Explorer 9|Not available|Best|Best|Not available|
|Internet Explorer 10|Not available|Not available|Best - plus offline access|Best - plus offline access|
|Internet Explorer 11|Not available|Not available|Best - plus offline access|Best - plus offline access|
|Firefox 17 or later|Good|Good|Best|Best|
|Safari 5 or later|Light|Light|Light|Light|
|Chrome 24 or later|Good - plus offline access|Good - plus offline access|Best - plus offline access|Best - plus offline access|

> [!NOTE]
>
> - In previous versions, Outlook Web App had a built-in spell checker. In Exchange Server 2013, Outlook Web App relies on the web browser for spell checking, which Internet Explorer prior to version 10 doesn't provide.
> - Microsoft 365 users will be limited to the light version of Outlook Web App when using Internet Explorer 8. Users whose mailboxes are on a locally managed Exchange server will continue to see the standard version of Outlook Web App when using Internet Explorer 8, but may experience slow or otherwise unsatisfactory performance.

### Other Windows operating system and browser combination

|Web Browser|Mac OS X v10.7 or later|Linux|
|---|---|---|
|Firefox 23 or later versions|Best - plus offline access|Best - plus offline access|
|Safari 6 or later versions|Best - plus offline access|Not available|
|Chrome 24 or later versions|Best - plus offline access|Best - plus offline access|

> [!NOTE]
> Operating system and browser combinations not listed display the light version of Outlook Web App.

## Supported browsers for tablets and smartphones

You can use the web browser on a tablet or smartphone to sign in to Outlook Web App. The available Outlook Web App features depends on the operating system and browser combination in use, as follows:

- Best: All Outlook Web App features for smartphones and tablets are supported.

- Light: The browser displays the light version of Outlook Web App.

### Outlook Web App features available on tablets and smartphones

|Device|Application|Support|
|---|---|---|
|Windows 8 tablet|Web browser|Best|
|iOS 6 or later for iPhone 4s or later|Web browser|Best|
|iOS 6 or later for iPad 2 or later|Web browser|Best|
|All other smartphones and tablets|Web browser|Light|

## OWA for Devices app

The OWA for Devices app lets users in an Exchange 2013 on-premises deployment with a Microsoft 365 or Office 365 mailbox or in a Microsoft 365-only or Office 365-only organization use their iPhone or iPad access their mailbox. The OWA for iPhone and OWA for iPad apps simplify signing in to their mailbox and allows them access their mailbox even when they don't have an Internet connection. The OWA for iPhone or OWA for iPad apps are recommended instead of using your iPhone's or iPad's browser. For Exchange on-premises deployments, you need to enable push notifications for OWA for Devices to work, see [Configuring push notifications proxying for OWA for Devices](configuring-push-notifications-proxying-for-owa-for-devices-exchange-2013-help.md).

You can download the OWA for iPhone and OWA for iPad apps from the Apple App Store by searching for OWA for iPhone or OWA for iPad or download them from [OWA for iPhone in the Apple Store](https://itunes.apple.com/app/owa-for-iphone/id659503543) or [OWA for iPad in the Apple Store](https://itunes.apple.com/app/owa-for-ipad/id659524331). The table below shows the versions of iPad and iPhone that are supported.

To learn more about OWA for iPhone and OWA for iPad, see [OWA for iPhone and OWA for iPad](https://support.microsoft.com/office/7edbf8c6-1a0e-4be8-a374-2809e754eaaf).

|Device|OS version required|
|---|---|
|iPhone 4S, iPhone 5, iPhone 5c or iPhone 5s. This app is optimized for iPhone 5.|iOS 6 or later versions|
|iPad Wi-Fi (3rd generation), iPad Wi-Fi + Cellular (3rd generation), iPad Wi-Fi (4th generation), iPad Wi-Fi + Cellular (4th generation), iPad mini Wi-Fi, iPad mini Wi-Fi + Cellular, iPad Air, iPad Air Wi-Fi + Cellular, iPad mini with Retina display, iPad mini with Retina display Wi-Fi + Cellular|iOS 6 or later versions|

## OWA for Android

OWA for Android lets you interact with your Microsoft 365 or Office 365 mailbox to get to your email, Calendar, and People from anywhere using your Android phone running Kit Kat 4.4 or higher. You can download the OWA for Android app at the [Google Play Store](https://play.google.com/store).

With the OWA for Android app, you can:

- Get, organize, search your email.

- Schedule meetings, locate rooms, see shared calendars and use your voice to get your schedule.

- Sync People with your phone.

- Skip the administrator phone setup.

- Keep your Microsoft 365 or Office 365 business data secure.

- Use the Remote Wipe feature.

Learn more about the background behind OWA for Android on this week's Garage Series. See [The Garage Series Under the Hood: Evolving Exchange ActiveSync and OWA for Devices](https://blogs.office.com/2014/6/11/the-garage-series-under-the-hood-evolving-exchange-activesync-and-owa-for-devices)

> [!NOTE]
> This app won't work with Outlook.com (formerly Hotmail) mailboxes.

## Unavailable features

The following Outlook Web App features are currently unavailable in Exchange 2013. Some of these features may be included in a future release.

- **Search scope**: The ability for Outlook Web App users to search their primary mailbox and their online archive simultaneously is no longer available in Exchange 2013. To search an online archive, users must first navigate to the archive and then conduct their search.

- **Distribution list moderation**: The ability to moderate distribution lists from Microsoft Outlook Web App isn't currently available in Exchange 2013.

- **Custom date on message flags**: The ability to set a custom date on a message flag isn't available in Outlook Web App 2013. You can use Outlook to set custom dates.

- **Reading pane at the bottom of the window**: The option to display the reading pane at the bottom of the Outlook Web App window isn't currently available in Exchange 2013.

- **Reply to embedded email messages**: The ability for users to reply to email messages sent as attachments isn't currently available in Exchange 2013.

- **Search folders**: The ability for users to use Search folders isn't currently available in Exchange 2013.

- **Access to legacy public folders**: The ability for users to access public folders located on servers running previous versions of Exchange isn't currently available in Exchange 2013.

- **Show Recovery option**: The ability for users to work with recovery passwords for their mobile devices with Outlook Web App isn't currently available in Exchange 2013.
