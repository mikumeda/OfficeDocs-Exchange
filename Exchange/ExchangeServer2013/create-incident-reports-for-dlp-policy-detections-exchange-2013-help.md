---
title: 'Create incident reports for DLP policy detections: Exchange 2013 Help'
TOCTitle: Create incident reports for DLP policy detections
ms:assetid: 8e807f94-384c-43f5-be6f-06c5587175a0
ms:mtpsurl: https://technet.microsoft.com/library/JJ150534(v=EXCHG.150)
ms:contentKeyID: 47560050
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: How to create incident reports for DLP policy detections in Exchange Server
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Create incident reports for DLP policy detections

_**Applies to:** Exchange Server 2013_

In Exchange Server 2013, you can establish an action to create an incident report within a DLP policy rule set. Additionally, you can indicate to whom the report should be sent and what to do with the original message. The incident report can contain any of the following information.

## Content of an incident management report

The **Generate Incident Report** action enables users to send incident reports to an incident management mailbox. A single incident report will be generated for each message only if the **Generate Incident Report** action is applied within a policy.

The following is a complete list of the line names in the incident report template. The format column describes how to recognize each field in the report. The optional field column specifies what fields might not be in the Report for each rule match. The DLP specific column shows what fields exist as a result of the DLP feature.

|Line name|Description|Format|Optional field|DLP specific|
|---|---|---|---|---|
|Message-Id|ID of the original sent message|Message-Id: ID of message|Mandatory|No|
|Sender|True sender of the original message|Sender: Email address of sender|Mandatory|No|
|Subject|Subject of the original message|Subject: end-user input subject string|Mandatory|No|
|To|Recipient or recipients of the original message <br/><br/> Each To line will only contain a single recipient, and there can be up to 10 recipients displayed in the Incident Report. If there are additional recipients, the next To line will display the remaining number of recipients.|To: Email address of recipient|Mandatory|No|
|CC|CC email address of the original message; the line is optional <br/><br/> Each CC line will only contain a single CC email address, and there can only be up to 10 CC email addresses that are displayed in the Incident Report. If there are additional CC addresses, the next CC line will display the remaining number of CC email addresses.|CC: Email address of CC recipient|Optional|No|
|BCC|BCC email address of the original message; the line is optional <br/><br/> Each BCC line will only contain a single BCC email address, and there can only be up to 10 BCC addresses that are displayed in the Incident Report. If there are additional BCC email addresses, the following BCC line will display the remaining number of BCC email addresses.|BCC: Email address of BCC recipient|Optional|No|
|Severity|Audit severity of the rule hit; displays the highest severity if multiple rules were hit.|Severity: Low, Medium, or High|Optional|No|
|Override|Displays if an override was reported for the message, and the justification of the override if provided.|Override: Yes, Justification: IW input justification string|Optional|Yes|
|False Positive|Displays if a false positive was reported for the message.|False Positive: Yes|Optional|Yes|
|Data Classification|Detected data classifications found in the original message; the line is optional. <br/><br/> Each data classification line will only contain a single detected classification along with its count, confidence, and recommended minimum confidence level. Up to 5 detected classifications will be displayed in the Incident Report. If the detected classification was an affinity, the count value does not apply and will not be shown.|Data Classification: sensitive information type, Count: instances of the sensitive information found in the message, Confidence: percent value, Recommended Minimum Confidence: percent value|Optional|Yes|
|Rule Hit|Displays all the rules that hit the original message. <br/><br/> Includes the name of the rule that was hit, the DLP Policy (optional) that the rule resides in, action(s) that were taken on the message because of the rule, data classification(s) in the rule that caused the rule to hit, and the definition of the rule.|Rule Hit: rule name, DLP Policy: DLP Policy name if applicable, Action: single action, Data Classification: sensitive information type, Definition: rule definition if applicable|Mandatory|No|
|ID Match|Displays the matched data classification, the exact matched content from the message, and the primary evidence of the data classification match; the line is optional.|ID Match: sensitive information type, Value: actual value of the sensitive data, Context: text around the sensitive data in the message|Optional|Yes|

## For more information

[View DLP policy detection reports](view-dlp-policy-detection-reports-exchange-2013-help.md)

[Data loss prevention](../ExchangeOnline/security-and-compliance/data-loss-prevention/data-loss-prevention.md)
