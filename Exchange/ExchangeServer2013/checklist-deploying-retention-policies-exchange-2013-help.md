---
title: 'Checklist: Deploying retention policies: Exchange 2013 Help'
TOCTitle: 'Checklist: Deploying retention policies'
ms:assetid: 59e299fd-b6a8-48f5-88ae-dc20dbe32e90
ms:mtpsurl: https://technet.microsoft.com/library/Ee364743(v=EXCHG.150)
ms:contentKeyID: 49318577
ms.reviewer: 
description:  Checklist for deploying retention policies in Microsoft Exchange
ms.topic: article
manager: serdars
ms.author: serdars
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Checklist: Deploying retention policies

_**Applies to:** Exchange Server 2013_

Use this checklist to deploy retention policies in your Microsoft Exchange Server 2013 organization. Before you start working with this checklist, make sure you're familiar with the concepts in the following topics:

- [Messaging records management](messaging-records-management-exchange-2013-help.md)

- [Retention tags and retention policies](retention-tags-and-policies-exchange-2013-help.md)

## Checklist for deploying retention policies

|Done?|Tasks|Resources|
|:---:|---|---|
|☐|Assess messaging records management (MRM) requirements for different sets of users.|[Messaging records management](messaging-records-management-exchange-2013-help.md)|
|☐|Determine which Microsoft Outlook client versions are in use.|Parse the RPC Client Access log files located at `%ExchangeInstallPath%Logging\RPC Client Access`.|
|☐|Create retention tags.|[Create a Retention Policy](create-a-retention-policy-exchange-2013-help.md)|
|☐|Create retention policies.|[Create a Retention Policy](create-a-retention-policy-exchange-2013-help.md)|
|☐|Add retention tags to retention policies.|[Add retention tags to or remove retention tags from a retention policy](add-or-remove-retention-tags-exchange-2013-help.md)|
|☐|Place mailboxes on retention hold.|[Place a mailbox on retention hold](mailbox-retention-hold-exchange-2013-help.md)|
|☐|Apply a retention policy to a single mailbox for testing purposes.|[Apply a retention policy to mailboxes](apply-retention-policy-exchange-2013-help.md)|
|☐|Optional: Implement client blocking to block legacy Outlook clients.|[Configure Outlook Client Blocking for Messaging Records Management](configure-outlook-client-blocking-exchange-2013-help.md)|
|☐|Begin user communication and training activities. Include a deadline when retention policies will be processed, and items moved or deleted.|Not applicable|
|☐|Apply retention policy to additional mailboxes.|[Apply a retention policy to mailboxes](apply-retention-policy-exchange-2013-help.md)|
|☐|A few days in advance, remind users about the deadline.|Not applicable|
|☐|At the deadline, remove the retention hold from mailboxes.|[Place a mailbox on retention hold](mailbox-retention-hold-exchange-2013-help.md)|
