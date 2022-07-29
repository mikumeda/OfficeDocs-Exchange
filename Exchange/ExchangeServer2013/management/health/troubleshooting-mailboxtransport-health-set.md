---
title: Troubleshooting MailboxTransport Health Set
TOCTitle: Troubleshooting MailboxTransport Health Set
ms:assetid: 02bfa4cf-6929-437e-bae5-079ea1b92373
ms:mtpsurl: https://technet.microsoft.com/library/ms.exch.scom.mailboxtransport(v=EXCHG.150)
ms:contentKeyID: 49720714
ms.reviewer: 
manager: serdars
ms.author: serdars
ms.topic: article
description: How to troubleshoot the MailboxTransport health set in Exchange 2013
author: msdmaguire
f1.keywords:
- NOCSH
mtps_version: v=EXCHG.150
---

# Troubleshooting MailboxTransport Health Set

_**Applies to:** Exchange Server 2013_

The **MailboxTransport** health set monitors the overall health of the Mailbox Transport Submission and Mailbox Transport Delivery services on Mailbox servers. These services are responsible for sending mail to and from mailbox databases. For more information, see [Mail flow](../../mail-flow-exchange-2013-help.md).

If you receive an alert that indicates that the **MailboxTransport** health set is unhealthy, this indicates an issue that may prevent mail from being sent or received from mailbox databases.

## Explanation

The **MailboxTransport** service is monitored using the following probes and monitors.

|Probe|Health Set|Associated Monitors|
|---|---|---|
|MailboxDeliveryAvailability|MailboxTransport|MailboxDeliveryAvailabilityMonitor|
|MailboxDeliveryAvailabilityAggregationProbe|MailboxTransport|MailboxDeliveryAvailabilityAggregationMonitor|
|MailboxDeliveryInstanceAvailabilityProbe|MailboxTransport|MailboxDeliveryInstanceAvailabilityMonitor|
|MailboxTransportDeliveryServiceRunning|MailboxTransport|MailboxTransportDeliveryServiceRunningMonitor|
|MailboxTransportSubmissionServiceRunning|MailboxTransport|MailboxTransportSubmissionServiceRunningMonitor|
|Mapi.Submit.Probe|MailboxTransport|Mapi.Submit.Monitor|
|none (notification or check)|MailboxTransport|CrashEvent.msexchangedelivery|
|none (notification or check)|MailboxTransport|CrashEvent.msexchangesubmission|
|none (notification or check)|MailboxTransport|DeliveryBackpressureSustainedTimeMonitor|
|none (notification or check)|MailboxTransport|DeliveryInterceptorStoreDriverAgentPctPermFailedMonitor|
|none (notification or check)|MailboxTransport|MailboxTransportUserQuarantineMonitor|
|none (notification or check)|MailboxTransport|MBTSubmissionInterceptorSubmissionAgentMonitor|
|none (notification or check)|MailboxTransport|MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor50|
|none (notification or check)|MailboxTransport|MSExchangeAsstAvgEventProcessingTimeSubmissionMonitor70|
|none (notification or check)|MailboxTransport|PrivateWorkingSetError.msexchangedelivery|
|none (notification or check)|MailboxTransport|PrivateWorkingSetError.msexchangesubmission|
|none (notification or check)|MailboxTransport|PrivateWorkingSetWarning.msexchangedelivery|
|none (notification or check)|MailboxTransport|PrivateWorkingSetWarning.msexchangesubmission|
|none (notification or check)|MailboxTransport|ProcessProcessorTimeError.msexchangedelivery|
|none (notification or check)|MailboxTransport|ProcessProcessorTimeError.msexchangesubmission|
|none (notification or check)|MailboxTransport|ProcessProcessorTimeWarning.msexchangedelivery|
|none (notification or check)|MailboxTransport|ProcessProcessorTimeWarning.msexchangesubmission|
|none (notification or check)|MailboxTransport|SubmissionBackpressureSustainedTimeMonitor|
|none (notification or check)|MailboxTransport|SubmissionInterceptorSubmissionAgentPctPermFailedMonitor|
|none (notification or check)|MailboxTransport|TransportDeliveryFailuresDeliveryStoreDriver560Monitor|

For more information about probes and monitors, see [Server health and performance](../../server-health-and-performance-exchange-2013-help.md).

## User Action

It's possible that the service recovered after it issued the alert. Therefore, when you receive an alert that specifies that the **MailboxTransport** health set is unhealthy, first verify that the issue still exists. If the issue does exist, perform the appropriate recovery actions outlined in the following section.

## Verifying the issue

1. Identify the health set name and server name that are given in the alert.

2. The message details provide information about the exact cause of the alert. In most cases, the message details provide sufficient troubleshooting information to help identify the root cause. If the message details are not clear, do the following:

   1. Open the Exchange Management Shell, and run the following command to retrieve the details of the health set that issued the alert:

      ```powershell
      Get-ServerHealth <server name> | ?{$_.HealthSetName -eq "<health set name>"}
      ```

      For example, to retrieve the **MailboxTransport** health set details about mailbox1.contoso.com, run the following command:

      ```powershell
      Get-ServerHealth mailbox1.contoso.com | ?{$_.HealthSetName -eq "MailboxTransport"}
      ```

   2. Review the command output to determine which monitor reported the error. The **AlertValue** value for the monitor that issued the alert will be **Unhealthy**.

   3. Rerun the associated probe for the monitor that's in an unhealthy state. Refer to the table in the [Explanation](troubleshooting-activesync-health-set.md) section to find the associated probe. To do this, run the following command:

      ```powershell
      Invoke-MonitoringProbe <health set name>\<probe name> -Server <server name> | Format-List
      ```

      For example, assume that the failing monitor is **MailboxDeliveryAvailabilityMonitor**. The probe associated with that monitor is **MailboxDeliveryAvailability**. To run this probe on mailbox1.contoso.com, run the following command:

      ```powershell
      Invoke-MonitoringProbe MailboxTransport\MailboxDeliveryAvailabilityMonitor -Server mailbox1.contoso.com | Format-List
      ```

   4. In the command output, review the "Result" section of the probe. If the value is **Succeeded**, the issue was a transient error, and it no longer exists.
