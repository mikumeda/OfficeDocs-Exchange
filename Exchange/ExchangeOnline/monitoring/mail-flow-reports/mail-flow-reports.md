---
title: "Mail flow reports in the new EAC in Exchange Online"
f1.keywords:
- NOCSH
ms.author: chrisda
author: chrisda
manager: dansimp
audience: ITPro
ms.topic: article
ms.service: exchange-online
ms.localizationpriority: medium
ms.assetid:
description: Admins can learn about the mail flow reports that are available in the new Exchange admin center.
ms.custom:
---

# Mail flow reports in the new Exchange admin center in Exchange Online

Admins can use mail flow reports in the new Exchange admin center (new EAC) to establish baselines and discover trends to fix issues related to mail flow in their organization.

The following mail flow reports are available:

- [Auto forwarded messages report](mfr-auto-forwarded-messages-report.md)
- [Email issues for priority accounts report](mfr-email-issues-for-priority-accounts-report.md)
- [Exchange transport rule report](mfr-exchange-transport-rule-report.md)
- [Inbound messages report](mfr-inbound-messages-and-outbound-messages-reports.md)
- [Non-accepted domain report](mfr-non-accepted-domain-report.md)
- [Non-delivery details report](mfr-non-delivery-details-report.md)
- [Outbound messages report](mfr-inbound-messages-and-outbound-messages-reports.md)
- [Queued messages report](mfr-queued-messages-report.md)
- [SMTP AUTH clients report](mfr-smtp-auth-clients-report.md)
- [Top domain mailflow status report](mfr-top-domain-mailflow-status-report.md)
- [Mailboxes exceeding receiving limits report](mailboxes-exceeding-receiving-limits-report.md)

## Permissions required to view mail flow reports

To view and use mail flow reports, you need to be a member of one of the following role groups in Exchange Online:

- Compliance Administrator
- Exchange Administrator
- Organization Management
- Security Administrator<sup\>*</sup>
- Security Reader<sup>\*</sup>
- View-Only Recipients

For more information, see [Permissions in Exchange Online](../../permissions-exo/permissions-exo.md) and [Manage role groups in Exchange Online](../../permissions-exo/role-groups.md).

<sup\>*</sup> You manage these role groups in the Azure Active Directory admin center (<https://aad.portal.azure.com>).

## Where to find mail flow reports

Open the new EAC at <https://admin.exchange.microsoft.com>, expand **Reports**, and then select **Mail flow**.

To go directly to the mail flow reports, open <https://admin.exchange.microsoft.com/#/reports/mailflowreportsmain>
