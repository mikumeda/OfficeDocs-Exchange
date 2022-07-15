---
title: 'Transport rules in Exchange 2013: Exchange 2013 Help'
TOCTitle: Transport rules
ms:assetid: c3d2031c-fb7b-4866-8ae1-32928d0138ef
ms:mtpsurl: https://technet.microsoft.com/library/Dd351127(v=EXCHG.150)
ms:contentKeyID: 49289403
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: Transport rules in Exchange 2013 
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Transport rules in Exchange 2013

_**Applies to:** Exchange Server 2013_

You can use transport rules to identify and take action on messages that flow through your Exchange 2013 organization. Transport rules are similar to the Inbox rules that are available in Outlook and Outlook Web App. The main difference is transport rules take action on messages while they're in transit, and not after the message is delivered to the mailbox. Transport rules contain a richer set of conditions, exceptions, and actions, which provides you with the flexibility to implement many types of messaging policies.

This article explains the components of transport rules, and how they work.

You can use the Exchange admin center (EAC) or the Exchange Management Shell to manage transport rules. For instructions on how to manage transport rules, see [Manage transport rules in Exchange 2013](manage-transport-rules-exchange-2013-help.md).

For each rule, you have the option of enforcing it, testing it, or testing it and notifying the sender. To learn more about the testing options, see [Test a transport rule](../ExchangeOnline/security-and-compliance/mail-flow-rules/test-mail-flow-rules.md) and [Policy Tips](../ExchangeOnline/security-and-compliance/data-loss-prevention/policy-tips.md).

To implement specific messaging policies by using transport rules, see these topics:

- [Use transport rules to inspect message attachments in Exchange 2013](use-transport-rules-to-inspect-message-attachments-exchange-2013-help.md)

- [Common attachment blocking scenarios for transport rules](../ExchangeOnline/security-and-compliance/mail-flow-rules/common-attachment-blocking-scenarios.md)

- [Organization-wide disclaimers, signatures, footers, or headers in Exchange 2013](organization-wide-disclaimers-signatures-footers-or-headers-exchange-2013-help.md)

- [Use transport rules so messages can bypass Clutter](../ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-bypass-clutter.md)

- [Use transport rules to route email based on a list of words, phrases, or patterns](../ExchangeOnline/security-and-compliance/mail-flow-rules/use-rules-to-route-email.md)

- [Common message approval scenarios](../ExchangeOnline/security-and-compliance/mail-flow-rules/common-message-approval-scenarios.md)

## Transport rule components

A transport rule is made of conditions, exceptions, actions, and properties:

- **Conditions**: Identify the messages that you want to apply the actions to. Some conditions examine message header fields (for example, the To, From, or Cc fields). Other conditions examine message properties (for example, the message subject, body, attachments, message size, or message classification). Most conditions require you to specify a comparison operator (for example, equals, doesn't equal, or contains) and a value to match. If there are no conditions or exceptions, the rule is applied to all messages.

    For more information about transport rule conditions in Exchange 2013, see [Transport rule conditions and exceptions (predicates) in Exchange 2013](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md).

- **Exceptions**: Optionally identify the messages that the actions shouldn't apply to. The same message identifiers that are available in conditions are also available in exceptions. Exceptions override conditions and prevent the rule actions from being applied to a message, even if the message matches all of the configured conditions.

- **Actions**: Specify what to do to messages that match the conditions in the rule, and don't match any of the exceptions. There are many actions available, such as rejecting, deleting, or redirecting messages, adding additional recipients, adding prefixes in the message subject, or inserting disclaimers in the message body.

    For more information about transport rule actions in Exchange 2013, see [Transport rule actions in Exchange 2013](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md).

- **Properties**: Specify other rules settings that aren't conditions, exceptions or actions. For example, when the rule should be applied, whether to enforce or test the rule, and the time period when the rule is active.

    For more information, see the Transport rule properties section in this topic.

## Multiple conditions, exceptions, and actions

The following table shows how multiple conditions, condition values, exceptions, and actions are handled in a rule.

|Component|Logic|Comments|
|---|---|---|
|Multiple conditions|AND|A message must match all the conditions in the rule. If you need to match one condition or another, use separate rules for each condition. For example, if you want to add the same disclaimer to messages with attachments and messages that contain specific text, create one rule for each condition. In the EAC, you can easily copy a rule.|
|One condition with multiple values|OR|Some conditions allow you to specify more than one value. The message must match any one (not all) of the specified values. For example, if an email message has the subject **Stock price information**, and the **The subject includes any of these words** condition is configured to match the words **Contoso** or **stock**, the condition is satisfied because the subject contains at least one of the specified values.|
|Multiple exceptions|OR|If a message matches any one of the exceptions, the actions are not applied to the message. The message doesn't have to match all the exceptions.|
|Multiple actions|AND|Messages that match a rule's conditions get all the actions that are specified in the rule. For example, if the actions **Prepend the subject of the message with** and **Add recipients to the Bcc box** are selected, both actions are applied to the message. <br/><br/> Keep in mind that some actions, such as the **Delete the message without notifying anyone** action, prevent subsequent rules from being applied to a message. Other actions such as **Forward the message** do not allow additional actions. <br/><br/> You can also set an action on a rule so that when that rule is applied, subsequent rules are not applied to the message.|

## Transport rule properties

The following table describes the rule properties that are available in transport rules.

|Property name in the EAC|Parameter name in PowerShell|Description|
|---|---|---|
|**Priority**|_Priority_|Indicates the order that the rules are applied to messages. The default priority is based on when the rule is created (older rules have a higher priority than newer rules, and higher priority rules are processed before lower priority rules). <br/><br/> You change the rule priority in the EAC by moving the rule up or down in the list of rules. In the PowerShell, you set the priority number (0 is the highest priority). <br/><br/> For example, if you have one rule to reject messages that include a credit card number, and another one requiring approval, you'll want the reject rule to happen first, and stop applying other rules. <br/><br/> For more information, see [Set the priority of a transport rule](manage-transport-rules-exchange-2013-help.md#set-the-priority-of-a-transport-rule).|
|**Mode**|_Mode_|You can specify whether you want the rule to start processing messages immediately, or whether you want to test rules without affecting the delivery of the message (with or without Data Loss Prevention or DLP Policy Tips). <br/><br/> Policy Tips present a brief note in Outlook or Outlook on the web that provides information about possible policy violations to the person that's creating the message. For more information, see [Policy Tips](/exchange/security-and-compliance/data-loss-prevention/policy-tips). <br/><br/> For more information about the modes, see [Test a transport rule](/exchange/security-and-compliance/mail-flow-rules/test-mail-flow-rules).|
|**Activate this rule on the following date** <br/><br/> **Deactivate this rule on the following date**|_ActivationDate_ <br/><br/> _ExpiryDate_|Specifies the date range when the rule is active.|
|**On** check box selected or not selected|New rules: _Enabled_ parameter on the **New-TransportRule** cmdlet. <br/><br/> Existing rules: Use the **Enable-TransportRule** or **Disable-TransportRule** cmdlets. <br/><br/> The value is displayed in the **State** property of the rule.|You can create a disabled rule, and enable it when you're ready to test it. Or, you can disable a rule without deleting it to preserve the settings.|
|**Defer the message if rule processing doesn't complete**|_RuleErrorAction_|You can specify how the message should be handled if the rule processing can't be completed. By default, the rule will be ignored, but you can choose to resubmit the message for processing.|
|**Match sender address in message**|_SenderAddressLocation_|If the rule uses conditions or exceptions that examine the sender's email address, you can look for the value in the message header, the message envelope, or both.|
|**Stop processing more rules**|_SenderAddressLocation_|This is an action for the rule, but it looks like a property in the EAC. You can choose to stop applying additional rules to a message after a rule processes a message.|
|**Comments**|_Comments_|You can enter descriptive comments about the rule.|

## How transport rules are applied to messages

All messages that flow through your organization are evaluated against the enabled mail flow rules in your organization. Rules are processed in the order listed on the **Mail flow** \> **Rules** page in EAC, or based on the corresponding _Priority_ parameter value in the Exchange Management Shell.

Each rule also offers the option of stopping processing more rules when the rule is matched. This setting is important for messages that match the conditions in multiple mail flow rules (which rule do you want applied to the message? All? Just one?).

## Differences in processing based on message type

There are several types of messages that pass through an organization. The following table shows which messages types can be processed by transport rules.

|Type of message|Can a rule be applied?|
|---|---|
|**Regular messages**: Messages that contain a single rich text format (RTF), HTML, or plain text message body or a multipart or alternative set of message bodies.|Yes|
|**Microsoft 365 or Microsoft Purview Message Encryption**: Messages encrypted by Microsoft 365 or Office 365. For more information, see [Encryption](/microsoft-365/compliance/encryption).|Rules can always access envelope headers and process messages based on conditions that inspect those headers. <br/><br/> For a rule to inspect or modify the contents of an encrypted message, you need to verify that transport decryption is enabled (Mandatory or Optional; the default is Optional). For more information, see [Enable or disable transport decryption](/exchange/enable-or-disable-transport-decryption-exchange-2013-help). <br/><br/> You can also create a rule that automatically decrypts encrypted messages. For more information, see [Define mail flow rules to encrypt email messages](/microsoft-365/compliance/define-mail-flow-rules-to-encrypt-email).|
|**S/MIME encrypted messages**|Rules can only access envelope headers and process messages based on conditions that inspect those headers. <br/><br/> Rules with conditions that require inspection of the message's content, or actions that modify the message's content can't be processed.|
|**RMS protected messages**: Messages that had an Active Directory Rights Management Services (AD RMS) or Azure Rights Management (RMS) policy applied.|Rules can always access envelope headers and process messages based on conditions that inspect those headers. <br/><br/> For a rule to inspect or modify the contents of an RMS protected message, you need to verify that transport decryption is enabled (Mandatory or Optional; the default is Optional). For more information, see [Enable or disable transport decryption](/exchange/enable-or-disable-transport-decryption-exchange-2013-help).|
|**Clear-signed messages**: Messages that have been signed but not encrypted.|Yes|
|**UM messages**: Messages that are created or processed by the Unified Messaging service, such as voice mail, fax, missed call notifications, and messages created or forwarded by using Microsoft Outlook Voice Access.|Yes|
|**Anonymous messages**: Messages sent by anonymous senders.|Yes|
|**Read reports**: Reports that are generated in response to read receipt requests by senders. Read reports have a message class of `IPM.Note*.MdnRead` or `IPM.Note*.MdnNotRead`.|Yes|

## Transport rules and group membership

When you define a transport rule using a condition that expands membership of a distribution group, the resulting list of recipients is cached by the Transport service on the Mailbox server that applies the rule. This is known as the *Expanded Groups Cache* and is also used by the Journaling agent for evaluating group membership for journal rules. By default, the Expanded Groups Cache stores group membership for four hours. Recipients returned by the recipient filter of a dynamic distribution group are also stored. The Expanded Groups Cache makes repeated round-trips to Active Directory and the resulting network traffic from resolving group memberships unnecessary.

In Exchange 2013, this interval and other parameters related to the Expanded Groups Cache are configurable. You can lower the cache expiration interval, or disable caching altogether, to ensure group memberships are refreshed more frequently. You must plan for the corresponding increase in load on your Active Directory domain controllers for distribution group expansion queries. You can also clear the cache on a Mailbox server by restarting the Microsoft Exchange Transport service on that server. You must do this on each Mailbox server where you want to clear the cache. When creating, testing, and troubleshooting transport rules that use conditions based on distribution group membership, you must also consider the impact of Expanded Groups Cache.

## Rule storage and replication

Transport rules that you create and configure on Mailbox servers are stored in Active Directory, and they're read and applied by the Transport service on all Mailbox servers in the organization. When you create, modify, or remove a transport rule, the change is replicated between the domain controllers in your organization. This allows Exchange to provide a consistent set of transport rules across the organization.

**Notes**:

- Replication between domain controllers depends on factors that aren't controlled by Exchange (for example, the number of Active Directory sites, and the speed of network links). Therefore, you need to consider replication delays when you implement transport rules in your organization. For more information about Active Directory replication, see [Introduction to Active Directory Replication and Topology Management Using Windows PowerShell](/windows-server/identity/ad-ds/manage/powershell/introduction-to-active-directory-replication-and-topology-management-using-windows-powershell--level-100-).

- Each Mailbox server caches expanded distribution groups to avoid repeated Active Directory queries to determine a group's membership. By default, entries in the expanded groups cache expire every four hours. Therefore, changes to the group's membership aren't detected by transport rules until the expanded groups cache is updated. To force an immediate update of the cache on a Mailbox server, restart the Microsoft Exchange Transport service. You need to restart the service on each Mailbox server where you want to forcibly update the cache.

Transport rules that you create and configure on Edge Transport servers are stored in the local instance of AD LDS on the server. No automated replication of transport rules occurs on Edge Transport servers. Rules on the Edge Transport server apply only to messages that flow through the local server. If you need to apply the same set of transport rules on multiple Edge Transport servers, you can clone the Edge Transport server configuration, or export and import the transport rules. For more information, see [Edge Transport server cloned configuration](edge-transport-server-cloned-configuration-exchange-2013-help.md) and [Import or export a transport rule collection](manage-transport-rules-exchange-2013-help.md#import-or-export-a-transport-rule-collection).

Whenever the Transport service on a Mailbox server or Edge Transport server detects a modified transport rule, an event is logged in the Application log in the Event Viewer (Event ID 4002 on Mailbox servers, and Event ID 16028 on Edge Transport servers).

## Rule replication and storage in mixed environments

There are two mixed environment scenarios that are common in Exchange 2013:

- **Hybrid deployments where part of your organization resides in Microsoft 365 or Office 365**

  In a hybrid environment, there's no replication of rules between your on-premises Exchange organization and Microsoft 365 or Office 365. Therefore, when you create a rule in Exchange, you need to create a matching rule in Microsoft 365 or Office 365. Rules you create in Microsoft 365 or Office 365 are stored in the cloud, whereas the rules you create in your on-premises organization are stored locally in Active Directory. When you manage rules in a hybrid environment, you need to keep the two sets of rules synchronized by making the change in both places, or making the change in one environment and then exporting the rules and importing them in the other environment.

  > [!IMPORTANT]
  > Even though there is a substantial overlap between the conditions and actions that are available in no Microsoft 365 or Office 365 and Exchange Server, there are differences. If you plan on creating the same rule in both locations, make sure that all conditions and actions you plan to use are available. To see the list of available conditions and actions that are available in Microsoft 365 or Office 365, see the following topics:
  >
  > [Transport rule conditions and exceptions (predicates) in Exchange Online](/exchange/security-and-compliance/mail-flow-rules/conditions-and-exceptions)
  >
  > [Mail flow rule actions in Exchange Online](/exchange/security-and-compliance/mail-flow-rules/mail-flow-rule-actions)

- **Coexistence with Exchange 2010 or Exchange 2007**

  When you coexist with Exchange 2010 or Exchange 2007, all transport rules are stored in Active Directory and replicated across your organization, regardless of the Exchange Server version you used to create the rules. However, all transport rules are associated with the Exchange Server server version that was used to create them, and are stored in a version-specific container in Active Directory. When you first deploy Exchange 2013 in your organization, any existing rules are imported to Exchange 2013 as part of the setup process. However, any changes afterwards would need to be made with both versions. For example, if you change an existing rule in Exchange 2013 (Exchange Management Shell or the EAC), you need to make the same change in Exchange 2010 (Exchange Management Shell or the Exchange Management Console (EMC)). Or, you can export the rules from Exchange 2013 and import them into Exchange 2010.

  Exchange 2010 can't process rules that have the **Version** or **RuleVersion** value 15._n_._n_._n_. To be sure all your rules can be processed, only use rules that have the value 14._n_._n_._n_.

## For more information

[Manage transport rules in Exchange 2013](manage-transport-rules-exchange-2013-help.md)

[Transport rule conditions and exceptions (predicates) in Exchange 2013](mail-flow-rule-conditions-and-exceptions-predicates-in-exchange-2013-exchange-2013-help.md)

[Transport rule actions in Exchange 2013](mail-flow-rule-actions-in-exchange-2013-exchange-2013-help.md)

[Transport agents](transport-agents-exchange-2013-help.md)