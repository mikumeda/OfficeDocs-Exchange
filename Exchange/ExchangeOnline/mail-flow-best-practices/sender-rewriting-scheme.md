---
title: Sender Rewriting Scheme (SRS) in Microsoft 365
description: Describes Sender Rewriting Scheme (SRS) in Office 365.
author: Benny-54
ms.author: v-bshilpa
manager: serders
audience: ITPro
ms.topic: article
localization_priority: Normal
ms.service: exchange-online
ms.assetid:
ms.reviewer:
ms.collection:
- exchange-online
- M365-email-calendar
f1.keywords:
---

# Sender Rewriting Scheme (SRS) in Microsoft 365

> [!NOTE]
> A new relay IP pool has been introduced in Microsoft 365 which might affect the current SRS rewriting behavior. Messages that qualify for this relay pool won't be rewritten by SRS but will be sent out of IPs that won't be a part of the Microsoft 365 SPF record. The main change is for messages that fail SPF checks when they are entering Exchange Online because SRS will no longer fix these failures. For more information, check the post about the relay pool change in the [Message Center](/microsoft-365/admin/manage/message-center) or see [Outbound delivery pools](/microsoft-365/security/office-365-security/high-risk-delivery-pool-for-outbound-messages?#relay-pool).
>
> In an upcoming change, SRS will rewrite all messages forwarded by using SMTP or mailbox forwarding. This will consolidate the behavior to use SRS for all message forwarding in the service. Due to this change, some disruptions might occur such as messages being sent through on-premises not being rewritten. To fix these disruptiones, see [Sender Rewriting Scheme Upcoming Changes](https://techcommunity.microsoft.com/t5/exchange-team-blog/sender-rewriting-scheme-upcoming-changes/ba-p/2632829).

The Sender Rewriting Scheme (SRS) functionality was added to Microsoft 365 to resolve a problem in which autoforwarding was incompatible with SPF. The SRS feature rewrites the **P1 From** address (also known as the Envelope From address) for all applicable messages that are sent externally from Microsoft 365.

> [!NOTE]
> The **From** header, also known as the Display From address or P2 From address, that is displayed by email clients remains unchanged.

The SRS functionality improves the delivery of applicable messages that pass Sender Policy Framework (SPF) checks when they arrive from the original sender but fail SPF checks at the final external destination after they're forwarded.

SRS rewrites the **P1 From** address in the following scenarios:

- Messages in Microsoft 365 that are autoforwarded (or redirected) to an external recipient by using any of the following methods:
  - SMTP forwarding
    *Some messages forwarded by using SMTP Forwarding won't be rewritten by SRS because they would have already been rewritten. In an upcoming change, the SMTP Forwarding method will be covered under SRS as well.*
  - Mailbox Rule (or Inbox rule) redirection
  - Transport Rule redirection
  - Groups or DLs that have external members
  - Mail Contact forwarding
  - Mail User forwarding
- Messages that are autoforwarded (or redirected) from a customer's on-premises environment and relayed through Exchange Online.

It's important to note that SRS rewriting is used to prevent spoofing of unverified domains. You should send messages only from domains that you own and for which you've verified your ownership through the Accepted Domains list. For more information about Accepted Domains in Microsoft 365, see [Manage accepted domains in Exchange Online](/exchange/mail-flow-best-practices/manage-accepted-domains/manage-accepted-domains).

> [!NOTE]
> SRS rewriting does not fix the issue of DMARC passing for forwarded messages. Although an SPF check will now pass by using a rewritten **P1 From** address, DMARC also requires an alignment check for the message to pass. For forwarded messages, DKIM always fails because the signed DKIM domain does not match the **From** header domain. If an original sender sets their DMARC policy to reject forwarded messages, the forwarded messages are rejected by Message Transfer Agents (MTAs) that honor DMARC policies.

This scenario causes Non-Delivery Reports (NDRs) to be returned to Exchange Online instead of the original sender, which is the case when SRS isn't used. Therefore, part of the SRS implementation is to reroute returning NDRs to the original sender if a message can't be delivered.

The following sections present different autoforwarding scenarios and information on how SRS handles them.

## Autoforwarding emails for a mailbox hosted on Microsoft 365

For a message that is sent to a hosted mailbox and is autoforwarded by using mechanisms such as SMTP forwarding, Mailbox Rule redirection or Transport Rule redirection, the **P1 From** address is rewritten before the message leaves Exchange Online. The address is rewritten by using the following pattern:

```powershell
<Forwarding Mailbox Username>+SRS=<Hash>=<Timestamp>=<Original Sender Domain>=<Original Sender Username>@<Forwarding Mailbox Domain>
```

In the following example, a message is sent from Bob (bob@fabrikam.com) to John's mailbox in Exchange Online (john.work@contoso.com). John has set up autoforwarding from this mailbox to his home email address (john.home@example.com). Notice how the P1 From address is rewritten by SRS.

|&nbsp;|Original message|Autoforwarded message|
|---|---|---|
|**Recipient**|`john.work@contoso.com`|`john.home@example.com`|
|**P1 From**|`bob@fabrikam.com`|`john.work+SRS=44ldt=IX=fabrikam.com=bob@contoso.com`|
|**From header**|`bob@fabrikam.com`|`bob@fabrikam.com`|

When SRS rewrites the **P1 From** address, it increases the length of the username portion of the email address. However, the email address has a limit of 64 characters. So if the length of the rewritten email address exceeds 64 characters, it will take the following form:

```powershell
bounces+SRS=<Hash>=<Timestamp>@<Default Accepted Domain>
```

where `<Default Accepted Domain>` is the name of the default Accepted Domain set up for the tenant.

## Relaying from a customer's on-premises server

When a message that originates from a non-verified domain is relayed from a customer's on-premises server, or an application through Exchange Online, the **P1 From** address is rewritten before it leaves Exchange Online. The address is rewritten by using the following pattern:

```powershell
bounces+SRS=<Hash>=<Timestamp>@<Default Accepted Domain>
```

In the following example, a message is sent from Bob (bob@fabrikam.com) to John's mailbox (john.onprem@contoso.com) which is on his company's server that is running Exchange Server. John has set up autoforwarding from this mailbox to his home email address (john.home@example.com). Notice how the **P1 From** address is rewritten by SRS in this scenario.

|Type|Original message|Relayed message received by Exchange Online|Relayed message sent from Exchange Online|
|---|---|---|---|
|**Recipient**|`john.onprem@contoso.com`|`john.home@example.com`|`john.home@example.com`|
|**P1 From**|`bob@fabrikam.com`|`bob@fabrikam.com`|`bounces+SRS=44ldt=IX@contoso.com`|
|**From header**|`bob@fabrikam.com`|`bob@fabrikam.com`|`bob@fabrikam.com`|

In some situations, the relayed messages that are rewritten by SRS might not get delivered, and a Non Delivery Report (NDR) might be generated.

To receive those NDRs, the tenant administrator must create a mailbox named "bounces" that is hosted either on Exchange Online or on-premises. The domain for this mailbox must be set to the default Accepted Domain for the tenant.

## Forwarded messages sent to a customer's on-premises server

By design, SRS considers on-premises servers to be within the trust boundary and doesn't rewrite forwarded messages that are bound to on-premises. However, for complex routing configurations that use on-premises servers to route messages to the Internet, the forwarded messages won't be rewritten and will be rejected due to SPF failure. To solve this issue, administrators can enable the SRS rewrite for traffic flowing through an on-premises outbound connector. For more information about this SRS parameter on outbound on-premises connectors, see [Sender Rewriting Scheme Upcoming Changes](https://techcommunity.microsoft.com/t5/exchange-team-blog/sender-rewriting-scheme-upcoming-changes/ba-p/2632829).
